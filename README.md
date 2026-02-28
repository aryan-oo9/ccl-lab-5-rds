# Cloud Computing Lab 5: AWS RDS Deployment

## 1. Database Deployment Steps (AWS RDS)
* Navigated to the Amazon RDS Console and clicked **Create database**.
* Selected **MySQL** as the database engine and the Free Tier template (db.t3.micro).
* Configured the Master username as `admin` and set a secure Master password.
* Under Connectivity, selected the Lab 4 VPC and created a new Security Group (`rds-gitea-sg`).
* Disabled "Public access" to ensure the database is isolated within the VPC.
* Launched the database and copied the Endpoint URL.

## 2. Database Connection Steps (Gitea on EC2)
* SSH'd into the running Lab 4 EC2 instance.
* Opened the Gitea configuration file using `sudo nano /etc/gitea/app.ini`.
* Modified the `[database]` section to replace the local SQLite configuration with the new RDS credentials:
  * `DB_TYPE = mysql`
  * `HOST = gitea-db.c7wsy8w8kd6m.eu-north-1.rds.amazonaws.com:3306`
  * `NAME = gitea`
  * `USER = admin`
* Saved the file and restarted the application using `sudo systemctl restart gitea`.
* Verified the connection by loading the Gitea web interface and successfully performing CRUD operations.
