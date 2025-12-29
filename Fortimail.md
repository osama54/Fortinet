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






























































































