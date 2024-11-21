# docker-step-by-step

# Criando e Executando um Contêiner Docker no Windows com WSL2

Este guia descreve como criar uma imagem Docker personalizada com NGINX no Windows usando o WSL2.

---

## **1. Pré-requisitos**
- Certifique-se de que o Docker Desktop está instalado e em execução.
- Tenha o WSL2 configurado com uma distribuição Linux (ex.: Ubuntu).

---

## **2. Passo a Passo**

### **1. Inicie o Docker Desktop**
- Abra o Docker Desktop no Windows.
- Aguarde até que a mensagem **"Docker is running"** seja exibida.

### **2. Abra o Ubuntu no WSL**
- No menu Iniciar do Windows, pesquise e abra o **Ubuntu**.
- Verifique se o Docker está funcionando executando:
```
docker --version
```
### **3. Crie um Diretório de Trabalho** 

No terminal do WSL, execute o comando abaixo para criar um diretório e acessá-lo:
```
mkdir ~/meu_nginx && cd ~/meu_nginx
```
### **4. Crie o Arquivo Dockerfile**

Crie o arquivo Dockerfile:
```
vim Dockerfile
```
Adicione o seguinte conteúdo:
```
FROM nginx
COPY index.html /usr/share/nginx/html/
```
Salve e feche o arquivo: <br>
Pressione `esc` + `:wq` para salvar.

### **5. Crie o Arquivo index.html**
```
vim index.html
```
Adicione o seguinte conteúdo:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Meu Docker Customizado</title>
</head>
<body>
    <h1>Olá, Docker no Windows e WSL2!</h1>
</body>
</html>
```
Salve e feche o arquivo: <br>
Pressione `esc` + `:wq` para salvar.

### **6. Construa a Imagem Docker**

Execute o seguinte comando para criar a imagem:
```
docker build -t meu_nginx_customizado .
```
### **7. Execute o Contêiner**

Execute o contêiner usando a imagem criada:
```
docker run -d -p 8080:80 meu_nginx_customizado
```
### **8. Teste no Navegador**

Abra o navegador no Windows e acesse:
```
http://localhost:8080
```
Você verá a página personalizada exibindo: "Olá, Docker no Windows e WSL2!"

## **3. Comandos Úteis para Gerenciamento de Docker**

Verificar imagens disponíveis:
```
docker images
```
Verificar todos os contêineres (ativos e inativos):
```
docker ps -a
```
Remover uma imagem:
```
docker rmi nome_da_imagem
```
Acessar o shell dentro de um contêiner em execução:
```
docker exec -it meu_nginx bash
```
Agora você sabe como criar uma imagem Docker personalizada e gerenciá-la no WSL2! 🚀

## **4 - Parar e deletar o contêiner**

### **1. Localizar o Contêiner**

Liste todos os contêineres em execução:
```
docker ps
```
Você verá uma saída semelhante a esta:
```
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS                  NAMES
07980c58840e   meu_nginx_customizado   "/docker-entrypoint.…"   30 minutes ago   Up 30 minutes   0.0.0.0:8080->80/tcp   eloquent_noyce
```
O CONTAINER ID é 07980c58840e. <br>
O NAMES é eloquent_noyce.

### **2. Parar o Contêiner**

Use o nome ou o ID do contêiner para pará-lo:

Com o nome do contêiner:

```
docker stop eloquent_noyce
```
Ou com o ID do contêiner:
```
docker stop 07980c58840e
```
Verifique se o contêiner foi parado:
```
docker ps
```
O contêiner não aparecerá na lista se tiver sido parado com sucesso.

### **3. Listar Todos os Contêineres (Ativos e Parados)** 

Para confirmar que o contêiner ainda existe, mas está parado:
```
docker ps -a
```
A saída mostrará todos os contêineres, incluindo os parados.

### **4. Deletar o Contêiner**

Use o comando docker rm para deletar o contêiner:

Com o nome do contêiner:
```
docker rm eloquent_noyce
```
Ou com o ID do contêiner:
```
docker rm 07980c58840e
```
Verifique novamente:
```
docker ps -a
```
O contêiner não aparecerá mais na lista.

Agora, o contêiner foi localizado, parado e deletado com sucesso! 🚀
