# PROTOCOLO HTTP / HTTP2

Hypertext Transfer Protocol (HTTP)

Requisição(cliente) -> Resposta(servidor)

HTTP 2

- Multiplexing - requests e respostas paralelos em uma única coneão
- Melhorias de performance

## Apache Http Server

Possui o arquivo de configuração `httpd.conf`, cujas configurações principais são:

- DocumentRoot: Diretório base onde as páginas web são armazenadas. Esta diretiva indica ao Apache onde buscar os arquivos que serão servidos aos clientes.

- ServerRoot: Diretório principal onde estão armazenados os arquivos de configuração do servidor.

- ServerName: Nome que identifica o servidor, essencial em configurações de VirtualHost para hospedagem de múltiplos sites.

```
DocumentRoot “/var/www/html”
ServerRoot “/etc.httpd”
ServerName “meusite.com”
```

## NGINX

O NGINX usa um arquivo de configuração localizado normalmente em /etc.nginx/nginx.conf

```
server {
root /usr/share/nginx/html;
server_name meusite.com;
location / {
try_files $uri $uri/ =404;
}
}
```

## IIS (Internet Information Services)

O IIS, servidor web da Microsoft, utiliza uma interface gráfica para a maioria das configurações, mas também pode ser configurado pelo arquivo `applicationHost.config` (para o servidor) e `web.config` (por site ou aplicação). Algumas das configurações principais incluem:

- Physical Path: Caminho físico no servidor onde os arquivos da aplicação estão armazenados, semelhante ao DocumentRoot e root nos outros servidores.

- Bindings: Define o domínio, IP e porta de escuta para o site, análogo ao ServerName do Apache e server_name do NGINX.

- Modules: Permite a adição de módulos que controlam funcionalidades, como autenticação e manipulação de requisições.

Ex. de configuração do `web.config`:

```
<configuration>
<system.webServer>
<defaultDocument>
<files>
<add value=“index.html” />
</files>
</defaultDocument>
</system.webServer>
</configuration>
```

## Virtual Hosts

O VirtualHost é uma funcionalidade que permite hospedar vários sites em um único servidor físico, seja com base no nome (name-based) ou no IP (IP-based). O Apache permite a configuração de múltiplos hosts virtuais, cada um com suas próprias configurações e diretórios. Ex.:

```
<VirtualHost *:80>
ServerName www.site1.com
DocumentRoot “/var/www/site1”
</VirtualHost>
<VirtualHost *:80>
ServerName www.site2.com
DocumentRoot “/var/www/site2”
</VirtualHost>
```
## Códigos de status HTTP

1. 1xx (Informativos): Indicam que a solicitação foi recebida e o processo continua.

2. 2xx (Sucesso): Indicam que a solicitação foi bem-sucedida.

- 200 OK: A solicitação foi bem-sucedida e o servidor retornou o conteúdo solicitado.

3. 3xx (Redirecionamento): Indicam que é necessário mais alguma ação para concluir a solicitação.

4. 4xx (Erro do Cliente): Indicam problemas na requisição feita pelo cliente.

- 404 Not Found: O recurso solicitado não foi encontrado no servidor.

- 403 Forbidden: O acesso ao recurso solicitado é proibido.

5. 5xx (Erro do Servidor): Indicam problemas internos no servidor.

 500 Internal Server Error: O servidor encontrou uma condição inesperada que o impediu de atender à solicitação.

## Balanceamento de Carga (Load Balancing)

O balanceamento de carga distribui o tráfego entre vários servidores para otimizar o desempenho e a disponibilidade. No NGINX, o balanceamento de carga é configurado usando a diretiva upstream para definir um grupo de servidores que processarão as requisições.

Exemplo de configuração:

```
http {
upstream meuservidores {
server servidor1.com;
server servidor2.com;
server servidor3.com;
}
server {
listen 80;
location / {
proxy_pass http://meuservidores;
}}}
```
