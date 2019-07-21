# docker-amp-php5-debug

Ambiente com php-5.5, apache2.4 & mysql-5.5

Você pode mudar as versões como quiser, só leve em conta as possíveis dependências e incompatibilidades que podem surgir.

## Dependências

### docker

Se você precisar de ajuda, pode seguir o guia de instalação em:
><https://docs.docker.com/install/>

### docker-compose

Se você precisar de ajuda, pode seguir o guia de instalação em:
><https://docs.docker.com/compose/install/>

## .env

Crie o arquivo .env usando o EXEMPLO.env

```bash
    cp EXEMPLO.env .env
```

### PREFIX_CONTAINER

Precisamos de um nome único entre os containers criados em todo o seu sistema
>PREFIX_CONTAINER=working
>
### APACHE_SERVER_NAME

Defina um nome de domínio para acessar a aplicação. Não esqueça de registrar esse nome em /etc/hosts ou qualquer outro lugar que seu sistema use para fazer isso.
>APACHE_SERVER_NAME=working.local

Se você não mudou o IP definido no docker-composer.yml, poderia fazer algo como:

```bash
sudo echo '10.1.2.3 working.local' >> /etc/hosts
```

### APACHE_DOCUMENT_ROOT

Defina o diretório root usado pelo apache. Lembre-se da relação do endereço definido daqui com o da variável WORKDIR
>APACHE_DOCUMENT_ROOT=/var/www/html

### WORK_DIR

Se você tiver dúvidas sobre workdir, <https://docs.docker.com/engine/reference/builder/#workdir>
>WORK_DIR=/var/www/
