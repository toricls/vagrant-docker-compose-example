vagrant-docker-compose-example
==

A Simple example to use Docker Compose as Vagrant provisioner, with CoreOS.

Created on following environments.

- OS X El Capitan 10.11.1
- Vagrant 1.7.4
- VirtualBox 5.0.8
- CoreOS stable 766.5.0
- Docker Compose 1.5.0

## Requirements

- [vagrant-docker-compose](https://github.com/leighmcculloch/vagrant-docker-compose)
- [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater)

Install plguins

```
$ vagrant plugin install vagrant-docker-compose
$ vagrant plugin install vagrant-hostsupdater
```

## Start Virtual Machine

```
$ cd /path/to/repos
$ vagrant up
```

Once provisioning done successfully, you can confirm a working nginx application via browsers by accessing to [`http://vagrant-docker-compose-example.localhost.com`](http://vagrant-docker-compose-example.localhost.com).

## Contribution

1. [Fork](https://github.com/orih/vagrant-docker-compose-example/fork)
2. Create a feature branch
3. Commit your changes
4. Rebase your local changes against the master branch
5. Create a new Pull Request

## Licence

[MIT](https://github.com/orih/vagrant-docker-compose-example/blob/master/LICENCE)

## Author

[Orih](https://github.com/orih)
