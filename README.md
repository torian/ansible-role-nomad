# Ansible role for Hashicorp Nomad

[![Build Status](https://travis-ci.org/torian/ansible-role-nomad.svg)](https://travis-ci.org/torian/ansible-role-nomad)

An Ansible Role that installs and configures Hashicorp Nomad on Red Hat/CentOS or Debian/Ubuntu.

## Tested On

  * EL / Centos (7 / 6)
  * Ubuntu (Xenial / Trusty / Precise)


## Role Variables

FIXME


## Usage

The role does not lock you down to a number of supported variables that map to nomad configuration settings, but rather grants you all the freedom that you want by using YAML blocks where you can specify the configuration, and even split it in different files.

The following example will install and configure nomad version `0.5.0`, and will create two different hcl configuration files, `/etc/nomad.d/{base,server}.hcl`. This can give you an idea on how to use it:

```yaml
    - hosts: nomad_servers
      
      vars:
        - nomad_version: 0.6.0
        - nomad_config:
            base: |
              bind_addr = "{{ansible_default_ipv4.address}}"
              log_level = "DEBUG"
              data_dir  = "{{ nomad_data_dir }}"

            server: |
              server {
                enabled = true
                bootstrap_expect = 3
              }

              consul {
                server_auto_join = true
              }

      roles:
        - { role: torian.nomad, become: true }
```


## License

See [License](LICENSE)


## Author Information

This role was created in 2017 by Emiliano Castagnari.

