# Praticando Docker
🟢 Fácil
# 1 - rodando um container basico:
Execute um container usando a imagem do Nginx e acesse a página padrão no navegador.
🔹 Exemplo de aplicação: Use a landing page do TailwindCSS como site estático dentro do container.

crie uma pasta chamada sites, depois use o git clone https://github.com/tailwindtoolbox/Landing-Page.git para baixar o site diretametne do git hub.
execute o comando docker: ``` docker run --name meu-site -d -p 8085:80 --volume=/sites/Landing-Page:/usr/share/nginx/html nginx ```</br>
<img src="img/exe1.png" width="800px" hight="600px" />

agora digite no navegador o ip do servidor+porta configurada exemplo: 192.168.0.103:8085 + enter </br>
<img src="img/exe1-2.png" width="800px" hight="600px" />

# 2 - Criando e rodando um container interativo

Inicie um container Ubuntu e interaja com o terminal dele.
🔹 Exemplo de aplicação: Teste um script Bash que imprime logs do sistema ou instala pacotes de forma interativa.

se nao tiver a imagem do ubuntu baixe com docker pull ubuntu.
execute um container para interagir com o comando: docker run --name ubuntu-teste -ti ubuntu /bin/bash
dentro do container crie uma pasta por exemplo script: atualize com apt update e instale o nano com apt install -y nano
depois execute o namo e crie um script exemplo: nano logs_sistema e escreva o script abaixo:

```
#!/bin/bash
echo "Logs do sistema:"
dmesg | tail -n 10
```

</br>
<img src="img/exe2.png" width="300px" hight="200px" />

de permissão para executar: ``` chmod +x logs_sistema.sh ```

e execute o script: ./logs_sistema.sh

<img src="img/exe2-1.png" width="800px" hight="600px" />

# 3 - Listando e removendo containers
Liste todos os containers em execução e parados, pare um container em execução e remova um container específico.
🔹 Exemplo de aplicação: Gerenciar containers de testes criados para verificar configurações ou dependências.

primeiro vou criar um container para isto faça o seguinte: baixe uma versao do php com o comando docker pull php:7.4-apache
crie uma pasta com mkdir chamada container e dentro um diretorio php-teste, dentro do diretorio container execute :``` docker run --name php-teste -d -p 8080:80 --volume=/container/php-teste:/var/www/html php:7.4-apache```

verifique listando como docker ps (containers emexecução) e docker ps -a (para ver containers que foram executados), pare um container com docker stop + nome docontainer ou ID , pare o exemplo que criamos usando docker stop php-teste.
e para remover use ``` docker rm php-teste ```.

<img src="img/exe3.png">

# 4- Criando um Dockerfile para uma aplicação simples em Python:

Crie um Dockerfile para uma aplicação Flask que retorna uma mensagem ao acessar um endpoint.
🔹 Exemplo de aplicação: Use a API de exemplo Flask Restful API Starter para criar um endpoint de teste.

crie uma pasta com mkdir app_flask, dentro do diretorio crie o script python digitando nano autoapp.py e escreva o codigo a seguir:
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def acesso_flask():
    return 'sucesso ao acessar um endpoint'
```

depois crie o arquivo txt "requirements.txt" escreva dentro:
```
Flask==2.2.2
Werkzeug==2.2.2
```
logo em seguida crie o dockerfile:

```
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
ENV FLASK_APP=autoapp.py
CMD ["flask", "run", "--host=0.0.0.0"]
```

execute ocomando para criar a imagem:


``` docker build -t flask-app . ```
 
carregue  a aplicação: 

``` docker run -p 5000:5000 flask-app ```

<img src="img/exe4.png">

acesse no nevgador digitando <b> http://localhost:5000 </b>

<img src="img/exe4-1.png">


🟡 Médio

# 5 - Criando e utilizando volumes para persistência de dados
Execute um container MySQL e configure um volume para armazenar os dados do banco de forma persistente.
🔹 Exemplo de aplicação: Use o sistema de login e cadastro do Laravel Breeze, que usa MySQL.

# 6 - Criando e rodando um container multi-stage
Utilize um multi-stage build para otimizar uma aplicação Go, reduzindo o tamanho da imagem final.
🔹 Exemplo de aplicação: Compile e rode a API do Go Fiber Example dentro do container.

# 7 - Construindo uma rede Docker para comunicação entre containers
Crie uma rede Docker personalizada e faça dois containers, um Node.js e um MongoDB, se comunicarem.
🔹 Exemplo de aplicação: Utilize o projeto MEAN Todos para criar um app de tarefas usando Node.js + MongoDB.

# 8 - Criando um compose file para rodar uma aplicação com banco de dados
Utilize Docker Compose para configurar uma aplicação Django com um banco de dados PostgreSQL.
🔹 Exemplo de aplicação: Use o projeto Django Polls App para criar uma pesquisa de opinião integrada ao banco.

🔴 Difícil

9 - Criando uma imagem personalizada com um servidor web e arquivos estáticos
Construa uma imagem baseada no Nginx ou Apache, adicionando um site HTML/CSS estático.
🔹 Exemplo de aplicação: Utilize a landing page do Creative Tim para criar uma página moderna hospedada no container.