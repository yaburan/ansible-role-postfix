# ansible-role-postfix

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-postfix)

RHEL/CentOS - A free and open-source mail transfer agent

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    postfix_version: 2.10.1
    postfix_pacakges: []
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
          postfix_packages:
            - cyrus-sasl
            - cyrus-sasl-lib
            - cyrus-sasl-plain
          postfix_parameters:
            smtp_sasl_auth_enable: True
            smtp_sasl_password_maps: 'hash:/etc/postfix/sasl_passwd'
            smtp_sasl_security_options: noanonymous
            smtp_use_tls: True

## License

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
