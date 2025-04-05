   

# decoys

  

**scan network with decoys**

it scans network together with random or specified ip addresses

it would be difficult to sift the ip addresses

limit: 300

dont use a lot since it would be detected by IDS and/or firewalls

nmap -D RND:15 132.168.X.X

(uses 15 random decoys )

nmap -D RND:15 ip address1, ip address2, ...ip address15 192.168.x.x

(uses specified ip addresses as decoys)