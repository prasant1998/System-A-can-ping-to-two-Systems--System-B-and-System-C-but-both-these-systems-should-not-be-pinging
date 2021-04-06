# Creating a network Topology Setup in such a way so that System A can ping to two Systems, System B and System C but both these systems should not be pinging each other without using any security rule, eg firewall etc

This Task is an very interesting Task ,which can be used in many types of used case, We need to be well versed with concept of Network Name, Netmask, and Routing Table ,etc

I have done this practical in same network or same range ,As we know If there are many systems in same Network and in order to connect those systems to each other ,We need switch for connecting same networks .

Here I am using Oracle Virtual box and this virtual box gives us pre-created switch , So if we want to attach that switch to VM .We have to go VM setting and in sub heading of network there We just need to select the Option Host only . Same I did for rest of my VM.

![1](https://user-images.githubusercontent.com/67523396/113772069-cfce3c00-9741-11eb-993b-0808a85b9d77.jpeg)



What actually I did …

In System A ,

System B and System C would be in the same network. To ensure this I created a network and then I created a Routing Table in such a way that System A can create packets only for 2 IP’s that will be assigned to System B and System C

Creating IP 192.168.30.1 with range /24 or 255.255.255.0

Commands used :

ifconfig enp0s3 192.168.30.1/24 and ifconfig enp0s3

![2](https://user-images.githubusercontent.com/67523396/113772087-d6f54a00-9741-11eb-9bbc-68a0831a37d0.jpeg)


Now ,Creating a new rule for the network card enp0s3 in the Route Table. It will allow to create packets only for 2 IP’s.

Commands used :

route add -net 192.168.30.0/30 enp0s3 and route -n

![3](https://user-images.githubusercontent.com/67523396/113772104-df4d8500-9741-11eb-9a6b-3a9636e774f0.jpeg)




In System B ,

I created IP (192.168.30.2)which remains in the range of System A and also I created Routing Table in such a way that System B can create packets only for one IP ,ie System A
Creating IP 192.168.30.2 with range /24 or 255.255.255.0

Commands used :

ifconfig enp0s3 192.168.30.2/24 and ifconfig enp0s3

![4](https://user-images.githubusercontent.com/67523396/113772134-eaa0b080-9741-11eb-9751-dc6a42493380.jpeg)


Creating a new rule for the Network card enp0s3 in the Route Table. It will allow to create packets only for 1 IP.

Commands used :

route add -net 192.168.30.0/31 enp0s3 and route -n


![5](https://user-images.githubusercontent.com/67523396/113772182-fbe9bd00-9741-11eb-9e30-25328c47e6dd.jpeg)




In System C ,

I Created IP (192.168.30.3)which remains in the range of System A and also I created Routing Table in such a way that System C can create packets only for one IP ,ie System A
Creating IP 192.168.30.3 with range /24 or 255.255.255.0

Commands used :

ifconfig enp0s3 192.168.30.3/24 and ifconfig enp0s3

![6](https://user-images.githubusercontent.com/67523396/113772198-02783480-9742-11eb-8980-07c0f1fddd21.jpeg)



Creating a new rule for the network card enp0s3 in the Route Table. It will allow to create packets only for 1 IP.


![7](https://user-images.githubusercontent.com/67523396/113772210-07d57f00-9742-11eb-90f7-d88fd839dc3a.jpeg)




Now we have ,

System A — 192.168.30.1

System B — 192.168.30.2

System C — 192.168.30.3

Now testing my Setup

System A

First pinging to System B (192.168.30.2) from System A (192.168.30.1)

We can easily ping from A to B

Command used :

ping 192.168.30.2


![8](https://user-images.githubusercontent.com/67523396/113772230-0dcb6000-9742-11eb-9128-6100a6960070.jpeg)



Pinging from System A (192.168.30.1) to System C (192.168.30.2)

We can easily ping from A to C

Command used:

ping 192.168.30.3

![9](https://user-images.githubusercontent.com/67523396/113772246-115ee700-9742-11eb-949b-defd91e51c1a.jpeg)



System B

First pinging from System B (192.168.30.2) to System A (192.168.30.1)

We can easily ping from B to A

Command used:

ping 192.168.30.1


![10](https://user-images.githubusercontent.com/67523396/113772258-14f26e00-9742-11eb-920e-d18b8df991ff.jpeg)




Pinging from System B (192.168.30.2) to System C (192.168.30.3)

I can’t ping from B to C

Command used:

ping 192.168.30.3


![11](https://user-images.githubusercontent.com/67523396/113772299-23408a00-9742-11eb-8811-9e3cf08f44f2.jpeg)




System C

First pinging from System C(192.168.30.3) to System A (192.168.30.1)

We can easily ping from C to A

Command used:

ping 192.168.30.1

![12](https://user-images.githubusercontent.com/67523396/113772313-2c315b80-9742-11eb-92b5-1c13d2b891c5.jpeg)




Pinging from System C (192.168.30.3) to System B (192.168.30.2)

I can’t ping from C to B

Command used:

ping 192.168.30.2


![13](https://user-images.githubusercontent.com/67523396/113772342-35bac380-9742-11eb-9e07-11d9064963ef.jpeg)


Here I successfully created the Topology that I explained in the Top of my Heading .

Thankyou
