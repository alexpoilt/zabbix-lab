# Laboratório simples em docker para o Zabbix com PostgreSQL, Grafana e Zapix(Testes em API)

## Conteúdo

- Zabbix:
  - Zabbix Server zabbix-server:10051
  - Zabbix Agent em: zabbix-agent:10050
  - Zabbix Frontend em: http://zabbix-frontend:8080
- Banco de dados:
  - Postgresql em : postgresql:5432
  - PGAdmin em : http://pgadmin:5050
- Ferramentas de apoio:
  - Zapix em: http://zapix
  - Grafana em: http://grafana:3000
  - Mailhog:
    - WEB Client: http://mailhog:8025
    - SMTP Servidor: mailhog
    - SMTP Server Port: 1025
    - SMTP Helo: mailhog
    - SMTP Email: admin@mailhog

## Como usar:

- [Instalar os pré-requisitos](./REQUIREMENTS.md)
- Copiar o projeto e a dependência do zapix para sua estação:
  ```sh
  $ git clone --recurse-submodules https://git.serpro/monitoracao/zabbix-lab.git
  ```
- Em caso de esquecimento do parâmetro "--recurse-submodules" acima, ative o zapix usando os comandos abaixo:
  ```sh
  $ git submodule init
  $ git submodule update
  ```
- **Se necessário** editar as variaveis de opções de versão:
  ```sh
  $ vim .env
  ```
  | Environment      | Padrão |
  | ---------------- | ------ |
  | ZABBIX_VERSION   | 4.0    |
  | POSTGRES_VERSION | 11     |
- Iniciar o gestor do hosts para facilitar acesso:
  ```sh
  $ docker run -d \
      -v /var/run/docker.sock:/tmp/docker.sock \
      -v /etc/hosts:/tmp/hosts \
      dvdarias/docker-hoster
  ```
- Iniciar o projeto com o docker-compose
  ```sh
  $ docker-compose up -d
  ```
- O Grafana já vem pré-configurado com o plugin e datasources para o Zabbix e para o banco postgres do Zabbix
- **Observe** que a estrutura em docker **não usa 'localhost'** então não use esse hostname 'localhost' para configurar o PGAdmin para PostgreSQL e no mailhog. Para configurar os mesmos, atentar-se para a opção de hostname para cada contêiner dentro da configuração do arquivo docker-compose.yml.

# Sobre o Zabbix

![Zabbix](https://assets.zabbix.com/img/logo/zabbix_logo_500x131.png)

O Zabbix é uma solução de monitoramento distribuído de código aberto para grandes ambientes - O repositório base desse projeto que contem todos os **Dockerfiles** do [Zabbix](https://zabbix.com/) para [Docker](https://www.docker.com/) é o [zabbix-docker](https://github.com/zabbix/zabbix-docker) com [builds automáticas](https://registry.hub.docker.com/u/zabbix/) publicadas no [Docker Hub Registry](https://registry.hub.docker.com/).

# Sobre o Zapix

Ferramenta Online para testes e desenvolvimento usando pesquisas dentro da API Web do Zabbix - Projeto original em: [Github Zapix](https://github.com/monitoringartist/zapix) por [monitoringartist](https://monitoringartist.com/).

# Sobre o Grafana

![Grafana](https://raw.githubusercontent.com/grafana/grafana/master/docs/logo-horizontal.png)

[Grafana](https://grafana.com) é uma ferramenta para relatórios e análise de dados - Versão em container já configurada para uso com o plugin do zabbix

- O Grafana já vem pré-configurado com o plugin e datasources para o Zabbix e para o banco postgres do Zabbix

# Sobre o Mailhog

![MailHog](https://raw.githubusercontent.com/mailhog/MailHog-UI/master/assets/images/hog.png)

Ferramenta para teste de envio de emails para desenvolvedores - [MailHog](https://github.com/mailhog/MailHog).
