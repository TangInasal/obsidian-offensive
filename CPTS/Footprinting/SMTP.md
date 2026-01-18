By default, SMTP servers accept connection requests on port `25`. However, newer SMTP servers also use other ports such as TCP port `587`.

|Client (`MUA`)|`➞`|Submission Agent (`MSA`)|`➞`|Open Relay (`MTA`)|`➞`|Mail Delivery Agent (`MDA`)|`➞`|Mailbox (`POP3`/`IMAP`)|
|---|---|---|---|---|---|---|---|---|

But SMTP has two disadvantages inherent to the network protocol.

1. The first is that sending an email using SMTP does not return a usable delivery confirmation. Although the specifications of the protocol provide for this type of notification, its formatting is not specified by default, so that usually only an English-language error message, including the header of the undelivered message, is returned.
    
2. Users are not authenticated when a connection is established, and the sender of an email is therefore unreliable. As a result, open SMTP relays are often misused to send spam en masse. The originators use arbitrary fake sender addresses for this purpose to not be traced (mail spoofing). Today, many different security techniques are used to prevent the misuse of SMTP servers. For example, suspicious emails are rejected or moved to quarantine (spam folder). For example, responsible for this are the identification protocol [DomainKeys](http://dkim.org/) (`DKIM`), the [Sender Policy Framework](https://dmarcian.com/what-is-spf/) (`SPF`).
---
## Default Configuration

| **Command**  | **Description**                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------ |
| `AUTH PLAIN` | AUTH is a service extension used to authenticate the client.                                     |
| `HELO`       | The client logs in with its computer name and thus starts the session.                           |
| `MAIL FROM`  | The client names the email sender.                                                               |
| `RCPT TO`    | The client names the email recipient.                                                            |
| `DATA`       | The client initiates the transmission of the email.                                              |
| `RSET`       | The client aborts the initiated transmission but keeps the connection between client and server. |
| `VRFY`       | The client checks if a mailbox is available for message transfer.                                |
| `EXPN`       | The client also checks if a mailbox is available for messaging with this command.                |
| `NOOP`       | The client requests a response from the server to prevent disconnection due to time-out.         |
| `QUIT`       | The client terminates the session.                                                               |

#### Telnet - HELO/EHLO
To interact with the SMTP server, we can use the `telnet` tool to initialize a TCP connection with the SMTP server. The actual initialization of the session is done with the command mentioned above, `HELO` or `EHLO`.
```shell-session
telnet 10.129.14.128 25
```
```output
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 
```

```shell-session
HELO mail1.inlanefreight.htb
```
```output
250 mail1.inlanefreight.htb
```

```shell-session
EHLO mail1
```
```output
250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```

The command `VRFY` can be used to enumerate existing users on the system. 
However, this does not always work. Depending on how the SMTP server is configured.
The SMTP server may issue `code 252` and confirm the existence of a user that does not exist on the system. A list of all SMTP response codes can be found [here](https://serversmtp.com/smtp-error/).

#### Telnet - VRFY
```shell-session
telnet 10.129.14.128 25
```
```output
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 
```

```shell-session
VRFY root
```
```output
252 2.0.0 root
```

```shell-session
VRFY cry0l1t3
```
```output
252 2.0.0 cry0l1t3
```

```shell-session
VRFY testuser
```
```output
252 2.0.0 testuser
```

```shell-session
VRFY aaaaaaaaaaaaaaaaaaaaaaaaaaaa
```
```output
252 2.0.0 aaaaaaaaaaaaaaaaaaaaaaaaaaaa
```

Sometimes we may have to work through a web proxy. 
We can also make this web proxy connect to the SMTP server. The command that we would send would then look something like this: `CONNECT 10.129.14.128:25 HTTP/1.0`

#### Send an Email
```shell-session
telnet 10.129.14.128 25
```
```output
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server
```

```shell-session
EHLO inlanefreight.htb
```
```output
250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```

```shell-session
MAIL FROM: <cry0l1t3@inlanefreight.htb>
RCPT TO: <mrb3n@inlanefreight.htb> NOTIFY=success,failure
DATA

354 End data with <CR><LF>.<CR><LF>

From: <cry0l1t3@inlanefreight.htb>
To: <mrb3n@inlanefreight.htb>
Subject: DB
Date: Tue, 28 Sept 2021 16:32:51 +0200
Hey man, I am trying to access our XY-DB but the creds don't work. 
Did you make any changes there?
.
```
```output
250 2.0.0 Ok: queued as 6E1CF1681AB
```

```shell-session
QUIT
```
---
## Dangerous Settings
Often, administrators have no overview of which IP ranges they have to allow. This results in a misconfiguration of the SMTP server that we will still often find in external and internal penetration tests. Therefore, they allow all IP addresses not to cause errors in the email traffic and thus not to disturb or unintentionally interrupt the communication with potential and current customers.
#### Open Relay Configuration


