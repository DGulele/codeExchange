# codeExchange
A change to win a cisco t-shirt

This short script helps network engineers automate basic swicth configuration,
specifically for this code create vlans.


import getpass
import telnetlib

HOST = "192.168.122.10"
user = input("Enter your username: ")
password = getpass.getpass()

tn = telnetlib.Telnet(HOST)

tn.read_until(b"Username: ")
tn.write(user.encode('ascii') + b"\n")
if password:
    tn.read_until(b"Password: ")
    tn.write(password.encode('ascii') + b"\n")

tn.write(b"enable\n")
tn.write(b"cisco\n")
tn.write(b"conf t\n")

for n in range (2,6):
    tn.write(b"vlan " + str(n).encode('ascii') + b"\n")
    tn.write(b"name VLAN_" + str(n).encode('ascii') + b"\n")

tn.write(b"end\n")
tn.write(b"wr\n")
tn.write(b"exit\n")

print(tn.read_all().decode('ascii'))
