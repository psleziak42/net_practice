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
<br>
<br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl2.PNG)

<br><br>
First thing we have to do here is copy mask from A1 to B1. Then using B1 IP and correct mask we can calculate number of hosts avaliable in this network. Take a look here: <br>
<br>11111111.11111111.11111111.11100000 - MASK (also can be written as /27, that is how many bits belongs to network (they are nr 1))
<br>11000000.10101000.01110000.110|11100 - | shows you values that can be changed in this addres. If you count we have 31 addreses. The 1st one (network addres) is .192 the last one is .223. So host min is 193 and host max is 222.
<br><br>
On the other example you can see /30, that means .11111100. This means you have only 3 addreses to assign. To fulfill the exercice you can choose any other addres than 127.0.0.1 because any addres starting from 127 is special addres and serves as a loopback and it is used to test network cards. Read more about it somewhere in the internet :).

![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl2.PNG)
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl3.PNG)
<br><br>
Here the new element is coming - it is a switch. Before we had 2 computers, but imagine you want to create network of 10 or 200 of them. You would need to have corresponding number of ports in each of your computers to contect all of them with each other. So people invented HUBs and SWITCHes. According to my knowledge Switches are smarter, this means if a message is sent from computer A to computer C Switch knows it and pass it only to computer C, while HUB would forward it to all computers everytime. What would happen next is that the computer(s) that MAC address is not the destination would deny the packet. Still only the destination would accept it but it creates unnecesary traffic. Switches are smart and they have ARP tables that 
<br><br>
So switch is layer 2 device (this in simple words means it operates only inside the network, [router is layer 3 device it connects networks]).
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
<br> ------------------------------------------------------------------------------------------------------------------------------------------------------- <br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl4.PNG)
<br><br>
New element: Router. Router is layer 3 device that is used to connect different networks together (or subnetworks). Routers have multiple entrances and each entry must be places within the same network (have addres IP on the same scope as other components). Anything between routers or on their ends is called LAN - local area network. Hence on this example we have LAN.
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl4.PNG)
<br> ------------------------------------------------------------------------------------------------------------------------------------------------------- <br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl5.PNG)
<br><br>
Here we have one router and 2 LANs. As you can see on the picture below, I marked some elements - they are routing tables. The way it works is that 1. is the destination network and 2 is the exit gateway of the network. Whenever computer creates L3 packet it can say by its network addres and mask if it belongs to his network or foreign network. If it belongs to foreing network it knows imidiatelly that it must be forwarded towards gateway ( talk about obtaining mac adreses and what router sees (directly conected).
<br><br>
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl5.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl6.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl6.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl7.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl7.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl8.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl8.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl9.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl9.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl10.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl10.PNG)
