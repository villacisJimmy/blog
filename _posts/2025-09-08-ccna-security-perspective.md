 ---
layout: post
title: "Cisco - CCNA Security Perspective"
date: 2025-09-08
categories: [blog]
 ---
 
# Title  
Cisco - CCNA Security Perspective

This write is my perspective on CCNA with a focus on cybersecurity. 


Device access:
- SSH (encrypts the content)
- Telnet (sends data as clear-text data)
- Console cable to the port console
 User modes:
1. User EXEC mode (user mode), the prompt shows “>”
2. Enable mode (privileged mode or privileged EXEC mode) (gets its name from the enable command), the prompt shows “#”
3. Configuration mode (non-disruptive commands, display some information, change switch configuration), commands that tell the switch the details of what to do and how to do it. Changes the configuration immediately. - hostname(config)# -> [Global] mode, first mode after [configure terminal] command.
 Password Security for CLI Access from the console: ■ By default, the console requires no password at all, and no password to reach enable mode for users that happened to connect from the console.
	■ The reason is that if you have access to the physical console port of the switch, you already have pretty much complete control over the switch. As an example, Follow well-published procedures to go through password recovery to break into the CLI and then configure anything you want to configure.

——————> [Password Recovery to gain access] <————————

The next method is just a reference, but you can search on the internet for documentation and instructions for your device model. 

- You would enter the [break sequence] on the keyboard when first powering up the router to access the common prompt
- When you get access to the common prompt, you should be able to see the [rommon 1>]
- Rommon 1 > confreg 0x2142 
- It’s used on Cisco routers to set the configuration register value to 0x2142, which causes the router to ignore the startup configuration stored in NVRAM during the next boot.
- rommon 2 > reset
- The device should boot into the setup wizard. Exit out of the wizard. You will see something like this:

— System Configuration Dialog —
Continue with configuration dialog? [yes/no]: no   (write no into this option)

- # show running-config
- The running configuration should be empty because the router bypassed loading the startup config on boot up. The startup config should remain unchanged, and all previous configurations should still be there.
- # show running-config
- On this point, if you want to conserve the information without applying a factory reset, you must copy the startup config to the running config
- # copy startup-config running-config
- Remove the enable secret
- (config)# no enable secret
- Ensure the router will reboot normally on the next reload, and you will be able to access the device
- (config)# config-register 0x2102
- (config)# end
- # copy running-config startup-config
- Reboot the device to confirm
- # reload

——————> [Password Recovery to gain access] <————————


Many people go ahead and set up simple password protection for console users. Simple passwords can be configured at two points in the login process from the console:
- When the user connects from the console
- When any user moves to enable mode (“enable” command)


Basic password configuration: 
This configuration defines the password that all users must use to reach enable mode. No matter whether users connect from the [Console, Telnet, SSH], they would use the password [test] when prompted for a password after typing the [enable command]
 1. # enable secret [test]

The next configuration configures the console password 

2. 	# line console 0			[identifies the console, means “these next commands apply to the console only”] 2.1 	# login 				[Tells IOS to perform simple password checking (at the console)] 2.2	# password [ccnapass]	[Defines the password, the console user must type when prompted]  [IMPORTANT]: By default, the switch does not ask fro password for console users, as consequence you can acquire privileges options direct on [privileged EXEC mode “#”].
 Three internal types of memory on Cisco Switches: ■ RAM (DRAM): Working storage, running active configuration file is stored here. ■ ROM: stores the bootstrap (boot-helper) program that is loaded when the switch is first powered on. Manage the process of loading CiscoIOS into RAM. ■ NVRAM: Stores the initial or startup configuration file or startup configuration file. Used when the switch is first powered on and when the switch is reloaded.

NVRAM -> startup-config -> initial configuration used anytime the switch reloads Cisco IOS.
RAM -> running-config -> currently used configuration (If I changed any configuration must be saved on NVRAM to make the configuration permanent)


From a security perspective is relevant to understand these commands: ■ # copy running-config startup-config [overwrite the initial configuration]
The next three erase the initial configuration
■ # write erase
■ # erase startup-config
■ # erase nvram:
  [IMPORTANT]: 
- Switches work on layer 2; there’s one exception, a “layer 3 switch”.
- The communication is through the use of the MAC address 
- The MAC address table has other names as switching table, bridging table, and Content-Addressable Memory (CAM) table.
- The forwarding decision is based on the MAC address table [mac address + switch port]

Learning MAC addresses process: “Switches build the address table by listening to incoming frames and examining the source MAC address in the frame. If a frame enters the switch and the source MAC address is not in the MAC address table, the switch creates an entry in the table. That table entry lists the interface from which the frame arrived.”


————————> [ARP attack] <—————————————

LAN network attack

ARP is the protocol responsible for relating the IP and MAC addresses
- Obtaining the physical address of a system by knowing its IP address

The address resolution protocol 
- IP routing logic requires that hosts and routers encapsulate IP packets inside data-link layer frames. 
- For Ethernet interfaces, how does a router know what MAC address to use for the destination? It uses ARP. 

On Ethernet LANs, whenever a host or router needs to encapsulate an IP packet in a new Ethernet frame, the host or router knows all the important facts to build that header—except for the destination MAC address. 
- The host knows the IP address of the next device, either another host IP address or the default router IP address. 
- The hosts and routers do not know those neighboring devices’ MAC addresses beforehand.

TCP/IP defines the Address Resolution Protocol (ARP) as the method by which any host or router on a LAN can dynamically learn the MAC address of another IP host or router on the same LAN.
- ARP defines a protocol that includes the ARP Request, which is a message that makes a simple request, “if this is your IP address, please reply with your MAC address.”
- ARP also defines the ARP Reply message, which indeed lists both the original IP address and the matching MAC address. 

ARP Request sent by node1, as a LAN broadcast
All devices on the LAN will then process the received frame. 
Host node2 sends back an ARP Reply, identifying node2’s MAC address
Each message shows the contents inside the ARP message itself, which lets node2 learn node1’s IP address and matching MAC address, and node1 learn node2’s IP address and matching MAC address. 

[IMPORTANT]: Note that hosts and routers remember the ARP results, keeping the information in their ARP cache or ARP table. 

A host or router only needs to use ARP occasionally, to build the ARP cache the first time. 
- Each time a host or router needs to send a packet encapsulated in an Ethernet frame, it first checks its ARP cache for the correct IP address and matching MAC address. 
- Hosts and routers will let ARP cache entries time out to clean up the table, so occasional ARP Requests can be seen. 

**You can see the contents of the ARP cache on most PC operating systems by using the [arp -a] command from a command prompt.**

[ARP Spoofing Tool]: Cain & Abel (Windows environments)

With the information arriving in the system, there’s no mechanism to prevent the information will being processed by those who shouldn’t. Sniff has been called a technical denomination.

"Sniffing" is the technique that limits precisely that bit of chivalry with which communications technology was conceived.
- The technique makes it prone to processing any information that reaches it using [promiscuous mode].
- The sniffer is simply the tool that does just that: it allows a network card to behave promiscuously.

The sniffer doesn't capture traffic; it simply processes the packets it receives.

In an Ethernet network with switches, frames must be considered to have a specific source and destination at the Layer 2 level, and switches enforce this. This way, a third party won't receive the conversation being held by two other systems on a network with switches.

[Sniffing]: technique
[Sniffer]: tool

[Spoofing]: Identify all the techniques focused on impersonation

[Hijacking]: Data hijacking encompasses a set of techniques in which the alteration of data, sessions, communications, or behavior is the fundamental element.


[Link to short lab]:  


————————> [ARP attack] <—————————————

Flooding Unknown Unicast and Broadcast Frames:
When there is no matching entry in the table, switches forward the frame out to all interfaces (except the incoming interface) using a process called flooding. 


■ Know Unicast
■ Unknown Unicast

Useful command on switches: 
# show mac address-table [complements]
# clear mac address-table [complements]
 By VLAN: clear mac address-table dynamic vlan vlan-number 
By Interface: clear mac address-table dynamic interface interface-id 
By MAC address: clear mac address-table dynamic address mac-address. Securing the Switch CLI  By default, a Cisco Catalyst switch allows anyone to connect to the console port, access user mode, and then move on to enable and configuration modes without any kind of security. That default makes sense, given that if you can get to the console port of the switch, you already have control over the switch physically. However, everyone needs to operate switches remotely, and the first step in that process is to secure the switch so that only the appropriate users can access the switch command-line interface (CLI). 

From enable mode, an attacker could reload the switch or change the configuration. 
From user mode is also important, because attackers can see the status of the switch, learn about the network, and find new ways to attack the network. 

Login security topics:
■ Securing user mode and privileged mode with simple passwords
■ Securing user mode access with local usernames
■ Securing user mode access with external authentication servers
■ Securing remote access with Secure Shell (SSH)

By default, Cisco Catalyst switches allow full access from the console but no access via Telnet or SSH. Using default settings, a console user can move into user mode and then privileged mode with no passwords required; however, default settings prevent remote users from accessing even user mode.  
You should not open the switch for just anyone to log in and change the configuration, so some type of secure login should be used.  
Most people use a simple shared password for access to lab gear. This method uses a password only—with no username—with one password for console users and a different password for Telnet users. 

Console users must supply the [console password], as configured in console line configuration mode. 
Telnet users must supply the Telnet password, also called the [vty password], so called because the configuration sits in vty line configuration mode. 

——————> [Hijacking Telnet] <————————


——————> [Hijacking Telnet] <————————

 
[Shared passwords]: Users share these passwords in so all users must know and use the same password. In other words, each user does not have a unique [username/password] to use, but rather, all the appropriate staff know and use the same password.
—> This is considered a bad practice and has a direct impact on non-repudiation

Login process from the perspective of the network engineer:
1. Connecting to the CLI of the switch, once in user mode
2. The user types the enable EXEC command. This command prompts the user for the enable password; if the user types the correct password, IOS moves the user to enable mode. 

Example: 
(User now presses enter to start the process. This line of text does not appear.) 
User Access Verification 

Password: ccnapass 
Switch> enable 
Password: test 
Switch# 

**In reality, the switch hides the passwords when typed, to prevent someone from reading over your shoulder to see the passwords. 

■ console mode for the console (line con 0) 
# line console 0
# password [password-value]
# login

■ vty line configuration mode for the Telnet password (line vty 0 15). 
# line vey 0 15
# password [password-value]
# login

password password-value: Defines the actual password used on the console or vty 
login: Tells IOS to enable the use of a simple shared password (with no username) on this line (console or vty), so that the switch asks the user for a password 


Console
 User mode.           enable secret test     Enable Mode
(Switch>)—————————————> (Switch#)

Telnet
(vty)

The configured enable password, shown on the right side of the figure, applies to all users, no matter whether they connect to user mode via the console, Telnet, or otherwise. 
■ enable password global configuration 
# enable secret [password-value]

 Step 1. Configure the enable password with the enable secret password-value command. 

Step 2. Configure the console password: 
* Use the line con 0 command to enter console configuration mode. 
* Use the password password-value subcommand to set the value of the console password. 
* Use the login subcommand to enable console password security using a simple password.  
Step 3. Configure the Telnet (vty) password: 
* Use the line vty 0 15 command to enter vty configuration mode for all 16 vty lines (numbered 0 through 15). 
* Use the password password-value subcommand to set the value of the console password. 
* Use the login subcommand to enable console password security using a simple password. 


Switch# configure terminal 
Switch(config)# enable secret test 

Switch#(config)# line console 0 Switch#(config-line)# password ccnapass Switch#(config-line)# login Switch#(config-line)# exit  Switch#(config)# line vty 0 15 Switch#(config-line)# password cisco Switch#(config-line)# login Switch#(config-line)# end Switch#  
Securing User Mode Access with Local Usernames and Passwords 

Cisco switches support two other login security methods that both use per-user username/ password pairs instead of a shared password with no username. 

One method, referred to as [local usernames and passwords], configures the username/password pairs locally—that is, in the switch’s configuration. 
- Switches support this local username/password option for the console, for Telnet, and even for SSH, but do not replace the enable password used to reach enable mode. 



Step 1. Use the username name secret password global configuration command to add one or more username/password pairs on the local switch. 

Step 2. Configure the console to use locally configured username/password pairs: 
* Use the line con 0 command to enter console configuration mode. 
* Use the login local subcommand to enable the console to prompt for both username and password, checked against the list of local usernames/passwords. 
* (Optional) Use the no password subcommand to remove any existing simple shared passwords, just for good housekeeping of the configuration file. 

Step 3. Configure Telnet (vty) to use locally configured username/password pairs. 
* Use the line vty 0 15 command to enter vty configuration mode for all 16 vty lines (numbered 0 through 15)
* Use the login local subcommand to enable the switch to prompt for both username and password for all inbound Telnet users, checked against the list of local usernames/passwords. 
* (Optional)Use the [no password] subcommand to remove any existing simple shared passwords, just for good housekeeping of the configuration file.  
Log in local line. Basically, this command means “use the local list of usernames for login.” You can also use the no password command (without even typing in the password) to clean up any remaining password subcommands from console or vty mode because these commands are not needed when using local usernames and passwords. 


Switch# configure terminal 
Switch(config)# enable secret test 

Switch#(config)# line console 0 Switch#(config-line)# login local Switch#(config-line)# no password Switch#(config-line)# exit  Switch#(config)# line vty 0 15 Switch#(config-line)# login local Switch#(config-line)# no password Switch#(config-line)# exit 
Switch(config)# username [user] secret [secretpass] 


Securing User Mode Access with External Authentication Servers 

A better option would be to use tools like those used for many other IT login functions. Those tools allow for a central place to securely store all username/password pairs, with tools to make users change their passwords regularly, tools to revoke users when they leave their current jobs, and so on. 

Cisco switches allow exactly that option using an external server called an authentication, authorization, and accounting (AAA) server. 
- Many production networks use AAA servers for their switches and routers today. 

[RADIUS or TACACS+] Protocols, both of which encrypt the passwords as they traverse the network 
 




LAYER 2 

Layer 2 is widely used on any kind of connection, even if LAN or WAN, both are fundamental for communications.

- MAC address (BIA) — 24bits (OUI) / 24bits(vendor assigned) —> burned into the ROM chip on the NIC
    - The manufacturer has a universally unique 3-byte code, called the organizationally unique identifier (OUI) 
    - The manufacturer also assigns a unique value for the last 3 bytes, a number that the manufacturer has never used with that OUI 

- Unicast (refers to a unique device, a one-to-one communication)
- Multicast (a group of devices on the LAN)
- Broadcast (all the devices on the LAN)

MAC-48
EUI-48
EUI-64 (not only 48 bits, instead 64 bits longer), same concept, 24 first bits for the vendor and then the rest to identify the device 


Data-link Protocols (Leased lines): PPP, HDLC, Ethernet(802.3), EoMPLS








08 September 2025
[J x 2] 

 
---

[← Volver al inicio]({{ "/" | relative_url }})
