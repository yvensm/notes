- [1. :wrench: Criando um container](#1-wrench-criando-um-container)
  - [1.1 Baixando a imagem base](#11-baixando-a-imagem-base)
  - [1.2 Dockerfile](#12-dockerfile)
    - [1.2.1 Estrutura Básica para o Exemplo](#121-estrutura-básica-para-o-exemplo)
    - [1.2.2 Comandos Dockerfile](#122-comandos-dockerfile)
  - [1.3 Criando uma imagem](#13-criando-uma-imagem)
  - [](#)

# 1. :wrench: Criando um container  
Nessa seção descreverei os passos para inicializar um container, como exemplo utilizarei a criação de um container servidor web com [nginx](https://www.nginx.com/).

<div style="width:200px"><a href="https://www.nginx.com/"><img src="https://www.nginx.com/wp-content/uploads/2018/08/NGINX-logo-rgb-large.png" /></a></div>


## 1.1 Baixando a imagem base
```console
    foo@bar:~$ docker pull nginx
```

Para visualizar as imagens diponíveis basta utilziar o comando
```console
    foo@bar:~$ docker images
```

## 1.2 Dockerfile
Antes de criar uma imagem para o container devemos configurar o ambiente por meio de um arquivo de configuração chamado Dockerfile que pode está localizado dentro da pasta do projeto ou não (Recomenda-se que seja dentro da pasta para salvar no seu repositório online).

### 1.2.1 Estrutura Básica para o Exemplo
        
```Dockerfile
//Dockerfile.txt
    FROM nginx
    COPY static-html-directory /usr/share/nginx/html 
    
```

Onde `static-html-directory` é o diretório da sua pagina html.

### 1.2.2 Comandos Dockerfile
```Dockerfile
    FROM  #Refência a imagem que deseja utilizar como base
    COPY  #Copia arquivos de um diretório da maquina para um diretorio dentro do container
    RUN  #Executa um comando no console dentro do container
    WORKDIR  #diretório de trabalho. O container iniciará dentro desse diretório.
```

## 1.3 Criando uma imagem  
        foo@bar:~$ docker build

## 