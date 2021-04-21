<h6>Docker</h6>
<h1 align="center"> Dockerizando um ambiente Elixir e Phoenix </h1>
<h6 align="center">by Keiko</h6>

Iniciando Elixir e Phoenix no Docker de maneira simples e sem complicações!!

Copie este repositório na pasta do seu projeto:

```
git clone https://github.com/keikomori/docker-elixir-phoenix
```

Acesse a pasta do projeto:

```
cd docker-elixir-phoenix
```

Crie uma pasta com o nome `/src`

```
mkdir src
```
Execute a imagem do Dockerfile

```
docker-compose build
``` 

Crie sua aplicação

```
docker-compose run --rm phoenix mix phx.new . --app <nome da aplicação> --no-html --no-webpack
```

Essa parte é bem importante, então não esqueça dela. Acesse o arquivo da pasta `/scr/config/devs.exs`
 - mude o nome que está no `hostname` de `localhost` para `db`

```
# Configure your database
config :inmana, Inmana.Repo,
adapter: Ecto.Adapters.Postgres,
  username: "postgres",
  password: "postgres",
  database: "inmana_dev",
  hostname: "db",
  show_sensitive_data_on_connection_error: true,
  pool_size: 10
```

> Vai ficar da forma que está acima

Agora vamos inicializar o banco de dados com o Ecto

```
docker-compose run --rm phoenix mix ecto.create
```

Agora podemos testar se o Elixer e Phoenix estão funcionando devidamente executando

```
docker-compose up
```

No navegador acesse a página

```
http://localhost:4000/dashboard
```

Seu ambiente Docker está pronto para criar sua aplicação!!!


<h4>Extras</h4>

Para fechar os containers utilize

```
docker-compose down -v
```

Caso adicione alguma dependência execute

```
docker-compose run --rm phoenix mix deps.get
```

<h4>Comandos Docker Úteis</h4>

 - `docker ps` lista todos os container que estão em execução no momento
 - `docker container ls --all` lista todos os container que estão disponíveis
 - `docker logs <container>` mostra o registro do container
 - `docker start/stop <container>` inicia ou para um container
 - `docker rm <container>` remove o container
 - `docker images` lista todas as imagens disponíveis
 - `docker rmi <images>` remove uma imagem
 - `docker-compose down --volumes` destrói os volumes criados
