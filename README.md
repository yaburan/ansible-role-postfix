# ansible-role-postfix

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-postfix)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-postfix-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/postfix)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - A free and open-source mail transfer agent

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    postfix_generic_maps: {}
    postfix_packages: []
    postfix_parameters:
      alias_database: 'hash:/etc/aliases'
      alias_maps: 'hash:/etc/aliases'
      command_directory: /usr/sbin
      daemon_directory: /usr/libexec/postfix
      data_directory: /var/lib/postfix
      debug_peer_level: 2
      debugger_command: 'PATH=/bin:/usr/bin:/usr/local/bin:/usr/X11R6/bin ddd $daemon_directory/$process_name $process_id & sleep 5'
      html_directory: False
      inet_interfaces: localhost
      inet_protocols: all
      mail_owner: postfix
      mailq_path: /usr/bin/mailq.postfix
      manpage_directory: /usr/share/man
      mydestination:
        - $myhostname
        - localhost.$mydomain
        - localhost
      newaliases_path: /usr/bin/newaliases.postfix
      readme_directory: "/usr/share/doc/postfix-{{ postfix_version }}/README_FILES"
      sample_directory: "/usr/share/doc/postfix-{{ postfix_version }}/samples"
      sendmail_path: /usr/sbin/sendmail.postfix
      setgid_group: postdrop
      queue_directory: /var/spool/postfix
      unknown_local_recipient_reject_code: 550

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.postfix
          postfix_generic_maps:
            root: email@address
          postfix_packages:
            - cyrus-sasl
            - cyrus-sasl-lib
            - cyrus-sasl-plain
          postfix_parameters:
            smtp_sasl_auth_enable: True
            smtp_sasl_password_maps: 'hash:/etc/postfix/sasl_passwd'
            smtp_sasl_security_options: noanonymous
            smtp_use_tls: True
          postfix_sasl_username: email@address
          postfix_sasl_password: kkpgfccailg5c

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
