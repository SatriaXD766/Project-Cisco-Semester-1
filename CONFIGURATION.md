# 🛜 Cisco Portfolio - Semester 1 
Dokumentasi lengkap 2 Project

PROJECT 1: Topologi Jaringan Hybrid 3 Segmen
File: Topologi_Jaringan_Hybrid_3_Segmen.pkt

# Topologi:
Internet -> Router0 -> 3 Switch -> 9 PC

# IP TABLE
Segmen 1 (VLAN Kantor 1):
`Network: 192.168.1.0/24
Gateway: 192.168.1.1
PC1: 192.168.1.10
PC2: 192.168.1.11
PC3: 192.168.1.12`

Segmen 2 (VLAN Kantor 2):
`Network: 192.168.2.0/24
Gateway: 192.168.2.1
PC4: 192.168.2.10
PC5: 192.168.2.11
PC6: 192.168.2.12`

Segmen 3 (VLAN Kantor 3):
`Network: 192.168.3.0/24
Gateway: 192.168.3.1
PC7: 192.168.3.10
PC8: 192.168.3.11
PC9: 192.168.3.12 `

# KONFIGURASI ROUTER
enable
configure terminal
hostname Router-Hybrid
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface GigabitEthernet0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
interface GigabitEthernet0/2
 ip address 192.168.3.1 255.255.255.0
 no shutdown
end
write memory

PROJECT 2: Enterprise Office Network Infrastructure
File: enterprise-office-network-infrastructure.pkt
Skenario: PT. Satria TBK

# Topologi
ISP (Cloud) -> R1-Core Router (2911) -> Switch Utama (2960-24TT) -> 
-> Switch-Access-Finance
-> Switch-Access-HRD
-> Switch-Access-IT
+ Server-PT (Server 1)
+ AccessPoint Kantor PT. Satria TBK

# 1. R1-Core Router (2911)
enable
configure terminal
hostname R1-Core-Router

interface GigabitEthernet0/0
 description Link to ISP
 ip address 10.10.10.2 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 description Link to Switch Utama
 ip address 192.168.10.1 255.255.255.0
 no shutdown

ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp excluded-address 192.168.10.100

ip dhcp pool OFFICE-POOL
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.10.100
 domain-name ptsatria.co.id
 lease 7

end
write memory

# 2. Switch Utama (2960-24TT)
enable
configure terminal
hostname Switch-Utama
vlan 10
 name FINANCE
vlan 20
 name HRD
vlan 30
 name IT
exit
interface range FastEthernet0/1-24
 switchport mode access
end
write memory

# 3. Switch Access (Ulangi untuk Finance, HRD, IT)
enable
conf t
hostname Switch-Access-Finance
interface range Fa0/1-10
 switchport mode access
end

# 4. Server-PT - Server 1
IP Configuration:
IP Address: 192.168.10.100
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
DNS Server: 192.168.10.100

Services:
- HTTP: ON
- DNS: ON (A Record ptsatria.co.id -> 192.168.10.100)
- DHCP: OFF

# 5. Access Point
SSID: KANTOR-SATRIA
Authentication: WPA2-PSK
Password: satria123
Channel: 6

# 6. End Devices (12 Laptop + 9 PC + Smartphone)
IP Configuration: DHCP (Automatic)
Laptop Kantor 1-6: 192.168.10.11 - 192.168.10.16
Laptop Pribadi 1-6: 192.168.10.17 - 192.168.10.22
PC Finance/HRD/IT: 192.168.10.23 - dst

# VERIFIKASI (PING)
Dari Laptop Kantor 1:
ping 192.168.10.100 (ke Server) -> Success
ping 192.168.10.17 (ke Laptop Pribadi) -> Success
ping ptsatria.co.id -> Success

Status Akhir: All Green / Reply Success ✅

Dibuat oleh Satria - Semester 1
Tujuan: Membangun Portfolio Mandiri & Mengulik Dunia Networking dengan Cisco Packet Tracert
