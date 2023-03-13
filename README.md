### Ref
- Appplication [https://github.com/docker/awesome-compose/tree/master/gitea-postgres]
- Install docker [https://docs.docker.com/engine/install/ubuntu/]

### wakatime swarm01
- [https://wakatime.com/@spcn12/projects/uojazsynms]


### Create VM template 3 node (manager, work1,work2)
  * Os Ubuntu 22.04
  * Cpu 2 core
  * Memory 2024 MB
  * Storege 32 GB

### requrement
  * Docker
  * Wakatime
  * Github
  * Folder swarm01, swarm02 (managernode) choose app frome Reference to swarm01 floder
  
### BUILD-IMAGE --> TAG ---> LOGIN DOCGER IN VM --> PUSH TO DOCKER
  * Build images
  * cd to path folder swarm01 and run this command
```
sudo docker compose "django/compose.yaml" up -d --build
```
  * Tag images 
```
  sudo docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```
  * Login to docker
```
  docker login
```
  * Push to docker
```
  docker push TARGET_IMAGE[:TAG]
```

### Create stack deploy
  * Create file docker=coompose.yml in swarm path
```
version: '3.3' 
services:
  web: 
    image: kantapongkk/gitea:v1
    networks: 
    - webproxy 
    logging:
      driver: json-file
    container_name: spcn12gitea
    deploy: 
      replicas: 1
      labels: 
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.spcn12gitea-https.entrypoints=websecure 
        - traefik.http.routers.spcn12gitea-https.rule=Host("spcn12gitea.xops.ipv9.xyz")
        - traefik.http.routers.spcn12gitea-https.tls.certresolver=default
        - traefik.http.services.spcn12gitea.loadbalancer.server.port=3000
      resources: 
        reservations: 
          cpus: '0.1'
          memory: 10M
        limits: 
          cpus: '0.4'
          memory: 120M
networks: 
  webproxy: 
    external: true
```
  * stack de ploy on portainer
  * go to view result
```
spcn12gitea.xops.ipv9.xyz
```


![image](https://github.com/Kantapong11755/swarm01/issues/2#issue-1620721363)
  
  
  
  
