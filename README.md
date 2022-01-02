# Configurando um servidor com sonar
Esse projeto tem por finalidade disponibilizar uma forma simples de subir o sonar junto com sua stack em um servidor e colocar o proxy reverso na frente do mesmo para disponibilizar acesso https ao mesmo.

## Configurações no Servidor
Você vai precisar do docker e docker compose intalado no servidor. Utilizamos containers para subir as aplicações

## Tecnologias

* [PostgresSQL](https://www.postgresql.org/) - Banco de dados utilizado pelo sonar
* [Sonarqube](https://www.sonarqube.org/) - É Software de analise estática de codigo que estamos disponibilizando
* [Traefik](https://doc.traefik.io/traefik/) - É um roteador de borda que iremos utilizar como Proxy reverso


## Instalando

* Instale o docker e docker compose no servidor.
* Execute o comandos abaixo de configuração de parâmetros do docker como root: Esses valores são recomendados pela propria equipe do sonar para execução dentro do docker, pelo fato dele utilizar um elasticsearch embutido. [doc](https://hub.docker.com/_/sonarqube?tab=description) 
```sh
ulimit -u 8192
ulimit -n 131072
sysctl -w fs.file-max=131072
sysctl -w vm.max_map_count=524288
```
* Substitua os valores destacados abaixo no arquivo docker-compose.yml
    * `example@mail.com` pelo seu email
    * `sonar.example.com` pelo seu DNS
    * recomendo trocar também o usuário e senha do banco de dados (não esqueça de trocar no serviço do banco e no do sonar)

* Execute o docker-compose através do comando `docker-compose up -d`

* Configure no seu serviço de dns o direcionamento de rota para o ip do seu servidor.

## Dica

Caso não tenha um DNS registrado o [Freenom](https://www.freenom.com/pt/index.html) permite que você crie um sem custo