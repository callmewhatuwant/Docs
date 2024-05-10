# Lab: Docker Networking

## Host Networking

```sh
  * bridge
  * host
  * peer
  * none
```

Examine the existing network

```sh
docker network ls

NETWORK ID          NAME                DRIVER              SCOPE
b3d405dd37e4        bridge              bridge              local
7527c821537c        host                host                local
773bea4ca095        none                null                local
```

Creating new network

```sh
docker network create -d bridge mynet
```

validate

```sh
docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
b3d405dd37e4        bridge              bridge              local
7527c821537c        host                host                local
4e0d9b1a39f8        mynet               bridge              local
773bea4ca095        none                null                local
```

```sh
docker network inspect mynet


[
   {
       "Name": "mynet",
       "Id": "4e0d9b1a39f859af4811986534c91527146bc9d2ce178e5de02473c0f8ce62d5",
       "Created": "2018-05-03T04:44:19.187296148Z",
       "Scope": "local",
       "Driver": "bridge",
       "EnableIPv6": false,
       "IPAM": {
           "Driver": "default",
           "Options": {},
           "Config": [
               {
                   "Subnet": "172.18.0.0/16",
                   "Gateway": "172.18.0.1"
               }
           ]
       },
       "Internal": false,
       "Attachable": false,
       "Ingress": false,
       "ConfigFrom": {
           "Network": ""
       },
       "ConfigOnly": false,
       "Containers": {},
       "Options": {},
       "Labels": {}
   }
]
```

### Launching containers in different bridges

Launch two containers **nt01** and **nt02** in **default** bridge network

```sh
docker container run -idt --name nt01 alpine sh
docker container run -idt --name nt02 alpine sh
```

Launch two containers **nt03** and **nt04** in **mynet** bridge network

```sh
docker container run -idt --name nt03 --net mynet alpine sh
docker container run -idt --name nt04 --net mynet alpine sh
```

Now, lets examine if they can interconnect,

```sh
docker exec nt01 ifconfig eth0
docker exec nt02 ifconfig eth0
docker exec nt03 ifconfig eth0
docker exec nt04 ifconfig eth0
```

This is what I see

nt01 :  172.17.0.18

nt02 :  172.17.0.19

nt03 :  172.18.0.2

nt04 :  172.18.0.3

Create a table with the ips on your host.  Once you do that,

Try to,

```sh
  * ping from **nt01** to **nt02**  
  * ping from **nt01** to **nt03**  
  * ping from **nt03** to **nt04**  
  * ping from **nt03** to **nt02**  
```

e.g.

[replace ip addresses as per your setup]

```sh
docker exec nt01  ping 172.17.0.19

docker exec nt01  ping 172.18.0.2

docker exec nt03  ping 172.17.0.19

docker exec nt03  ping 172.18.0.2
```

Clearly, these two are two differnt subnets/networks even though running on the same host. **nt01** and **nt02** can connect with each other, whereas **nt03**  and **nt04** can connect. But connection between containers attached to two different subnets is not possible.

#### Using None Network Driver

```sh
docker container run -idt --name nt05 --net none alpine sh

docker exec -it nt05 sh

ifconfig
```

#### Using Host Network Driver

```sh
docker container run -idt --name nt05 --net host  alpine sh

docker exec -it nt05 sh

ifconfig
```

### Observe docker bridge, routing and port mapping

Exercise: Read about [**netshoot** utility here](https://github.com/nicolaka/netshoot)

Launch netshoot and connect to the host network

```sh
docker run -it --net host --privileged  nicolaka/netshoot
```

Examine port mapping,

```sh
iptables -nvL -t nat
```

Traverse host port to container ip and port.

Observe docker bridge and routing with the following command,

```sh
brctl show

ip route show
```
