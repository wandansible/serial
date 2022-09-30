Ansible role: Serial
====================

Manage a serial terminal server.
Installs packages for a serial terminal server and
configures Minicom profiles for devices connected over serial.

Role Variables
--------------

```
ENTRY POINT: main - Manage a serial terminal server

        Install packages for a serial terminal server and configure
        Minicom profiles for devices connected over serial.

OPTIONS (= is mandatory):

- minicom_minirc
        List of serial devices to manage
        [Default: (null)]
        elements: dict
        type: list

        OPTIONS:

        = baudrate
            Serial device baudrate

            type: int

        - extra
            Extra minicom options
            [Default: (null)]
            type: str

        = name
            Name of the device

            type: str

        = port
            Path to serial device

            type: str

- serial_packages
        List of packages to install
        [Default: ['minicom', 'picocom']]
        elements: str
        type: list
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/serial,main,wandansible.serial
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.serial
      src: https://github.com/wandansible/serial

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: serial_terminal_servers
      roles:
         - role: wandansible.serial
           become: true
           vars:
             minicom_minirc:
               - name: router
                 port: /dev/ttyS1
                 baudrate: 9600
                 extra: |
                   pu scriptprog       /usr/bin/runscript
                   pu minit
                   pu mreset
                   pu mdialpre
                   pu mdialsuf
                   pu mdialpre2
                   pu mdialsuf2
                   pu mdialpre3
                   pu mdialsuf3
                   pu mconnect
                   pu mnocon1
                   pu mnocon2
                   pu mnocon3
                   pu mnocon4
                   pu mhangup
                   pu mdialcan
                   pu mdialtime        0
                   pu mrdelay          0
                   pu mretries         o
                   pu mdropdtr         0
                   pu multiline        No
                   pu rtscts           No
