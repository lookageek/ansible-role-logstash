# Ansible Role: Logstash

An Ansible Role that installs Logstash on Debian/Ubuntu with systemd.

## Requirements

Requires at least Java 7 (Java 8+ preferred). Install OpenJDK or Oracle JDK using any galaxy role.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticstack_deb_repo: "5.x"

The elasticstack debian repo version

    logstash_version: "1:5.3.2-1"

Specific logstash version to install

    logstash_listen_port_beats: 5044

The port over which Logstash will listen for beats.

    logstash_elasticsearch_hosts:
      - http://localhost:9200

The hosts where Logstash should ship logs to Elasticsearch.

    logstash_ssl_dir: /etc/pki/logstash
    logstash_ssl_certificate_file: logstash-forwarder-example.crt
    logstash_ssl_key_file: logstash-forwarder-example.key

Local paths to the SSL certificate and key files, which will be copied into the `logstash_ssl_dir`.

For utmost security, you should use your own valid certificate and keyfile, and update the `logstash_ssl_*` variables in your playbook to use your certificate.

To generate a self-signed certificate/key pair, you can use use the command:

    $ sudo openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout logstash.key -out logstash.crt

Note that filebeat and logstash may not work correctly with self-signed certificates unless you also have the full chain of trust (including the Certificate Authority for your self-signed cert) added on your server. See: https://github.com/elastic/logstash/issues/4926#issuecomment-203936891

    logstash_enabled_on_boot: yes

Set this to `no` if you don't want logstash to run on system startup.

    logstash_install_plugins:
      - logstash-input-beats

A list of Logstash plugins that should be installed.

    logstash_queue_type: persisted

Queue type of logstash. Available values `memory` and `persisted`

    logstash_log_level: info

Logging for logstash level configuration. Available levels `trace`, `debug`, `info`, `warn`, `error`, and `fatal`.

    logstash_xpack_enabled: true
    logstash_xpack_monitoring_enabled: "true"

X-Pack configuration for Logstash.

## License

MIT / BSD

## Author Information

This role was created in 2017 by Jayanth Manklu cloning from [geerlingguy/ansible-role-logstash](https://github.com/geerlingguy/ansible-role-logstash).
