# multiswitch

Multi-Layer Switching Lab

In this lab I’m going to configure my switches and configure vlans. Vlans are logical segmentation of a physical network that groups devices together even though they are all connected to the different physical switches. This segmentation helps with optimizing network performance and efficient resource allocation.

<img width="757" height="378" alt="image" src="https://github.com/user-attachments/assets/1682be11-9d99-49cb-86d9-6a1c8c7594cd" />
 
Multilayer Switch configurations.
Switch>en
Switch#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname MultilayerSwitchA
MultilayerSwitchA#config
Configuring from terminal, memory, or network [terminal]? 
Enter configuration commands, one per line.  End with CNTL/Z.
MultilayerSwitchA(config)#vlan 10
MultilayerSwitchA(config-vlan)#name HR
MultilayerSwitchA(config-vlan)#vlan 20
MultilayerSwitchA(config-vlan)#name sales
MultilayerSwitchA(config-vlan)#vlan 30
MultilayerSwitchA(config-vlan)#name public
MultilayerSwitchA(config)#int vlan 1
MultilayerSwitchA(config-if)#ip address 192.168.1.100 255.255.255.0
MultilayerSwitchA(config-if)#no shut
MultilayerSwitchA(config-if)#int vlan 10
MultilayerSwitchA(config-if)#ip address 192.168.10.100 255.255.255.0
MultilayerSwitchA(config)#int vlan 20
MultilayerSwitchA(config-if)#ip address 192.168.20.100 255.255.255.0
MultilayerSwitchA(config)#int vlan 30
MultilayerSwitchA(config-if)#ip address 192.168.30.100 255.255.255.0
Then configuring the Trunk Port 
MultilayerSwitchA(config)#ip routing
MultilayerSwitchA(config)#int f0/23
MultilayerSwitchA(config-if)#switchport trunk encap dot1q
MultilayerSwitchA(config-if)#switchport mode trunk
MultilayerSwitchA(config-if)#duplex full
Viewed my configurations of the vlan with sh vlan brief

 <img width="632" height="541" alt="image" src="https://github.com/user-attachments/assets/1ac2a437-6688-4089-b327-22fdae97e2a5" />
 
SwitchA configurations.
Switch>
Switch>en
Switch#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SwitchA
Here I am now creating the vlans 
SwitchA(config)#vlan 10
SwitchA(config-vlan)#name HR
SwitchA(config-vlan)#vlan 20
SwitchA(config-vlan)#name Sales
SwitchA(config-vlan)#vlan 30 
SwitchA(config-vlan)#name Public
SwitchA(config)#int vlan 10
Assigning port to the vlans
SwitchA(config-if)#int range f0/7 - 9
SwitchA(config-if-range)#switchport mode access
SwitchA(config-if-range)#switchport access vlan 10
SwitchA(config-if-range)#int vlan 20
SwitchA(config-if)#int range f0/10 - 13
SwitchA(config-if-range)#switchport mode access
SwitchA(config-if-range)#switchport access vlan 20
SwitchA(config-if-range)#int vlan 30
SwitchA(config-if)#
SwitchA(config-if)#int range f0/14 - 17
SwitchA(config-if-range)#switchport mode access
SwitchA(config-if-range)#switchport access vlan 30
Assigning IP Address and default gateway to the Switch
SwitchA(config)#int vlan 1
SwitchA(config-if)#ip address 192.168.1.50 255.255.255.0
SwitchA(config-if)#no shut
SwitchA(config-if)#exit
SwitchA(config)#ip default-gateway 192.168.1.100
Configure Trunk Port on the Switch: Some switches duplex must be set to full (duplex full)
SwitchA(config)#int f0/23
SwitchA(config-if)#duplex auto
SwitchA(config-if)#switchport mode trunk
SwitchA(config-if)#int f0/24
SwitchA(config-if)#switchport mode trunk
View my changes

 <img width="687" height="569" alt="image" src="https://github.com/user-attachments/assets/19c04ea7-6055-455a-a339-00b8572e2d6b" />

SwitchB configurations.
Switch>
Switch>en
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SwitchB
Creating the VLans
SwitchB(config)#vlan 10
SwitchB(config-vlan)#name HR
SwitchB(config-vlan)#vlan 20
SwitchB(config-vlan)#name Sales
SwitchB(config-vlan)#vlan 30 
SwitchB(config-vlan)#name Public
SwitchB(config)#int vlan 10
Assigning Port to the Vlans
SwitchB(config-if)#int range f0/7 - 9
SwitchB(config-if-range)#switchport mode access
SwitchB(config-if-range)#switchport access vlan 10
SwitchB(config-if-range)#int vlan 20
SwitchB(config-if)#int range f0/10 - 13
SwitchB(config-if-range)#switchport mode access
SwitchB(config-if-range)#switchport access vlan 20
SwitchB(config-if-range)#int vlan 30
SwitchB(config-if)#
SwitchB(config-if)#int range f0/14 - 17
SwitchB(config-if-range)#switchport mode access
SwitchB(config-if-range)#switchport access vlan 30
Assigning IP Address and default gateway to the Switch
SwitchB(config)#int vlan 1
SwitchB(config-if)#ip address 192.168.1.150 255.255.255.0
SwitchB(config-if)#no shut
SwitchB(config-if)#exit
SwitchB(config)#ip default-gateway 192.168.1.100

Configure Trunk Port on the Switch: Some switches are going to be set to full (duplex full)
SwitchB(config-if)#int f0/24
SwitchB(config-if)#switchport mode trunk

 <img width="457" height="376" alt="image" src="https://github.com/user-attachments/assets/b3397508-3ac6-4938-be9b-9a91a9c78307" />

Pinging nodes for communication
PC0 – PC1

 <img width="534" height="252" alt="image" src="https://github.com/user-attachments/assets/a8a9637e-3c0a-4a75-afe7-3ec2e5e5e95a" />

PC0 – PC2
 
 <img width="532" height="265" alt="image" src="https://github.com/user-attachments/assets/e4e7aef3-9b76-4260-9be4-2f5879aca37b" />

PC0 – PC3

 <img width="742" height="354" alt="image" src="https://github.com/user-attachments/assets/2111956a-240c-4f75-94d9-92e588652295" />

PC0 – PC4

 <img width="696" height="332" alt="image" src="https://github.com/user-attachments/assets/39ffc14b-4615-48d6-876d-4aa91759723f" />

PC0 – PC5

 <img width="731" height="348" alt="image" src="https://github.com/user-attachments/assets/44fab19e-a177-4903-aad9-aa41845213a5" />

PC0 – PC6

 <img width="627" height="339" alt="image" src="https://github.com/user-attachments/assets/4064780f-4565-4232-92b4-5d0f8c994118" />

PC0 – PC7

 <img width="641" height="318" alt="image" src="https://github.com/user-attachments/assets/fd1c6902-7152-4173-bd54-bc4970f5fc2b" />
