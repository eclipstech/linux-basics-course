# Switching & Routing 

  - Take me to the [Tutorial](https://kodekloud.com/topic/networking-basics/)

  #### Switching

  - Switching helps to connect the interface within same network.

    ![switch](../../images//switch.PNG)

  - To see the interfaces on the hosts use **`ip link`** command

  ```
  [~]$ ip link
  eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode
  DEFAULT group default qlen 1000
  ```

  -  To connect to the switch we use **`ip addr add`** command

  ```
  [~]$ ip addr add 192.168.1.10/24 dev eth0
  ```

  #### Routing

  - Router helps to connect to two seprate networks together.

    ![route](../../images//routing.PNG)

  - To see the existing routing table configuration run the **`route`** command.

  ```
  [~]$ route
  Kernel IP routing table
  Destination Gateway Genmask Flags Metric Ref Use Iface
  ```

  - To configure a gateway on system B to reach the system on other network run

  ```
  [~]$ ip route add 192.168.2.0/24 via 192.168.1.1
  ```
  
  ```
  [~]$ route
  
  Kernel IP routing table
  Destination Gateway Genmask Flags Metric Ref Use Iface
  192.168.2.0 192.168.1.1 255.255.255.0 UG 0 0 0 eth0
  ```

  - To see the ip addresses assign to interfaces use

  ```
  [~]$ ip addr
  ```

  - 

  ```
  [~]$ ip route
  ```

  - To make this changes permanent you must set them in **`/etc/network/interfaces`** file.


# HANDS-ON LAB

  -  Lets get our hands on [LABS](https://kodekloud.com/courses/873064/lectures/17074533)

**LAB NETWORK-Basics**


Run: **ip a** and check the IP address assigned (besides the localhost 127.0.0.1)

Q: What is the name of the interface that has this IP (from the previous question) address assigned?

S: Run: **ip a** and check the interfaces to which the IP's is assigned or
   Run: **ip link**
Q: What is the default gateway configured in the system?

S: Run: **ip r** and check the GW assigned to default route.It should be 172.16.238.1

Q: We have an apache which should be accessible on devapp01-web. 
   This server runs on port 80 on the server and should be accessible from Bob's laptop.
   However, something seems to be wrong with the network! 
  Check if you are able to connect to the HTTP port 80 on the server devapp01-web from Bob's laptop?
  Run a **Telnet port 80 on devapp01-web** to test.
  
S: Run: **telnet devapp01-web 80** and check if it's successful.

Q: Are you able to ping devapp01-web server?

S: **sudo ping devapp01-web**

Q: Luckily, this webserver has two interfaces. The second interface is on another network and is identified by the name devapp01. Check if you are able to ping devapp01
  Is ping working now?
  
S: **sudo ping devapp01**

Q: Let's troubleshoot from the other end. SSH to the webserver by running ssh devapp01
   Use Bob's default password: caleston123
   Inspect the interface eth0 on devapp01, is it UP?
   
S: run: **ip link** and look at the status of the interface starting with **eth0**

Q: Bring up the eth0 interface

S: Run: **sudo ip link set dev eth0 up**

Q: While we are at it, there is also a missing default route on the server devapp01.
   Add the default route via eth0 gateway.
   
S: To add the default route via eth0 gateway, run the following command: 
   **sudo ip r add default via 172.16.238.1**
   To delete the default route using the ip r command, you can use the following command:
  ** sudo ip r del default**
   This command removes the default route from the routing table. Make sure to run the command with appropriate permissions, such as using sudo, to have the necessary privileges     to modify the routing table.
