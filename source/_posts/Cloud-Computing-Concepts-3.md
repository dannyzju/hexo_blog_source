---
title: P2P Systems
toc: true
categories: tech
tags:
- 学习笔记
- tech
---

Peer-to-Peer Systems is important because it is a precursor to today's cloud computing.

What will be covered in this chapter:
- Unstructured p2p systems, e.g., Gnutella, Napster, etc.
- Structured p2p systems, e.g., Chord, Pastry, etc.
- Latter is a pre-cursor to key-value/NoSQL storage systems (which comes in next chapter)

### P2P Systems Introduction
Why Study Peer to Peer Systems?
- First distributed systems that seriously focused on scalability with respect to number of nodes
- P2P techniques abound in cloud computing systems
	- Key-value stores (e.g., Cassandra, Riak, Voldemort) use Chord p2p hashing

A Brief History
- [06/1999] Shawn Fanning (Freshman Northeastern U.) releases Napster online music service
- [12/99] RIAA sues Napster, asking $100K per download
- [03/2000] 25% UWisc traffic Napster many Universities ban it
- [2000] 60M users
- [02/2001] US Federal Appeals Court: users violating copyright laws, Napster is abetting this
- [09/2001] Napster decides to run paid service, pay % to songwriters and music companies
- [Today] Napster protocol is open, people free to develop open nap clients and servers [http://opennap.sourceforge.net](http://opennap.sourceforge.net)
	- Gnutella: [http://www.limewire.com](http://opennap.sourceforge.net)(deprecated)
	- Peer to peer working groups: [http://p2p.internet.edu](http://p2p.internet.edu)

What We Will Study
- Widely-deployed P2P Systems
	- Napster
	- Gnutella
	- Fastback (Kazaa, Kazaalite, Grokster)
- P2P Systems with Provable Properties
	- Chord
	- Pastry
	- Kelps


### Napster
#### Napster Structure
![Napster Structure](https://lh3.googleusercontent.com/1xUO2uOVFcxMrRtxu5aPHmaYQ0ki5OurLTb6V_vKHhbxqYKWpDgkmlU4F0C1UwdMJ81HNdW44B5FFKR5H9dx6bTJOGFCky1rQTQWjh9juN0J3sYQtjMOeLA21cjEVoPH4Tr1B-EXkrxR6X3QaJJg-HWGj6_EaJKhle0v7JfLLLRKlwDHclNUIgwpQl10KLTKsLKpEALbl7uDpLI2oiaTrKCgiwiWftBO_9lEiargpxg3kaFSZZaLjy1q1H8J9aGYBM-XffE3BOpSPLWiS88Mf9TbBvbBtwOv1z-8uh59auq2_Hj67JOjcCxZE6oAhhdpa7Eu_GOlXieOY6JyPCYq1vfi94fVMjUgitYejNV3UlnRKHtyh0DDhKSP49hsd02llPToYiqZQQf2TcsOz1cXTpbrJAObAxdw2omyEjQCOvY3kTZ4BBfScGnGefcykyIU5l9nlkOyivRzwgtl-6HgqT7xsMrIi6mB9MqAvYMh2ynpA0-06nBHfDpjmIFLvRVGlgPL0r73i47_FsWmy82yXCCDv2EHAlPmhXxKhrphs675t0rmDLCNyJE3WHNcqPB_RZoOrbHjTLvfFn1Y8xTpbjmEgZf9tgxGbrGqoKYDn46088PdDONgPjK3S9UMsw3GCtYO39CCrC06xPzgaqMe_mKsKbMAG37HOE8gedc8Nw=w993-h624-no)
#### Napster Operations
Client
- Connect to a Napster server
	- Upload list of music files that you want to share
	- Server maintains list of <filename, ip_address, portnum> tuples. **Server stores no files**.
- Search
	- Send server keywords to search with
	- (Server searches its list with the keywords)
	- Server returns a list of hosts -<ip_address, portnum>
 tuples - to client
	- Client pings each host in the list to find transfer rates
	- Client fetches file from best host
- All communication uses TCP (Transmission Control Protocol)
	- Reliable and ordered networking protocol

#### Napster Search
![Napster Search](https://lh3.googleusercontent.com/nEPVln8yqe-XrB9M5K1QfFfJdEYL-zmtFAJhmr28YFUBttMqHuI2kdejhh4Xd24KTEO2anFMrz-NA0v5X-5QPsx7t6-Vzs_TdwTyvqrL1yFjSamzQ5fbmIkw4TH1zlSyEM8MLiFnoW_VzGZ0IFb0mE1ptrp_cFfxh83Y7wJv-uVyhQj5hDceBpPEwI3LZ94wfgIOV1PA2NxytgsIHwnD6pHRtYqwvJkCn-0ovsx8RCvpeCqSuTmyrfq8-LbSEMg1r54EJqnlEFMbXiGjpTIoQSzV-QwvhIjPGMLPdqM8bGwhZdSJGb_9T-LEboMyKGlm_8rL-2yTEJD52qBeUriUFZn_pc5nX2WAvgrU1Gu0h0_osotM1xDwpzJpv9eam_hXr40b-s5AUubAk1CDgVEn1SluDNZ4zNiB1iJmQVu2-jakCfpE1541CI6QeAWuk48vraUNSq4JiJF67x9UvcvW4sf3si1Zcx-RfdkdldFKcL-tr7RwFdbYh6NelgUve29Z2x0WwxfmNDwWV9jf8IkiklflvFc3Ft2EjRBukMU6aIvnYy7NLAoLuw3mtFycdZjGh-up0MhFlcBtYfskopuZQVaABbCM0I5vtGfAH3JtFO6eNausAOUOTPGYeRg_NZMFL-1CFKmgQTuYi4_-De2HSBnOHx0rRN01GMvP21TW_w=w997-h622-no)

#### Joining a P2P System
Can be used for any p2p system
- Send an http request to well-known url for that P2P service - http:www.myp2pservice.com
- Message routed (after lookup in DNS = Domain Name System) to introducer, a well known server that keeps track of some recently joined nodes in p2p system
- Introducer initializes new peers’ neighbor table

#### Problems
- Centralized server a source of congestion
- Centralized server single point of failure
- No security: plaintext messages and passwords
- napster.com declared to be responsible for users’ copyright violation
	- “Indirect infringement”
	- Next system: Gnutella

### FastTrack and BitTorrent

### Chord

### Failures in Chord

### Pastry

### Kelips

(更新中，预计完成于03/25/2017)
