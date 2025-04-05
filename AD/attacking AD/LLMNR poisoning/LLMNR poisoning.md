<h3>LLMNR Poisoning</h3>

**LLMNR** - Link Local Multicast Name Resolution
Used to identify hosts when DNS fails to do

**key flaw** - respomses with username w/ password hash when we respond to it thru MITM

1. the user mistyped who to connect, the dns cannot repond because of mistype
2. the user broadcast who can make it connect to it.
3. the hacker reponds (MITM thru responder)
4. the user sends username and pword hash to the hacker

step 1: run responder
step 2: event occurs
step 3: responder responds broadcast and user will send username and passwd hash
step 4: crack the hash using hashcat

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)