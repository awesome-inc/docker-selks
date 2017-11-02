# docker-selks

Docker based Suricata, Elasticsearch, Logstash, Kibana, Scirius aka SELKS.

Similar to [StamusNetworks/Amsterdam](https://github.com/StamusNetworks/Amsterdam) but without Python.

## Setup

On Linux

- Install [docker](http://docker.io).
- Install [docker-compose](http://docs.docker.com/compose/install/).
- Clone this repository

Then, start your stack using *docker-compose*:

```bash
docker-compose up
```

On Windows, use [Vagrant](https://www.vagrantup.com/) or [Docker for Windows](https://docs.docker.com/docker-for-windows/)

For Vagrant be sure to have the following vagrant plugins installed

- [vagrant-proxyconf](https://github.com/tmatilai/vagrant-proxyconf) when behind a croporate proxy
- [vagrant-docker-compose](https://github.com/leighmcculloch/vagrant-docker-compose)
- [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)
- [vagrant-cachier](https://github.com/fgrehm/vagrant-cachier)

Start up the box

```bash
vagrant up
```

Next, access

- [Scirius](http://localhost:8080/) with `scirius/scirius` as login/password,
- [Kibana](http://localhost:5601/) and
- [Evebox](http://localhost:5636/).

Connect into the box via ssh/putty on `127.0.0.1:2222` with standard login `vagrant/vagrant`. Then,

```bash
cd /vagrant
docker-compose [ps,logs, ...]
```
