# kubernetes-learn
Playground with Kubernetes (k8s) in Docker Desktop and real GCP account

## Kubernetes cluster in docker-desktop
Basically, after installing docker, we go to Docker Desktop settings and enable kubernetes there

1. Download & install docker, enable kubernetes settings
2. Download & install gcloud and kubectl (for this scope, no gcloud needed, but we will keep it here)
https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl
3. Check what contexts available: `kubectl config get-contexts`
4. Tell k8s to use docker-desktop cluster: `kubectl config use-context docker-desktop`
5. Check current context: `kubectl config current-context`
6. Check actually where config parameters are stored: `cat ~/.kube/config`
7. Run `kubetcl apply -f app.yml`. You should see deployment and service are created.
8. Open `localhost:4444`, you should see the website is accessible
9. Check how the deployment is set up by some kubectl commands: 
```
kubetcl get pods
kubetcl get services
kubectl get deployments

kubetcl describe pods
kubetcl describe services
kubectl describe deployments
```
10. Demo video: https://youtu.be/H9wOCqDeuug

Note that k8s/gcloud have concepts here that might look confused: cluster, namespace, context, node.
Asking bard.google.com is what I normally do to understand each of them and the differences. Fairly quick.


## Kubernetes cluster in real gcp account
Note that I choose the default region for my gcp account is `asia-southeast1`

1. Login gcloud: `gcloud login`. Note that here you will have to fill in a payment method
2. Create a project in Google Cloud console https://console.cloud.google.com/
3. Under Kubernetes Engine tab, create a new autopilot cluster (for quickstart with auto setup from gcp)
4. See list projects: `gcloud projects list`
5. Select a project to be active on: `gcloud config set project hello-world-project-390209` (replace to your project nme)
6. See list clusters: `gcloud container clusters list`
7. Generate a link to kubeconfig for this cluster: `gcloud container clusters get-credentials autopilot-cluster-1 --region=asia-southeast1`
8. Check it: `cat ~/.kube/config`
9. Change current context of kubernetes to this new cluster: `kubectl config set-context gke_hello-world-project-390209_asia-southeast1_autopilot-cluster-1`
10. Run `kubetcl apply -f app.yml`. You should see deployment and service are created.
11. Open `http://34.143.203.89`, you should see the website is accessible. The IP here can be taken from the tab "Kubernetes Engine > Service & Ingress" in Google Cloud console  
12. In the Google Cloud console, delete your cluster.
13. Demo video: https://youtu.be/A8En5SjZ17c

# License
MIT. See more at LICENSE file.
