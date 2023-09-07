
### What is a DNS?

DNS(Domain Name System) provides a simple way for us to communicate with devices on the internet without remembering complex numbers.
When we want to visit a website, it's not exactly convenient to remember this complicated set of numbers, and that's where DNS can help.

![[dns.png]]


---

### Domain Heirarchy

![[dnsHeirarchy.png]]


TLD(Top Level Domain)

A TLD is the most righthand part of a domain name. So, for example, the tryhackme.com TLD is **.com**. There are two types of TLD, gTLD (Generic Top Level) and ccTLD (Country Code Top Level Domain). Historically a gTLD is meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for an organisation, .edu for education and .gov for government. And a ccTLD is used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom and so on. Due to such demand, there is an influx of new gTLDs ranging from .online , .club , .website , .biz and so many more.

Second Level Domain

Taking tryhackme.com as an example, the .com part is the TLD, and tryhackme is the Second Level Domain. When registering a domain name, ***the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).***

Subdomain

A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name admin.tryhackme.com the admin part is the subdomain. ***A subdomain name has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens). you can use multiple subdomains split with periods to create longer names, such as jupiter.servers.tryhackme.com. But the domain name length must be kept to 253 characters or less. There is no limit to the number of subdomains you can create for your domain name.***

*Maxium domain name length=253*


---

### DNS Record Types

DNS isn't just for websites though, and multiple types of DNS record exist.


**A Record**

Purpose: Maps a domain name to an IPv4 address.

```sh
host -t A example.com
```

example.com.   IN   A   192.168.1.1

**AAAA Record**

Purpose: Maps a domain name to an IPv6 address.

```sh
host -t AAAA example.com
```

example.com.   IN   AAAA   2001:0db8:85a3:0000:0000:8a2e:0370:7334

**CNAME Record**

Purpose: Creates an alias or canonical name for an existing A or AAAA record. Useful for creating subdomains or domain aliases.

These records resolve to another domain name, for example, TryHackMe's online shop has the subdomain name store.tryhackme.com which returns a CNAME record shops.shopify.com. Another DNS request would then be made to shops.shopify.com to work out the IP address.

```sh
host -t cname www.example.com
```

\www.example.com.   IN   CNAME   example.com.

So typing example.com is same as typing \www.example.com
DNS needs to be performed twice

Example

1) **Initial DNS Query:** Suppose you have a CNAME record like this:
```sh
host -t cname www.example.com
www.example.com. IN CNAME example.com.
```

When someone queries DNS for the IP address of \www.example.com the DNS resolver receives this CNAME record as the response.


2) **Second DNS Query:** The DNS resolver, upon encountering the CNAME record, needs to resolve the new domain name ("example.com" in this case) to an IP address. To do this, it performs a second DNS query to look up the A or AAAA record for "example.com."

```sh
example.com. IN A 192.168.1.1
```

3) **Final Resolution:** After resolving "example.com" to its IP address, the DNS resolver finally has the IP address for \www.example.com and can return this IP address to the original query.


***The reason for this indirection is that CNAME records are designed to allow you to change the target of an alias without having to update multiple DNS records. This can be particularly useful when you need to change the IP address of a website or service. Instead of updating multiple A or AAAA records for different subdomains, you can update the CNAME record to point to the new target.***

**MX Record**

These records resolve to the address of the servers that handle the email for the domain you are querying, for example an MX record response for tryhackme.com would look something like alt1.aspmx.l.google.com. These records also come with a priority flag. This tells the client in which order to try the servers, this is perfect for if the main server goes down and email needs to be sent to a backup server.

**TXT Record**

TXT records are free text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones can be to **list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spam and spoofed email). They can also be used to verify ownership of the domain name when signing up for third party services.**


---

### Making A DNS Request

![[dnsProcedure.png]]


1) When you request a domain name, your computer first checks its local cache to see if you've previously looked up the address recently; if not, a request to your Recursive DNS Server will be made.

2) A Recursive DNS Server is usually provided by your ISP, but you can also choose your own. This server also has a local cache of recently looked up domain names. If a result is found locally, this is sent back to your computer, and your request ends here (this is common for popular and heavily requested services such as Google, Facebook, Twitter). If the request cannot be found locally, a journey begins to find the correct answer, starting with the internet's root DNS servers.
3) The root servers act as the DNS backbone of the internet; their job is to redirect you to the correct Top Level Domain Server, depending on your request. If, for example, you request \www.tryhackme.com, the root server will recognise the Top Level Domain of .com and refer you to the correct TLD server that deals with .com addresses
4) The TLD server holds records for where to find the authoritative server to answer the DNS request. The authoritative server is often also known as the nameserver for the domain. For example, the name server for tryhackme.com is kip.ns.cloudflare.com and uma.ns.cloudflare.com. You'll often find multiple nameservers for a domain name to act as a backup in case one goes down
5) An authoritative DNS server is the server that is responsible for storing the DNS records for a particular domain name and where any updates to your domain name DNS records would be made. Depending on the record type, the DNS record is then sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client that made the request. DNS records all come with a TTL (Time To Live) value. This value is a number represented in seconds that the response should be saved for locally until you have to look it up again. Caching saves on having to make a DNS request every time you communicate with a server.