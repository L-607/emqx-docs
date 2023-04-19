# EMQX & Watsons SDES Script - CopyFile

## Function Explanation
## Configuration method
The main process is: Add Job--->Add Task--->Edit Script
## Demo Screenshot
add job
![set_job_1](./assets/sdes/set_job_1.png)
To configure the relevant configuration items of Job, you need to configure `Job Start Times` `Priority` `Max Retries` `Retry Wait` etc.
![set_job_2](./assets/sdes/set_job_2.png)
![set_job_3](./assets/sdes/set_job_3.png)
After configuring the Job, add and configure the Task. After the Task is added successfully, select Add Job and select the created Job just now.
![task_add_job](./assets/sdes/task_add_job.png)
![select_job](./assets/sdes/select_job.png)
Then you need to configure the script, set `Target Path` and `File Path`.
![add_script_1](./assets/sdes/add_script_1.png)
![add_script_2](./assets/sdes/add_script_2.png)