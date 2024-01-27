# Web Development Template


Repositório para desenvolvimento local e treinamentos


# Localmente via Docker

Para a execução local via docker devemos seguir os seguintes passos.


## Visão Geral

Este projeto oferece uma estrutura modelo e arquivos Docker para serviços essenciais, como `apache`, `php` e `redis`, possibilitando a execução deste projeto localmente.

Para executar o projeto no Docker, basta adicionar esse projeto no diretório www e adicionar um host virtual para o mesmo no arquivo apache/httpd-vhosts.conf.



## Pre-requisitos

Certifique-se de ter o Docker instalado. Siga as etapas mencionadas no site oficial se você ainda não o tiver.



## Development Setup


1. Faça o clone do repositório (`git clone`).
2. Abra um terminal (Git Bash / CMD) no diretório do projeto.
3. Execute `docker-compose up -d --build apache` (`--build` só é necessário quando um dos arquivos Docker no `docker-compose.yml` é atualizado).
4. Uma vez concluído, execute docker ps. Isso deve mostrar os containers apache, fpm e redis em execução.
5. (Opcional) Execute qualquer comando pontual para construir/instalar dependências do projeto, se necessário.
6. Acesse o projeto no navegador com base na configuração de host virtual no apache.
7. Quando terminar o desenvolvimento, você pode executar `docker-compose down`, que interromperá a execução dos containers do seu projeto.
   

Observe que em um dos passos acima, você pode receber uma notificação pedindo permissão para compartilhar o diretório do seu projeto com o ambiente do Docker, o que você deve permitir. Como estamos compartilhando o diretório de código com o contêiner Docker como um volume para evitar a reconstrução da imagem sempre que ocorre uma alteração.

Também observe que todos os comandos Docker especificados devem ser executados a partir do diretório do projeto, onde o arquivo docker-compose.yml está presente, pois contém toda a lógica de configuração.


## Executando Tarefas Pontuais

1. Para utilizar o Composer para qualquer finalidade (instalação, remoção etc.), em vez de executar o comando usual composer, executaremos `docker-compose run --rm composer`. Exemplo: `docker-compose run --rm composer` install para instalar as dependências do projeto.
2. Para utilizar o npm para qualquer finalidade, em vez de executar o comando usual npm, executaremos `docker-compose run --rm npm`. Exemplo: `docker-compose run --rm npm run build`, onde o comando `build` é definido no arquivo package.json do projeto.
3. Para utilizar os comandos `php artisan`, utilize o seguinte comando: `docker-compose run --rm artisan`. Exemplo: Para colocar o aplicativo em modo de manutenção no Laravel, executamos `docker-compose run --rm artisan down`.

Como nosso projeto está contido em containers, os comandos acima criarão um container para npm/composer/php artisan, executarão o comando necessário no seu diretório de código/pasta de trabalho e, em seguida, removerão esse container, eliminando a necessidade de ter essas dependências instaladas em nosso sistema.