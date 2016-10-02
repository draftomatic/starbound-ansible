# Starbound Server Ansible Role (CentOS 7)

Installs/updates and configures Starbound server on a CentOS 7 machine. 

Example playbook run:
	
    ansible-playbook roles/starbound-ansible/main.yml -e "hosts=server1 steam_user=steamuser steam_password=abc123 config_file=files/starbound_server.config"

`config_file` is optional and will copy a server configuration file. An example configuration file is in `files/starbound_server.config`. You should edit this file (such as changing the default admin password) before running.

NOTE: The first time you log in with steamcmd (which this role does) from a new IP address, you will be sent an email with a verification code. This will cause this role to fail as it cannot enter the code. Log in to the server and run `/opt/steamcmd/steamcmd.sh +login myuser mypassword` to verify the machine, then re-run the role.

A [systemd](https://en.wikipedia.org/wiki/Systemd) service will be installed and enabled for the `starbound` user, which will start the starbound server on boot. 

To start the server manually:
	
    systemctl start starbound

This role does not configure iptables or other firewalls. Make sure the configured bind port (default 21025) is open in iptables and your network firewall.