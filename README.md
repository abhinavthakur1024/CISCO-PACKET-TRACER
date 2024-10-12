# CISCO-PACKET-TRACER
company network system 

base network = 192.168.1.0
no of subnets = 3

formula of subnets = 2^n 
2^n=3== n=2 (2 bits borrowed)

class C = 255.255.255.0 -> 11111111.11111111.11111111.00000000      (8 times)   total 1 is 26 this will represent slash notation ie /26

after borrowing 2 bits 

new binary form = 11111111.11111111.11111111.11000000  this is network id representation 

converting this into decimal 

//  0 to 7 = 8 digit starting from last 2^0=0 upto 5 zero we have all term is zero at position 6 we have one so 2^6=64 and again one 2^7=128 now adding 0+0+0+0+0+64+128=192
 
new subnetmass = 255.255.255.192  // check subnet mask block calculaltion image screenshot

192 represent block size of 64

1st subnet   
              network id:192.168.1.0
              broadcast id:192.168.1.63        less than 2nd subnet network id
              host range:192.168.1.1-192.168.1.62           between broad cast id and network id

2nd subnet 
              network id:192.168.1.64             0 +64
              broadcast id:192.168.1.127          less than 3rd subnet network id
              host range:192.168.1.65-192.168.1.126


3rd subnet 
             network id:192.168.1.128            64+64
             broadcast id:192.168.1.191          128+64=192 will be 4th subnet so 191 is broadcast id
             host range:192.168.1.129-192.168.1.190


in switch config 
type enter 
en  //(enable )
config t

int range fa0/2-4                          <--in 1st box
now we setup vlan 
switchport  access  vlan 10

int range fa0/8-10
switchport  access vlan 20             <--in 2nd box

int range fa0/5-7
switchport  access vlan 30             <--in 3rd box

now 
go to box one 
access point 
config
port1
Port status - Admin
WPA2-PSK
PSK PASS Phase --write any password

similarly do this with 2nd box access point
port status  - finance-WIFI

similarly do this with 3rd box access point
port status  - CS-WIFI   (costomer wifi)


do write 
exit
do show start
enter enter enter 



now we connect router so 

go to switch in cli
en
config t
interface fa0/1
switchport mode trunk
do write 


now in router
cli 


enter 
//router> 
enable or en
config t
interface gig0/0
no shutdown
do write
enter 
exit

int gig0/0.10
enter
encapsulation dot1Q 10
ip address 192.168.1.1 255.255.255.192  //(host range  + subnet mass address) of 1st subnet
exit


int gig0/0.20
enter
encapsulation dot1Q 20
ip address 192.168.1.65 255.255.255.192  //(host range  + subnet mass address) of 2nd subnet
exit


int gig0/0.30
enter
encapsulation dot1Q 30
ip address 192.168.1.129 255.255.255.192  //(host range  + subnet mass address) of 3rd subnet
do write

exit


do show start

//router
en
config t
service dhcp
ip dhcp pool Admin-Pool
network 192.168.1.0 255.255.255.192
default-router 192.168.1.1
dns-server 192.168.1.1
domain-name Admin.com



service dhcp
ip dhcp pool Finance-Pool
network 192.168.1.64 255.255.255.192
default-router 192.168.1.65
dns-server 192.168.1.65
domain-name Finance.com


service dhcp
ip dhcp pool CS-Pool
network 192.168.1.128 255.255.255.192
default-router 192.168.1.29
dns-server 192.168.1.29
domain-name CS.com

exit
do wr
do show start

go to pc 1
destop
ip configuration 
DHCP


all process is done 
now take 1 laptop and 1 smart Phone 
provide to every subnet 


to connect smart phone with admin-wifi

go to access point 
under config port 1 check ssid name and password
now go to smartphone 
config --> wireless0
ssid name 
WPA22-PSK enter password



in 2subnet 
To connect laptop
open laptop
zoom in 
turn on power
remove existing -->FASt 
to become port empty
now put WPC300N(2nd position)
check ssid and pass from access point
laptop --> destop--> PC wireless (tower)
connect
refress
