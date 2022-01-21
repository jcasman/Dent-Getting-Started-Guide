# Features, how to use
This section will cover userspace tools available in the dentOS.

## dentOS userspace

Upon booting and logging into the Linux shell, dentOS provides various standard Linux commands and utilities to configure and monitor the system, such as `coreutils`, `vim`, `htop`, `tree`, etc.
Providing access to the outside network is one of the most important switch functionalities. There are numerous tools to verify a working network connection, with perhaps the most commonly used being `ping` tool provided by the `iputils` package. 
```
root@localhost ~ # ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=116 time=30.5 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=116 time=30.3 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=116 time=29.8 ms
```

dentOS also provides various userspace tools that support different network protocols, such as `frr` [1], `mstpd` [2], `iproute` [3], `bridge-utils` [4] and others.
There are several documentation resources for tools that are included in the dentOS:
- Official web pages
- Project git repositories
- Man pages

Official web pages can be found by typing the name of the relevant tool in a web search engine, which will usually lead us to the official web page for a project. 
Project git repositories can also provide additional information in form of documents such as READMEs, HOWTOs and others.
Another useful documentation resource are man pages, which are reference manuals, each of which covers a specific Linux tool, command or a library. They are easily accessible from the command line and can be navigated through using only keyboard. Manpages will often mention the official web page of a given project/tool and the link is usually located at the bottom of the page.


In the following paragraphs we will provide basic templates for configuring tools such as `frr` and `mstpd`.

## FRR
[FRR](https://frrouting.org/) is a software IP routing suite. It includes daemons for various routing protocols such as BGP, RIP, OSFP and others. It is a suite of daemons where each major protocol is implemented in its own daemon, who communicate with the "middle" daemon, `zebra` which handles routing decisions and talking to the dataplane.
FRR provides many daemons and offers a multitude of configuration options so we will be able to only briefl cover basic configuration. For more detailed instructions please refer to the official [FRR documentation](https://docs.frrouting.org/en/latest/overview.html).

Before starting FRR we need to enable daemons by editing the configuration file, which is located at `/etc/frr/daemons` and determines which daemons will be activated. By default all daemons are turned off so we have to enable ones we want to start. Example snippet od the default configuration file:
```
bgpd=no
ospfd=no
ospf6d=no
ripd=no
ripngd=no
isisd=no
pimd=no
ldpd=no
nhrpd=no
```
For a given daemon we want to enable, change the corresponding value to from `no` to `yes`. 
In order for the changes to take effect we need to reload the entire `frr` servoce. 
This includes starting daemons that were previously stopped (and vice-versa) and applying any changes to deamon configuration files. 
If a daemon is currently not runing and we want to enable it, we can do so with the following change:
```diff
# enable ripd daemon
- ripd=no
+ ripd=yes
```
We can use the `/usr/lib/frr/frrinit.sh` script to reload all daemons:
```
# reload all daemons
~ $ sudo sh /usr/lib/frr/frrinit.sh reload
```

FRR provides a interactive shell tool `vtysh` where we can run individual configuration or show various commands.

## mstpd
[Mstpd](https://github.com/mstpd/mstpd) (Multiple Spanning Tree daemon) is a user-space daemon which supports STP, RSTP and MSTP protocols, and contain various useful features for switching devices, such as Bridge assurance, BPDU guard and Enhances statistics.  
`mstpctl(8)` tool is used to configure the mstpd daemon itself. It is also used to configure STP bridges that have user-space STP enabled. Note that STP is currently disabled by default on the bridge, so we need to enable it using `brctl` or `ip` tools:
```
# enable user-space STP using brctl
~ $ brctl stp <bridge> on

# enable user-space STP using ip
~ $ ip  link  set <bridge> type bridge stp_state 1
```
`mstpctl(8)` can be used to configure certain spanning tree protocol parameters according to the IEEE 802.1D-2004 and 802.1Q-2005(-2011) standards.

Example commands for STP configuration:
```
# set maximum age (in seconds) of a given bridge
~ $ mstpctl setmaxage <bridge> <max_age>

# set forward delay (in seconds) for a given bridge
~ $ mstpctl setdelay <bridge> <time>

# set maximum number of hops for a given bridge
~ $ mstpctl setmaxhops <bridge> <max_hops>
```

Example STP show commands:
```
# show information of a given bridge's CIST instance (if <bridge> parameter is not passed, it will show info for all bridges)
~ $ mstpctl showbridge [<bridge>]

# show information about the port of a given bride's CIST instance (if <port> parameter is not passed, it will show info for all ports)
~ $ mstpctl showport <bridge> [<port>]

# show information of the bridge's MST instance with id (mstid)
~ $ mstpctl showtree <bridge> <mstid>
```

For more information about `mstpd` please consult the [mstpd GitHub repository](https://github.com/mstpd/mstpd) and the `mstpctl(8)` man page (`man mstpctl`).


[1] - https://frrouting.org/

[2] - https://github.com/mstpd/mstpd

[3] - https://wiki.linuxfoundation.org/networking/iproute2

[4] - https://www.linuxfromscratch.org/blfs/view/svn/basicnet/bridge-utils.html
