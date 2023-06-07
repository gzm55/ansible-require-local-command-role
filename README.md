require_local_command (0.0.3)
=========

Require that one or more local commands are present.
If a command is not found, error out the play.
If detected before, just skip the command.

output global flag variable:

```
  require_local_command: {
    "PATH=<ENV-1>": {
        "command-1": true,
        "command-2": false
    },
    "PATH=<ENV-2>": {
        "command-2": true
    }
  }
```

Requirements
------------

1. `command` or `which` command is availiable on the controling machine.
This should be true for almost all linux machines.
2. jinja2 >= 2.7

Role Variables
--------------

`command` (optionl) could be:
- unset (default), for dependencies
- a string of some command name or executable path
- a list of strings of command names or executable paths

`only_check` (optionl) could be:
- True: if not find the command, only set the flag to false
- False (default): if not find the command, error out the play

Dependencies
------------

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - gzm55.require_local_command
         - { role: gzm55.require_local_command, command: ssh }
         - { role: gzm55.require_local_command, command: [ ls, mv, ssh, ssh-keygen ] }
         - { role: gzm55.require_local_command, command: [ should-fail ], only_check: True }
         - role: gzm55.require_local_command, command: [ should-fail ] }
         - role: ansible-require-local-command-role
           command: "may-by-success-with-new-PATH-env"
           environment:
             PATH: "{{lookup('env', 'PATH')}}:{{ playbook_dir }}"

License
-------

BSD
