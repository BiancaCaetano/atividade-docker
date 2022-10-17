# Compass - Atividade de Docker

## WordPress no Docker

### Docker Compose

> O Docker Compose é uma ferramenta que auxilia na declaração, compartilhamento e execução de aplicações que são compostas por múltiplos containers. E é por isso que o Docker Compose se encaixa muito bem nessa atividade, pois uma aplicação de WordPress em Docker não precisa somente de um container para o WordPress, mas também de um outro container para o MySQL.

1. crie uma pasta com um nome qualquer (por example, `docker-wp`) em uma localidade de fácil acesso
2. abra o PowerShell e use o comando `cd` para mudar de diretório e ir para a pasta criada no passo anterior
3. faça o download do arquivo [`docker-compose.yml`](docker-compose.yml) e use o comando `move` para mover esse arquivo da pasta `Downloads` para o *working directory* configurado no passo anterior
4. dentro dessa pasta crie 2 arquivos: `db_root_password.txt` contendo a senha do usuário root e `db_password.txt` contendo a senha do administrador da database do WordPress 
5. execute o commando `docker compose up` para criar e inicializar os containers
6. aguarde os containers serem inicializados e quando o terminal ficar inativo por alguns segundos e o último log conter "ready for connections", você poderá usar o WordPress na [porta 80](http://localhost:80) e o phpMyAdmin na [porta 82](http://localhost:82)
