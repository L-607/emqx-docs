# EMQX & Watsons SDES Deploy

## Architecture Design

### EMQX Enterprise Watsons SDES customized version

Based on EMQX Enterprise Edition, custom-developed plug-ins include the following functions

- Authentication: store startup authentication (issue store information, authentication information based on IP address), connection management and authentication management after the device BOOT process
- Authentication: business process authentication, file transfer based on SDES Job management, authorization of both ends (server and store) during file transfer
- File transfer protocol: file fragmentation, integrity check, file broadcast, partition push
- Protocol control: business management, flow control, device information delivery, file transfer service delivery
- Device management plug-in: store message channel management, instant notification of online and offline

For the opening and starting of the module, please refer to the `Watsons Module` chapter.

The EMQX Enterprise version uses a three-node cluster to ensure high service availability.

### EMQX Backend API

Microservices written using the Java SpringBoot framework, RESTFul API. Serves the SDES front-end console. For detailed API interface documentation, refer to the `API docs` chapter.

### MySQL database

Provide data support for the SDES platform. For database table design, refer to `MySQL DataBase` chapter.

### Front-end interactive component SDES Dashboard

#### Function (3 sections: access, message distribution, data cache)

#### Rule engine use (just write MySQL resource configuration, log report persistence rules. Online and offline events have been transferred to the internal implementation of the plug-in)

## Architecture Diagram

![sdes_architecture](./assets/sdes/sdes_architecture.png)

## Resource information

Resource configuration and port information are as follows

|   Services   |     Resource Configuration      | Minimum Resources | Ports                                                   |
| :----------: | :-----------------------------: | ----------------- | ------------------------------------------------------- |
| EMQX Cluster |           3 * (8c16g)           | 1c1g              | 1883<br/>8883<br/>8083<br/>8084<br/>8081<br/>18083<br/> |
|  BackendAPI  | API(Java SpringBoot)2 * (8c16g) | 0.5c500m          | 9000                                                    |
|    MySQL     |           1 * (8c16g)           | 1c1g              | 3306                                                    |
|   Frontent   |           2 * (1c2g)            | 0.5c500m          |                                                         |

## Start deploy

## Deploy emqx-ee

Open the daocloud platform, click on the application and choose to arrange the application through YAML. Fill in the type as follows YAML file.

![daocloud_1](./assets/sdes/daocloud_1.png)

Configure and fill in the application name, and fill in the following YAML file.

![daocloud_2](./assets/sdes/daocloud_2.png)

The content of the component EMQX cluster yaml file is as follows:

~~~yaml
---
# create ns emqx
apiVersion: v1
kind: Namespace
metadata:
  labels:
    kubernetes.io/metadata.name: emqx-ee
  name: emqx-ee
---
# Source: rbac.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  namespace: emqx-ee
  name: emqx-ee

---
# rbac.yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: emqx-ee
  name: emqx-ee
rules:
- apiGroups:
  - ""
  resources:
  - endpoints 
  verbs: 
  - get
  - watch
  - list
---
# rbac.yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: emqx-ee
  name: emqx-ee
subjects:
  - kind: ServiceAccount
    name: emqx-ee
    namespace: emqx-ee
roleRef:
  kind: Role
  name: emqx-ee
  apiGroup: rbac.authorization.k8s.io  

---
# Source: configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: emqx-ee-env
  namespace: emqx-ee
  labels:
    app.kubernetes.io/name: emqx-ee
     
data:
    EMQX_CLUSTER__K8S__ADDRESS_TYPE: "hostname"
    EMQX_CLUSTER__K8S__APISERVER: "https://kubernetes.default.svc:443"
    EMQX_CLUSTER__K8S__SUFFIX: "svc.cluster.local"
    EMQX_LOG__TO: "both"
    EMQX_LOG__LEVEL: "error"
    EMQX_dashboard__default_user__login: "admin"
    EMQX_dashboard__default_user__password: "J#i2&Dbfc!od"
   
---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: emqx-ee
  namespace: emqx-ee
  labels:
    app.kubernetes.io/name: emqx-ee
       
spec:
  type: NodePort
  ports:
  - name: mqtt
    port: 1883
    protocol: TCP
    targetPort: mqtt
  - name: mqttssl
    port: 8883
    protocol: TCP
    targetPort: mqttssl
  - name: mgmt
    port: 8081
    protocol: TCP
    targetPort: mgmt
  - name: ws
    port: 8083
    protocol: TCP
    targetPort: ws
  - name: wss
    port: 8084
    protocol: TCP
    targetPort: wss
  - name: dashboard
    port: 18083
    protocol: TCP
    targetPort: dashboard
  selector:
    app.kubernetes.io/name: emqx-ee
    
---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: emqx-ee-headless
  namespace: emqx-ee
  labels:
    app.kubernetes.io/name: emqx-ee
       
spec:
  type: ClusterIP
  publishNotReadyAddresses: true
  sessionAffinity: None
  clusterIP: None
  ports:
  - name: mqtt
    port: 1883
    protocol: TCP
    targetPort: mqtt
  - name: mqttssl
    port: 8883
    protocol: TCP
    targetPort: mqttssl
  - name: mgmt
    port: 8081
    protocol: TCP
    targetPort: mgmt
  - name: ws
    port: 8083
    protocol: TCP
    targetPort: ws
  - name: wss
    port: 8084
    protocol: TCP
    targetPort: wss
  - name: dashboard
    port: 18083
    protocol: TCP
    targetPort: dashboard
  - name: ekka
    port: 4370
    protocol: TCP
    targetPort: ekka
  selector:
    app.kubernetes.io/name: emqx-ee
    
---
# StatefulSet.yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: emqx-ee
  namespace: emqx-ee
  labels:
    app.kubernetes.io/name: emqx-ee
        
spec:
  serviceName: emqx-ee-headless
  podManagementPolicy: Parallel 
  
  updateStrategy:
    type: RollingUpdate 
  
  replicas: 3
  selector:
    matchLabels:
      app.kubernetes.io/name: emqx-ee
      
  template:
    metadata:
      labels:
        app: emqx-ee
        version: Watsons
        app.kubernetes.io/name: emqx-ee
        
    spec:
      volumes:
     
      - name: host-time
        hostPath: 
          path: /etc/localtime
      serviceAccountName:  emqx-ee
      
      containers:
        - name: emqx
          image: "10.95.35.98/emqx/emqx-ee:202304261421"
          imagePullPolicy: IfNotPresent
          
         
          ports:
          - name: mqtt
            containerPort: 1883
          - name: mqttssl
            containerPort: 8883
          - name: mgmt
            containerPort: 8081
          - name: ws
            containerPort: 8083
          - name: wss
            containerPort: 8084
          - name: dashboard
            containerPort: 18083
          - name: ekka
            containerPort: 4370
          envFrom:
            - configMapRef:
                name: emqx-ee-env
          env:
          - name: EMQX_NAME
            value: emqx
          - name: EMQX_CLUSTER__K8S__APP_NAME
            value: emqx
          - name: EMQX_CLUSTER__DISCOVERY
            value: k8s
          - name: EMQX_CLUSTER__K8S__SERVICE_NAME
            value: emqx-ee-headless
          - name: EMQX_CLUSTER__K8S__NAMESPACE
            value: emqx-ee
          resources: {}
          volumeMounts:
          - name: host-time
            mountPath: /etc/localtime
          
          readinessProbe:
            httpGet:
              path: /status
              port: 8081
            initialDelaySeconds: 10
            periodSeconds: 5
            failureThreshold: 30
            
          livenessProbe:
            httpGet:
              path: /status
              port: 8081
            initialDelaySeconds: 60
            periodSeconds: 30
            failureThreshold: 10  
~~~
Note that `namespace: emqx-ee` needs to be modified to the corresponding k8S namespace, and the value corresponding to `EMQX_CLUSTER__K8S__NAMESPACE` should also be modified to the corresponding namespace. The image name and image tag need to be changed to `image: "10.95.35.98/emqx/emqx-ee:202304261421"` corresponding to the private warehouse. YAML specifies the default password `J#i2&Dbfc!od` of the EMQX Dashboard user through configmap.

After the configuration is complete, you can see the service port information corresponding to the application through the Daocloud page, and you can see the corresponding relationship as follows.

![daocloud_3](./assets/sdes/daocloud_3.png)

### Log in to EMQX background management Dashboard

Account and password, the password is the password set above

~~~shell
admin/J#i2&Dbfc!od
~~~

### Module

Find `Modules` in the left navigation bar, click to enter and click `Add Module`.

![image](./assets/sdes/init_modules.png)

Click on `Local Modules` to find `Watsons Server`. Or enter `Watsons Server` in the search bar on the right

![image](./assets/sdes/lookup_w_module.png)

Click `Select` to enter the module configuration.

Here you need to fill in the corresponding MySQL database address and other information according to the actual situation.

![image](./assets/sdes/config_module.png)

configuration parameters

| Name | Type | Info |
| -------------------- | ------ | --------------------- --------------- |
| MySQL Server IP Port | String | MySQL database address and service port number |
| MySQL Database Name | String | MySQL database name |
| MySQL User Name | String | MySQL database login user, must have read and write permissions |
| MySQL Password | String | MySQL database login password |

Click the `Add` button, and the plug-in will load data from the MySQL database when it starts, and also initialize some business query processes. According to the MySQL performance and network speed, the startup will be slow, generally taking 4 to 5 seconds.

### The module started successfully

![image](./assets/sdes/ensure_module.png)

### Module Considerations

The module only needs to be started once, and the startup process will be automatically synchronized in the cluster.

### Rule

After the module configuration is completed, a rule needs to be configured through the EMQX rule engine. This rule is mainly used for Job log report. First you need to configure MySQL resources.

![daocloud_3](./assets/sdes/rule_4.png)

Fill in the main MySQL-related information, and then click Add Rule.

![daocloud_3](./assets/sdes/rule_1.png)

The SQL content of the rule is as follows.

~~~sql
SELECT
     payload.report_id as report_id,
     payload.status as job_status,
     payload.start_time as start_time,
     payload.end_time as end_time,
     payload.now as script_now,
     payload.job_id as job_id,
     payload.task_id as task_id,
     payload.script_id as script_id,
     payload.order as script_order,
     payload.type as script_type,
     payload.error_code as error_code,
     payload.message as script_error_message,
     clientid as client_id
FROM
     '$report/job/+/task/+'
~~~

Then the action that needs to configure the rules will output the relevant data to the MySQL database after processing.

![daocloud_3](./assets/sdes/rule_2.png)

![daocloud_3](./assets/sdes/rule_3.png)

Fill in the insert statement in the SQL Template content, the content is as follows

~~~sql

INSERT INTO
     job_logs (
         `status`,
         start_time,
         end_time,
         now_time,
         job_id,
         task_id,
         script_id,
         `order`,
         error_code,
         `error_message`,
         mqtt_client_id,
         report_id,
         script_type
     )
VALUES
(
     ${job_status},
     ${start_time},
     ${end_time},
     ${script_now},
     ${job_id},
     ${task_id},
     ${script_id},
     ${script_order},
     ${error_code},
     ${script_error_message},
     ${client_id},
     ${report_id},
     ${script_type}
     );
~~~

After all configurations are complete, click confirm to submit.

### deploy backend-api

Open the daocloud platform, click on the application and choose to arrange the application through YAML. The steps here are the same as above.

~~~yaml
kind: Deployment
apiVersion: apps/v1
metadata:
  name: emqx-backend-api
  namespace: emqx-ee
  labels:
    app.kubernetes.io/name: emqx-backend-api
spec:
  replicas: 1
  selector:
    matchLabels:
      app.kubernetes.io/name: emqx-backend-api
  template:
    metadata:
      name: emqx-backend-api
      labels:
        app.kubernetes.io/name: emqx-backend-api
    spec:
      volumes:
        - name: backend-api-configmap
          configMap:
            name: emqx-backend-api
            items:
              - key: application.yml
                path: application.yml
            defaultMode: 420
      containers:
        - name: emqx-backend-api
          image: '10.95.35.98/emqx/sdes-api:202305101513'
          imagePullPolicy: IfNotPresent
          ports:
            - name: backend-api
              containerPort: 9000
              protocol: TCP
          resources:
            limits: {}
          volumeMounts:
            - name: backend-api-configmap
              mountPath: /config/application.yml
              subPath: application.yml
              readOnly: false

---
kind: Service
apiVersion: v1
metadata:
  name: emqx-backend-api
  namespace: emqx-ee

  labels:
    app.kubernetes.io/name: emqx-backend-api

spec:
  ports:
    - name: backend-api
      protocol: TCP
      port: 9000
      targetPort: backend-api
  selector:
    app.kubernetes.io/name: emqx-backend-api

  type: NodePort

---
kind: ConfigMap
apiVersion: v1
metadata:
  name: emqx-backend-api
  namespace: emqx-ee

  labels:
    app.kubernetes.io/name: emqx-backend-api
data:
  application.yml: |-
    spring:
      application:
        name: sdes-api
    ---
    spring:
      datasource:
        url: jdbc:mysql://10.95.35.226:3306/sdes_asia?useUnicode=true&characterEncoding=utf-8
        username: u_sdes_asia
        password: n^vSUb6MAM
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: com.mysql.cj.jdbc.Driver
      mvc:
        view:
          prefix: classpath:/templates/
          suffix: .html
      thymeleaf:
        cache: false
      devtools:
        restart:
          enabled: true
          exclude: static/**,templates/**
        livereload:
          enabled: true
        remote:
          debug:
            enabled: true
      http:
        encoding:
          charset: UTF-8
          enabled: true
          force: true
      output:
        ansi:
          enabled: always
    mybatis:
      mapper-locations: classpath*:mapper/**/*.xml
      type-aliases-package: cn.xiaohuodui.model
    server:
      port: 9000
    logging:
      level:
        root: info
    sdes:
      baseUrl: http://10.95.35.93:33816
      token: Basic YWRtaW46SiNpMiZEYmZjIW9k
~~~
Note that you need to modify the jdbc-related configuration information and sdes-related configuration information in `confingmap`.

~~~yml
datasource:
url: jdbc:mysql://10.95.35.226:3306/sdes_asia?useUnicode=true&characterEncoding=utf-8
username: u_sdes_asia
password: n^vSUb6MAM
~~~

The configuration here needs to be changed to the corresponding MySQL address, user name, password and other information that are the same as those on EMQX.

At the same time, you need to modify the relevant information of the sdes configuration item.

~~~yml
sdes:
baseUrl: http://10.95.35.93:33816
   token: Basic YWRtaW46YWRtaW4=
~~~

Here, the baseUrl address is the EMQX Dashboard address, and token is its authentication information. If the password needs to be changed, it needs to be modified.