# Ansible Role: Munin

[![CI](https://github.com/geerlingguy/ansible-role-munin/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-munin/actions?query=workflow%3ACI)

Installs munin, a monitoring system, on RedHat/CentOS/Rocky Linux or Debian/Ubuntu Linux servers.

## Requirements

If you are running a RedHat-based distribution, you need to install the EPEL repository, which can be simply installed via the `geerlingguy.repo-epel` role.

If you would like to view munin's graphs and output via HTTP, you will need an HTTP server like Apache or Nginx running.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    munin_packages:
      - python-passlib
      - munin

Packages installed for Munin. If you are running Python 3, you should override this variable and set the first item to `python3-passlib`.

    munin_dbdir: /var/lib/munin
    munin_htmldir: /var/www/html/munin
    munin_logdir: /var/log/munin
    munin_rundir: /var/run/munin
    munin_includedir: /etc/munin/conf.d

Some default locations for Munin-generated files, configurations, logs, etc.

    munin_html_strategy: cron
    munin_graph_strategy: cron
    munin_max_processes: 12

See the official Munin documentation for [munin.conf](http://munin.readthedocs.org/en/latest/reference/munin.conf.html) for more information on these and other optional directives.

    munin_cron_job: present

Determines whether the munin cron job (which runs every 5 minutes) should be active. By setting this to `absent`, you can leave munin installed and configured on your server but effectively disable it. This allows quick enabling or disabling for munin monitoring.

    munin_admin_user: munin
    munin_admin_password: munin

These values will be used to generate a user via htpasswd under which the munin pages will be password protected with basic HTTP authentication. (*Note*: This method only works when Munin is running under default Apache configurations; if you use Nginx or a customized Apache server, you will need to configure authentication on your own).

    munin_hosts:
      - name: "localhost"
        address: "127.0.0.1"
        extra: ["use_node_name yes"]

A listing of hosts to which munin will connect and monitor. Each item in the list will be added to your munin configuration like the following (assuming you're using the above example):

    [localhost]
      address: 127.0.0.1
      use_node_name yes

See documentation for [Munin Node Definitions](http://munin.readthedocs.org/en/latest/reference/munin.conf.html#node-definitions) for more details as to what values to use here.

    munin_alerts:
      - name: "JohnDoe"
        email: "johndoe@example.com"
        subject: "Munin-notification for ${var:group} :: ${var:host}"
        level: "warning critical"

You can configure email alerts using the `munin_alerts` variable.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      roles:
        - geerlingguy.munin

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
