Instance used Amazon Linux 2 with t2.medium and 25 Gig storage

	Use the following command to update the current OS
	
		sudo yum update -y


	Copy and install the latest stable build for kubectl

		curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

		curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

		echo "$(<kubectl.sha256)  kubectl" | sha256sum --check

		sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
		
	
	Copy and install minikube

		curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

		sudo install minikube-linux-amd64 /usr/local/bin/minikube
		
		
	Install docker and have it setup to automatically start up even after reboot

		sudo yum install docker -y

		sudo usermod -a -G docker ec2-user
		
		sudo systemctl enable docker.service

		sudo systemctl start docker.service


	Install conntrack

		sudo yum install conntrack -y
		
		
	Start minikube

		minikube start --vm-driver=none


	Install git
	
		sudo yum install git

	
	Clone files from repository
	
		git clone https://github.com/KrishAcu/3TierApp.git


	Change directory and launch application
	
		cd 3TierApp/

		kubectl apply -f mongo-config.yaml

		kubectl apply -f mongo-secret.yaml

		kubectl apply -f mongo.yaml

		kubectl apply -f webapp.yaml


	Access the web application via web browser
	
		Public IPv4 address:30100

