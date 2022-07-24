# Helm
* Hands-on helm using custom docker image on my dockerhub repo:
    https://hub.docker.com/repository/docker/rizk95/helmapp

* The image below is based on project: https://github.com/tradebyte/DevOps-Challenge

* i created a dockerfile and upload it to my dockerhub
```yaml
# MUST use python 3.9.X version, i had python 3.10.4 version but it seem there are problems with the application and this version
FROM python:3.9-alpine
# cd app
WORKDIR /app
# Copy from my local to /app inside the container
COPY . ./

# Install Requirements and redis 
RUN pip install -r requirements.txt
RUN apk --update add redis

# Expose appliaction in port 8000
EXPOSE 8000

# Set Environment Variables 
ENV REDIS_HOST=localhost
ENV REDIS_PORT=6379
ENV REDIS_DB=0
ENV HOST=localhost
ENV PORT=8000
ENV ENVIRONMENT=DEV

# run the 
CMD [ "sh","initial.sh" ]
```
 
* i used minikube as kubernertes cluster
 - First Create you project 
```bash
helm create helm-app
```
 - after Creating and modifing your templates, variables and chart yaml files , we check syntax
```bash
helm template <path-of-your-project>
```

 - Third release your project 
```bash
helm release helm-app-release-1
```

 - Finally install your app inside kubernetes
```bash
helm install helm-app-release-1
```

## RESULTS
![image](https://user-images.githubusercontent.com/30655799/180666959-db752146-eab6-4c6b-ad67-28cae6cee8bb.png)




