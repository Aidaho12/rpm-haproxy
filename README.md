[![Github All Releases](https://img.shields.io/github/downloads/DBezemer/rpm-haproxy/total.svg)](https://github.com/DBezemer/rpm-haproxy/releases)

This repository contains some build artifacts of HAproxy that are provided with no support and no expectation of stability.
The recommended way of using the repository is to build and test your own packages.

# RPM Specs for HAproxy on CentOS / RHEL / Amazon Linux with default syslog

Perform the following steps on a build box as a regular user.

## Install Prerequisites for RPM Creation

    sudo yum groupinstall 'Development Tools'

## Checkout this repository

    cd /opt
    git clone https://github.com/DBezemer/rpm-haproxy.git 
    cd ./rpm-haproxy
    git checkout 2.1

## Build using makefile
### Basic building, no additional components
    make

### With Lua support
    make USE_LUA=1
    
### With Prometheus Module support
    make USE_PROMETHEUS=1
    
### Without sudo for yum
    make NO_SUDO=1

### With a custom release iteration, e.g. '2' (default '1'):
    make RELEASE=2

### Custom CFLAGS, e.g. '-O0' to disable optimization for debug:
    make EXTRA_CFLAGS=-O0

Resulting RPM will be in `/opt/rpm-haproxy/rpmbuild/RPMS/x86_64/`

## Build using Docker
    make run-docker
    
    Resulting RPMs will be in `./RPMS/`
    When updating any of the files that are included in the build phase, ensure that you also bump the release number


## Credits

Based on the Red Hat 6.4 RPM spec for haproxy 1.4 combined with work done by 
- [@nmilford](https://www.github.com/nmilford)
- [@resmo](https://www.github.com/resmo) 
- [@kevholmes](https://www.github.com/kevholmes)
- Update to 1.8 contributed by [@khdevel](https://github.com/khdevel)
- Amazon Linux support contributed by [@thedoc31](https://github.com/thedoc31) and [@jazzl0ver](https://github.com/jazzl0ver)
- Version detect snippet by [@hiddenstream](https://github.com/hiddenstream)
- Conditional Lua build support by [@Davasny](https://github.com/Davasny)
- Conditional Prometheus support by [@mfilz](https://github.com/mfilz)
- Debug Building and Dynamic Release version support by [@bugfood](https://github.com/bugfood)

Additional logging inspired by https://www.percona.com/blog/2014/10/03/haproxy-give-me-some-logs-on-centos-6-5/
