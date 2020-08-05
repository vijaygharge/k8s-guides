# k8s-guides
apt update # Update APT as first step

apt install -y sshpass

apt install ansible -y

apt install ansible-doc -y

ssh cloud_user@$IP OR disable strict_host_key_checking functionality 


# Steps to Install Docker manually over ubuntu systems

apt-get update && apt-get install -y apt-transport-https ca-certificates curl software-properties-common gnupg2

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
  
apt-get install -y containerd.io docker-ce docker-ce-cli

cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF

mkdir -p /etc/systemd/system/docker.service.d

systemctl daemon-reload

systemctl restart docker

systemctl enable docker

# ELK on Docker 

docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk

