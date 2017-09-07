
0# osx-commands
usefull osx commands

## set input volume for mic in osx to fixed value ( no auto adjust )
`while sleep 2; do osascript -e "set volume input volume 50"; done`

# WSL ubuntu
## intellij run gui
xming

`sudo apt-get install libxtst6`

`sudo apt-get install libxi6`

`sudo updatedb`

`export DISPLAY=:0`

# linux-commands

## SSH
add ssh key to the agent to not type pasphrase every time
```
ssh-add ~/.ssh/id_rsa
```

check server fingerprints
```
ssh-keygen -lf <(ssh-keyscan serverhost 2>/dev/null)
```

## tunnel ports from remote host to your local machine
port on remote host is 9000 local host port is 9090

`ssh -L 9090:host_name:9000 user@host_name`

for non interactive mode use

`ssh -NL 9090:host_name:9000 user@host_name`

or

`ssh -NL 9090:localhost:9000 user@host_name`

for many tunnels to single host use 

`ssh -NL 9090:localhost:9000 -L 9091:localhost:9001 user@host`

## easy fire wall
```
apt-get install ufw
ufw default deny
ufw allow ssh
ufw allow http
ufw enable
```
# minikube/kubectl

## add new cluster to config
after adding to bashrc `k8s_merge.sh`
```
kmerge kubeconfig_file_from_provider
```

## remove cluster config from contexts
```
kubectl config unset users.user_name
kubectl config unset contexts.context_name
kubectl config unset clusters.cluster_name
```

## install package in alpine linux
```
apk update
apk add package_name
```

## debug k8s init commands in containers
```
kubectl logs po/pod_name -c command_name
```

## scale rc
```
kubectl scale --replicas=3 rc/name_here
```

## deletet rc
```
kubectl delete rc name_here
```

## get kubernetes nodes with labels
```
kubectl get nodes --show-labels
```

## set label on kubernetes node
```
kubectl label nodes node_name label=value
```

## delete label on kubernetes node
```
kubectl label nodes node_name label-
```

## get prompt on pod
```
kubectl exec -it pod-name -- /bin/bash
```

## configure kubectl to use gcloud
```
gcloud container clusters get-credentials cluster_name --zone zone
```

## kubectl add ssl certificate
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=foo.com"
kubectl create secret tls foo-secret --key /tmp/tls.key --cert /tmp/tls.crt
```

## kubectl port forwarding
```
kubectl port-forward kibana-0 5601:5601
```

## kubectl get env variable
```
kubectl exec -it core-admin-0 -- printenv | grep 'VAR_NAME'
```

## update k8s deployment with changes from file
```
kubectl apply -f file.yaml
```

## static IP on GCE
```
gcloud compute addresses create ip-name --global
gcloud compute addresses describe ip-name --global
```

# Docker

## remove everything
```
docker system prune --all --force --volumes
```

## delete local docker images to clear cache
```
docker rmi -f $(docker images -a -q)
```

## delete all stopped docker containers
```
docker rm $(docker ps -a -q)
```

## connection form container to container
```
docker network create mynet
docker run --name foo --net mynet img
docker run --name bar --net mynet img
```

## run docker image in interactive mode
```
docker run -it openjdk:8-jre-alpine /bin/sh
```

## "ssh" into container
```
docker exec -it container_name /bin/sh
```

## get container IP
```
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name 
```

# Kafka

## create topic
```
kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic topic_name
```

## list all topics
```
kafka-topics.sh --list --zookeeper localhost:2181
```

## send messages
```
kafka-console-producer.sh --broker-list localhost:9092 --topic topic_name
```

## get messages from offset 0
```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic_name --from-beginning
```

## get info about topic
```
kafka-topics.sh --zookeeper localhost:2181 --describe --topic topic_name
```

# Others

## pretty print Akka members json in bash
```
curl akka:19999/members | python -m json.tool
```

## ssh
```
.ssh/config
AddKeysToAgent yes
```
```
chmod 600 .ssh/config
```
```
.zshrc
if [ -z $SSH_AGENT_PID ]; then  # if no agent & not in ssh
    eval `ssh-agent -s`
fi
```
or with oh my zsh
```
plugins=(git ssh-agent)
```

## spacemacs
```
sudo update-alternatives --config editor
```
```
.spacemacs
dotspacemacs-mode-line-unicode-symbols nil
```

## create folder with name set to current date
```
mkdir `date +'%d-%m-%Y'`
```

## install mosh
```
sudo apt-get install software-properties-common
sudo apt-get install mosh

export LANGUAGE=pl_PL.UTF-8
export LANG=pl_PL.UTF-8
export LC_ALL=pl_PL.UTF-8
locale-gen pl_PL.UTF-8
sudo dpkg-reconfigure locales
```

## Create new go lang module
```
go mod init hello
go build
```

## Parse json with unix cmd
```
curl -sS "https://api.convertkit.com/v3/subscribers?api_secret=SECRET_HERE" | python -c "import sys, json; print json.load(sys.stdin)['total_subscribers']"
```

## use sed to remove \n from file
```
sed -e ':a' -e 'N' -e '$!ba' -e 's/\n//g' file_name
```
