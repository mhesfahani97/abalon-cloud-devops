# On Kubernetes cluster do these

0. Create Digitalocean Droplet
  - one droplet as master
  - one droplet as worker

1. Create Kubernetes Cluster
  - install containerd on worker and master
  - install k8s tools on worker and master
  - on master, initialize the control node(pay attention to change the --apiserver-advertise-address)
  - on worker, join it to cluster
  - on worker, `mkdir -p /mnt/data/postgres`(for kubernetes PV)
  - let master to connect container registry, kubectl create secret docker-registry gitlab-registry --docker-server=<fill-it> --docker-username=<fill-it> --docker-password=<fill-it> --dry-run=client -o yaml > gitlab-secret.yml

2. Containerization
  - develop a python app
  - write a dockerfile

3. Kubernetes Manifests
  - postgresql
  - python application
  - monitoring
    - [create-slack-channel](app.slack.com)
    - [create-new-app](api.slack.com)
    - active incoming webhook
    - copy webhook url and channel in to alerting configmap
  - nginx
## helpful resources
[monitoring](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/)
4. Gitlab

