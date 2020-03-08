Do Not Stop
=====

## Category: Networking

> "I found some weird data while monitoring my network, but I didn't catch it all. See if you can make sense of it."

## Methodology
We are given a PCAP file, so naturally that is where we start. A lot of the traffic is a bit strange here but my midset is to always ignore the TLS encrypted traffic until I've made sure an easier avenue hasn't presented itself. I noticed some base64 enctrypted data inside of Ping reply packets, which is a little more than just odd. I decided to decode the first payload and it produced a lot of binary data, but a string fell out that said "flag.png". Thats interesting!

### False assumptions
At this point I'm thinking I'm recovering a png image from some packets. Too easy. I write a script that should extract all base64 encoded payloads from the ping reply packets, decode, and write the image. Little did I know that I had not fully read the description. There appears to be missing data from this payload. This is where I put on my forensics hat and went down the rabbit hole of trying to figure out PNG file structure, maybe patch the header and recover the image. No. Wrong move. I need to contact the server and pull the image down myself.

### Back to Scapy
So now, we need to write a python script that will 1. be an ICMP request, 2. have an ID of 0x1337 and 3. have increasing sequence numbers starting at 1 and ending at the last packet. Of course, when I write all this it doesn't work. The IP address of the machine I'm trying to reach is down. But why? At this point I'm feeling a little deja vu since I had just completed Do Not Stop a few hours before. I decided to scroll up the PCAP and look for DNS traffic, and wouldn't you know that there was a DNS resolution occuring for the machine I'm targetting? I notice that a DNS query happens for a pingable.tk, so I use nslookup to resolve the IP for me. I then use that IP address 

>from scapy.all import *
>
>import base64
>
>import re
>
>b64 = []
>
>for x in range(1, 17):
>	pkt = IP(dst="3.88.183.122", flags="DF", proto="icmp")/ICMP(type=8, code=0, id=0x1337, seq=x)/Raw(load="\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00")
>	ans = sr1(pkt)
>	b64.append(ans.load)
>pic = "".join(b64)
>newPic = re.sub(r"[\n\t\s]*", "", pic)
>print newPic
>
>picture = base64.b64decode(newPic)
>fd = open('flag.png', 'wb')
>fd.write(picture)
