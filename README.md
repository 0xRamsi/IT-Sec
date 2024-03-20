# Security in the digital space

What do non-experts think?
- Use anti-virus
- Use strong password
- Change passwords frequently
- Only visit known websites
- Don't share personal data

What do experts think?
- Install software updates
- Use unique passwords
- Use 2FA
- Use strong passwords
- Use a password manager

### Update you devices!

## There is no silver bullet
Tools can help you, they all have pros and cons. There is not one solution fits all. You need to keep thinking about your situation.

What you really want is OpSec. The digital world is just a part of security.

## Risk assesment
A few questions to ask yourself:
- What do I need to protect?
- Who do I need to protect it from?
- What happens if they do get it?
- How much do they want that information, and how easy is it for them to get it?

You cannot hide everything from everybody, that is paranoia.
- Examples of different things to hide from different people.

Broader questions:
- Do I want to keep off the radar?
- Can I confront authorities with "It's my right to do that" or "Do you have evidence?"?

## What is encryption?
Rotation cypher
- Rotation cypher
- I use ROT13 twice!

Public-Private key (asymetric encryption)

A public key looks like this:
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBN1N2AiSxq6+DgR3sgUT8NORMLGsWm74tMEb7ZjVJbi ramzi@laptop
```

A private key looks like this:
```
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACATdTdgIksauvg4Ed7IFE/DTkTCxrFpu+LTBG+2Y1SW4gAAAJC/E28+vxNv
PgAAAAtzc2gtZWQyNTUxOQAAACATdTdgIksauvg4Ed7IFE/DTkTCxrFpu+LTBG+2Y1SW4g
AAAED9p9fdeA0GoP9HalR4np3Zk1Zxy94SfeMDjuvVZn1lFxN1N2AiSxq6+DgR3sgUT8NO
RMLGsWm74tMEb7ZjVJbiAAAADHJhbXppQGxhcHRvcAE=
-----END OPENSSH PRIVATE KEY-----
```
### What is the deal with Metadata? Does encryption save the day?
Let's look at the following chat:

![](chat.png)

Assuming the chat has proper encryption, what will the different actors learn?

The ISP will see the communication from you to the chat server. They will not know who you texted, or what the content of the text is.
Something like this:

**ISP logs**
| Timestamp | Sender | Reciever | Message |
|-----------|--------|----------|---------|
| 2024-03-14 23:58 | \<MyIP\> | \<chatIP\> | OqfqWML8zGw+6l1y6E |
| 2024-03-14 23:58 | \<chatIP\> | \<MyIP\> | NE0GsA0YAlnkC1PX1G |
| 2024-03-14 23:58 | \<MyIP\> | \<chatIP\> | HirzeJfL+rUzYFci45 |
| 2024-03-14 23:59 | \<chatIP\> | \<MyIP\> | uVuJKMRpprJc9PfSB7 |

So they know, that I send 2 messages and got 2 replies. They can only assume that it is from the same person.

**Chat logs**
| Timestamp | Sender | Reciever | Message |
|-----------|--------|----------|---------|
| 2024-03-14 23:58 | \<MyUser\> | \<otherUser\> | 5rHs/ukyVaFqYyf1x0 |
| 2024-03-14 23:58 | \<otherUser\> | \<myUser\> | yXrOiE9L/1EphiKr0Y |
| 2024-03-14 23:58 | \<MyUser\> | \<otherUser\> | JctqI+NGIsi7w1qD84 |
| 2024-03-14 23:59 | \<otherUser\> | \<myUser\> | wn75eOlgoqA0su23aH |

They also know both IPs, and the obvious information, that you are online. The chat company could also notice 30 mins later, that both users are connected via the same wifi.

## ISP, VPN and Tor

### ISP - Internet Service Provider
An ISP is a company like Telekom, O2 and Vodafone.

- What does your ISP know about you?
Your ISP is the one giving you an IP-Adress and in most countries they are obligated to keep logs of who has which IP-Adress at which time, and they are required to hand them over to the authorities - normally only after being presented a warrent.

Your ISP is also handeling ALL of your communication. Every website you visit, every text you send, every video you watch. That said, they handle the forwarding of information, but if it is encrypted, they can only know that you sent something, and to who you send it.

You may have more than one ISP. Eg you have a wifi from Vodafone and a cellphone SIM from O2. Nonetheless, both are on your name.

In case of a shared flat, certain copy-right violations (downloading a movie) can be refuted by saying "I don't know who downloaded it. That day we also had guests who could have done it.". This is just a leagal trick, in other accusations this means: the authorities are watching you.

Public wifi is typically anonymous. Their also sometimes restricted, and they may log device information.

### VPN - Virtual Private Network
TLDR; It's just replacing your ISP.

![](What-is-a-VPN.png)

An attacker who "tapped your wire", can not konw what you are communicating and to who. They can learn, that you are using a VPN, when you are using it, how much data is going back and forth. They cannot learn if you are watching a stream on twich or downloading a movie, as it is roughly the same amount of encrypted data. They can know that you are reading websites, but not which. They also cannot tell if you are texting one person a lot, or many people a little. And even learning that is an effort.

On the other hand, all data is decrypted at the VPN server, which is your proxy. That means, your VPN provider knows everything your ISP would normally know. So basically you just shifted your trust from the ISP to the VPN.

One thing to consider is, that your VPN provider can be in a different country, and not obligated to cooperate with authorities in your country. But they can.

### Tor - The Onion Router

![](Tor-Network.png)

The idea is that every message (or image or whatever) is encrypted at least 3 times, and routed throgh at least 3 nodes before reaching the other end. By that, no one node can know who is communicating with who. It's kind of like chaining 3 VPNs one after the other, except they don't require a login for the connection and keep getting mixed around.

It's meant to give complete anonymity, as no one node knows the origin and destination of a message. The NSA repeatedly claims to control a big chunk of the Tor exit nodes, and that this gives them an idea of what is happening in the dark net.

Originally developed by USA to communicate with their spys/informants. Later is was funded by different Gov and humand rights institutions, and today it's about half funded by the USA gov, and the other half is a mix of individuals, foundations and cooperations.

## Messengers

| Messenger | open source client | open source server | Database | Notes |
|-----------|--------------------|--------------------|------|-------|
| Signal | ✓ | x | x | Has a centrelised server |
| Matrix | ✓ | ✓ | ✓ | Slow and bloated, gaining traction. |
| SimpelX | ✓ | ✓ | x | Has no identifier |
| IRC | ✓ | ✓ | x | It's one of the absolute oldest system on the internet. |
| Briar | ✓ | ✓ | ✓ | Made for revolution scenarios. Mesh network, anonymus. Possibly slow. |

## Cloud drives - Proton vs Google vs Self hosted
- Google is reading your data, and not even trying to hide it.
- Proton is promissing to encrypt your data, and has a solid case to prove it - the client is open source.
- Self hosted is technically the best. But... you need money, you need time to set it up, you can make mistakes with the configuration. Your hoster still gets some information.

So, you can pick and choose, depending on your risk assesment. Technically, some things are "okay to post online" but will draw attention, which can conflict with your model of staying below the radar.

## Resources:
- https://activisthandbook.org/tools/security
- https://media.ccc.de/v/35c3-10018-verhalten_bei_hausdurchsuchungen - Talk aobut behaviour during a police raid in your house (German)
