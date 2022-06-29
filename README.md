                                                    Cloud-DevOps-assignment
In this assigment I used the Microsoft Azure cloud resources to carry out the operations that I was required to carry out.
                                      This is the workflow diagram of the assisgment

![DevOps workflow](https://user-images.githubusercontent.com/95041171/176384192-d75b2a9b-f089-4944-bf04-cd60397a200b.png)

Note: The Deployments and YAML pipelines that are screenshot in this writeup are in the repository, you can check them out.

                                                        Tools used:

Git and Azure Git Repos – Source Code Management and Version control system

Docker – Application Containerization system

Azure Container Registry – Managing container images

DockerHub - Sharing container images

Azure Kubernetes Service - Managed container workloads and services

Azure Pipeline - Continuous Integration (CI) and Continuous Delivery (CD)

Datadog – Metrics collection and monitoring.

                                               React-and-Spring-data-rest
Deploy a pipeline to build, test and push the docker image to Azure Container Registry.

As requested, that the pipeline should build, test and push the docker image to a repository. The pipeline built and pushed the Docker images (Front-end and Back-end) to Azure Container Registry known as abimbolacontainerregistry as seen below.


The pipeline below built and pushed the front-end Docker image to the Azure Container Registry.

![image](https://user-images.githubusercontent.com/95041171/176218164-c6f01fbb-b1aa-4e2a-a8e6-22cc5cca407a.png)

The Docker image for the front-end app was successfully built and pushed to the Azure Container Registry as seen in the screenshot below

![image](https://user-images.githubusercontent.com/95041171/176218247-b0470515-6680-4bb2-a3ff-a31c2c3c396b.png)

The Docker image is in the Azure repository, the image could also be pushed to DockerHub and other container image repositories.
The pipeline below built and pushed the back-end Docker image to the Azure Container Registry

![image](https://user-images.githubusercontent.com/95041171/176218488-f0b214fc-7a03-4ae7-afbd-9a84ab4626ed.png)

The Docker image for the back-end app was successfully built and pushed to the Azure Container Registry as seen in the screenshot below

![image](https://user-images.githubusercontent.com/95041171/176218633-5e0ff1f0-4950-40c4-bf02-d7425a621075.png)

The Docker images can be seen in the repository.

![image](https://user-images.githubusercontent.com/95041171/176218763-1f20d00f-548a-4a36-8598-bb8315588477.png)

                           Deploy the infrastructure using Infrastructure as Code (Terraform)
I understand that you would like the deployment pipelines to deploy the applications across different environments on the target infrastructure, however, we would first need to build the target infrastructure, in this assignment I would be using Terraform as the Infrastructure as Code (IaC) to deploy the target Infrastructure.

The target Infrastructure would be a Managed Service known as (Azure Kubernetes Service).
I used the below pipeline to deploy the Azure Kubernetes Service cluster

![image](https://user-images.githubusercontent.com/95041171/176219245-9cb5b43a-cec4-4bfb-9553-8d16fb79e0e6.png)

The Azure Kubernetes Service cluster screenshot can be seen below

![image](https://user-images.githubusercontent.com/95041171/176219350-002e3ca2-ab8a-493a-a62e-1b0719cd5126.png)

                    The next line of action is to deploy the applications across different environments on the target infrastructure
I created a secret for the imagepullsecret and MySQL database using the YAML file below. This was done from the terminal, this will allow authentication to the repository and the MySQL database.   

![image](https://user-images.githubusercontent.com/95041171/176220273-24bdab10-9123-43cc-9937-aba1d094df22.png)

                Deploying the front-end application using the frontend docker image in ACR, I used this YAML pipeline
                
![image](https://user-images.githubusercontent.com/95041171/176221267-2782b343-db06-4bdb-bf8e-aebe0346e017.png)

The front-end was successfully deployed

![image](https://user-images.githubusercontent.com/95041171/176221535-2921fe37-a848-44d3-8a7d-4850b6ec6f6b.png)

Front-end application is deployed to the Azure Kubernetes Cluster as seen below.

![image](https://user-images.githubusercontent.com/95041171/176221631-36684b92-8f4e-4e0a-927d-963de496b52c.png)

The front-end application can be accessed using the load balancer IP address and port 8080, in the deployment YAML file, there is a service that exposed the deployment with type=LoadBalancer

![image](https://user-images.githubusercontent.com/95041171/176221931-f4384cba-52bc-4c73-8f05-197a5d5297a9.png)

I created a scaling policy that makes the infrastructure scale automatically.

![image](https://user-images.githubusercontent.com/95041171/176222040-8029ca04-6ed8-4f9b-a89c-97457e6fccea.png)

When the CPUs of the nodes in the Kubernetes Cluster gets to 70% threshold for 10 minutes, the node scales out by 1 automatically, also, if the CPUs of the cluster get to below the average threshold, it scales down the nodes.

                                                  Deploying the back-end application
Before deploying the back-end application, I first deployed a storage class to the Kubernetes cluster, then created the persisted volume claim, lastly, I deployed the MySQL database to consume the persistent volume claim and ensure that the data in the database are persistent. Once this is done the back-end application would make use of the MySQL database.

See below Storage class and persistent volume claim YAML file

![image](https://user-images.githubusercontent.com/95041171/176222525-aef5ede6-f383-4147-b55d-4c12c411291f.png)

![image](https://user-images.githubusercontent.com/95041171/176222676-dfa4d253-613f-4af7-abe9-4edca17c86c9.png)

I deployed the Storage Class and Persistent Volume Claim from the terminal

                                            Deploying the MySQL database, I used this YAML pipeline
                                              
![image](https://user-images.githubusercontent.com/95041171/176222995-5fc99ab9-c8a4-4485-abff-289cf848236c.png)

Database created successfully

![image](https://user-images.githubusercontent.com/95041171/176223139-aafb9cce-78ab-4cab-989d-06e2030aa739.png)

MySQL database deployed to Kubernetes cluster as a deployment

![image](https://user-images.githubusercontent.com/95041171/176223230-94f25390-a5de-48fd-b898-e06e3ef6e87b.png)

Persistent volume claim to persist the data in MySQL database bound successfully

![image](https://user-images.githubusercontent.com/95041171/176223719-8dda8cad-e8fc-41a4-ae5a-ab9308ea03a1.png)

                                    Deploying the back-end application using the backend docker image in ACR, I used this YAML pipeline
                                    
![image](https://user-images.githubusercontent.com/95041171/176226299-99e18016-f0f6-41a2-98e5-2603b82eee95.png)

The MySQL environment variables was used to deploy the backend application as it can be seen in the YAML pipeline.

                                                 Monitoring the Infrastructure
                                                    
Datadog can help you get full visibility into your AKS deployment by collecting metrics, distributed request traces, and logs from Kubernetes, Azure, and every service running in your container infrastructure. To start monitoring AKS with Datadog, all you need to do is configure the integrations for Kubernetes and Azure. Deploy the containerized Datadog Agent as a DaemonSet within your AKS cluster using the Helm chart.

                                                         Install Datadog into Kubernetes using Helm chart

API_KEY="<YOUR DATADOG API KEY>"

helm repo add datadog https://helm.datadoghq.com

helm install datadog `
             --set datadog.site='datadoghq.com' `
             --set datadog.apiKey=$API_KEY `
             --set datadog.apm.enabled=true `
             datadog/datadog
  
The nodes in the kubernetes cluster can be seen below
  
![image](https://user-images.githubusercontent.com/95041171/176254896-57ed618d-28ab-4338-b132-fc1f8e1866b4.png)
  
The Datadog agent was deployed as a Daemonset, the agent can be seen in the Datadog portal

![image](https://user-images.githubusercontent.com/95041171/176255227-46dc737a-de07-41c0-81ad-02aef0607380.png)
  
The agents represent the node running in the Kubernetes cluster, once an agent is selected you will be able to see the properties of the node in the cluster as you can see in the below screenshot.
  
![image](https://user-images.githubusercontent.com/95041171/176255727-2ff1dc04-f262-4054-aadc-9c280aef7a91.png)

                                             Create a dashboard and start monitoring the cluster
  
![image](https://user-images.githubusercontent.com/95041171/176255980-3858c481-aaaa-4bf3-a6df-6b83a8d65c6f.png)
  
                                                 Terraform Pipeline to clean up the infastructure
  
![image](https://user-images.githubusercontent.com/95041171/176500723-e9bc60b1-04bc-4c23-ad1c-af72613cf601.png)
  
This is a Public repository, to fork kindly select FORK and you have it.

![image](https://user-images.githubusercontent.com/95041171/176508760-c4294b6a-b6f4-4f0f-9425-d0fc67f684f3.png)

  
Thank You


  


  
  

                                     

                    
 
