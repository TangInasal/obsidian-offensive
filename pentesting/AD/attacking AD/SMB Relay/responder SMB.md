**responder**
NOTE: edit responder.conf before running
configure ntlmrelayx after configuring

we are going to use responder to listen but we will not respond

edit responder.conf
SMB - off
HTTP - off
run responder

responder -I eth0 -rdw

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)

![file:///tmp/.HZGD42/2.png](file:///tmp/.HZGD42/2.png)