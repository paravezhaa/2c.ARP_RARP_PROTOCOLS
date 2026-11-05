# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
#### Developed by: PARAVEZHAA M
#### Register number: 212225220070
### SERVER:
```import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("ARP Server is waiting...")
c, addr = s.accept()
print("Connected to client:", addr)

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

ip = c.recv(1024).decode()
print("Received IP Address:", ip)

mac = arp_table.get(ip, "MAC Address not found")

c.send(mac.encode())

c.close()
s.close()
```
### CLIENT:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

ip = input("Enter IP Address: ")

s.send(ip.encode())

mac = s.recv(1024).decode()

print("MAC Address:", mac)

s.close()
```

## OUPUT - ARP
### server:
<img width="1462" height="365" alt="Screenshot 2026-11-04 105505" src="https://github.com/user-attachments/assets/0142afd1-950b-4ebb-8715-ba8852d04071" />

### client:
<img width="1446" height="193" alt="image" src="https://github.com/user-attachments/assets/d629e46f-d00f-464b-a3ce-fd7829bb6c8e" />

## PROGRAM - RARP
### SERVER:
```
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(1)

print("RARP Server is waiting...")
c, addr = s.accept()
print("Connected to client:", addr)

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

mac = c.recv(1024).decode()
print("Received MAC Address:", mac)

ip = rarp_table.get(mac, "IP Address not found")

c.send(ip.encode())

c.close()
s.close()
```
### CLIENT:
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

mac = input("Enter MAC Address: ")

s.send(mac.encode())

ip = s.recv(1024).decode()

print("IP Address:", ip)

s.close()
```

## OUPUT -RARP
### server:
<img width="1437" height="236" alt="image" src="https://github.com/user-attachments/assets/ccde357d-2a65-4619-8511-e203cb3b7bf1" />

### client:
<img width="1432" height="277" alt="image" src="https://github.com/user-attachments/assets/fcdf284b-29e6-4774-9256-dcc25666cbe0" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
