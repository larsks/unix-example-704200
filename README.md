# Linux can't route traffic from bridge interface

This reproduces the network environment described in <https://unix.stackexchange.com/questions/704200/linux-cant-route-traffic-from-bridge-interface>.

## Requirements

- [Vagrant][]
- Libvirt
- [Ansible][]

[vagrant]: https://www.vagrantup.com/
[ansible]: https://ansible.com/

## Bringing things up

### Create libvirt networks

Vagrant doesn't want to create libvirt networks without setting an address on the host bridge, so instead we pre-create the networks:

```
for lan in {0..2}; do
  virsh net-define net/lan$lan.xml
  virsh net-start lan$lan
done
```

### Start vagrant machines

Due to [bugs in Vagrant][], you must bring the environment up with the `--no-parallel` option:

```
vagrant up --no-parallel
```

[bugs in vagrant]: https://github.com/hashicorp/vagrant/issues/12782
