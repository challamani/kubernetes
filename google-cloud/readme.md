* Install gcloud utility
* gcloud components install kubectl
* gcloud config set project [PROJECT#]
* gcloud config set compute/zone us-central1-b
* gcloud container clusters create [CLUSTER_NAME] --num-nodes=3
* gcloud container clusters delete [CLUSTER_NAME]
* gcloud container clusters describe [CLUSTER_NAME]
* docker build -t gcr.io/${PROJECT_ID}/app-name:v1 . (build image in local machine)
* gcloud docker -- push gcr.io/${PROJECT_ID}/app-name:v1
* gcloud compute ssh <node-logical-name>
