# Compass - Atividade de Docker

## WordPress no Docker

### Dockerfile

1. abra o terminal e use o comando `git clone` para fazer o download desse repositório
2. use o comando `cd` para mudar o diretório e ir para a pasta [Dockerfile](./Dockerfile/) do repositório baixado no passo anterior
3. use `chmod u+x script.sh` para tornar o script bash executável 
4. execute o script usando `./script.sh root admin`, note que o script deve receber 2 argumentos:
  - o primeiro argumento é a senha do usuário root
  - o segundo argumento é a senha do administrador da database do WordPress
    - poderíamos usar o root para conectar o WordPress ao servidor MySQL, no entanto, com o intuito de obedecer o *Principle of least privilege*, o script criará outro usuário que possui privilégios de administrador apenas na database dedicada ao WordPress
5. após aguardar alguns segundos para os containers serem criados e inicializados, você poderá acessar o WordPress na [porta 80](http://localhost:80) e o phpMyAdmin na [porta 82](http://localhost:82)

### Docker Compose

> O Docker Compose é uma ferramenta que auxilia na declaração, compartilhamento e execução de aplicações que são compostas por múltiplos containers. E é por isso que o Docker Compose se encaixa muito bem nessa atividade, pois uma aplicação de WordPress em Docker não precisa somente de um container para o WordPress, mas também de um outro container para o MySQL.

1. crie uma pasta com um nome qualquer (por example, `docker-wp`) em uma localidade de fácil acesso
2. abra o PowerShell e use o comando `cd` para mudar de diretório e ir para a pasta criada no passo anterior
3. faça o download do arquivo [`docker-compose.yml`](docker-compose.yml) e use o comando `move` para mover esse arquivo da pasta `Downloads` para o *working directory* configurado no passo anterior
4. dentro dessa pasta crie 2 arquivos: `db_root_password.txt` contendo a senha do usuário root e `db_password.txt` contendo a senha do administrador da database do WordPress 
5. execute o commando `docker compose up` para criar e inicializar os containers
6. aguarde os containers serem inicializados e quando o terminal ficar inativo por alguns segundos e o último log conter "ready for connections", você poderá usar o WordPress na [porta 80](http://localhost:80) e o phpMyAdmin na [porta 82](http://localhost:82)

## Referências

- [Bitnami Docker Image for WordPress README](https://github.com/bitnami/bitnami-docker-wordpress)
- [Communication between multiple docker-compose projects](https://stackoverflow.com/questions/38088279/communication-between-multiple-docker-compose-projects)
- [Compose file version 3 reference](https://docs.docker.com/compose/compose-file/compose-file-v3/)
- [Docker Compose Restart Policies](https://www.baeldung.com/ops/docker-compose-restart-policies)
- [Docker compose version 3.8 or 3.9 for latest?](https://forums.docker.com/t/docker-compose-version-3-8-or-3-9-for-latest/102439)
- [Multiple Dockerfiles in One Project](https://www.baeldung.com/ops/multiple-dockerfiles)
- [MySQL](https://hub.docker.com/_/mysql), [WordPress](https://hub.docker.com/_/wordpress) e [phpMyAdmin](https://hub.docker.com/_/phpmyadmin) (DockerHub - documentação das imagens)
- [Quickstart: Compose and WordPress](https://docs.docker.com/samples/wordpress/)
- [The Complete Guide to Docker Secrets](https://earthly.dev/blog/docker-secrets/)
- [The Complete Guide to Docker Volumes](https://towardsdatascience.com/the-complete-guide-to-docker-volumes-1a06051d2cce)
- [Understanding Docker’s “latest” Tag](https://www.howtogeek.com/devops/understanding-dockers-latest-tag/)
- [Wordpress latest does not works with mysql latest container](https://github.com/docker-library/wordpress/issues/313)
