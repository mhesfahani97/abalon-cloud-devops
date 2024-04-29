# what is arcitecture

## kubernetes cluster(production)

0. Infrastructure
  - using digitalocean droplets(4G RAM & 2 CPU)
    - master node
    - worker node

1. initializing nodes for creating cluster
  - installing container runtime on each node
    - IPV4 packet forwarding
    - containerd
    - runc
    - CNI
  - kubernetes tools
    - kubectl
    - kubelet
    - kubeadm
  - podnetwork
    - calico
  - apiserver-advertise-address
    - master node VPC network IP address

2. microservices on kubernetes cluster
  - database
    - postgresql
    - replication(not done)
    - backup(not done)
  - python app
  - monitoring
    - prometheus
      - monitoring ns, daemonset, 
      - rbac (get, list, and watch permissions to nodes, services endpoints, pods, and ingresses.)
      - configmap (alerting rules + prometheus main config)
      - deployment, and nodeport service
    - kubestate metrics (monitor all your kubernetes API objects like deployments, pods, jobs, cronjobs etc)
    - node exporter
      - daemonset, service
    - alerting
      - configmap, deployment, service, template-configmap, and slack
    - grafana
      - configmap, deployment, and nodeport service
  - webserver
    - nginx
      - webserver ns, service, deployment, hpa

## python app
  - app.py
  - containerization
    - dockerfile

## gitlab server(staging)
  - install gitlab community edition
  - install docker for compose file
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

## VPN
  - using openvpn on server side and client
