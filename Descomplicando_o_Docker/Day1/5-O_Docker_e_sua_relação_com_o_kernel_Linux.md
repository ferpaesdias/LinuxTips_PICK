# Docker Internals

O Docker utiliza algumas features básicas do kernel Linux para o seu funcionamento. A seguir temos um diagrama no qual é possível visualizar os modulos do kernel de que o Docker faz uso:

```mermaid
flowchart TD;
  docker[docker];
  libcontainer([libcontainer]);
  lxc[lxc];
  systemd-nspawn[systemd-nspawn]
  libvirt[libvirt];
  grupo_linux[**Linux** <br> cgroups namespaces netlink selinux netfilter selinux capabilities apparmor];
  docker --> lxc;
  docker --> systemd-nspawn;
  docker --> libcontainer
  docker --> libvirt;
  libcontainer --> grupo_linux;
  libvirt --> grupo_linux;
  lxc --> grupo_linux;
  systemd-nspawn --> grupo_linux;
```
