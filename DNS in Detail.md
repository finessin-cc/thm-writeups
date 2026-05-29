# TryHackMe: DNS in Detail

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | DNS Fundamentals            |
| Difficulty    | Beginner                    |
| Date          | July 10, 2021               |

## Task 1: What is DNS?

DNS (Domain Name System) provides a simple way to communicate with internet devices without remembering complex IP addresses. While IP addresses like 104.26.10.229 are difficult to remember, domain names like tryhackme.com are much more user-friendly.

**Question:** What does DNS stand for?
- **Answer:** Domain Name System

## Task 2: Domain Hierarchy

### Domain Structure

**TLD (Top-Level Domain)**
- Most right-hand part of a domain name
- Examples: .com, .org, .edu, .gov
- Types:
  - gTLD (Generic Top Level): .com, .org, .net
  - ccTLD (Country Code Top Level): .ca, .co.uk

**Second-Level Domain**
- The part immediately to the left of the TLD
- Example: "tryhackme" in tryhackme.com
- Limited to 63 characters plus TLD
- Can only use a-z, 0-9, and hyphens (no leading/trailing hyphens or consecutive hyphens)

**Subdomain**
- Parts to the left of the second-level domain
- Example: "admin" in admin.tryhackme.com
- Same naming restrictions as second-level domains
- Maximum total length of 253 characters
- No limit to number of subdomains

**Questions:**
- What is the maximum length of a subdomain?
  - **Answer:** 63
- Which of the following characters cannot be used in a subdomain ( 3 b _ - )?
  - **Answer:** _
- What is the maximum length of a domain name?
  - **Answer:** 253
- What type of TLD is .co.uk?
  - **Answer:** ccTLD

## Task 3: Record Types

DNS supports multiple record types beyond simple website resolution:

**A Record**
- Resolves domain names to IPv4 addresses
- Example: 104.26.10.229

**AAAA Record**
- Resolves domain names to IPv6 addresses
- Example: 2606:4700:20::681a:be5

**CNAME Record**
- Resolves to another domain name
- Example: store.tryhackme.com → shops.shopify.com

**MX Record**
- Resolves to email server addresses
- Includes priority flags for backup server selection
- Example: alt1.aspmx.l.google.com

**TXT Record**
- Free text fields for various purposes:
  - Email authentication (SPF, DMARC)
  - Domain ownership verification
  - Example values:
    - `_acme-challenge.example.com TXT "token_value_here"`
    - `@ TXT "v=spf1 ip4:192.0.2.0/24 include:_spf.google.com include:amazonses.com ~all"`

**Questions:**
- What type of record would be used to advise where to send email?
  - **Answer:** MX
- What type of record handles IPv6 addresses?
  - **Answer:** AAAA

## Task 4: Making A Request

### DNS Resolution Process

1. **Local Cache Check**: Client checks its local DNS cache first
2. **Recursive DNS Server**: If not cached, request sent to ISP-provided recursive DNS server
3. **Root DNS Servers**: If not found locally, request forwarded to root servers
4. **TLD Servers**: Root servers direct to appropriate TLD server (.com, .org, etc.)
5. **Authoritative Servers**: TLD servers direct to authoritative nameserver for domain
6. **Response**: Authoritative server returns DNS record, cached locally, and returned to client

**Key Concepts:**
- **TTL (Time To Live)**: Specifies how long DNS records should be cached in seconds
- **Recursive DNS Server**: Usually provided by ISP; maintains local cache
- **Authoritative DNS Server**: Stores actual DNS records for a domain and handles updates

**Questions:**
- What field specifies how long a DNS record should be cached for?
  - **Answer:** TTL
- What type of DNS Server is usually provided by your ISP?
  - **Answer:** recursive
- What type of server holds all the records for a domain?
  - **Answer:** authoritative

## Task 5: Practical

Using the DNS query website interface, practical DNS queries can be performed to examine various record types.

**Questions:**
- What is the CNAME of shop.website.thm?
  - **Answer:** shops.myshopify.com
- What is the value of the TXT record of website.thm?
  - **Answer:** THM{7012BBA60997F35A9516C2E16D2944FF}
- What is the numerical priority value for the MX record?
  - **Answer:** 30
- What is the IP address for the A record of www.website.thm?
  - **Answer:** 10.10.10.10
