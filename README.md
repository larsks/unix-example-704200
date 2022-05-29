# Linux can't route traffic from bridge interface

This reproduces the network environment described in <https://unix.stackexchange.com/questions/704200/linux-cant-route-traffic-from-bridge-interface>.

## Requirements

- [Vagrant][]
- Libvirt
- [Ansible][]

[vagrant]: https://www.vagrantup.com/
[ansible]: https://ansible.com/

## Bringing things up

Due to [bugs in Vagrant][], you must bring the environment up with the `--no-parallel` option:

```
vagrant up --no-parallel
```

[bugs in vagrant]: https://github.com/hashicorp/vagrant/issues/12782
