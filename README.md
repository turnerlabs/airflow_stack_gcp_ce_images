# What is this?

**Major Wip**

**Since Google now has composer, this has been shelved but I didn't want to lose what I've done**

Tentative plans below but not implemented....

**Support version 1.10.x of Airflow**

This contains the packer code to create the AMI's for the Webserver / Scheduler(combined) and the Worker for Airflow.

The airflow_websched path contains the code to generate a python 3.x(latest on Ubuntu 16.04) AMI of an airflow webserver and scheduler that works with Airflow.

The airflow_worker path contains the code to generate a python 3.x(latest on Ubuntu 16.04) AMI of an airflow worker that works with Airflow.

The airflow AMI's also have the following additions / assumptions:

- AIRFLOW_HOME is /home/ubuntu/airflow
- Python uses a virtual environment that can be activated by `source ~/venv/bin/activate`
- S3 fuse will be used to mount airflow home directory
- Task logs will be sent to S3 bucket using settings in Airflow config
- Airflow service logs are located at /home/ubuntu/airflow/logs(and in S3 via fuse mount)
- The logs are being pushed to cloudwatch logs for easier viewing as well
- The logs are being zipped every hour(and removed every 24 hours) via crontab using logrotate.
- The services are using systemd services so you can stop and start the 3 services as follows:
  - `systemctl stop airflow-webserver`
  - `systemctl stop airflow-scheduler`
  - `systemctl stop airflow-worker`
