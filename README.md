Para executar os contêineres do Windows, você precisa do Windows 10 ou Windows 11 edição Profissional ou Enterprise. As edições do Windows Home ou Education só permitirão que você execute contêineres Linux.

# Instalando o docker no windows 

Os contêineres e imagens criados com o Docker Desktop são compartilhados entre todas as contas de usuários em máquinas onde ela está instalada. Isso ocorre porque todas as contas do Windows usam o mesmo VM para construir e executar contêineres.

1. Verifique qual tipo de windows sua máquina suporta .

2. Vá até o site do docker, baixe o docker Desktop  installer.exe

3. Obtenha o instalador no docker hub ( Se não tem uma conta, é importante criá-la.)

4. Certifique-se de que a opção Use WSL 2 em vez de Hyper-V.

5. Siga as instruções do assistente de instalação para autorizar o instalador e proceda com a instalação.

6. Quando a instalação for bem sucedida, clique em Fechar para concluir o processo de instalação.

Segue link da documentação para o auxilio do Docker Desktop no Windows 

https://docs.docker.com/desktop/install/windows-install/


# Usando o terminal para instalar :

1. Depois de baixar o Docker Desktop  installer.exe 

2. "Docker Desktop Installer.exe" install

3. Start-Process 'Docker Desktop Installer.exe' -Wait install

4. start /w "" "Docker Desktop Installer.exe" install

5. Se sua conta de administração for diferente da sua conta de usuário, você deve adicionar o usuário ao grupo de usuários docker:
 net localgroup docker-users <user> /add.

6. O Docker Desktop não é iniciado automaticamente após a instalação, pois o computador precisa ser reiniciado. Para iniciar o Docker Desktop:
Pesquise por Docker e selecione Docker Desktop nos resultados de pesquisa.
  
7. Após isso, a instalação será iniciada se o Hyper-V estiver habilitado. Caso dê outros problemas, podem ser relacionados a bios do computador. 
  
8. Mas se tudo ocorrer bem, um símbolo de uma baleia vai aparecer na setinha da barra de notificações do lado direito inferior do seu computador e o docker desktop irá ficar verde com a mensagem running, ou seja, que está rodando corretamente.
  
9. Depois ao logar na janela com sua conta docker hub, é só iniciar o seu primeiro container . Para isso é importante que se tenha o powershell também  instalado para comandos no terminal ou o wsl com ubuntu, para executar as tarefas do windows .
  
  Feito isso a instalação completa contém o docker compose já estará também instalado.

# Verifique se o Docker Compose está instalado corretamente verificando a versão.

 -docker compose version

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
