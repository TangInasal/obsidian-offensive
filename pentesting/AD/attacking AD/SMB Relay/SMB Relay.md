instead of cracking hashes captured by responder
we would relay these hashes to other machines

requirements:
1. SMB Signing - disabled
2. relayed user credentials must be admin on machine

step 1: identify SMB Signing (on/off)
step 2: save hosts with disabled smb sigining on different text files
step 3: edit responder.conf
step 4: run responder