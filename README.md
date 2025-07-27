# KCEVE 10 Port KVM Control with NanoKVM

- I picked up this 10 port KVM Switch from Amazon: https://amzn.to/3H4COiA Its from a Chinese Brand called KCEVE, and the documentation from them is kind of Sh*t, so I made this repo.
- The KVM Switch is going to a NanoKVM and a MOXA RS232-Ethernet controller.

## Serial Settings

The KVM switch communicates with the following configuration:
- **Baud rate:** 115200
- **Data bits:** 8
- **Stop bits:** 1
- **Parity:** None
- **FIFO:** Disabled
- **Flow control:** None

## Notes about the RS232 Hookup

- The RS232 Port on the KVM switch is labeled backwards, so TX is RX and RX is TX. Not a big deal, but annoying. 
- I had some issues with the Moxa not dropping the connection, easy fix was to set the inactive timeout on the Moxa to 30000Ms(30Sec)

## Usage

Upload these scripts to your NanoKVM device to select inputs on the KVM switch. Each script sends the appropriate select command using `netcat` (nc) over TCP.

### Example Script

```sh
#!/bin/sh
# Switch to input 4 on the KVM
printf "X4,1$" | nc 1.2.3.4 8000
```

- Replace `X4,1$` with the desired port selection:
  - `X1,1$` For Port 1
  - `X2,1$` For Port 2
  - `X3,1$` For Port 3
  - `X4,1$` For Port 4
  - `X5,1$` For Port 5
  - `X6,1$` For Port 6
  - `X7,1$` For Port 7
  - `X8,1$` For Port 8
  - `X9,1$` For Port 9
  - `XA,1$` for port 10  
- Adjust the IP address (`1.2.3.4`) and TCP port (`8000`) to match your RS232 endpoint.

## Script List

Create individual scripts for each port (e.g., `select1.sh`, `select2.sh`, …, `select10.sh`) with the above format, updating the `X#` command and file name accordingly.
Upload the scripts to NanoKVM
