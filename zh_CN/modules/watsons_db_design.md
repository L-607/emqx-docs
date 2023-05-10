# EMQX & Watsons SDES DB Design

MySQL 数据库为 SDES 平台提供数据支撑。数据库表设计完整 SQL 语句如下,可以直接在 MySQL 数据库导入执行此 SQL 语句。

~~~sql
/*!40101 SET NAMES utf8 */;
/*!40014 SET FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET SQL_NOTES=0 */;
DROP TABLE IF EXISTS actions_email;
CREATE TABLE `actions_email` (
  `action_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `message` varchar(2550) DEFAULT NULL,
  `to` varchar(2550) DEFAULT NULL,
  `subject` varchar(2550) DEFAULT NULL,
  `include_links` tinyint(1) DEFAULT '1' COMMENT '0 - not include 1 - include',
  `include_alert_details` tinyint(1) DEFAULT '0' COMMENT '0 - not include 1 - include',
  `include_event_details` tinyint(1) DEFAULT '0' COMMENT '0 - not include 1 - include',
  PRIMARY KEY (`action_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS actions_run_program;
CREATE TABLE `actions_run_program` (
  `action_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `path` varchar(2550) DEFAULT NULL,
  `arguments` varchar(2550) DEFAULT NULL,
  PRIMARY KEY (`action_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS actions_syslog;
CREATE TABLE `actions_syslog` (
  `action_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `message` varchar(2550) DEFAULT NULL,
  PRIMARY KEY (`action_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS admin;
CREATE TABLE `admin` (
  `admin_id` bigint NOT NULL AUTO_INCREMENT,
  `username` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NOT NULL COMMENT 'Administrator name',
  `encrypted_password` varchar(128) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NOT NULL COMMENT 'Password hash',
  `salt` varchar(64) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NOT NULL COMMENT 'Password salt',
  `ban` tinyint(1) NOT NULL DEFAULT '0' COMMENT '0 not banned 1 banned',
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Creation time',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT 'Whether to delete 0 means not deleted 1 means deleted',
  PRIMARY KEY (`admin_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci ROW_FORMAT=DYNAMIC COMMENT='管理账户';

DROP TABLE IF EXISTS alert_actions;
CREATE TABLE `alert_actions` (
  `alert_action_id` bigint NOT NULL AUTO_INCREMENT,
  `alert_id` bigint NOT NULL,
  `action_id` bigint NOT NULL,
  PRIMARY KEY (`alert_action_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS alert_events_criteria;
CREATE TABLE `alert_events_criteria` (
  `event_criteria_id` bigint NOT NULL AUTO_INCREMENT,
  `alert_id` bigint NOT NULL,
  `event_id` bigint NOT NULL,
  `alert_every_event` tinyint(1) DEFAULT '0',
  `occurrences` int DEFAULT NULL,
  `time_frame` int DEFAULT NULL COMMENT 'in minutes',
  `condition_operation` enum('EQUALS','NOT_EQUALS','CONTAINS','REGEX') DEFAULT 'EQUALS',
  `condition_subject` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`event_criteria_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS alerts;
CREATE TABLE `alerts` (
  `alert_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `severity` int DEFAULT NULL,
  `acknowledgement_required` tinyint(1) DEFAULT '0',
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  PRIMARY KEY (`alert_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS attributes;
CREATE TABLE `attributes` (
  `attribute_id` bigint NOT NULL AUTO_INCREMENT,
  `attribute_name` varchar(255) DEFAULT NULL COMMENT 'Attribute name',
  `type` tinyint DEFAULT NULL COMMENT '0 - custom 1 - sys',
  `default_value` varchar(255) DEFAULT NULL COMMENT 'Default value',
  `display` tinyint(1) DEFAULT '0' COMMENT '0 - not display 1 - display',
  `read_only` tinyint(1) DEFAULT '0' COMMENT '0 - not read only 1 - read only',
  PRIMARY KEY (`attribute_id`)
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS client_attributes;
CREATE TABLE `client_attributes` (
  `client_attribute_id` bigint NOT NULL AUTO_INCREMENT,
  `client_id` bigint DEFAULT NULL,
  `attribute_id` varchar(255) DEFAULT NULL COMMENT 'Attribute name',
  `attribute_value` varchar(255) DEFAULT NULL COMMENT 'Attribute value',
  PRIMARY KEY (`client_attribute_id`)
) ENGINE=InnoDB AUTO_INCREMENT=144 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS client_settings;
CREATE TABLE `client_settings` (
  `client_setting_id` bigint NOT NULL AUTO_INCREMENT,
  `auto_enable_new_clients` tinyint(1) DEFAULT '0' COMMENT '0 - not auto enable 1 - auto enable',
  PRIMARY KEY (`client_setting_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS clients;
CREATE TABLE `clients` (
  `client_id` bigint NOT NULL AUTO_INCREMENT,
  `mqtt_client_id` varchar(255) DEFAULT NULL COMMENT 'MQTT client id',
  `user_name` varchar(255) DEFAULT NULL COMMENT 'Client username',
  `enable` tinyint(1) DEFAULT '0' COMMENT '0 - disable 1 - enable',
  `status` enum('online','offline') DEFAULT NULL COMMENT 'Clinet status. Online or offline',
  `connected_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Client connected timestamp',
  `disconnected_at` timestamp NULL DEFAULT NULL COMMENT 'Client disconnected timestamp. NULL means client is online and never disconnected',
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Client created timestamp',
  `ip` varchar(255) DEFAULT NULL COMMENT 'Client IP Address',
  `role` enum('SERVER','STORE') NOT NULL DEFAULT 'STORE',
  PRIMARY KEY (`client_id`),
  UNIQUE KEY `mqtt_client_id` (`mqtt_client_id`)
) ENGINE=InnoDB AUTO_INCREMENT=3797 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS clients_jobs_cache;
CREATE TABLE `clients_jobs_cache` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `client_id` bigint NOT NULL COMMENT 'Client ID',
  `job_cache` mediumtext COMMENT 'Client Job Cache',
  `reload_boot_info` mediumtext CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci,
  PRIMARY KEY (`id`),
  UNIQUE KEY `cache_key` (`id`,`client_id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=107 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS condition_script;
CREATE TABLE `condition_script` (
  `condition_script_id` bigint NOT NULL AUTO_INCREMENT,
  `order` int NOT NULL,
  `file_path` varchar(1024) NOT NULL,
  `block` tinyint(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`condition_script_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS copy_file_script;
CREATE TABLE `copy_file_script` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `order` int DEFAULT NULL COMMENT 'Order',
  `file_path` varchar(255) DEFAULT NULL COMMENT 'File Path',
  `target_file_path` varchar(255) DEFAULT NULL COMMENT 'Target File Path',
  `block` tinyint(1) NOT NULL DEFAULT '0',
  `create_file_path` tinyint(1) NOT NULL DEFAULT '1',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS del_file_script;
CREATE TABLE `del_file_script` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `order` int DEFAULT NULL COMMENT 'Order',
  `file_path` varchar(255) DEFAULT NULL COMMENT 'File Path',
  `block` tinyint(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS events;
CREATE TABLE `events` (
  `event_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `category` enum('Admin','Job','Task','Client','System') DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `send_to_syslog` enum('true','false','use_category_default') DEFAULT NULL,
  `history_retention` int DEFAULT '0' COMMENT 'in days',
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  PRIMARY KEY (`event_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS exe_bat_script;
CREATE TABLE `exe_bat_script` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `order` int DEFAULT NULL COMMENT 'Order',
  `file_path` varchar(255) DEFAULT NULL COMMENT 'File Path',
  `duration` bigint DEFAULT NULL,
  `block` tinyint(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=15 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS file_transfer_script;
CREATE TABLE `file_transfer_script` (
  `recv_file_script_id` bigint NOT NULL AUTO_INCREMENT,
  `type` enum('SEND','RECV','BROADCAST','UPLOAD_TO_SERVER') NOT NULL,
  `order` int NOT NULL,
  `max_retry_time` int NOT NULL,
  `file_path` varchar(1024) NOT NULL,
  `target_file_path` varchar(1024) NOT NULL,
  `create_file_path` tinyint(1) NOT NULL DEFAULT '0',
  `ignore_hidden_file` tinyint(1) NOT NULL DEFAULT '0',
  `transfer_operation` varchar(1024) DEFAULT NULL,
  `is_item` tinyint DEFAULT '0',
  `compress_file` int NOT NULL DEFAULT '0',
  `block` tinyint(1) NOT NULL DEFAULT '0',
  `retry_times` int NOT NULL DEFAULT '4' COMMENT '重试次数',
  `retry_interval` int NOT NULL DEFAULT '20',
  `overwrite` enum('OVERWRITE','NOT_OVERWRITE','COMPARE_OVERWRITE') DEFAULT NULL,
  `groups` json DEFAULT NULL,
  PRIMARY KEY (`recv_file_script_id`)
) ENGINE=InnoDB AUTO_INCREMENT=81 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS general_settings;
CREATE TABLE `general_settings` (
  `general_setting_id` bigint NOT NULL AUTO_INCREMENT,
  `management_server_time_zone` varchar(255) DEFAULT NULL COMMENT 'Management server time zone',
  `communication_server_time_zone` varchar(255) DEFAULT NULL COMMENT 'Communication server time zone',
  `region` varchar(255) DEFAULT NULL COMMENT 'Region',
  `admin_timeout` int DEFAULT NULL COMMENT 'Admin timeout',
  PRIMARY KEY (`general_setting_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS groups;
CREATE TABLE `groups` (
  `group_id` bigint NOT NULL AUTO_INCREMENT,
  `group_name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '0' COMMENT '0 - disable 1 - enable',
  `type` tinyint DEFAULT NULL COMMENT '0 - static 1 - dynamic',
  `query_property` varchar(255) DEFAULT NULL,
  `query_operation` varchar(255) DEFAULT NULL,
  `query_value` varchar(255) DEFAULT NULL,
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `assignments_changed_at` timestamp NULL DEFAULT NULL,
  `membership_changed_at` timestamp NULL DEFAULT NULL,
  `last_refreshed_at` timestamp NULL DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`group_id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS groups_clients;
CREATE TABLE `groups_clients` (
  `group_client_id` bigint NOT NULL AUTO_INCREMENT,
  `group_id` bigint DEFAULT NULL,
  `client_id` bigint DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`group_client_id`)
) ENGINE=InnoDB AUTO_INCREMENT=15 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS if_conditions;
CREATE TABLE `if_conditions` (
  `if_conditions_id` bigint NOT NULL AUTO_INCREMENT,
  `if_script_id` bigint NOT NULL,
  `condition_script_id` bigint NOT NULL,
  `condition_script_type` enum('GET_FILE_STATUS') DEFAULT NULL,
  PRIMARY KEY (`if_conditions_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS if_false_script;
CREATE TABLE `if_false_script` (
  `if_false_script_id` bigint NOT NULL AUTO_INCREMENT,
  `if_script_id` bigint NOT NULL,
  `false_script_id` bigint NOT NULL,
  `false_script_type` enum('SEND_FILE','RECV_FILE','COPY_FILE','DELETE_FILE','EXECUTE_FILE','WAIT_FLAG_FILE') DEFAULT NULL,
  PRIMARY KEY (`if_false_script_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS if_script;
CREATE TABLE `if_script` (
  `if_script_id` bigint NOT NULL AUTO_INCREMENT,
  `order` int DEFAULT NULL,
  PRIMARY KEY (`if_script_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS if_true_script;
CREATE TABLE `if_true_script` (
  `if_true_script_id` bigint NOT NULL AUTO_INCREMENT,
  `if_script_id` bigint NOT NULL,
  `true_script_id` bigint NOT NULL,
  `true_script_type` enum('SEND_FILE','RECV_FILE','COPY_FILE','DELETE_FILE','EXECUTE_FILE','WAIT_FLAG_FILE') DEFAULT NULL,
  PRIMARY KEY (`if_true_script_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS job_execution_opts;
CREATE TABLE `job_execution_opts` (
  `job_execution_opt_id` bigint NOT NULL AUTO_INCREMENT,
  `job_id` bigint DEFAULT NULL,
  `priority` int DEFAULT NULL,
  `cycle_type` int NOT NULL DEFAULT '0' COMMENT '0 - not repeat 1 - day 2 - weeks 3 - months 4 - years',
  `execution_time` varchar(255) DEFAULT NULL COMMENT 'CRON',
  `max_retries` int DEFAULT NULL,
  `retry_wait` bigint DEFAULT NULL,
  `duration` bigint DEFAULT NULL COMMENT 'job执行时长，单位s',
  `max_curren_session` int DEFAULT NULL,
  PRIMARY KEY (`job_execution_opt_id`)
) ENGINE=InnoDB AUTO_INCREMENT=12 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS job_logs;
CREATE TABLE `job_logs` (
  `log_id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `status` varchar(255) NOT NULL COMMENT 'Status of the script result',
  `start_time` bigint NOT NULL COMMENT 'Start time of the script',
  `end_time` bigint NOT NULL COMMENT 'End time of the script',
  `now_time` bigint NOT NULL COMMENT 'Current time of the script',
  `job_id` bigint NOT NULL COMMENT 'Job ID',
  `task_id` bigint NOT NULL COMMENT 'Task ID',
  `script_id` bigint NOT NULL COMMENT 'Script ID',
  `order` int NOT NULL COMMENT 'Order of the script',
  `error_code` int DEFAULT NULL COMMENT 'Error code of the script',
  `error_message` varchar(255) DEFAULT NULL COMMENT 'Error message of the script',
  `mqtt_client_id` varchar(255) NOT NULL,
  `report_id` varchar(255) DEFAULT NULL,
  `script_type` enum('SEND_FILE','RECV_FILE','COPY_FILE','DELETE_FILE','EXECUTE_FILE','WAIT_FLAG_FILE','GET_FILE_STATUS','IF') DEFAULT NULL,
  PRIMARY KEY (`log_id`)
) ENGINE=InnoDB AUTO_INCREMENT=35 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS jobs;
CREATE TABLE `jobs` (
  `job_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `last_run_at` timestamp NULL DEFAULT NULL,
  `assignments_changed_at` timestamp NULL DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`job_id`)
) ENGINE=InnoDB AUTO_INCREMENT=75 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS jobs_clients;
CREATE TABLE `jobs_clients` (
  `job_client_id` bigint NOT NULL AUTO_INCREMENT,
  `job_id` bigint DEFAULT NULL,
  `client_id` bigint DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`job_client_id`)
) ENGINE=InnoDB AUTO_INCREMENT=33 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS jobs_groups;
CREATE TABLE `jobs_groups` (
  `job_group_id` bigint NOT NULL AUTO_INCREMENT,
  `job_id` bigint DEFAULT NULL,
  `group_id` bigint DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`job_group_id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS jobs_settings;
CREATE TABLE `jobs_settings` (
  `jobs_setting_id` bigint NOT NULL AUTO_INCREMENT,
  `enabled` tinyint(1) DEFAULT '0' COMMENT '0 - disable 1 - enable',
  `max_retries` int DEFAULT NULL,
  `retry_wait` int DEFAULT NULL,
  `max_concurrent_session` int DEFAULT NULL,
  PRIMARY KEY (`jobs_setting_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS jobs_tasks;
CREATE TABLE `jobs_tasks` (
  `job_task_id` bigint NOT NULL AUTO_INCREMENT,
  `job_id` bigint DEFAULT NULL,
  `task_id` bigint DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `create_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`job_task_id`)
) ENGINE=InnoDB AUTO_INCREMENT=19 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS statistics_log;
CREATE TABLE `statistics_log` (
  `statistic_log_id` bigint NOT NULL AUTO_INCREMENT,
  `data_type` int NOT NULL COMMENT '0-jobs; 1 onlineClient; 3-alerts;',
  `time` bigint DEFAULT NULL COMMENT '时间戳',
  `count` int DEFAULT NULL,
  `create_at` bigint DEFAULT NULL,
  PRIMARY KEY (`statistic_log_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='数据统计表';

DROP TABLE IF EXISTS task_script;
CREATE TABLE `task_script` (
  `task_script_id` bigint NOT NULL AUTO_INCREMENT,
  `task_id` bigint DEFAULT NULL,
  `script_id` bigint NOT NULL,
  `script_type` enum('SEND_FILE','RECV_FILE','COPY_FILE','DELETE_FILE','EXECUTE_FILE','WAIT_FLAG_FILE','GET_FILE_STATUS','IF','BROADCAST','UPLOAD_TO_SERVER') NOT NULL,
  PRIMARY KEY (`task_script_id`)
) ENGINE=InnoDB AUTO_INCREMENT=104 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS task_settings;
CREATE TABLE `task_settings` (
  `task_setting_id` bigint NOT NULL AUTO_INCREMENT,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `priority` int DEFAULT NULL,
  `disable_validation` tinyint(1) DEFAULT '1' COMMENT '0 - validate task result 1 - not validate task result',
  PRIMARY KEY (`task_setting_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS tasks;
CREATE TABLE `tasks` (
  `task_id` bigint NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `enabled` tinyint(1) DEFAULT '1' COMMENT '0 - disable 1 - enable',
  `priority` int DEFAULT NULL,
  `disable_validation` tinyint(1) DEFAULT '1' COMMENT '0 - validate task result 1 - not validate task result',
  `last_edited_at` timestamp NULL DEFAULT NULL,
  `last_run_at` timestamp NULL DEFAULT NULL,
  `assignments_changed_at` timestamp NULL DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`task_id`)
) ENGINE=InnoDB AUTO_INCREMENT=15 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

DROP TABLE IF EXISTS wait_flag_file_script;
CREATE TABLE `wait_flag_file_script` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary Key',
  `interval` bigint DEFAULT NULL COMMENT 'ms',
  `block` tinyint(1) NOT NULL DEFAULT '0',
  `order` int DEFAULT NULL COMMENT 'Order',
  `file_path` varchar(255) DEFAULT NULL COMMENT 'Watin Flag File Path',
  `time_out` int DEFAULT NULL COMMENT 'Time Out, in millisecond',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
~~~