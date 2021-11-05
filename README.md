
# Projeto Docker 
#### Stack deploy usando o compose
<pre>
docker stack deploy -c docker-compose.yml nginx
</pre>

#### Escalar o serviço
<pre>
docker service scale nginx_web-nginx=3
</pre>

# Play docker


Passo a passo:

- Iniciar o docker swarm adicionando o ip da instancia

<pre>
Linux: ifconfig
Windowns: ipconfig

ip docker 172.17.0.1 
</pre>
<br>

<pre>
docker swarm init --advertise-addr 172.17.0.1
</pre>
<br>

- Vizualizar os nós do cluster 
<pre>
docker node ls
</pre>
<br>

- Clone do repositório da aplicação esta hospedada
<pre>
git clone https://github.com/WeslleyFratini/docker-repo.git
</pre>
<br>

- Abrir pasta
<pre>
cd docker-repo
</pre>
<br>

- Lista os arquivos que tem no repositório
<pre>
ls -la
</pre>
<br>

- Abrir a stack YML
<pre>
cd stack
</pre>
<br>

- Vizualiar o arquivo YML no terminal
<pre>
cat stack.yml
</pre>
<br>

-  Comando para instalar o Docker UCP, estamos passando a flag -c que indica o caminho do arquivo yml, e o final ucp é o nome da stack. Coloquei “ucp” para facilitar a identificação do que essa stack faz.
<pre>
docker stack deploy -c stack.yml ucp
</pre>
<br>

- Sair da pasta stack
<pre>
cd ..
</pre>
<br>

- Lista os arquivos do diretório
<pre>
ls -la
</pre>
<br>

- Fazer o build da imagem que será usada para o nosso serviço. Lembrando que o build precisa ser executado no diretório do Dockerfile, o mesmo nó no qual executamos o git clone.
<pre>
docker build -t bbnginx:1.0 .
</pre>
<br>

- A imagem será buildada e já podemos criar nosso serviço, com este comando:
(O comando é bem simples, só usar create para criar o serviço e informar para meu cluster que essa aplicação roda na porta 80.)
<pre>
docker service create --publish 80:80 bbnginx:1.0
</pre>

- Para sair do docker swarm
<pre>
docker swarm leave -f
</pre>

