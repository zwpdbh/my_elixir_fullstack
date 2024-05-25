# Prerequisites

## Install Erlang and Elixir

- [Install asdf](https://asdf-vm.com/guide/getting-started.html)
- Install erlang and elixir via asdf
  
```sh
asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git
asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git
asdf list all erlang
asdf install erlang 26.2.5
asdf list all elixir
asdf install elixir main-otp-26

# set specific version and check it
asdf list erlang
asdf global erlang 26.2.5
asdf list elixir 
asdf global elixir main-otp-26

erl -eval 'erlang:display(erlang:system_info(otp_release)), halt().'
elixir -v
```

## Setup specific elixir and erlang version per project

Edit `.tool-versions` file in the root of your project:

```txt
elixir 1.16.1-otp-26
erlang 26.2.2
```

## Start Postgres via dockerfile

- Create a `dev.yaml`:

```yaml
services:
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: postgres
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - 5432:5432
  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
      
volumes:
  pgdata:
```

- Start up using `sudo docker compose -f dev.yaml up`
- Visit: [Login - Adminer](http://localhost:8080/)
  
## Install Phoenix

- [Installation](https://hexdocs.pm/phoenix/installation.html)
  
```sh 
mix local.hex
mix archive.install hex phx_new
```

## Create hello project

- [Up and running](https://hexdocs.pm/phoenix/up_and_running.html)
- Don't forget to run `mix ecto.create`.

## Proxy hex packages

- Elixir use `hex` to manage packages.
- Permanently select a mirror
  - For mix
  
      ```sh
      # For mix 
      mix hex.config mirror_url https://repo.hex.pm 
      ```

  - For rebar3
  
    Add to the global or a project’s top level `rebar.config, {rebar_packages_cdn, "https://repo.hex.pm"}.`. For more information see rebar3’s package support and configuration documentation.

  See: [Mirrors](https://hex.pm/docs/mirrors)

- Temporarily select a mirror, Hex commands can be prefixed with an environment variable in the shell.
  
  ```sh
  HEX_MIRROR=https://repo.hex.pm mix deps.get
  HEX_CDN=https://repo.hex.pm rebar3 update

  # Or 
  export HEX_MIRROR="https://hexpm.upyun.com"
  export HEX_CDN="https://hexpm.upyun.com"
  ```

## Proxy docker images

Edit or create the Docker daemon configuration file (`sudo vi /etc/docker/daemon.json`) to include the following mirror configurations:

```json
{
  "registry-mirrors": [
    "https://registry.docker-cn.com",
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```

After adding the mirror configurations, restart the Docker daemon to apply the changes:

```sh
sudo service docker restart
sudo docker info
```

You shall see information like:

```txt
 Registry Mirrors:
  https://registry.docker-cn.com/
  https://docker.mirrors.ustc.edu.cn/
  https://hub-mirror.c.163.com/
  https://mirror.baidubce.com/
```