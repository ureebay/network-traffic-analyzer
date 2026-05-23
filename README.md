# Network Traffic Analyzer

Python-based packet capture tool that monitors live network traffic in real time, identifies protocols, tracks bandwidth, and displays statistics. Deployed and run on Windows using Scapy, Rich, and Matplotlib.

## Environment
- Windows 11, Python 3.14.5
- Npcap driver for Windows packet capture
- Administrator privileges required for raw socket access

## My Findings

### Session 1: Multi-Protocol Capture (466 packets, 4.9 seconds)
![Capture Summary](screenshots/Capture-Summary.webp)

- Captured 5 protocols: UDP, TCP, DNS, HTTPS, ARP across 12 unique endpoints
- UDP accounted for 91.4% of traffic, consistent with real time streaming behavior
- HTTPS confirmed active encrypted web sessions
- DNS revealed constant background domain resolution activity
- Identified Cloudflare CDN servers as top external endpoints
- Results exported to JSON for offline analysis

### Session 2: Verbose Packet Flow (50 packets)
![Packet Flow](screenshots/packet-flow.webp)


- Captured individual packet level data showing bidirectional UDP traffic
- Source: 192.168.1.158 (local machine), Destination: Cloudflare servers
- Packet sizes ranged from 89 to 283 bytes

### Session 3: First Successful Capture (100 packets)
![First Capture](screenshots/first-capture.webp)

- Initial capture confirming tool worked on Windows with Npcap
- 3 unique endpoints, 21.8 KB captured in 0.8 seconds
- Established baseline for subsequent sessions

## What I Learned
- Packet capture requires Administrator privileges on Windows because it accesses raw sockets at the kernel level
- UDP dominates real time traffic because it sends without waiting for confirmation, making it faster than TCP
- DNS queries happen constantly in the background even when no browser is open
- ARP packets operate at Layer 2 and map IP addresses to MAC addresses on the local network
- BPF filters run inside the kernel and drop irrelevant packets before they reach the application
- Producer-consumer threading keeps capture running at wire speed by separating packet ingestion from processing into two threads connected by a bounded queue

## How to Run
Requires Windows with Npcap installed. Must run as Administrator.

git clone https://github.com/ureebay/network-traffic-analyzer
cd network-traffic-analyzer/python
pip install -e .
python -m netanal capture -i "YOUR_INTERFACE" --count 500 -o results.json

To find your interface:
python -c "from scapy.all import conf; print(conf.iface)"

## Next Extensions
- Bandwidth spike alerting
- TCP handshake tracking to detect incomplete connections
- Packet size distribution histogram
- DNS query correlation
