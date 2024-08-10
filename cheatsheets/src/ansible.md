# Ansible

Ansible es una plataforma de software libre para configurar y administrar ordenadores. 
Combina instalación multi-nodo, ejecuciones de tareas ad hoc y administración de configuraciones. 
Adicionalmente, Ansible es categorizado como una herramienta de orquestación.

Los archivos de órdenes se llaman "playbook" y tienen extensión "yaml".

- [Documentación](https://docs.ansible.com/ansible/latest/index.html)

El orden de prioridad de las configuraciones es de mayor a menor;

1. Variables de entorno
2. Keyword de Playbooks
3. CLI
4. Archivo de configuración

## Requisitos

- En el control node y managed node debe estar instalado Python.

  [Matriz de version de ansible a version de python](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#support-life)

- En el managed node debe estar habilitado ssh y la autenticación por llave

  Si la llave está cifrada se debe usar;

> ssh-agent bash && ssh-add [path]/[priv_key]

- En el control node; python-pipx (en algunas distros es; python3-pipx ó py3-pipx)

- La máquina target debe tener sudo como passwordless

  Se puede hacer que ansible solicite la contraseña para escalar con el argumento de "-\-ask-become-pass" al ejecutar el playbook.

## Instalación

- Full

> pipx install --include-deps ansible

- Minimal

> pipx install ansible-core

- Versión específica

> pipx install ansible-core==[version]

- Upgrade

> pipx upgrade --include-injected ansible

- Dependencia de autocompletado

> pipx inject --include-apps ansible argcomplete

> bash -c "activate-global-python-argcomplete --user"

## Configuración

[Documentacion y variables de entorno](https://docs.ansible.com/ansible/latest/reference_appendices/config.htm)

- Archivo de configuración

> ./ansible.cfg

> /etc/ansible/ansible.cfg

> ~/.ansible.cfg

ó variable de entorno

> ANSIBLE_CONFIG

- Home de Ansible

> ~/.ansible

- Generar archivo template de configuración

> ansible-config init --disabled -t all > ansible.cfg

- Por defecto no loguea, si se quiere se debe habilitar en el cfg

> log_path = [absolute_path]/[file]

loguea en el controller

- Conf para syslog, se debe habilitar en el cfg

> syslog_facility = [ip]:[port]

- Verbose en el log, se debe habilitar en el cfg

> log_verbosity = [0-3]

## Conectividad a los target

Ansible necesita conectarse por ssh con llave, no admite contraseña

1. Crear llave

> ssh-keygen

2. Copiar llave pública

> ssh-copy-id -i [path_absoluto]/[llave].pub

## Archivos playbook y hosts

- Verificar sintaxis del playbook

> ansible-playbook [archivo].yml --syntax-check --check

- Correr playbook

> ansible-playbook [archivo].yml -u [usuario_ssh] -t [playbook_tag_to_run] -l [specific_server_or_not_in_run] -k --verbose

   "-k" indica que pregunte la clave de la llave ssh
  
   "-t" y "-l" son opcionales

- Dry-run playbook

> ansible-playbook [archivo].yml --check

- Archivo "hosts" que contiene el inventario de máquinas aplicar el playbook

> ansible-playbook [archivo].yml -i [inventario_1] -i [inventario_n] -i [directorio_con_los_inventarios]

> /etc/ansible/hosts

Ejemplo;

```
[[group_name]]
[name] [variable_n_to_use_in_playbook]=[value] ansible_host=[IP] ansible_port=[SSH_PORT] ansible_ssh_private_key_file=[aboslute_path_ssh_key]

[[group_name_2]]
[IP] [variable_n_to_use_in_playbook]=[value] ansible_port=[SSH_PORT] ansible_ssh_private_key_file=[aboslute_path_ssh_key]

[[group_name:childen]]
[parent_group-1]
[parent_group-N]
```

Así mismo, si los servers cambian con el tiempo hay dos opciones;

1. Se crea un script que cambie el archivo cuando se ejecuta
2. Se utiliza un plugin de inventario específicamente según si es AWS, Azure, GCP, OpenStack, etc.

- Archivo que tiene las variables de entorno a utilizar en el playbook

> vars.yml

- Archivo playbook de ejemplo

Cada task es un plugin, por lo que ansible tiene para casi cualquier programa.

Los plugins se ven con

> ansible-doc -l

Un plugin específico se obtiene su man con

> ansible-doc [plugin]

La variable hosts es muy personalizable; [url](https://docs.ansible.com/ansible/latest/inventory_guide/intro_patterns.html#common-patterns)

```yml
---
- name: [string_name]
  hosts: [group_name_or_all_or_IPs/CNAMES/GROUPS_separeted_with_:]
  remote_user: [ssh_remote_user]
  become: [true_to_execute_as_root]
  vars:
    [variable_X]: [value]

  tasks:
  - name: [task_name]
    [plugin]:
      [plugin_configuration]
      [plugin_variable]: "{{ [variable_X] }}"

  - name: Start service
    ansible.builtin.service:
      name: [servie_name]
      state: started

  - name: Copy file
    ansible.builtin.copy:
      src: [path]/[file]
      dest: [path]/[file]
      onwer: [owner]
      group: [group]
      mode: '[unix_numeric_mode]'

  - name: Changeing file
    ansible.builtin.file:
      dest: [path]/[file]
      mode: '[unix_numeric_mode]'
      register: [return_variable]
      failed_when:
        - [return_variable].rc =! 0
        - "[Error message]"
      ...

  - name: Tasks block
    block:
      - name: Install trough legacy yum
        ansible.builtin.yum:
          name:
          - httpd
          - memcached
          state: present

      ...
    when: ansible_facts['distribution'] == 'CentOS'
    rescue:
      - name: Rescue tasks if above fail
        when: ansible_failed_task.name == "[task_failed]"
        ansible.builtin.debug:
          msg: 'Message to show in verbose mode'
    always:
      - name: Tasks to run even if block fails
        ...
    
```

Se pueden incluir tantos "- name" con tasks y hosts como se quiera

## Comandos de una linea

> ansible [group_name] -m [plugin] -a "[plugin_arguments]"

## Templates

Ansible usa el motor Jinja2 para procesar las variables que se encuentren en "vars" del playbook y luego proceder.

Ubicación;

> ./templates/[name].j2

Luego se llama por módulo. Lo que se ejecute se guardará en el dest del nodo slave.

```yaml
ansible.builtin.template:
  src: templates/[name].j2
  dest: /tmp/hostname
```

Así mismo, dentro del playbook lo que está dentro de; "{{ xxx }}" forma parte de Jinja2 pero sin ir a su archivo específico.

## Condicionales

Son todos los "when" debajo de cada task.

Están los "ansible_facts" que lo que hacen es chequear cosas comunes a todos los Linux,
de ahí que existen;

- ansible_facts['os_family'] == "Debian"
- ansible_facts['distribution'] == "CentOS"
- ansible_facts['distribution_major_version'] == "6"
- ansible_facts['lsb']['major_release'] | int >= 6
- ansible_facts['cpu_temperature']

entre otros.

- ansible_selinux.status == "enabled"

Se pueden combinar mediante paréntesis para crear condicionales juntos ('and') o excluyentes ('or')

También se pueden usar los register para evaluar una tarea y como salió;

- [register_name].rc != 0
- [register_name].stdout == ""

## Retorno ('register') de una task

```yml
- name: Test play
  hosts: all

  tasks:

      - name: Register a variable
        ansible.builtin.shell: cat /etc/motd
        register: [name_to_save_return_status]
```
