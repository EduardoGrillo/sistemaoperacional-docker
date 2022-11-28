# Docker

<h2> Comando necessários caso instale docker no seu Linux: </h2>

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install docker.io
```

<h2> Definição de usuário sem privilégios em diferentes maneiras </h2>

- Durante a execução utilizando -u com docker run 

```
docker run -u 4000 alpine
```

- Adicionando o usuário no Dockerfile 

```
FROM alpine
RUN groupadd -r myuser && useradd -r -g myuser myuser
< HERE DO WHAT YOU HAVE TO DO AS A ROOT USER LIKE INSTALLING PACKAGES ETC . >
USER myuser
```

<h2> Limitando recursos </h2>

```
docker run -- cap - drop all -- cap - add CHOWN alpine
```

> Utilizar ```--cap-drop``` para fortalecer seus conteiners docker ou ```--cap-add``` para adicionar recursos.

<h2> Definindo o sistema de arquivos e os volumes como somente leitura </h2>

- Para executar conteiners com um sistema de arquivos, basta utilizar ```--read-only```. Caso um aplicativo estiver dentro de um conteiner, basta combinar ```--read-only``` com ```-- tmpfs```.

```
docker run -- read - only alpine sh -c ’ echo " whatever " > / tmp ’
docker run -- read - only -- tmpfs / tmp alpine sh -c ’ echo " whatever " >/ tmp / file ’
```

> Se o volume for montado apenas como leitura, é necessário montar apenas com leitura. É utilizado ```:roao``` e ```-v```. 

```
docker run -v volume - name :/ path / in / container : roao alpine
```
> Outra opção para montar com volume, seria utilizando o ```-- mount```.
```
docker run -- mount source = volume - name , destination =/ path / in / container, readonly alpine
```
