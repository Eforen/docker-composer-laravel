# World Builder
My WorldBuilder

## Recommended Workflow

Add to your `~/.bashrc` the following:
```shell
#My custom aliases
alias dcr="docker-compose run --rm"
```

This will allow you to run the following commands:

```shell
dcr artisan migrate
dcr composer install
dcr npm install
```

instead of

```shell
docker-compose run --rm artisan migrate
docker-compose run --rm composer install
docker-compose run --rm npm install
```