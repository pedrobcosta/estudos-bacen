# Ansible: boas práticas

## Preferir módulos específicos em vez de comandos diretos

Exemplo ruim (uso de shell):
```yaml
- name: Instalar Nginx com shell
    shell: apt-get install -y nginx
```

Correto (uso de módulo):
```yaml
- name: Instalar Nginx de forma idempotente
    apt:
        name: nginx
        state: present
```

## Modularizar utilizando roles

Exemplo:
```yaml
- name: Aplicar configuração do Nginx
    hosts: web
    become: true
    roles:
        – nginx
```