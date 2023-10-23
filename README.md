# ansible-infra
ansible infra creation
1. Download Sonatype Nexus Repository Manager with URI module:
get_url:
  url: https://download.sonatype.com/nexus/3/nexus-3.21.1-02-unix.tar.gz
  dest: /opt/nexus-3.21.1-02-unix.tar.gz
2. Extract Sonatype Nexus Repository Manager with URI module:
unarchive:
  src: /opt/nexus-3.21.1-02-unix.tar.gz
  dest: /opt/nexus
3.Create Nexus user and group with URI module:
user:
  name: nexus
  group: nexus
4.Change ownership of Nexus home directory with URI module:
file:
  path: /opt/nexus
  owner: nexus
  group: nexus
5.Create Nexus systemd service file:
template:
  src: nexus.service.j2
  dest: /etc/systemd/system/nexus.service
6.Reload systemd configuration:
systemd:
  daemon_reload: yes
7.Start Nexus service:
service:
  name: nexus
  state: started
8.Enable Nexus service to start on boot:
systemd:
  name: nexus
  enabled: yes

