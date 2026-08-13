# Networking-Final-Project
A Step by step process on how I did my final project as a network specialist, I made it very simple to Understand so even someone who is not grounded in networking can understand it
# Network Topology

This is a logical diagram consisting of the network connectivity, 4 switches, 2 routers, 2 Alternative systems, and 6 PCs.
<img width="975" height="457" alt="image" src="https://github.com/user-attachments/assets/c11cf742-9b64-46c7-8290-056ef12e5d1e" />

## Procedures

1. I brought out the devices used for the project, which consist of **4 switches**, **2 routers**, and **6 PCs**.
2. The first 2 switches, 1 router, and 3 PCs are connected together in one network — the **Headquarters**.
3. The first top-left PC is for the **Admin**, while the remaining 2 are for the **Employees**.
4. The second 2 switches, 1 router, and 3 PCs connected together form the **Branch Network**.
5. The top-right PC is for the **Branch Admin**, while the remaining 2 are for the **Employees**.

   ## Connections for the HQ Switch Network
   <img width="975" height="653" alt="image" src="https://github.com/user-attachments/assets/889bd217-013b-4d50-b7ec-5b6300b1d162" />

1. I created 3 VLANs — the Admin is in a separate VLAN from the Employees.
2. VLAN 100 is for the Admin, while VLAN 2 and VLAN 3 are for the Employees.
3. VLAN 100 is known as **MGMT**, VLAN 2 is the **Sales** VLAN, and VLAN 3 is the **Marketing** VLAN.
4. I also allocated:
   - **Fa0/3 – Fa0/4** → VLAN 100
   - **Fa0/5 – Fa0/11** → VLAN 2
   - **Fa0/12 – Fa0/24** → VLAN 3
5. I also created a hostname for the switch, passwords, a banner message, and Telnet connection.
   1. I also created the same VLANs in Switch 2 to enable communication and also assigned ports accordingly.
      <img width="865" height="600" alt="image" src="https://github.com/user-attachments/assets/655e773a-762e-4bab-bef0-bebb3d631b43" />
2. Gave VLAN 100 an IP address (**192.168.1.2**) with a subnet mask of **255.255.255.244**, all done inside the switch.
   ## Router
1. Created sub-interfaces on the router for the 3 VLANs and gave each an IP address, which will later be used as the default gateway for the PCs in this network to enable communication.
   <img width="746" height="633" alt="image" src="https://github.com/user-attachments/assets/f2ddcd6b-9437-47c6-bd2a-4813b8799a1c" />
3. To enable the router to communicate via serial interface, I gave **Serial 1/2/0** an IP address of **192.168.1.193** and turned up (activated) the interface.

## The PCs

1. I gave **PC1**, the Admin PC, an IP address of **192.168.1.6** with a subnet mask of **255.255.255.224**.
2. I gave **PC2**, for Employees (Sales dept), an IP address of **192.168.1.34** with the same subnet mask.
3. I gave **PC3**, for Employees (Marketing dept), an IP address of **192.168.1.68** with the same subnet mask.
4. I also set the default gateway on the PCs to the IP of the router; this enables the PCs to ping and communicate.
5. Just like this.
   <img width="975" height="513" alt="image" src="https://github.com/user-attachments/assets/9f72b060-a9df-4364-94ab-2d00fef4bda5" />
Admin Pc |Ip address & default gateway.
## Pinging the Departments in the HQ Network
<img width="975" height="485" alt="image" src="https://github.com/user-attachments/assets/08d5bc87-c938-4cff-914e-b19fade2f382" />

1.  I pinged from PC1 (Admin) to PC2 (Sales) and PC3 (Marketing) to confirm inter-VLAN communication was successful.
2.  I also pinged from PC2 to PC3 to confirm that the Sales and Marketing departments could communicate with each other.
3.  All pings were successful, confirming that the router's sub-interfaces (Router-on-a-Stick configuration) correctly routed traffic between VLAN 100, VLAN 2, and VLAN 3.
   ### N/B

Before this was possible, I created VLANs in both switches and made **3 trunk links** to carry multiple VLAN traffic — at the interface leading from Switch 1 to Switch 2, and from Switch 1 to the Router. The sole purpose of this was also to enable the HQ and Branch networks to communicate successfully.

# Submission B

## Switch Configuration for Branch Network
<img width="870" height="701" alt="image" src="https://github.com/user-attachments/assets/b8aa852b-fcfc-4402-a269-cfa0ee41b35c" />

1. I created 3 VLANs — the Admin is in a separate VLAN from the Employees.
2. VLAN 100 is for the Admin, while VLAN 5 and VLAN 6 are for the Employees.
3. VLAN 100 is known as **MGMT**, VLAN 2 is for **Dept1**, and VLAN 3 is for **Dept2**.
<img width="886" height="751" alt="image" src="https://github.com/user-attachments/assets/81631081-9496-47cd-911f-f955df8a537b" />

1. I also allocated:
   - **Fa0/3 – Fa0/4** → VLAN 100
   - **Fa0/5 – Fa0/11** → VLAN 5
   - **Fa0/12 – Fa0/24** → VLAN 6
2. I also created a hostname for the switch, passwords, a banner message, and Telnet connection.
3. Gave VLAN 100 an IP address (**192.168.1.97**) with a subnet mask of **255.255.255.224**.

   ## SSH Configuration
<img width="898" height="860" alt="image" src="https://github.com/user-attachments/assets/6fec3966-42af-4e64-a66e-eb58d0bf7107" />

I did the SSH configuration for the switches by carrying out the following steps:

1. Configured a hostname on the switch, since SSH requires a unique hostname (not the default).
2. Configured a domain name using the `ip domain-name` command, which is required to generate RSA keys.
3. Generated RSA encryption keys using the `crypto key generate rsa` command to enable secure communication.
4. Created a local username and password using the `username` command, to authenticate SSH users.
5. Enabled SSH version 2 for stronger security using the `ip ssh version 2` command.
6. Accessed the VTY lines (`line vty 0 15`) and set the login method to use the local username/password database (`login local`).
7. Restricted remote access to SSH only (disabling Telnet) using the `transport input ssh` command on the VTY lines.
8. Tested the configuration by SSH-ing into the switch from a PC to confirm successful connectivity.
