# Compass - Atividade de Docker

> O Docker Desktop para Windows deve estar configurado para utilizar o **backend WSL 2**. No Windows 10/11 Home esse é o único backend disponível. Nas versões Education, Pro e Enterprise, o usuário deve ser certificar de que o backend ativado é o WSL e não a outra alternativa disponível — o Hyper-V. Para mais informações, visite esse [link](https://docs.docker.com/desktop/install/windows-install/#system-requirements).

## Instalando o Docker Desktop no Windows

Os contêineres e imagens criados com o Docker Desktop são compartilhados entre todas as contas de usuários nas máquinas onde ele está instalado. Isso ocorre porque todas as contas do Windows usam o mesmo VM para construir e executar contêineres.

Você pode acessar a documentação do Docker Desktop nesse [link](https://docs.docker.com/desktop/install/windows-install/).

### Instalando interativamente (GUI)

1. Visite o site do [Docker](https://www.docker.com/) e baixe o instalador do Docker Desktop for Windows (`Docker Desktop Installer.exe`).
2. Caso ainda não tenha uma conta no Docker Hub, seria importante criá-la.
3. Caso a opção de backend apareça, certifique-se de que WSL 2 seja escolhido como o backend ao invés do Hyper-V.
4. Siga as instruções do assistente de instalação para autorizar o instalador e proceda com a instalação.
5. Quando a instalação for finalizada, clique em fechar para concluir o processo de instalação.
6. Para testar se a instalação foi bem-sucedida: execute `docker run hello-world` (caso não apareça nenhum erro, tudo está ok) e `docker compose version` (para constatar que o Docker Compose foi instalado juntamente com o Docker Desktop).

### Instalando usando a linha de comando

1. Visite o site do [Docker](https://www.docker.com/) e baixe o instalador do Docker Desktop for Windows (`Docker Desktop Installer.exe`).
2. Abra o PowerShell e use o comando `cd` para ir até a pasta em que se encontra o arquivo baixado no passo anterior.
3. Para iniciar a instalação execute: `Start-Process 'Docker Desktop Installer.exe' -Wait install`.
4. Se sua conta de administração for diferente da sua conta de usuário, você deve adicionar o usuário ao grupo de usuários docker: `net localgroup docker-users username /add` (substitua 'username' por o seu Windows username).
5. O Docker Desktop não é iniciado automaticamente após a instalação, pois o computador precisa ser reiniciado.
6. Após a máquina ser reiniciada, tudo deve funcionar normalmente. Caso haja algum problema, tente achar a solução para o problema pesquisando na internet.
7. Mas se tudo ocorrer bem, um símbolo de uma baleia vai aparecer na setinha da barra de notificações do lado direito inferior do seu computador e o Docker Desktop irá ficar verde com a mensagem running, ou seja, que está rodando corretamente.
8. Depois ao logar na janela com sua conta Docker Hub, é só iniciar o seu primeiro container. Para isso é importante que se tenha o Powershell também instalado para comandos no terminal ou o wsl com ubuntu, para executar as tarefas do windows.
9. Para testar se a instalação foi bem-sucedida execute: `docker run hello-world` (caso não apareça nenhum erro, tudo está ok) e `docker compose version` (para constatar que o Docker Compose foi instalado juntamente com o Docker Desktop).
 
## WordPress no Docker

### Usando o Dockerfile

1. abra o terminal e use o comando `git clone` para fazer o download desse repositório
2. use o comando `cd` para mudar o diretório e ir para a pasta [Dockerfile](./Dockerfile/) do repositório baixado no passo anterior
3. use `chmod u+x script.sh` para tornar o script bash executável 
4. execute o script usando `./script.sh root admin`, note que o script deve receber 2 argumentos:
  - o primeiro argumento é a senha do usuário root
  - o segundo argumento é a senha do administrador da database do WordPress
    - poderíamos usar o root para conectar o WordPress ao servidor MySQL, no entanto, com o intuito de obedecer o *Principle of least privilege*, o script criará outro usuário que possui privilégios de administrador apenas na database dedicada ao WordPress
5. após aguardar alguns segundos para os containers serem criados e inicializados, você poderá acessar o WordPress na [porta 80](http://localhost:80) e o phpMyAdmin na [porta 82](http://localhost:82)

### Usando o Docker Compose

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
