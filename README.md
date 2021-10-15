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
In Client D - Client C example the mask is 255.255.0.0. That means 211.191.0.0 is the network adress and only this part has to be the same in both computers. Client D IP must then start with 211.191.__.___ and the values __ can be anything from 1 to 255 and ___ from 1 to 254. Remember last addres of the network is always used for Broadcast!
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
-
-

![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl3.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl3.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl4.PNG)
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/lvl4.PNG)
-
-
![alt text](https://github.com/psleziak42/net_practice/blob/main/screens/0lvl5.PNG)
-
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
