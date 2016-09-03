# Terraform

    resource "google_container_cluster" "cluster" {
      name = "terraform-cluster"
      zone = "europe-west1-d"
      initial_node_count = 3
    
      master_auth {
        username = "terraform"
        password = "crazyMasterPassword23"
      }
    
      node_config {
        oauth_scopes = [
          "https://www.googleapis.com/auth/compute",
          "https://www.googleapis.com/auth/devstorage.read_only",
          "https://www.googleapis.com/auth/logging.write",
          "https://www.googleapis.com/auth/monitoring"
        ]
      }
    }

# Download credentials

    gcloud container clusters get-credentials terraform-cluster -z europe-west1-d

# Deploy application using kubectl

   kubectl run terraform-node --image=centos/httpd:latest --port=80
   kubectl expose deployment terraform-node --type="LoadBalancer"
   kubectl get services terraform-node
   kubectl proxy
   kubectl delete service,deployment terraform-node

# An interesting blog post 
http://omerio.com/2016/01/02/getting-started-with-kubernetes-on-google-container-engine/

