# kubernetes-installation

On All nodes

•	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
•	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
•	curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
•	cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
•	sudo apt-get update
•	sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.12.2-00 kubeadm=1.12.2-00 kubectl=1.12.2-00
•	sudo apt-mark hold docker-ce kubelet kubeadm kubectl
•	echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf

On Master Node
•	sudo kubeadm init --pod-network-cidr=10.244.0.0/16
•	mkdir -p $HOME/.kube
•	kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml

On Slave Node
•	sudo kubeadm join $controller_private_ip:6443 --token $token --discovery-token-ca-cert-hash $hash
#hash - is the one displays when creating flannel

