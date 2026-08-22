# Ansible

O Ansible é uma ferramenta de automação de configuração e orquestração que opera de forma agentless, utilizando SSH para gerenciar sistemas Linux e WinRM para sistemas Windows, eliminando a necessidade de instalação de agentes nos nós gerenciados. Essa característica facilita a manutenção e reduz a complexidade da infraestrutura, permitindo automatizar tarefas como **instalação de pacotes, configuração de serviços, deploy de aplicações e orquestração de ambientes completos de forma consistente e repetível**. Utilizando arquivos YAML conhecidos como **playbooks**, o Ansible organiza de forma clara as **“plays”** (que definem os hosts) e as **“tasks”** (as ações que serão executadas), permitindo que os times de DevOps e infraestrutura descrevam de forma legível e versionável as configurações e processos necessários para o funcionamento de seus ambientes.

## Componentes

Os componentes do Ansible são a estrutura que organiza e executa as automações de forma limpa, rastreável e escalável. São eles:

### Playbook

Atua como um “roteiro” onde se define tudo que será feito em cada host, garantindo que a configuração desejada seja aplicada de forma consistente e automatizada. Ex.:

```yaml
- name: Configuração inicial de servidores web
hosts: web
become: true
tasks:
– name: Instalar Nginx
apt:
name: nginx
state: present
– name: Iniciar serviço Nginx
service:
name: nginx
state: started
```

### Plays

As plays são blocos dentro do playbook que definem quais hosts ou grupos receberão as configurações e em qual contexto as tasks rodarão. Elas permitem dividir a automação em fases, cada uma focando em uma função ou etapa do provisionamento. Ex.:

```yaml
- name: Atualizar pacotes nos servidores de aplicação
hosts: app_servers
become: true
tasks:
– name: Atualizar cache de pacotes
apt:
update_cache: yes
```

### Tasks

As tasks são as instruções específicas executadas em cada servidor, sendo as responsáveis por garantir a configuração desejada, como instalar pacotes, editar arquivos, reiniciar serviços ou criar usuários. Ex.:

```yaml
- name: Criar usuário de implantação
user:
name: deploy
state: present
```

### Módulos

Os módulos são responsáveis por executar as tarefas dentro das tasks, sendo como “ferramentas especializadas” para instalar pacotes (apt, yum), copiar arquivos (copy), gerenciar serviços (service), criar usuários (user), entre outros. Ex.:

```yaml
- name: Copiar arquivo de configuração para o servidor
copy:
src: /local/nginx.conf
dest: /etc/nginx/nginx.conf
owner: root
group: root
mode: ‘0644’
```

### Roles

As roles são estruturas modulares que organizam tasks, handlers, arquivos, templates e variáveis em pastas padronizadas, permitindo que automações complexas sejam reaproveitadas e mantidas de forma limpa e organizada.

```yaml
- name: Aplicar role de configuração de Nginx
hosts: web
become: true
roles:
– nginx
```

### Inventory

O inventory define os hosts gerenciados pelo Ansible, organizados em grupos conforme função ou ambiente, facilitando execuções específicas.

```yaml
[web]
192.168.0.10
[db]
192.168.0.20
```

### Idempotência

A idempotência garante que rodar o playbook repetidamente não causará alterações se o ambiente já estiver conforme desejado, evitando mudanças desnecessárias ou falhas inesperadas. Ex.:

Rodar repetidamente:
```yaml
- name: Garantir que o Nginx está instalado
    apt:
        name: nginx
        state: present
```

O Ansible não reinstala se o Nginx já estiver instalado, evitando inconsistências em execuções recorrentes.

### Agentless

Sem necessidade de instalar agentes nos servidores gerenciados. Isso reduz a complexidade de manutenção e facilita a adoção em ambientes heterogêneos.

### AWX/Tower

Interface gráfica do Ansible. Torna o uso mais seguro e rastreável.

### Ad-hoc Commands

Executam rapidamente tarefas sem criar playbooks, ideais para testes e operações pontuais. Ex.:

`ansible all -m ping`

Testa conectividade via SSH de todos os hosts definidos no inventory.