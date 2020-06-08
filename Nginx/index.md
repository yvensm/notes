- [1. Proxy reverso](#1-proxy-reverso)
  - [1.1 Criando um proxy reverso](#11-criando-um-proxy-reverso)

# 1. Proxy reverso

> No sistema operacional Linux, o Proxy Reverso age como uma ligação entre o host (cliente) e o servidor. Ele pega os pedidos do cliente e os repassa para outros servidores, para finalmente então entregar a resposta do servidor para o cliente. Essa resposta aparece como se fosse originada do próprio servidor proxy.  
> Fonte: [Tutorial proxy reverso Ngix.](https://www.hostinger.com.br/tutoriais/proxy-reverso-nginx/)

## 1.1 Criando um proxy reverso

Para criar um proxy reverso basta inserir no arquivo de configuração do nginx o seguinte código:

```
server {

    listen 80;

    location / {

        proxy_pass http://192.x.x.2;

    }

}
```
`location:` rota que será redirecionada para o proxy;  
`proxy_pass:` endereço destino;   

`Exemplo: `

```
server {
    listen 80;
    location /api {
        proxy_pass http://192.168.0.100:3000;
    }
}

```
Nesse exemplo estamos redirecionando o caminho `/api` para um serviço que esta rodando na porta `3000` da maquina com ip `192.168.0.100`.