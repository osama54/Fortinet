# FortiMail

### Mail Protocols: 

<img width="361" height="101" alt="1" src="https://github.com/user-attachments/assets/48ce311a-6067-46c2-959a-c88194056cf9" />

##### SMTP used to deliver emails between accounts in different domains. 
##### SMTP uses port 25 and 587, 25 tranisimsstion in plain test without authentication, while 587 uses encryption, authentication... 

### I have two types of Mail server, 
#### 1. Outgoing Mail Server 
##### * Outgoing Mail Server required DNS Resolution, the server uses DNS to determine the recipient mail server. 
##### * if the sender and receiver within same domain, the server will not do the DNS lookup

<img width="95" height="91" alt="2" src="https://github.com/user-attachments/assets/861999b8-a918-4223-9702-b22300150e71" />

#### 2. Relay Mail Server: 

<img width="84" height="102" alt="3" src="https://github.com/user-attachments/assets/311da7ab-d364-401e-8200-fd10d5636529" />


## POP/POP3
#### SMTP Deliver the email to the server, now the client use pop to retrive the email.
#### POP3 client dwoanlods an email from server to email user's computer.
#### POP3 usse port 110, it is the default and it is not encrypted
#### POP3 users port 995 for encrypted and work over TLS/SSL.
##### I can chagne the policy and make a copy in the server so i can retrive it if i lose it in my PC

<img width="276" height="83" alt="4" src="https://github.com/user-attachments/assets/eca03d1e-34cd-4319-9d59-54db503abba1" />

## IMAP
#### Another protocol the client use it to retrive the email from the mail server.
#### IMAP Clients donwload only the message header, they download the message body and attachement only when the email user selects to read the email.
##### When you read email, you aren't actually downloading or storing it on your computer, you are reading from the email server. 
#### the client not doesn't delete the emails from the servers. 
#### IMAP allows you to access your email from multiple devices. 
#### Uses two protocols, 143 for non-encryption and 993 works over TLS/SSL encryption 

### Which One is Better? 

<img width="264" height="132" alt="5" src="https://github.com/user-attachments/assets/391992c9-a2d4-45ed-9858-3918f74cc0d5" />

---
---
---
---
---

## Email Componenets and Roles: 

### Mail User Agent (MUA): Software application that allows users to send,receive, and read email messages. Interface between user and email system, interacting with Main Transfer Agents (MTA) and Mail Delivery Agents (MDA) to manage email communication. 
#### MUA typically use SMTP to send emails and IMAP or POP3 to retrieve the email from mail server. Examply: Outlook, Gmail... 

### Mail Transfer Agent (MTA): When email is sent, the MTA receives it from the sender email client or server, determines the best path to the recipient mail server, and then forwards or relays the message. 
#### Also known as Mail relay
#### Not all MTAs are full email servers, some MTA exist to relay email and do not host email user accounts. 
##### Common MTA: Postfix, Microsoft Exchange and FortiMail. 

### Mail Server: Host the users, sends, recieves, stores, and forwards the email over a network using standard protocols. 
#### Mail server might also support MTA and host user mailboxes.
#### Common Mail Server: Microsoft Exchange, FortiMail(Server Mode)

<img width="398" height="149" alt="6" src="https://github.com/user-attachments/assets/3990f70d-fe11-4c91-bcf5-4bb79cf0ee56" />

### FortiMail that opert in Gateway mode is an MTA
### FortiMail that operate in Server is both MTA and destination mail server. 
#### MTA implement a policy to check the authorization for the users 
#### MTA do a scan for the emails. 
#### If MTA don't implement this mechanism, this called open relays, open relays are widely exploited by spammers to send unsolicited spam. 

### FortiMail can work as MTA to scan the mails, and can work as open relay without scan to only forward the mails and also can work as a mail server with MTA (Server Mode). 

---
---
---
---
---



























































































