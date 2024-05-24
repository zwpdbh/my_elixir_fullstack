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