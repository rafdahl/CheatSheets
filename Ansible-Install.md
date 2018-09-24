### Purpose
Install kubernetes on 4 VM's, 1 Master and 3 Nodes or minions.


#### This install will have 1 master and 3 minions (nodes)
- Kube-master
- Kube-node1
- Kube-node2
- Kube-node3

#### On the master and all the nodes make sure we are using the same time zone
`# timedatectl set-timezone America/Phoenix`

`# timedatectl`

#### Verify time services are running, either chronyd or ntpd. I will use chronyd since it is installed with the initial install
`# chronyc tracking`

#### Update the /etc/hosts file with all the nodes and master of each one
```
192.168.0.223   kube-master
192.168.0.224   kube-node1
192.168.0.225   kube-node2
192.168.0.226   kube-node3
```

#### Now we need to add the docker repo to each of the nodes and master. On **each machine**  edit the following file
`# vi /etc/yum.repos.d/virt7.docker-common-release.repo`

**Add the following**
```
[virt7-docker-common-release]
name=virt7-docker-common-release
baseurl=http://cbs.centos.org/repos/virt7-docker-common-release/x86_64/os/
gpgcheck=0
```

#### Now run yum update
`# yum update -y`

#### Make sure we are not running firewalld or iptables

`# systemctl status firewalld`

`# systemctl status iptables`


#### On our boxes firewalld was running so we need to stop is and disable it from starting at bood
`# systemctl stop firewalld`

`# systemctl disable firewalld`

#### Now we are going to enable the new repo and install kubernetes and docker
`# yum install -y --enablerepo=virt7-docker-common-release kubernetes docker`


#### Now we need to configure the master and the nodes


## MASTER NODE

#### Install etcd service
`# yum install -y etcd`


#### On the master edit the /etc/kubernetes/config file
`# vi /etc/kubernetes/config`

#### ADD or MODIFY the following lines:
```
KUBE_MASTER="--master=http://kube-master:8080"                          <-- modified
KUBE_ETCD_SERVERS="--etcd-servers=http://kube-master:2379"      <-- added
```

#### Now edit the etcd file
`# vi /etc/etcd/etcd.conf`
```
MODIFY the following lines
ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://0.0.0.0:2379"
```
#### Now we need to edit the episerver
`# vi /etc/kubernetes/apiserver`

#### MODIFY
```
KUBE_API_ADDRESS="--address=0.0.0.0"
```

#### UNCOMMENT lines
```
KUBE_API_PORT="--port=8080"
KUBELET_PORT="--kubelet-port=10250"
```
#### COMMENT the line
```
# KUBE_ADMISSION_CONTROL="--admission-control=NamespaceLifecycle,NamespaceExists,LimitRanger,SecurityContextDeny,ServiceAccount,ResourceQuota"
```

#### Now we need to enable and start our services NOTE: MUST BE IN THIS ORDER
`# systemctl enable etcd kube-apiserver kube-controller-manager kube-scheduler`

`# systemctl start etcd kube-apiserver kube-controller-manager kube-scheduler`

#### Verify all 4 services are running
`# systemctl status etcd kube-apiserver kube-controller-manager kube-scheduler | grep "(running)" | wc -l`


## NODES

#### On each node
`# vi /etc/kubernetes/config`

#### ADD or MODIFY the following lines
```
KUBE_MASTER="--master=http://kube-master:8080"                            <-- modified
KUBE_ETCD_SERVERS="--etcd-servers=http://kube-master:2379"      <-- added
```

`# vi /etc/kubernetes/kubelet`

### MODIFY and/or UNCOMMENT lines
```
KUBELET_ADDRESS="--address=0.0.0.0"
KUBELET_PORT="--port=10250"
KUBELET_HOSTNAME="--hostname-override=kube-node1"              <-- match node name
KUBELET_API_SERVER="--api-servers=http://kube-master:8080"
```
#### COMMENT the line
```
# KUBELET_POD_INFRA_CONTAINER="--pod-infra-container-image=registry.access.redhat.com/rhel7/pod-infrastructure:latest"
```

#### Now we need to enable and start the 3 services
`# systemctl enable kube-proxy kubelet docker`

`# systemctl start kube-proxy kubelet docker`

`# systemctl status kube-proxy kubelet docker | grep "(running)" | wc -l`














