# Lab 9 Report
### By Miklashevskaya Daria, DS-02


- First, turn on Kubernetes on Docker
![](https://i.imgur.com/EJmvXuT.jpg)
![](https://i.imgur.com/Yd88oFV.png)

- Then, install helm:
```
brew install kubernetes-helm
```
- Initialize helm:
```
helm init
```
- Status of Kubernetes pods:
```
kubectl -n kube-system get po
```
- Create replicas:
```
helm install --name mongodb-replicaset stable/mongodb-replicaset
```
- The result:

![](https://i.imgur.com/ViWuGlJ.jpg)

- When the containers are up, execute the script:

```
for ((i = 0; i < 3; ++i)); 
do kubectl exec --namespace default mongodb-replicaset-$i -- sh -c 'mongo --eval="printjson(rs.isMaster())"';
done
```
- The result will be like this for each container:
![](https://i.imgur.com/I4j5TG3.jpg)

- Then installing the chat app from the source below:
```
git clone https://github.com/chpinan1128/chat-app
```
- Create the following Dockerfile:
```
FROM node:alpine

COPY . .

RUN npm install

CMD node server.js
```
- The repository with this Dockerfile can be found here (it's a pulled repo from the source above): https://github.com/dariamikl/chat-app

- Building the container for the chat-app:
```
docker build -t dariamikl/chatty-app:latest .
```
- Create new app with helm:
```
helm create app
```
```
helm install --name chatty ./app
```
- The result is:
![](https://i.imgur.com/ifkHbpG.jpg)
- Then do these instructions suggested above to run the application URL:
![](https://i.imgur.com/8OaFXPy.png)
- The result:
![](https://i.imgur.com/LRnz53x.jpg)
- Profit 👍👍👍

![](https://i.imgur.com/zruhJ66.png)

- Pushing to Docker Hub:
```
docker push dariamikl/chatty-app:latest
```
