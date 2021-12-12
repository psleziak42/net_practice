# net_practice
Establishing network adresses, ARP table, Route table, TCP/IP packets

![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl1.PNG)
<br><br>
So the first example is very imporatant. There are 2 sets of computers, both connected to each other directly. Let us focus on the left set.
<br><br>
Take look at the client B computer. There is IP and Mask. Both are grey-ish, that means those values are fixed.
<br><br>
Let us start from IPv4. What is that?
<br><br>
Its a number that is divided into 4 parts, separated by dots. Each number has 8 bits, so maximum value can be 255 (11111111), the minimum 0 (00000000).
<br><br>
What is mask? In the simple words it tells us what values can be changed in IP adress and how much. More precisely it defines NETWORK part of the adress and HOST part of the adress. In case of our example: MASK: 255.255.255.0 IP: 104.63.23.307 NETWORK part is 104.63.23.0 and HOST can be anything between 104.63.23.1 - 104.63.23.254. Why not 255? The last addres of the network is always broadcast. Broadcast message is sent by computer when it wants to discover MAC addreses of another device in the network. MAC addres is necesary to create TCP/IP packet, but i ll try to talk about it a bit later.
<br><br>
Now let us compare both IPs: 104.63.23.12 and 104.93.23.307. 104.63.23.12 - this IP is fixed, so we need to properly adjust IP in the Interface A1. This computers are in the same network, it seems like they are connected directly via cable. So the network part of both adresses must be the same, hence Interface A1 IP needs to start with 104.63.23.__ and __ can be substitued in this example with any value from 1 to 254, except 12 because this adress is already taken by client B.
<br><br>
In Client D - Client C example the mask is 255.255.0.0. That means 211.191.0.0 is the network adress and only this part has to be the same in both computers. Client D IP must then start with 211.191.xx.__ and the values xx can be anything from 1 to 255 and __ from 1 to 254. Remember last addres of the network is always used for Broadcast!
<br><br>
Check below examples, all of them show ok :).
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl1.PNG)
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl1.1.PNG)
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl1.2.PNG)

# Level 2
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl2.PNG)
<br><br>
First thing we have to do here is copy mask from A1 to B1. Then using B1 IP and correct mask we can calculate number of hosts avaliable in this network. Take a look here: <br>
<br>11111111.11111111.11111111.11100000 - MASK (also can be written as /27, that is how many bits belongs to network (they are nr 1))
<br>11000000.10101000.01110000.110|11100 - | shows you values that can be changed in this addres. If you count we have 31 addreses. The 1st one (network addres) is .192 the last one is .223. So host min is 193 and host max is 222.
<br><br>
On the other example you can see /30, that means .11111100. This means you have only 3 addreses to assign. To fulfill the exercice you can choose any other addres than 127.0.0.1 because any addres starting from 127 is special addres and serves as a loopback and it is used to test network cards. Read more about it somewhere in the internet :).
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl2.PNG)

# Level 3
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl3.PNG)
<br><br>
Here the new element is coming - it is a switch. So switch is layer 2 device (this in simple words means it operates only inside the network, [router is layer 3 device it connects networks]). Before we had 2 computers, but imagine you want to create network of 10 or 200 of them. You would need to have corresponding number of ports in each of your computers to contect all of them with each other. So people invented HUBs and SWITCHes. According to my knowledge Switches are smarter, this means if a message is sent from computer A to computer C Switch knows it and pass it only to computer C, while HUB would forward it to all computers everytime. What would happen next is that the computer(s) that MAC address is not the destination would deny the packet. Still only the destination would accept it but it creates unnecesary traffic.
<br><br>
Let us talk yet about ARP (Adres Resolution Protocol) and MAC Tables and how the packet travel across the network.
<br><br>
HOST A wants to communicate with HOST C. HOST A very likely knows all the IP addreses inside its own network (they could be put to any computer by network administrator) but it doesnt know MAC addresses. MAC addres is a unique addres of any device - computer, phone etc. It needs to know this information to create L2 packet (layer 2 packet) that contains of source MAC addres and destination MAC addres. So host a will send a broadcast message to every computer asking "are you 104.198.121.123? If yes give me your MAC addres. It will be answered back only by HOST C and ignored by HOST B. Once it knows HOST C mac address it will save it next to its IP in ARP table. Once packet arrives to HOST C, HOST C will save HOST's A MAC addres so in the future they can comunicate quicker. 
<br><br>
When the informacion is passing back and forth via Switch it saves MAC addreses in MAC table. For instance HOST A is connected to Port 1 HOST B is connected to Port 2 and HOST C is connected to Port 3, MAC table will save that to Port 1 is connected MAC addres aaaa.aaaa.aaaa and to Port 3 cccc.cccc.cccc.
<br><br>
Enough for now.
<br>
The task here is easy. You have given mask and IP and you must put them in the same network. Good luck!
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl3.PNG)

# Level 4
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl4.PNG)
<br>
<br>
New element: Router. Router is layer 3 device that is used to connect different networks together (or subnetworks). Routers have multiple entrances and each entry must be placed within the same network (have addres IP on the same scope as other components). Anything between routers or on their ends is called LAN - local area network. Hence on this example we have LAN.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl4.PNG)

# Level 5
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl5.PNG)
<br>
<br>
Here we have one router and 2 LANs. As you can see on the picture below, I marked some elements - they are routing tables. The way it works is that 1. is the destination network and 2 is the exit gateway of the network. Whenever computer computer gets the destination IP it can say by its network addres and mask if it belongs to his network or foreign network. If it belongs to foreing network it knows imidiatelly that it must be forwarded towards gateway. So first, if the ARP table is empty CLIENT A must obtain MAC addres from gateway, so later it can create Layer3 packet and forward it to neighbour network.
<br><br>
There is one thing I wanted to mention - router has its own routing table. Here 2 networks are directly connected and he sees them. But on the 7th example there will be 2 routers and we will have to manually fill its routing table :)
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl5.PNG)

# Level 6
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl6.PNG)
<br><br>
In this example we have LAN on the right side and Internet on the left side. Starting from the left, everything that goes towards network 50.237.137.128/25 (see picture with solution if you cant find it ;)) is forwarded to gate 163.172.250.12. IP in the LAN must belong to this network 50.237.137.128/25. I used here red circle because in my opinion this routing table is not necesary here. Router is directly connected to the network 55.237.127.128/25 so he knows where to forward traffic. Even if there were many other networks connected it would have them on its routing table knowing where trafic goes. This is useful if router cannot see the network and needs to do so called "hoop" to another router to reach its destination. You will see it in the next level.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl6.PNG)

# Level 7
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl7.PNG)
<br><br>
We have 3 LANs here. Let us call it LAN A1 and LAN C1 and LAN R (between routers it is also LAN even if there is no other computers connected). 
<br><br>
Wewant to forward traffic from A1 to C1. 1st you must notice that A1 and C1 for now have the same family of IP addreses. To make my life easier I used /30 mask that as you remember gives 2 addreses - and this is what we need everywhere. Secondly when the networks are correctly placed we can focus on routing tables. We want to send from A to C, so destination network is (in my case) 99.198.15.0/30 and gateway is 99.198.14.1 (marked as grey). The router R1 will receive the packet and here we have to tell him: whenever traffic goes to 99.198.15.0/30 forward it to the port 99.198.14.253 that is Router R21. This router is then directly connected with the network and it knows how to forward it to the destination. After destination is reached C1 must respond to A1 (it always works this way in any example in TCP/IP - it is slower than UDP protocol because it always requires confirmation that any packet has not been lost on the way. Packet by the way is just bunch of 01010101110 binary messages traveling across the network untill for example picture is fully sent).
<br><br>
On the way back then C1 must speak to A1 "hey i have receive the packet" so we have to configure routing table on router 2 that anytime when packet goes to network 99.198.14.0/30 it will be forwarded to 99.198.14.254.
<br><br>
Understand that its real life example when you establish real network and you must manually put into router's routing table informations so he knows what to do. As said somewhere before it is called static routing table, there exists also dynamic routing tables that fill this information automatically.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl7.PNG)

# Level 8
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl8.PNG)
<br><br>
Here Interface C must communicate with D and both with internet.
Here you have to take a look below on the image and focus on nr 1. It is similar to what we have described before. 
<br><br>
Nr 1 says any message for network 22.67.67.0/26 will be forwarded to router R12, IP 163.180.250.12. What it tells us? On the bottom we have Interface D1 and Interface C1. They are 2 different networks - so can't have the same addreses - and they addreses must fit inside 22.67.67.0/26 network. We must simply subnet the networkwe have and create smaller networks inside 22.67.67.0/26. The mask given on D is .240 on C we can choose so i have chosen .252 as we only have 2 devices. I decided that starting addres on D will be 1 so with .240 (4) mask the broadcast will be 15. So on D network the lowest addres we can choose is 17 (5), because 16 will be network addres. Then nr 3 IP is .62 because nr 2 it says that whenever we want to reach it will be forwarded to 22.67.67.62. I used /30 mask and add addres .61 to R21.
<br><br>
0.0.0.0/0 or default. Take a look on C1 and D1 Routes (routing table). The tasks asks us that C1 must communicate with D1 and with internet. Because we have only one position in the routing table we say that default network we want to reach we will forwart the packet to the gateway. In following exercices you gonna have bigger routing table and you will be able to manually forward trafic towards network you want. I hope it is understandable :).
<br><br>
Also I think that there is an error on R1 routing table. It says 0.0.0.0/0 is forwarded to 163.180.250.1 when the Interface R12 is .12. The white space we fill saying: whatever goes to 22.67.67.0/26 will hop to 22.67.67.61.
<br><br>
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl8.PNG)

# Level 9
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl9.PNG)
<br><br>
This level and level 10 i will leave for you to do. You must apply all the knowledge together and it should not be a big deal anymore.
<br><br>
One thing worth to mention here is: take a look on differences between private and public IPs. Private IPs are used only within network, so devices that belongs to to it can communicate with each other directly. It can be seen only by other devices on that network. Depending on the class (class A mask is 255.0.0.0, B 255.255.0.0 and C 255.255.255.0) the private IPs are as follows: A 10.0.0.0 - 10.255.255.255; B 172.16.0.0 - 172.31.255.255 and C 192.168.0.0 - 192.168.255.255. It seems there is not much of them but they are reused in every internal network. So my computer in my network will have one of this C 192.168.0.0 - 192.168.255.255 and your computher may have the same.
<br><br>
What cannot be duplicated is public IP addres. And usually the devices inside the network have private unique IPs and outside the network each network has one public IP where from and to the internet traffic is sent. This is a response to shortage of IPv4 addreses. There is too many devices and engineers are slowly substituing it with IPv6 that has billions and billions and billions and billions addreses.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl9.PNG)

# Level 10
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl10.PNG)
<br><br>
SOME USEFUL LINKS to understand the project:
<br>IP calculator: http://jodies.de/ipcalc?host=22.67.67.17&mask1=255.255.255.252&mask2=
<br>Packet Travel: https://www.youtube.com/watch?v=rYodcvhh7b8&t=32s
<br>ARP table:     https://www.youtube.com/watch?v=cn8Zxh9bPio
<br>Public/Private IP, NAT: https://www.youtube.com/watch?v=FTUV0t6JaDA
<br><br>
Thank you! I hope you found it usefull. I had enjoyed this project a lot but had some difficulties to understand it since the beginning. Because the program at 42 have changed, most of my friends had done another exercice related to System Administration, and I decided to write this tutorial as I think i am the 1st student at 42 Lisbon who had to face it and I could not find much info on github.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl10.PNG)
