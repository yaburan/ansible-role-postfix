# ansible-role-postfix

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-postfix)

RHEL/CentOS - A free and open-source mail transfer agent

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    postfix_command_directory: /usr/sbin
    postfix_debug_peer_level: 2
    postfix_daemon_directory: /usr/libexec/postfix
    postfix_data_directory: /var/lib/postfix
    postfix_html_directory: 'no'
    postfix_inet_interfaces: [ 'localhost' ]
    postfix_inet_protocols: all
    postfix_manpage_directory: /usr/share/man
    postfix_mail_owner: postfix
    postfix_mailq_path: /usr/bin/mailq.postfix
    postfix_newaliases_path: /usr/bin/newaliases.postfix
    postfix_packages: []
    postfix_readme_directory: /usr/share/doc/postfix-2.10.1/README_FILES
    postfix_sample_directory: /usr/share/doc/postfix-2.10.1/samples
    postfix_sendmail_path: /usr/sbin/sendmail.postfix
    postfix_setgid_group: postdrop
    postfix_queue_directory: /var/spool/postfix
    postfix_unknown_local_recipient_reject_code: 550

Additional variables available, not defined by default:

    postfix_alias_database: 'hash:/etc/aliases'
    postfix_alias_maps: 'hash:/etc/aliases'
    postfix_debug_peer_list: [ '127.0.0.1' ]
    postfix_default_destination_concurrency_limit: 20
    postfix_default_privs: nobody
    postfix_fallback_transport: 'lmtp:unix:/var/lib/imap/socket/lmtp'
    postfix_fast_flush_domains: '$relay_domains'
    postfix_header_checks: 'regexp:/etc/postfix/header_checks'
    postfix_home_mailbox: Mailbox
    postfix_in_flow_delay: 1s
    postfix_local_destination_concurrency_limit: 2
    postfix_local_recipient_maps: 'unix:passwd.byname $alias_maps'
    postfix_luser_relay: '$user@other.host'
    postfix_mail_spool_directory: /var/spool/mail
    postfix_mailbox_command: /some/where/procmail
    postfix_mailbox_transport: cyrus
    postfix_mydomain: "{{ ansible_domain }}"
    postfix_mydestination: [ '$myhostname', 'localhost.$mydomain', 'localhost' ]
    postfix_mynetworks: [ '168.100.189.0/28', '127.0.0.0/8' ]
    postfix_mynetworks_style: host
    postfix_myorigin: $myhostname
    postfix_myhostname: "{{ inventory_hostname }}"
    postfix_proxy_interfaces: 1.2.3.4
    postfix_recipient_delimiter: '+'
    postfix_relayhost: mail.host.com
    postfix_relay_domains: [ '$mydestination' ]
    postfix_relay_recipient_maps: 'hash:/etc/postfix/relay_recipients'
    postfix_smtpd_banner: '$myhostname ESMTP $mail_name'
    postfix_soft_bounce: False

You can also define additional parameters by using the following variable:

    postfix_additional_parameters:
      smtp_sasl_auth_enable: True
      smtp_sasl_password_maps: 'hash:/etc/postfix/sasl_passwd'
      smtp_sasl_security_options:
        - noanonymous
        - noplaintext
      smtp_use_tls: True

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.postfix
          postfix_additional_parameters:
            smtp_sasl_auth_enable: True
            smtp_sasl_password_maps: 'hash:/etc/postfix/sasl_passwd'
            smtp_sasl_security_options: noanonymous
            smtp_use_tls: True
          postfix_inet_protocols: ipv4
          postfix_mydomain: "{{ ansible_domain }}"
          postfix_myhostname: "{{ inventory_hostname }}"
          postfix_mynetworks:
            - 10.0.0.0/8
            - 192.168.0.0/16
          postfix_packages:
            - cyrus-sasl
            - cyrus-sasl-lib
            - cyrus-sasl-plain

## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
