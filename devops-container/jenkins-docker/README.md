docker build -t my-jenkins .


kind create cluster --config kind.yaml

docker pull jenkins/jenkins:lts-jdk17
docker run -d --name jenkins --network kind -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk17


docker pull sonarqube:latest
docker run -d --name sonarqube --network kind -p 9000:9000 sonarqube:lts-community


docker pull sonatype/nexus3
docker run -d --name nexus --network kind -p 8081:8081 sonatype/nexus3:latest


\\ This command uses Go templating to format the output of docker inspect. It iterates over the Networks map, printing the network name ($network) and the corresponding IP address ($details.IPAddress)

docker inspect -f '{{.Name}} - {{range $network, $details := .NetworkSettings.Networks}}{{$network}}: {{$details.IPAddress}} {{end}}' $(docker ps -aq)

/nexus - kind: 172.20.0.7
/sonarqube - kind: 172.20.0.6
/jenkins - kind: 172.20.0.5
/devops-cluster-k8-control-plane - kind: 172.20.0.4
/devops-cluster-k8-worker - kind: 172.20.0.3
/devops-cluster-k8-worker2 - kind: 172.20.0.2