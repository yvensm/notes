# Docker docs

<div style="max-width:200px !important"><a href="https://www.docker.com/"><img src="
https://www.docker.com/sites/default/files/d8/2019-07/Moby-logo.png" /></a></div>


- [Docker docs](#docker-docs)
- [1. :wrench: Criando um container](#1-wrench-criando-um-container)
  - [1.1 :arrow_down: :framed_picture: Baixando a imagem base](#11-arrow_down-framed_picture-baixando-a-imagem-base)
  - [1.2 :page_facing_up: Dockerfile](#12-page_facing_up-dockerfile)
    - [1.2.1 :office: Estrutura Básica para o Exemplo](#121-office-estrutura-básica-para-o-exemplo)
    - [1.2.2 :thought_balloon: Comandos Dockerfile](#122-thought_balloon-comandos-dockerfile)
  - [1.3 :framed_picture: Criando uma imagem](#13-framed_picture-criando-uma-imagem)
  - [1.4 ✨ Criando e executando um container](#14--criando-e-executando-um-container)
- [2. 👀 Tornando um container visível para outro](#2--tornando-um-container-visível-para-outro)
- [3. ⚙ Executando comandos dentro do container](#3--executando-comandos-dentro-do-container)



# 1. :wrench: Criando um container  
Nessa seção descreverei os passos para inicializar um container, como exemplo utilizarei a criação de um container servidor web com [nginx](https://www.nginx.com/).

<div style="max-width:200px !important"><a href="https://www.nginx.com/"><img src="https://www.nginx.com/wp-content/uploads/2018/08/NGINX-logo-rgb-large.png" /></a></div>


## 1.1 :arrow_down: :framed_picture: Baixando a imagem base
```shell
    foo@bar:~$ docker pull nginx
```

Para visualizar as imagens diponíveis basta utilziar o comando
```shell
    foo@bar:~$ docker images
```

## 1.2 :page_facing_up: Dockerfile
Antes de criar uma imagem para o container devemos configurar o ambiente por meio de um arquivo de configuração chamado Dockerfile que pode está localizado dentro da pasta do projeto ou não (Recomenda-se que seja dentro da pasta para salvar no seu repositório online).

### 1.2.1 :office: Estrutura Básica para o Exemplo
        
```Dockerfile
//Dockerfile.txt
    FROM nginx
    COPY static-html-directory /usr/share/nginx/html 
    
```

Onde `static-html-directory` é o diretório da sua pagina html.

### 1.2.2 :thought_balloon: Comandos Dockerfile
```Dockerfile
    FROM  #Refência a imagem que deseja utilizar como base
    COPY  #Copia arquivos de um diretório da maquina para um diretorio dentro do container
    RUN  #Executa um comando no console dentro do container
    WORKDIR  #diretório de trabalho. O container iniciará dentro desse diretório.
```

## 1.3 :framed_picture: Criando uma imagem  
Para criar a imagem do container basta executar o comando a seguir

```shell
    foo@bar:~$ docker build -t nome-da-imagem ./diretorio-do-Dockerfile
```

## 1.4 ✨ Criando e executando um container

Direto ao ponto, vamos criar e executar o container em um único comando.

```shell
    foo@bar:~$ docker run -d --restart always --name nome-do-container -p 80:3000 nome-da-imagem

    //-d : executa em segundo plano
    //--restart always : sempre que a maquina reiniciar ou caso algo faça o container desligar ele será reiniciado automaticamente
    //--name : define nome do container
    //-p : mapeamento de portas. Mapeia a porta 80 do servidor para a porta 3000 do container.
```

# 2. 👀 Tornando um container visível para outro

Podemos permitir que um container enxerge outro container, isso pode ser útil para aplicações em que a API e interface Web rodem na mesma maquina.

No exemplo a seguir criaremos 2 containers onde o segundo será visível para o primeiro.

```shell
    //container 1
    foo@bar:~$ docker run -d -p 80:80 --name sample1 sample
    //container 2
    foo@bar:~$ docker run -d -p 81:80 --link=sample1 --expose="80" --name sample2 sample
```
O parâmetro `--link` permite definir que um container possa visualizar o container criado.

O parâmetro `--expose` define a porta que será exposta para o container alvo.

Desse modo o container `sample2` se tornou visível para o container `sample1`.

Todo container possui um ip próprio, para descobrir como visualizar o ip do container `sample2` para ser acessado de dentro do container `sample3` veja a seção [3](#3-executando-comandos-dentro-do-container);


# 3. ⚙ Executando comandos dentro do container

Para executar comando dentro de um container devemos utilizar o seguinte comando:

```shell 
    foo@bar:~$ docker exec -it nome-do-conainer comando
```

Por exemplo, para visualizar o ip do container 

```shell 
    foo@bar:~$ docker exec -it nome-do-conainer ipconfig
```