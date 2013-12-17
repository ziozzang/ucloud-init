ucloud-init
===========

* code by Jioh L. Jung (ziozzang@gmail.com)

UCloud System Init Script

Installation
============

* Centos 5.X, 6.X/Fedora 13 ucloud-init installation

```
curl https://raw.github.com/ziozzang/ucloud-init/master/install-centos | bash
```


* Ubuntu 10.4, 12.4 /Debian 6 ucloud-init installation

```
wget -qO- https://raw.github.com/ziozzang/ucloud-init/master/install-ubuntu | bash
```


* SUSE 11 ucloud-init installation

```
wget -qO- https://raw.github.com/ziozzang/ucloud-init/master/install-suse | bash
```


* Reset ucloud-init installation

```
wget -qO- https://raw.github.com/ziozzang/ucloud-init/master/reset-ubuntu | bash
```


* Set Kernel Update Pending while apt-get upgrade (for Ubuntu)

```
wget -qO- https://raw.github.com/ziozzang/ucloud-init/master/kernel-pending-ubuntu | bash
```

Usages
======

```

Usage:
  cat userdata_file | ucloud-init --pre-config-commands
  cat userdata_file | ucloud-init --post-config-commands
  cat userdata_file | ucloud-init --config-commands [--as-if-first-boot]
  ucloud-init --make-as-first-boot
 
 
    -i, --pre-config-commands        Executes initial commands
    -f, --post-config-commands       Executes final commands
    -c, --config-commands            Executes configuration commands
    -b, --as-if-first-boot           Run as if first boot
    -m, --make-as-first-boot         Make as first boot

```


Syntax
======

```

# ucloud-init userdata example
 
 
# ucloud-init은 아래의 주석처럼 세 부분, 즉 pre-config commands, config
# commands, post-config commands, 으로 구성되며 이 순서대로 수행된다.
 
 
# start of config commands
#
# 다음과 같은 명령으로 이 섹션을 수행할 수 있다.
#
# `cat userdata_file | ucloud-init --config-commands [--as-if-first-boot]'
#
# 이 섹션은 최초의 부팅시에만 수행되는 데 --as-if-first-boot 옵션이 주어지면
# 가리지 않고 수행한다.
 
 
# 첫 부팅시에 패키지 업데이트 여부
#
# default: true
#
package_update: true
 
 
 
 
# 첫 부팅시 설치할 패키지 리스트
#
# 하나의 패키지라도 지정되면 package_update 값을 true로 설정한 것으로 간주한다.
#
packages:
- lame
- nodejs
 
 
 
 
# 첫 부팅시 호스트네임 설정
#
hostname: bahia
 
 
 
 
# 사용자 관리
#
# 첫부팅시 추가할 사용자와 비밀번호를 설정. 비밀번호로 R 또는 RANDOM으로
# 지정하면 임의의 값이 지정된다.
#
users:
  - hrcho qwer1234
  - neo 1111
  - yoodoc R
  - beergun jkljkl..
  - joybro hahaha
 
 
 
 
# ssh authorized keys 지정
#
# 해당 사용자의 ssh 키를 ~/.ssh/authorized_keys 파일에 추가한다. 이 기능을
# 이용하면 사용자가 패스워드 없이 PKI 기반으로 로그인할 수 있다.
#
ssh_authorized_keys:
  - hrcho ssh-dss AAAAB3NzaC1kc3MAAAEBAL2JJSvCeL8yb31gT3OsBz2LugGczY1f3IsTuIC6LRdRLUvKxWHTgh/oWVB2PSkcU/ozB71++EDU5lb/j9D9aChLb/y+y+BU3ORTkbQvg+V7K81VwXo7Z71lHOgh2mTRC25oHmEOtqFAzALHE5cB2f3hBSIWMREWRMSpJscaHPo9fZ5TRWoaHwhEosw+7vif4nXgV/mOfNxZ/O0twHDDGtRHzrOiXu7im6hfy9jGuulGhvrm8VoXwz5dO6VpTeFNblgSiNkVorv6Oun4FW0hN0p4hZ2SvJY66Dvc9GvXJjqXfUeNlRzttL5LknFhYQgnUyvhIolUrW1X1o2feuNRv6EAAAAVAJ8MMasdrG+mOhEghHjBQ8L1zgD7AAABAFyQ4ty9daIqSQ/c9qyZsqr4+dUhUt+fLhZvNOT5IdOxqgiAk3i8cN8lAYU77kt6tE2iTUKoNWDxY1nRb2EmPyJG6gHec/GJMGnL1V8umc8nE1kZj0xGxSOxzqQ4AuCwESbL++6STfhoQ5gqH/y4Eo6qLeVO0OrFkKkf4VwAVi0w1owqC4cDkhs+mePOTFmYqzyNVBCBauZ8Dx+B1d2fxshX72zs2FrppJgMbQZXCgwhsMH+u9hh1JvMjMGymYggyWM3MQ+G7j1j4ufDN4SmZeMCU8HrSIEqmwK3AviILTazZFa1g9W8oYhT0rOOJh2V/U0GJfMPVNI1JYPQeUwPCb0AAAEAcRvCQgZJcUEXvaieC5D18soeSD1blux3l5acFxzg/NGFM1iqqNR7tE2ke2LMLDIfCbWiSO1maVR8RlXyHdWOJHGDJC5XS4mhC/iPUDM5JjSalgdNeeZgHvrcAEL81DarkU6vSj0nViWYScC3iDFRuD74Zny5iG4P9NjRG/qoWc1VCYMNnvhKFuDGjINKXY4wXRuHdVzHQFsnzsNWkQByeG8dmf8uht0prBpFPGH0LzmxZI12j1fwSFKBYoUZYz5WSDwFwUwryN1Y8YgG84QyNDU0zhzJMgOYlA5Qxk6XA6nxcpSbBZTunQIYE1uUx9+ak7Pt986yPcU5LUl1pQN79g== seafarer@sea.local
  - yoodoc ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA3I7VUf2l5gSn5uavROsc5HRDpZdQueUq5ozemNSj8T7enqKHOEaFoU2VoPgGEWC9RyzSQVeyD6s7APMcE82EtmW4skVEgEGSbDc1pvxzxtchBj78hJP6Cf5TCMFSXw+Fz5rF1dR23QDbN1mkHs7adr8GW4kSWqU7Q7NDwfIrJJtO7Hi42GyXtvEONHbiRPOe8stqUly7MvUoN+5kfjBM8Qqpfl2+FNhTYWpMfYdPUnE7u536WqzFmsaqJctz3gBxH9Ex7dFtrxR4qiqEr9Qtlu3xGn7Bw07/+i1D+ey3ONkZLN+LQ714cgj8fRS4Hj29SCmXp5Kt5/82cD/VN3NtHw== smoser@brickies
 
 
shell_commands:
- "echo 'hello world!: I love this world!'"
 
 
# start of pre-config commands
#
# 매회 부팅시 루트 파일 시스템이 마운트된 직후 수행된다. 개별 아이템은 sh를
# 통해 수행된다. 다음과 같은 명령으로 이 섹션을 수행할 수 있다.
#
# `cat userdata_file | ucloud-init --pre-config-commands'
#
# 주의할 점은, yaml 형식에서 ':'와 같은 문자는 특수하게 해석되므로 아래의 첫
# 번째 예처럼 큰 따옴표로 둘러싸서 해석을 막아야 한다. 아래의 두번째 예 처럼
# 여러줄에 걸친 값을 표현하기 위한 yaml 문법, 즉 '|'을 사용할 때는 신경쓰지
# 않아도 된다.
#
pre-config-commands:
- "echo 'hello world!: I love this world!'"
- |
   #!/bin/sh
   date
 
 
 
 
# start of post-config commands
#
# pre-config commands와 비슷하지만 rc.local 수준에서 수행된다.
# 다음과 같은 명령으로 이 섹션을 수행할 수 있다.
#
# `cat userdata_file | ucloud-init --post-config-commands'
#
post-config-commands:
- echo hello!
- |
   #!/bin/sh
   ls
```
