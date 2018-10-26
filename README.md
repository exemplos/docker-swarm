# docker-swarm

## Passo 1:
```code bash
docker swarm init --advertise-addr <ip da instancia>
```
Ex.: docker swarm init --advertise-addr 192.168.45.244

Será retornado um conteúdo, parecido com este:
```code bash
docker swarm join \
    --token SWMTKN-1-068ymtey6wse092vcimn20zs2agcu9gz5pt8vkn07n6p3mpc4f-dealoh22dmo6si32662kpcpde \
    192.168.47.153:2377
```
Execute o comando acima na outra máquina, que será um worker

## Passo 2:
Criar a rede no manager
```code bash
docker network create \
 --driver overlay \
 --subnet 10.0.9.0/24 \
 --opt encrypted \
 minha-rede-gti3
``` 

## Passo 3: 
Criar o service no manager
```code bash
docker service create --replicas 3 -p 22083:80 --name minha-web1 --network minha-rede-gti3 nginx
``` 
## Passo 4:
Instalar o portainer no manager

```code bash
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer
``` 
## Passo 5:
Acessar o portainer no site:
http://192.168.45.244:9000
 
