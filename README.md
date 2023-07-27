Ansible role for rtx installation on MacOS
=========

A role for install [rtx](https://github.com/jdxcode/rtx) on MacOS.

How to Install
------------

Install from ansible galaxy

```
ansible-galaxy role install hesthub.rtx
```

Install from github

```
ansible-galaxy role install git+https://github.com/hesthub/ansible-rtx
```

the **RECOMMEND** way is to lock dependency version in your [requirements.yml](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-roles-and-collections-from-the-same-requirements-yml-file):

```
---
collections:

roles:
  #   - name: hesthub.rtx
  #     version: v0.2

  #   - src: https://github.com/hesthub/ansible-rtx
  #     type: git
  #     version: main
```

Compatibilities
--------------

Support Macos on Intel chips, currently not able to test the role using an ARM version.

- (11) Big Sur
- (12) Monterey
- (13) Ventura

Requirements
------------

Brew installed on system.
(https://brew.sh/)


Role Variables
--------------

```
rtx_user: "{{ ansible_user_id }}"
rtx_group: "{{ ansible_user_gid }}"
rtx_dir: "{{ ansible_user_id }}/.local/share/rtx"

shells_to_activate:
  - bash
  - zsh
  - fish

rtx_plugins: see example playbook
```

1. supports activating rtx on bash,zsh and fish shell, or all three if you like. 


2. currently only supports installing via brew (https://brew.sh/)


Dependencies
------------

None

Example Playbook
----------------

for example: 

This will install Go version `1.18`and `1.20` the sets the global version to `1.20` 
Rust installs version `1.71.0` and sets the global version, while specifying a plugin repository.

https://github.com/asdf-vm/asdf-plugins


```
    - hosts: servers
      become: true
      gather_facts: true
      roles:
        - role: "hesthub.rtx"
      vars:
        system_wide: false
        rtx_plugins:
          - name: golang
            repository: ""
            versions:
              - 1.20.6
              - 1.18
            delete_versions: []
            global: 1.20.6
          - name: rust
            repository: "https://github.com/code-lever/asdf-rust.git"
            versions:
              - 1.71.0
            delete_versions: []
            global: 1.71.0 
```
TODO
-------

- add option for manual, non-brew installation
- testing on ARM chips when possible.
- generate config file during installation
- extend plugin support

License
-------

MIT

