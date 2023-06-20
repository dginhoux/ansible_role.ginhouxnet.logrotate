# ROLE dginhoux.logrotate



## DESCRIPTION

This ansible role configure logrotate.


## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role is tested on the following platforms.<br />

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye, bookworm |
| Fedora | 33, 34, 35, 36, 37, 38 |
| EL | 7, 8 |

You can set this variable `check_compatibility` to let the role skip nodes with unsupporteds platforms to avoid any compatibility problems.<br />


#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.logrotate
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.logrotate dginhoux.logrotate
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.logrotate
      ansible.builtin.include_role:
        name: dginhoux.logrotate
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
logrotate_configure: install
logrotate_packages:
  - logrotate
logrotate_services:
  - logrotate
logrotate_enable: true

logrotate_main_conf_file: /etc/logrotate.conf
logrotate_custom_conf_dir: /etc/logrotate.d

logrotate_global_options:
  - weekly
  - rotate 4
  - create
  - dateext
  # - su root syslog
  - compress

logrotate_enable_cron_hourly_rotation: false

logrotate_custom_configure: true

# logrotate_custom_list: []
logrotate_custom_list:
  # - name: TEMPLATE
  #   state: present
  #   definitions:
  #     - logs:
  #         - /var/log/TEMPLATE.LOG
  #       options:
  #         - rotate 1
  #         - daily
  #         - missingok
  #         - notifempty
  #         - compress
  #       preremove: []
  #       postrotate: []
  #       firstaction: []
  #       lastaction: []
  - name: syslog
    state: absent
  - name: rsyslog
    state: absent
  - name: wtmp
    state: present
    definitions:
      - logs:
          - /var/log/wtmp
        options:
          - rotate 1
          - daily
          - missingok
          - notifempty
          - compress
          - create 0660 root utmp
  - name: btmp
    state: present
    definitions:
      - logs:
          - /var/log/btmp
        options:
          - rotate 1
          - daily
          - missingok
          - notifempty
          - compress
          - create 0660 root utmp
  - name: auth
    state: present
    definitions:
      - logs:
          - /var/log/auth.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: kern
    state: present
    definitions:
      - logs:
          - /var/log/kern.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: messages
    state: present
    definitions:
      - logs:
          - /var/log/messages
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: mail
    state: present
    definitions:
      - logs:
          - /var/log/maillog
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: daemon
    state: present
    definitions:
      - logs:
          - /var/log/daemon.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: cron
    state: present
    definitions:
      - logs:
          - /var/log/cron.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: lpr
    state: present
    definitions:
      - logs:
          - /var/log/lpr.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
  - name: bootlog
    state: present
    definitions:
      - logs:
          - /var/log/boot.log
        options:
          - rotate 5
          - daily
          - missingok
          - notifempty
          - compress
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
