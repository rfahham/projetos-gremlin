# Imagem do Docker

Como alternativa, em vez de instalar o Gremlin diretamente no sistema operacional host, você pode implantar o Gremlin a partir da imagem do Docker no DockerHub.

Para executar o daemon, use o comando a seguir. Substitua $GREMLIN_TEAM_ID pelo ID da sua equipe e $GREMLIN_TEAM_SECRET pela chave secreta da sua equipe:

```bash
docker run -d \
    --net=host \
    --pid=host \
    --cap-add=SYS_PTRACE \
    --cap-add=SYS_ADMIN \
    --cap-add=SYS_CHROOT \
    --cap-add=SYS_RESOURCE \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_BOOT \
    --cap-add=SYS_TIME \
    --cap-add=KILL \
    -v /var/lib/gremlin:/var/lib/gremlin \
    -v /var/log/gremlin:/var/log/gremlin \
    -v /sys/fs/cgroup:/sys/fs/cgroup \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -e GREMLIN_TEAM_ID \
    -e GREMLIN_TEAM_SECRET \
    gremlin/gremlin daemon
```

## Desinstalando a imagem do Docker

Se você implantou o Gremlin usando o Docker, use o comando a seguir para desinstalá-lo. Observe que o nome do contêiner pode ser diferente de gremlin , dependendo se você especificou um nome :

```bash
sudo docker stop gremlin
sudo docker rm gremlin
```