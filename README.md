## Description

### [App]

- Dockerfile -> lighter than a CokeZero with 0 vulnerabilities as scanned on Snyk, size 25mb
- requirements.txt -> python dependencies
- print_timestamp.py -> original code supplied 
- main.py -> my Python code, this is a basic Flask Python app that launches a subprocess every time the function is called at the / of the webpage
I included two other functions that return HTTP response 200 and 500 for the @app.route just so I can generate more replies for the integrated load tester and the Grafana dashboard.(more on that in just a sec!)
Also introduced a library needed for exporting the metrics from the Flask application to a Prometheus instance. 

###  [Generator]
- generate_events.py -> script that picks at random endpoints and keeps sending requests for generating load for testing autoscaling
- Dockerfile -> just another Dockerfile, 0 vulnerabilities, size 25mb
- requirements.txt -> python dependencies

### [Grafana]
- grafana config & dashboard files

### [Helmchart]
- Helm chart for deploying with Helm. 

### [Manual_gke_provisioning]
- Collection of yaml files that can be applied with kubectl -f . for a working cluster in GKE.

### [Prometheus]
- Prometheus and its config file

### [Terraform]
- Will create a separate VPC and separate subnets for the Kubernetes cluster, create the K8 cluster and deploy the Helm chart
- Will create a two node cluster with machine type: n1-standard-1
- Requires helm, terraform, gcloud SDK and a service account key (json) with enough privileges. 

### [LINKS]
The GKE cluster will expose the Grafana dashboard and the Flask application at these links:
- GRAFANA = http://lb-ip:3000/d/_eX4mpl3
- FLASK = http://lb-ip:5000/

### [Notes]
- Prometheus nor Grafana have any persistent volume claims, I would attach an NFS share in production for this. 
- All K8 deployments come with ConfigMaps defined
- Cluster monitoring is possible as well but wasn't mentioned under bonus objectives, at the same time a deployment on GKE has observability by default. 
- Default namespace used
- If you want to spin it locally all you have to do is docker-compose up
- Prototyped everything on GCP
- HPA autoscaling is configured in all deployment scenarios (manual, helm or terraform)
- Edit terraform.tfvars for declaring your GCP project and region


### [Pics]
![monitoring](https://github.com/AlexTzk/pythontime-to-simple-http/assets/138780223/2f503e44-e2b9-4d78-b158-958ef51e0ed8)

