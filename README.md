## Using Docker Macvlan in Virtualbox
04 Feb 2018



Suppose you need to get your containers exposed directly to the network via macvlan, and you have a network with the settings:
`192.168.1.0/24` and a gateway of `192.168.1.1`, with a host interface of `enp0s3`

Setting up the macvlan network would be as straightforward as configuring the setup with the parent interface:

`docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=enp0s3 macvlan`

then setting up two containers to test it:

`docker run -it --net=macnet --ip=192.168.1.10 --rm joffotron/docker-net-tools`
`docker run -it --net=macnet --ip=192.168.1.11 --rm joffotron/docker-net-tools`

Both containers would be able to ping each other, this works well enough in a normal machine.

However in Virtualbox the containers wouldn't be able to ping each other with the default network emulation.

You'll need to change the settings on the Adapter type to **PC-net-FAST III** to allow the containers to work.

