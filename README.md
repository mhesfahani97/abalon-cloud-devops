# XaaS Task
## Task Designer
[Arash-Iranpak](https://www.linkedin.com/in/arash-iranpak)

## 0. Create Digitalocean Droplet
  - one droplet as master
  - one droplet as worker
  - one droplet as VPN
  - all of them should in same VPC network

## 1. Create Kubernetes Cluster
  - install containerd on worker and master
  - install k8s tools on worker and master
  - on master, initialize the control node(pay attention to change the --apiserver-advertise-address)
  - on worker, join it to cluster
  - on worker, `mkdir -p /mnt/data/postgres`(for kubernetes PV)
  - let master to connect gitlab container registry, kubectl create secret docker-registry gitlab-registry --docker-server=<fill-it> --docker-username=<fill-it> --docker-password=<fill-it> --dry-run=client -o yaml > gitlab-secret.yml

## 2. Containerization
  - develop a python app
  - write a dockerfile

## 3. Kubernetes Manifests
  - postgresql
  - python application
  - monitoring
    - [create-slack-channel](app.slack.com)
    - [create-new-app](api.slack.com)
    - active incoming webhook
    - copy webhook url and channel in to alerting configmap
  - nginx
### helpful resources
[monitoring](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/)  
[nginx](https://dev.to/thenjdevopsguy/creating-a-custom-resource-definition-in-kubernetes-2k7o)

## 4. Gitlab
  - install gitlab community edition
  - install kubectl on gitlab server
  - connect gitlab to kubernetes cluster
    - create a k8s-connection project
      - create an agent `.gitlab/agents/k8s-connection/config.yaml`
      - connect gitlab to kubernetes cluster
  - create a new project `xaas`
    - create three runner(shell)
      - runner1 with dev tag
      - runner2 with prod tag
      - runner3 without tag
    - create `dev` and `prod` environments
    - write a .gitlab-ci.yml file
    - create variable in gitlab UI `PPF=/run/secrets/db-password`
      
## 5. VPN
  - install openvpn server and create client by this [script](https://github.com/angristan/openvpn-install)
  ```
  curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh
  chmod +x openvpn-install.sh
  ./openvpn-install.sh
  ```
  - use client.ovpn!
### helpful resources
[openvpn-kuber-pod!](https://bugraoz93.medium.com/openvpn-client-in-a-pod-kubernetes-d3345c66b014)  
[digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-an-openvpn-server-on-ubuntu-20-04#step-13-installing-the-client-configuration)
