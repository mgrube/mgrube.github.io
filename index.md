# Freenet as a self-scaling application backbone

Freenet is a private, decentralized file publication system that has existed since 1999. That means
that as of later this year, Freenet will be 20 years old. Over the years, Freenet has evolved from
a way to share controversial web content to a decentralized way to provide email, filesharing and 
forums without requiring a server or central party to handle requests. 

I'm currently in the process of building a software stack to allow people to create their own
decentralized, encrypted, invite-only forums and filesharing. Although it will turn 20 this year, 
I will detail why Freenet is the best choice for an application backbone and why I think it may 
be worth more than just my time. 

## Darknet mode
Freenet itself has many different security settings and modes of operation. If users care less
about anonymity and more about performance, they can set their node to operate on low security
mode. This entails a user asking a Freenet "seed node" to connect them with other users - strangers.
While it is fairly difficult to know what any given node is really doing, there are several published
correlation attacks for this mode of Freenet. This is actually true of any peer to peer system. 
When you connect to complete strangers, you may actually be connecting to malicious nodes who may
be sniffing traffic or doing timing and size side-channel analysis to determine what your node is 
doing. Freenet calls this mode "Opennet" mode - if you are the target of an attacker, this more
can be fairly dangerous(hence the name "low security mode"). 

A unique solution to this problem that Freenet employs is the creation of "darknet" nodes. In the
context of Freenet, a darknet is a network of nodes that trust each other to hide the fact of their
participation in the network. I've just used a security four-letter word: trust. Let's talk about 
this, as people who do not understand how Freenet employs trust have taken this to mean the wrong
thing. When I participate in a Freenet darknet, I trust my darknet peers simply to not share my IP
address. I am not trusting them not to read my traffic - indeed proper Freenet use makes this 
impossible. I am simply trusting them with my IP address and not allowing the outside world to know
it - through this, we can achieve relative anonymity. Whether my peers know what I am doing on 
Freenet is an entirely different question. Tor employs a similar concept called gaurd 
nodes, which are the first nodes that tor users connect to. These nodes knows the true addresses of all
connecting Tor nodes - the main difference with Freenet is that there is that instead of trusting
a small set of nodes operated by strangers, you are trusting whoever you elect to trust. 

## All Data Is Encrypted
All data published on Freenet is encrypted with a deterministic AES key based on either the content
or a randomly generated key. No data on Freenet can be decrypted unless the requester has access
to both the decrytpion key and the hash of the data they are interested in. This means that nodes
cannot snoop on each other by examining their own datastores unless they are given a key to the 
content that exists there. This also assumes that the data itself is not encrypted at the application
layer. If applications running on Freenet take advantage of end-to-end encryption, it is the 
distributed datastore equivalent of using https over Tor. Snooping becomes excessively difficult. 

## High Availability
Another attractive aspect of Freenet is that as long as content is used or popular, it will remain
available on the network. We do not have to trust anybody to host our content nor do we need a server
to stay online. Freenet currently has its own collection of "Freesites", which continue to serve 
content without the need for a server. Other software stacks that provide similar features still 
require nodes to voluntarily host and share specific content. Freenet is specifically designed against
this concept, as people who control which content is served are given an inordinate amount of control over the network. It is also extremely hard for data to stay private if people must elect to hosting it.

If we use these darknet and high availability features to our advantage, we have not only a relatively private filesharing and communication network, but also a self-sustaining application backbone upon which we may build whatever we like.

For a very practical introduction to the Freenet API using Python, read [this article](https://www.draketo.de/light/english/freenet/communication-primitives-1-files-and-sites).

## Phage
After noticing these attributes of Freenet, it occured to me that a golden opportunity exists to create
a radically different set of applications that are anonymous, encrypted and very hard to shut down.
I'm taking to this goal myself by attempting to provide a private service wherein users may connect
only to people they trust and communicate anonymously in a forum that only some may see. The code
is very very far from being usable, but I feel that I've given it at least a good start. You can follow
this project [here](https://github.com/mgrube/Phage).

That's all I've got for now - I will soon be providing documentation on the design of Phage and how
it allows moderated anonymous forums that only people with the proper invitation may read. 

