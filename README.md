*Please Note: I wrote the original documentation and built the app in early 2019. You can find the original repository [here](https://github.com/NandanDesai/PeerLink). Recently, I also created a [YouTube video](https://www.youtube.com/watch?v=GYbkg3mIhvI) where I demonstrate this project! This documentation is an improved version of the one that I wrote 2 years ago.* 

# PeerLink

People rely on instant messaging platforms for all kinds of sensitive conversations, including with their doctors, banks, families etc. Hence, privacy needs to be an integral part of any instant messaging platform. While most of the instant messaging apps aim at protecting user's privacy, they fail to achieve it by storing and analyzing the metadata. Instant messaging platforms with centralized architecture can be subjected to Data Exploitation and censorships which usually leads to suppression of free speech. To solve these issues, an instant messaging platform is required which should be either peer-to-peer or decentralized, end-to-end (E2E) encrypted and private (no processing of personally identifiable metadata).

## Introduction

In our project, we use Tor anonymity network to evade censorships. To avoid control of a single company/corporation, we start with the concept of building a Peer-to-Peer architecture.

Tor network will also be helpful here as it offers Onion Services which can be used to make peer-to-peer networks.

Hence, in our project, we have tried to solve the privacy related issues in the existing messaging platforms and give our users complete control over their data.

## Definitions

1. **Tor**: Tor is free and open source software for enabling anonymous communication.
2. **Onion Service**: Tor makes it possible for users to hide their locations while offering various kinds of services, such as web publishing or an instant messaging server. This service is known as an Onion Service (formerly known as Hidden Service).

## Design Challenges

There are several challenges that we will face while creating a P2P instant messaging app. They are:

### 1. Peer Reachability

Designing a peer-to-peer network requires the peers to have a static public IP address. Of course, this is not realistically possible in many cases. There might be some peers who are operating behind a NAT, or there are peers with dynamic IP address. To address this problem, there are solutions like NAT Traversal methods which allow hosts to communicate with each other directly even when they are in separate private networks. But, there is one flaw here. The hosts are still exposing their IP addresses (public IP address). And our goal is to avoid exposing any personally identifiable metadata including the actual IP address provided to the user by their Internet Service Provider (ISP).

### 2. Peer Availability & Network Scalability

In P2P architecture, there are cases when the peers are offline and this might disrupt the expected operation of the network. For example, if there are 3 peers who are involved in a group conversation through the app, let’s name them as A, B and C, and if A sends a message in the group and C is offline, then only B (who is online) receives the message. Now, if A goes offline and C comes online, then there should be a protocol designed in such a way that it should mandate B to forward A’s message to C. This seems acceptable, but if the group conversation involves, let's say, 100 members, then such a protocol doesn’t properly work and is not scalable. The protocol becomes even more broken if there are media files being shared in a 100 member group in this P2P network.

## Solutions to the Design Challenges

 1. To solve *Peer Reachability* and keeping user privacy in mind, we can use [Tor Onion Services](https://community.torproject.org/onion-services/overview/). Tor Onion Services makes it possible to reach peers who might have a dynamic IP address or who are behind a firewall.
 2. To solve *Peer Availability & Network Scalability*, a decentralized network architecture can be opted where anyone can setup a server and all the servers will be hosted on Tor. So, IP addresses of the users as well as the servers will be hidden. And Signal Protocol can be used to provide E2E encryption for the messages. Decentralized architecture makes our application's network more stable especially if we want our application to support Group chats.

## Proof of Concept (POC)

**Android app**: Refer [this repository](https://github.com/NandanDesai/PeerLink). The app uses [Orbot](https://play.google.com/store/apps/details?id=org.torproject.android&hl=en_IN&gl=US) to create the Onion Service and communicates with other instances of PeerLink through Tor in a Peer-to-Peer fashion. As this app is just a POC, it doesn't support Group chats and supports only one-to-one Direct Messaging.

**My YouTube video**: You can watch [my youtube video](https://www.youtube.com/watch?v=GYbkg3mIhvI) where I demonstrate this proof-of-concept app.

## Future Challenges

There are many challenges and issues with this concept.

 1. **Denial of Service**: There is a possibility where if a malicious entity knows a person’s Onion address, then they may try to flood the traffic and slow down the app or the mobile device.
 2. **Spamming**: In apps like WhatsApp, the user’s ID is their phone number. Ideally, it difficult to get a new SIM card or a new phone number for a user. So, if a WhatsApp user is receiving spam messages from another user, then that spammer can be blocked. And the spammer will have a hard time getting a new phone number for themselves if they want to start spamming the same user again. But, if an Onion address is the ID of a user, then the spammer can easily create a new Onion address when the previous address gets blocked.

Mitigating these issues is difficult.

## Conclusion

There are several apps that already use the similar ideas mentioned in this article. They are:

1. [Ricochet IM](https://ricochet.im/) : uses Tor network and onion addresses to communicate. But doesn’t support Group chat or File transfer. It is uses a Peer-to-Peer network architecture.
2. [Tox](https://tox.chat/index.html): has a peer-to-peer style protocol which includes text messaging and file sharing including voice and video calls. But, it exposes user’s IP address.

So, in conclusion, a proposed solution to solve the disadvantages of each of those apps is to use a decentralized (rather than Peer-to-Peer) network architecture that improves both scalability and reachability (as mentioned in Design Challenges of this article) and building the entire network architecture using Tor Onion Services and using Signal Protocol (or rather OMEMO protocol which is a combination of XMPP and Signal Protocol) to protect user privacy and also have features like confidentiality, integrity, authentication, forward secrecy etc. that the Signal Protocol offers.

Also, if you are interested in building your own Instant Messaging app, then you can refer my [AndroidIMTemplate](https://github.com/NandanDesai/AndroidIMTemplate) repository which is very well documented and the code is derived from the aforementioned POC app.

## License

Copyright 2021 Nandan Desai

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
