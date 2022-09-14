Первым делом обновите существующий список пакетов:

```bash
sudo apt update
```

 

Copy

Затем установите несколько необходимых пакетов, которые позволяют `apt` использовать пакеты через HTTPS:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

 

Copy

Добавьте ключ GPG для официального репозитория Docker в вашу систему:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

 

Copy

Добавьте репозиторий Docker в источники APT:

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

 

Copy

Потом обновите базу данных пакетов и добавьте в нее пакеты Docker из недавно добавленного репозитория:

```bash
sudo apt update
```

 

Copy

Убедитесь, что установка будет выполняться из репозитория Docker, а не из репозитория Ubuntu по умолчанию:

```bash
apt-cache policy docker-ce
```

 

Copy

Вы должны получить следующий вывод, хотя номер версии Docker может отличаться:

Output of apt-cache policy docker-ce

```bash
docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
```

 

Copy

Обратите внимание, что `docker-ce` не установлен, но является кандидатом на установку из репозитория Docker для Ubuntu 20.04 (версия `focal`).

Установите Docker:

```bash
sudo apt install docker-ce
```

 

Copy

Docker должен быть установлен, демон-процесс запущен, а для процесса активирован запуск при загрузке. Проверьте, что он запущен:

```bash
sudo systemctl status docker
```


## Шаг 2 — Настройка команды Docker без sudo (необязательно)

По умолчанию команда `docker` может быть запущена только пользователем **root** или пользователем из группы **docker**, которая автоматически создается при установке Docker. Если вы попытаетесь запустить команду `docker` без префикса `sudo` или с помощью пользователя, который не находится в группе **docker**, то получите следующий вывод:

```
Outputdocker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```

Если вы не хотите каждый раз вводить `sudo` при запуске команды `docker`, добавьте свое имя пользователя в группу `docker`:

```bash
sudo usermod -aG docker ${USER}
```

 

Copy

Чтобы применить добавление нового члена группы, выйдите и войдите на сервер или введите следующее:

```bash
su - ${USER}
```

 

Copy

Вы должны будете ввести пароль вашего пользователя, чтобы продолжить.

Проверьте, что ваш пользователь добавлен в группу **docker**, введя следующее:

```bash
id -nG
```

 

Copy

```
Outputsammy sudo docker
```

Если вам нужно добавить пользователя в группу `docker`, для которой вы не выполнили вход, объявите имя пользователя явно, используя следующую команду:

```bash
sudo usermod -aG docker username
```

 

Copy

В дальнейшем в статье подразумевается, что вы запускаете команду `docker` от имени пользователя в группе **docker**. В обратном случае вам необходимо добавлять к командам префикс `sudo`.

Давайте перейдем к знакомству с командой `docker`.

## Шаг 3 — Использование команды Docker

Использование `docker` подразумевает передачу ему цепочки опций и команд, за которыми следуют аргументы. Синтаксис имеет следующую форму:

```bash
docker [option] [command] [arguments]
```

 

Copy

Чтобы просмотреть все доступные субкоманды, введите:

```bash
docker
```

 

Copy

Для 19-й версии Docker полный список субкоманд выглядит следующим образом:

```
Output  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

```

Чтобы просмотреть параметры, доступные для конкретной команды, введите:

```bash
docker docker-subcommand --help
```

 

Copy

Чтобы просмотреть общесистемную информацию о Docker, введите следующее:

```bash
docker info
```

 

Copy

Давайте изучим некоторые из этих команд. Сейчас мы начнем работать с образами.

## Шаг 4 — Работа с образами Docker

Контейнеры Docker получают из образов Docker. По умолчанию Docker загружает эти образы из [Docker Hub](https://hub.docker.com/), реестр Docker, контролируемые Docker, т.е. компанией, реализующей проект Docker. Любой может размещать свои образы Docker на Docker Hub, поэтому большинство приложений и дистрибутивов Linux, которые вам потребуется, хранят там свои образы.

Чтобы проверить, можно ли получить доступ к образам из Docker Hub и загрузить их, введите следующую команду:

```bash
docker run hello-world
```