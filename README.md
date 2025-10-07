��� Jenkins + Ansible + Prometheus + Grafana Monitoring Stack (Docker Compose Setup)
This repository provides a containerized DevOps monitoring environment using Docker Compose.
It includes:

Jenkins for CI/CD pipelines
Ansible for configuration management
Prometheus for metrics collection
Grafana for visualization
Node Exporter for system metrics
���️ Folder Structure
. ├── docker-compose.yml ├── Dockerfile.jenkins ├── Dockerfile.ansible ├── Dockerfile.prometheus ├── Jenkinsfile ├── plugins.txt ├── prometheus/ │ └── prometheus.yml ├── grafana/ │ ├── provisioning/ │ │ ├── dashboards/ │ │ │ └── dashboard.yaml │ │ └── datasources/ │ │ └── prometheus.yml │ ├── dashboards/ │ │ ├── node_exporter.json │ │ └── jenkins_metrics.json │ └── datasources/ │ └── prometheus.yaml └── ansible/ ├── playbook.yml └── inventory

⚙️ Components Overview
Service Port    Description
Jenkins 8080    CI/CD automation server
Jenkins Agent   50000   Agent communication port
Ansible N/A Used for configuration & automation tasks
Prometheus  9090    Metrics collection & monitoring
Grafana 3000    Data visualization (Default login: admin/admin)
Node Exporter   9100    Host system metrics exporter
��� Setup & Run
1️⃣ Clone the Repository
git clone https://github.com//.git cd

2️⃣ Build and Start Containers docker-compose up -d --build

3️⃣ Verify Running Containers docker ps

Expected running containers: jenkins, ansible, prometheus, grafana, node_exporter

��� Jenkins Setup Access Jenkins: http://localhost:8080

Initial Admin Password Execute below command docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword

Then log in to Jenkins UI → install suggested plugins.

Enable Prometheus Plugin In Jenkins, go to Manage Jenkins → Manage Plugins Install Prometheus Metrics Plugin Then navigate to Manage Jenkins → Configure System → Prometheus Enable the checkbox “Enable metrics”

The endpoint will be available at: http://localhost:8080/prometheus

Access Prometheus UI: ��� http://localhost:9090

��� Grafana Configuration Grafana is pre-provisioned with:

Prometheus as data source Dashboards for Jenkins and Node Exporter

Access Grafana: ��� http://localhost:3000

Default Credentials: Username: admin Password: admin

Once logged in: Navigate to Dashboards → Manage Select Jenkins Metrics or Node Metrics dashboard

��� Ansible Container The Ansible container is available for automation testing.

Connect to it: docker exec -it ansible bash Run sample playbook:

ansible-playbook -i inventory playbook.yml ��� Stopping the Stack

To stop all containers: docker-compose down

To rebuild cleanly: docker-compose down -v --remove-orphans docker-compose up -d --build

��� Notes & Best Practices Jenkins container uses host Docker via mounted socket:

/var/run/docker.sock:/var/run/docker.sock This enables Jenkins to build Docker images on the host. Do not push volume data folders to GitHub (see .gitignore). Make sure your host Docker daemon is running before starting Jenkins.
✅ Troubleshooting Issue Possible Fix Jenkins not loading Wait 1–2 minutes after startup; it initializes plugins Prometheus not scraping Jenkins Ensure /prometheus endpoint is enabled and reachable from Prometheus Grafana dashboards empty Check if data source (Prometheus) is connected properly Port conflict Stop any other local Jenkins, Prometheus, or Grafana instances

��� License This project is open-source and can be freely used for DevOps learning and demonstration purposes.

��� Author Vishnu Sharma DevOps Engineer | Automation & Monitoring Enthusiast ��� Mumbai, India
