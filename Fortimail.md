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

## DNS 

<img width="233" height="93" alt="7" src="https://github.com/user-attachments/assets/73ba1f21-5efe-4598-836a-a6aef5d6bf37" />

### Important DNS Record: 
#### MX : Mail Exchange: Specifies mail server for a domain (used in domain routing) 

### DNS Role in Email Delivery: 
####  When MTA need to verify where to send an email, it performs a lookup for a specific type of DNS record on the domain portion of the recipient email address, this DNS record is MX record. 
##### The MX record are configured on DNS server. 
##### I may have many MX record, the lowest preferense is better, if the priority same we may use load balancing. 

### Only Microsoft Outlook and Microsoft Exchange servers use protocol called Messaging Application Programming Interface (MAPI). MAPI is used for both email transmission and retrieval between Outlook and Microsoft Exchange. 

---
---

### Message Header contain a lot of useful informaition, and often used to gather information or troubleshoot email issues, it contains: 
##### All hops that the email transfer through 
#### When i do forward for the email that i received to another email, there two types of forwarding 
##### Type1: Normal Forwarding, will remove all the old email hops that pass through before i received the email (Destroy the old email header) becuase the MUA  created new headers from the new point of origin.
##### Type2: Forwarding as an Attachment, the content of message header will remains 

---
---

## SMTP Authentication: 
### SMTP did not include any requirements for security mechanisms. Email was transmitted in plaintext by unauthenticated users. 
#### the AUTH extension was added later to verify sender identity. MTA that support ESMTP can enforce authentication to ensure that only authorized users are allowed to send email. 
##### This Verifies only the send identity for outbound emails from a protected domain, but it does not prevent spoofing of inbound emails comming from external mail servers. 

###### 1. SMTP: Send message with Cleartext
###### 2. STARTTLS: SMTP over TLS, doesn't encrypt all the message, start the encryption after the handshake messages, encrypt the sensitive data only. 
###### 3. SMTPS: Encrypt the entire session, including banner, Helo messages, and server extensions. 

<img width="233" height="113" alt="00" src="https://github.com/user-attachments/assets/66f25d67-97f6-4057-badc-2ad429d126a3" />

---
---
---
---
---

## FortiMail Operation Modes: 
### Gateway Mode: FortMail provides full MTA functionality. FortiMail will scan all incoming emails. 
#### DNS MX record change required to redirect all inbound email traffic to the FortiMail. 
###### All inbound email goees through FortiMails first, then is routed back to mail server. 
#### For complete protection, all outbound email should be routed through FortiMail for inspection.
###### FortiMail verifies if the sender of the email is valid and then performs its own DNS MX lookup for delivery unless email forwarding is configured. 

### Server Mode: FortiMail provides full email server and MTA. We can Use it in replacement for retiring email servers. 
#### Fortimail will store the end-user mailboxes, in addition the FortiMail in server mode provides a complete group calendar, webmail, and other advanced features. 
##### All emails received ad stored by FortiMail.

### Transparent Mode: Located on the email path to intercept email traffic transparently for inspection. 
#### No need to chanege the DNS MX or DNAT rules. 

---
---
---
---
---

### If I want to forward the email to FortiMail, i have two sets: 
#### 1. relay: this is used to access the external domain
#### 2. route: this is used to access another mail with internal domain 

---
---
---
---
---

## Access Control & Policies 
#### This is the first step when SMTP session reach the Fortimail, it allowrd or reject the email before any scanning. 
#### This is to prevent important vulnerability in the email world "Open Relay" 

### Access Control Roles: 
#### Receiving Rules: Apply when Fortimail receiving email from Internal/external. 
#### Delivery Rules: After receiveing the email, the fortimail need to deliver the email, for example will send the email with same IP that receiver or make NAT... 

---

## Receiving Roles 
#### If SMTP Session doesn't match any rule, the default behaviour is based on the RCPT TO: 
##### 1. If an email is destined to protected domain, Fortimail relays it.
##### 2. If an email is not destined to a protected domain, FortiMail rejects it.

### Access Receive Rule Actions: 
<img width="486" height="269" alt="Actions" src="https://github.com/user-attachments/assets/f4641e60-0158-4731-8da8-93dd31b838a0" />

---

## IP Policy and Recipient-based Policy
#### Recipient-based Policy take precedence over IP based policy match, unless if "Take precedence over recipient based policy match option enabled in IP based policy.
##### IP based policy, filter traffic by IP addressess
##### Recipient-based Policy: filter traffic by email ID. 

<img width="1005" height="186" alt="Reciepent" src="https://github.com/user-attachments/assets/4e4f54e4-4196-43d2-a6cf-888bb6670b8f" />

---
---
---
---
---

## FortiMail Session Profile
### Session Profile: Focus on the SMTP connection, controlling how email connection are established and filtered before deeper content inspection occurs
#### Detect Suspicious activity as soon as possiple, allow fortimail take action early.
#### This is can be done in IP Header and SMTP envelope. 

<img width="693" height="254" alt="SMTP envelope" src="https://github.com/user-attachments/assets/3f67bed9-ea84-4524-8ada-1bbd7e794ef8" />

##### By defualt, there are two main profiles ( inbound / outbound ) 
##### Session Profile can be applied on IP based policy
##### Example: I can set config like this email can send only 5 email in specific time.
##### We can restrict number of connection per client.

### Also I can make like Reputation on each sender IP address in real time, with score is increased the fortimail will reject the emails.
#### The Score will be saved in fortimail DB

<img width="507" height="137" alt="Reputation" src="https://github.com/user-attachments/assets/013d8150-ab37-48bc-9697-5f303af57d4c" />

#### Also in the FortiGuard IP Reputation Check, there are a global threat intelligence databse to assess the reputation of a sender's IP address in real time

<img width="432" height="122" alt="rEPTATINO2" src="https://github.com/user-attachments/assets/f6021b04-7028-4e56-9187-d2d085a3660b" />

#### Session Profile Config: 

<img width="671" height="167" alt="Session Profile Config" src="https://github.com/user-attachments/assets/95962c7b-df4b-4d7b-946b-ad09a9387933" />

---

## Session Profile, Sender Validation:
### The Validation is done by SPF record and DKIM record.
#### This is standard validation no only in fortimail 
##### for the SPF, it is a DNS TXT record that that specifies which mall servers are authorized to send email on behalf of a domain. Prevent Email Spoofing 
##### to use SFP, domain owner publishes formatted DNS 

---
---

# Antivirus Profiles: 
### Responsible for scanning and removing malicious content from inbound and outbound emails. 
### Helps to protect agains viruses, malware, spyware, trojans, worms and other malicious content.
## The Core Purpose: 
##### To detect and mitigate malware and virus threats in: Email Attachments, Email body content(malicious links, scripts), Email Header, Archive Files. 
#### It is not like a traditional antivirus scanning, it uses multi-layered to detect and block malware usign several techologies and threat intelligence sources. 

## Main Technologies usid in Fortimail to detect Malware: 
#### 1. FortiSandox Integration: This is for unknown attacks or zero day or anything coudln't find signature for it. 
#### 2. FortiNDR Integration: Will check the file behaviour or contents of malware and returned to FortiMail.
#### 3. FortiIsolator Integration: is browser isolation solution that protects users against zero-day malware and phishing threats that are delivered over the web and in email. 
##### With FortiIsolator, web content is executed in a remote disposable container and displayed to users. 
###### Remoteley executes web content and displays it
###### Creates a virtual air gap bbetween users browsers and websites
###### Can also be comibned with URL click protect

<img width="712" height="239" alt="FortiIsolator" src="https://github.com/user-attachments/assets/e9f82279-4827-468f-80b9-791459dcd1e8" />

#### 4. Local Malware Detection
##### Fortimail uses a local sandbox to evaluate executable content that has passed the FortiGuard antivirus signatures. 

### Local Malware Detection Include: 
#### A. Fortiguard Antivirus Service: 
##### 1. Signature based Detection
##### 2. Include Grayware: This is unwanted application, like when we install a program, other programs may also installed directly.
##### 3. Database updated through FortiGuard Distribution Netwoork (FDN)

#### B. Heuristic: Local sandbox emulation to detect virus-like attributes in files. 

#### C. File Signature Check: If I some signature i want to block it manually "Emergency Blocking", i need to upload it and enable this feature. 

#### D. Malware Outbreak: 
##### 1. Uses data analytics by FortiGuard to generate rating information on known.
##### 2. bad-sender IPs, content and attachments. 

## Local Malware Detection Flow: 

<img width="1066" height="484" alt="Malware Detection Flow" src="https://github.com/user-attachments/assets/54c22c6d-a1bc-4287-ae04-3c5b1b9986f7" />

---

### FortiNDR : Performs machine-learning-based threat classification, behavioural analysis, and threat scoring. 
#### This is ideal for catching advancet persistent threats (APT), or zero day exploits that evade signature and sandbox detecton. 

### FortiSandobx, i have two options to enable it: 
#### 1. Submit and wait for result: Send the file to sandbox and waiting the sandbox result before sending the email. 
#### 2. Submit Only: Send it to sandbox but also send the email before waiting the result. 

### URL Analysis: Enable to send the URLs also not just the files to FortiSandbo and i have two choices: 
#### 1. All email: Sacn all emails by sandbox. 
#### 2. Suspicious email: Scan only the suspicious emails. 

## Final Action: 

<img width="1280" height="538" alt="Action" src="https://github.com/user-attachments/assets/43a9bc2c-2704-4bd3-bd6f-f6e19b6ff4c2" />

---
---
---
---

## Why I need to enable the Antivirus for the Outbound emails ? 
### To keeb the MX IP reputation good by prevent malware from leaving your network. 

---
---
---
---
---

# Antispam Profile 

### Antispam Technique: 

<img width="556" height="239" alt="Antispam1" src="https://github.com/user-attachments/assets/405140f3-0d33-4334-bb33-b06be5e3b984" />

<img width="568" height="218" alt="Antispam2" src="https://github.com/user-attachments/assets/35d5c24b-f484-489b-9547-a8d4b5a20db7" />

### FortiGuard IP Reputation: 
#### It is part of FortiGuard Anstispam service to identifies known spam sources by IP address. \
#### The IP of sending MTA will be checked agains FortiGuard Global blocklist database. 
##### This helps stop spam early at connection level (Save bandwidth & processing) 

#### Optionally: we can enable Extract IP from Received Header: This will check every IP listed in received headear of the email. 
##### Useful if the spammer hides behind multiple relays. 

###  Reputation Levels (3 tiers)

Reputation Levels|Possible|Action Recommended
|---|---|--- 
Level 1 (Worst Reputation)| known spammers, infected servers, open relays.|Reject (Send SMTP 550 response to client) or Discard 
Level 2 (Medium Reputation)| Suspicious, possibly compromised, flagged recently|Quarantine or Tag (Admins or users can review)
Level 3 (Lowest Risk)| Not very common spammers, but still questionable|Quarantine, Tag, or allow

### FortiGuarl URL filtering: checks embededded email urls agains fortigurad cloud-base database of categorized urls. 
#### If match, fortimail classify as spam/malicious and apply the action. 

<img width="434" height="149" alt="Antispam3" src="https://github.com/user-attachments/assets/d3bfa8a7-b350-4a15-8412-55079858af1b" />

## FortiGuard Spam Outbreak Protection
### Is a real-time spam detection service provided by FortiGuard. Uses cloud-based intelligence to identify new spam campaigns as soon as they appear.

### Spam outbreak protection can be set on the following: 
##### 1. set to enable: suspicious email is held in spam outbreak and then re-evluated it. This gives FortiGuard an opportunity to learn about potential spam oubreak and update its database. After timeout for email expires, FortiMail queries the fortiGuard servers again. If the ratings come back as clean, Fortimail releases the email to the receipents, otherwise it applies action. 

##### 2. set to monitor only, email is not deferred, Insted "X-FEAS Spam-outbreak:monitor-only" is inserted as its header, and the email is logged. 

---

### FortiGuard Spam Submission: 
#### End users can submit suspicous email as spam using Outlook plugin, the email can then be either reviewed by and administrator or sent to FortiGuard for immediate evaluation. 

---
---

### Greylist Antispam Techniques: 
#### This technique is temporarily rejects emails from unknown senders for the first time thay try to deliver a message.
#### When an email arrives from an unknown sender (defined by a "triplet" of sending IP, sender address, and recipient address), the receiving server temporarily rejects it with a 4xx SMTP error code. A legitimate server will retry sending the email later, and on the second attempt the message will accepted.
##### Many spam bots and malware don't retry, so their email ere effectively blocked.
##### It's behaviour based filtering rather than content-based 

###### Low maintance: No need for manual Keyword or IP lists 
###### Saves resource >> Messages blocked at greylist never go through other filters. 
###### Extra SPAM protection >> The delay gives FortiGuard & DNSBL time to update their span sibnatures/blaklists. 

### How it works: 
#### Fortimail Looks a 3-part combination 

<img width="670" height="266" alt="Greylist" src="https://github.com/user-attachments/assets/11c5f3a1-5ce8-44b8-8a19-40645691a942" />

### Manual Greylist Exemptions Usage: 1. Bypass greylisting for trusted senders/doamins/partners. 
#### 2. Mail comes from large email farms /16,/8,etc. where retries could come from many different servers. 

### Types of Greylist Entries

Type|Description
---|---
Pending|Created on first delivery attempt, waiting for retry
Individual|Confirmed entry after retry, speceific to sende/receipiens/IP
Consolidated(Autoexempts)|To manage high volumes of greylist entries (e.g., when one organization sends email to many users in your organization) by replacing thousands of individual entries with a single entry, thus reducing resource consumption.

Manual Exempt|Auto Exempt
---|---
Manual Exempt (Security > Greylist > Exempt): These are user-defined entries that bypass the greylist delay entirely. They are useful for known, large email server farms (e.g., Office 365) that might use different IPs for retries, which could break the automatic, behavior-based process.|Auto Exempt (Monitor > Greylist > Auto Exempt): These are created automatically after a sender has successfully passed the initial greylist delay and subsequent scans, proving they are legitimate. 

---


































