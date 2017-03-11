---
title: Cloud Computing Concepts Notes (Part I)
date: 2017-02-25 21:21:37
tags:
- 学习笔记
---

Class notes for Cloud Computing Concepts by Indranil Gupta @ Coursera

(初稿完成于 02/25/2017)

## 0. Pre-Requirements
### 0.1. Basic Data Structures
- Queue: First-in First-out
- Stack: First-in Last-out
### 0.2. Process: A Program in Action
### 0.3. Computer Architecture (Simplified)
![Simplified Computer Architecture](https://lh3.googleusercontent.com/GMfMsR3vkGyXLt45RnixisMvF_Ye2G23wlVecbaInkuFRZ3kBjQR6JgAdbllBIRzEBIPtrEWLBjVNfQ1jHR92PZ4TuSN9gz99H3P3GCPEiulcbjmTcsmJmlS5E8VPNnoKPnUtWvgJ8XNQPJ6l37_Ml6_jevJMrfOPSjM1dpYxKCLexbEUp80vtJG72QhcHlKVdrr6STCmlcBhz3I5oqnm89Yzyf2XWxvj3cguIL3Gw4XFE2z6oyps5lIu9ZhJycag2H1W1j9AYXwJYSPF-v3rjamBOK8pMuOYNSHEDyNc5lThL09dnp_D_nKFoUBQYinj67R0H33Sc3jsRaZi8f65sPcFu-DvL2tQ2A8FmWmQg4yoSkXtZJ3ilkmfZ4NkFErQXOWMJREyG1SZFI4zjTnS0_Ve22dlxoXPNmixIH59ZBLmEndkR65ET45fpvkuiHpyoDCuUaNW_eAeEkKSaoTZDMLxUGaksmm62K9XU_lWHEiR1YwVW24V_vDYXH-Shmhpnt_qzDnBYF9NJXb321wmNmIEatmQMoc6vNXHHkNqpvEtMUiXlXEWCwrpK3_AdyOI9sCRyXL47jswkxCCANfwW3MKHppX3kHJLRJd19qrQSh5RlJ11k8eYnbZCwopaDWVjM3pbgPoXog56JSLNEKALGsUu2fUW9hbzx_aCj3EQ=w792-h798-no)

- A program you write (C++/Java etc.) gets compiled to low-level machine instructions
	- Stored in file system on disk
- CPU loads instructions in batches into memory(and cache, and registers)
- As it executes each instruction, CPU loads data for instruction into memory (and cache, and registers)
	- And does any necessary stores into memory
- Memory can also be flushed to disk
### 0.4. Big O() Notation
- One of the most basic ways of analyzing algorithms
- Describes ***upper bound*** on behavior of algorithm as some variable is scaled(increased) to infinity
- Analyzes run-time (or another performance metric)
- Worst-case performance
### 0.5. Basic Probability
### 0.6. DNS
- Domain Name Service
- Collection of servers, throughout the world
- Input to DNS: a domain name, e.g., coursera.org
- Output from DNS: IP address of a web server(that hosts that content)
- IP address may refer to either
	- Web server actually hosting that content, or
	- An indirect server, e.g., a CDN(content distribution network)server, e.g., from Akamai
### 0.7. Graphs

## I. Introduction to Clouds, MapReduce
### 1. Introduction to Clouds
#### 1.1. Why Cloud?
Two Categories of Clouds
- Public Clouds: provides service to any paying customer
	- Amazon S3(Simple Storage Service): store arbitrary datasets, pay per GB-month stored
	- Amazon EC2(Elastic Compute Cloud): upload and run arbitrary OS image, pay per CUP hour used
	- Google App Engine/Compute Engine: develop applications within their App Engine framework, upload data that will be imported into their format, and run
- Private Clouds: accessible only to company employees

Customers save time and money by using clouds.

#### 1.2. What is a Cloud?
Cloud = Lots of storage + compute cycles nearby
- A single-site cloud (aka “Datacenter”) consists of
	- Compute nodes (grouped into racks)
	- Switches, connecting the racks
	- A network topology, e.g., hierarchical
	- Storage (backend) nodes connected to the network
	- Front-end for submitting jobs and receiving client requests
	- Software Services
- A geographically distributed cloud consists of
	- Multiple such sites
	- Each site perhaps with a different structure and services

#### 1.3. Introduction to Clouds: History
Trends: Technology
- Doubling periods - storage: 12 months, bandwidth: 9 months（Moore's law）
- Then and Now
	- Bandwidth
		- 1985: mostly 56Kbps links nationwide
		- 2012: Tbps links widespread
- Disk capacity
	- Today’s PCs have TBs, far more than a 1990 super computer
- Biologists
	- 1990: were running small single-molecule simulations
	- 2012: CERN’s Large Hadron Collider producing many PB/year

In 1965, MIT’s Fernando Corbato and the other designers of the Multics operating system envisioned a computer facility operating “like a power company or water company.”

Plug your thin client into the computing utility and play your favorite Intensive Compute & Communicate Application
- Have today’s clouds brought us closer to this realty? ：）

#### 1.4. Introduction to Clouds: What’s New in Today’s Clouds
![A Cloud History of Time(1)](https://lh3.googleusercontent.com/_klWna3gomnU7K_kdB-ZgaVgvJVJ5Fd4GxFPO6RykM7Gci83sUHWyZx_u3q0hbAbLsRIOmJjQTmfiwirgvUdR2BB5GY1bt0BVmX8n4WYzTU9Q3oDGtT6RZW0WCtvxeckOclLu9_VGWcD_0oM7UARN0kYFWNBTS7lV5ego1jyvS6hKheFJMOEHawHPDv5JtqBnE-Zy4T5OaOTqSnGhMa30TxMgtDrt-AyIg_nM4lF39dVEbHRX3xI7k1U80KU3GUXe3p7kXjMgXNmXh9VJhf8ybmuckFivZp8AVbV1cc876SHIcOSwseFuLZkgX7A2zPgyF-r9h29pwTKZl6jAe82zXr5XLSbVr6l9m2axZTOd7dwRWG-3aGSxoQexEfw8x7l9JszreA8HQyfN0VhWNt3hEqUCP1fjpr5LUVcO-p0l82mHug3wT3gDI5q7CXpWwA6HbggJjUx79dedUHM9AcNWL14VtUo81X8Q3gWnxAF86HkyZMSeF6Q_SGz9EyTyv6gaJhs6koP0NsrTyVso8cVp2YN6X-M1nD6sVrjMxhfiiSpUhnAdl_tZTZ1f0POZVEk_path5pCMNjswTkn-A-u5JemaImNoT4Mxb3NdUj4p4N4HQwZ6sRPiIiUAK_YY9otUl_dzvtT0SmK3ZrnXPrWKCeTqMYT8e5vHT6xIUkkaw=w915-h516-no)

![A Cloud History of Time(2)](https://lh3.googleusercontent.com/3qBz0i1ihRrboZWMiF0JXRt1OnW6G8sObd6p8n3v5fbTWQ7vgcuVNkCYXBWhxeGHvmG4ahd7VR_c_YnBpfDXjv5x_fflfzUCI9Um01TLRt0G_x6jPThN6drwTUHQGM88lsdxx3h28ef3fxrZTJUAzk-lKImn84ENuACf6Rh-Z8TEvyjDa1btfQzIONnSOGJJBiW52eQKmmZqfFgZpBqBZRd-0eRuK80h0kTNwgUJSe5xWDJf8D1tkfaeNCxM8I34QVY826nz58MRD3kmiQSnCht8QQdN92atO89h_uoyu8v8bMnvChVpn_KGGRNbGy99SGdulBcY5I8BquYMa4VBJsZ0vO5wrriIPmVS9Z0IkHQqER5fbWo7t95HLZmhzJhmFRsDylXuWHq22jBjIqUvutGRU_TYKivQ3mEmiaQbFZtO_xHC0V-omd49UTeRbWd2V1UbNhMTbMy9f8fpPwO_PvjHp3ENEMGFBjoNTbR4X2lWvlvF4qOsIE0F45dFZch-2SSkKX3jRH75BcnLVLZ1vYeUjYZM16JXV-2L6n8yWh7vDmbqjm_4bG70gYmIrAY_6Cd21IQvhZ9Qf5S48Es9WUv7P5xz9sFhEjSe7o9HUBXFS9XfjVnJnX5B01dfRd4G-FKDH9Sq9e3EOKvdXII-ibZbuKrth_etQWSWjAyjMA=w915-h428-no)

Four Features New in Today’s Clouds
1. **Massive Scale**
- Facebook servers[GigaOM, 2012]:
	- 30K in 2009 -> 60K in 2010 -> 180K in 2012
- Microsoft[NYTimes, 2008]:
	- 150K machines
	- Growth rate of 10K per month
	- 80K total running Bing
- Yahoo![2009]:
	- 100K
	- Split into clusters of 4000
- AWS EC2[Randy Bias, 2009]
	- 40,000 machines
	- 8 cores/machine
- eBay[2012]: 50K machines
- HP[2012]: 380K in 180 DCs
- Google: A lot

2. **On-demand access**: Pay-as-you-go, no upfront commitment
- Anyone can access it
3. Data-intensive Nature: What was MBs has now become TBs, PBs, and XBs.
- Daily logs, forensics, Web data, etc.
- Humans have data numbness: Wikipedia (large) compress is only about 10GB!
4. New Cloud Programming Paradigms: MapReduce/Hadoop, NoSQL/Cassandra/MongoDB and many others
- High in accessibility and ease of programmability
- Lots of open-source


#### 1.5. Introduction to Clouds: New Aspects of Clouds
**On-Demand Access: *AAS Classification**
- On-demand: renting a cab vs (previously) renting a car, or buying one. E.g.:
	- AWS Elastic Compute Cloud(EC2): a few cents to a few $ per CPU hour
	- AWS Simple Storage Servie (S3): a few cents to a few & per GB-month
- HaaS: Hardware as a Service
	- You get access to barebones hardware machines, do whatever you want with them, Ex: your own cluster
	- Not always a good idea because of security risks
- IaaS: Infrastructure as a Service
	- You get access to flexible computing and storage infrastructure. Virtualization is one way of achieving this (what’s another way, e.g., using Linux). Often said to subsume HaaS.
	- Ex: Amazon Web Service (AWS: EC2 and S3), Eucalyptus, Rightscale, Microsoft Azure.
- PaaS: Platform as a Service
	- You get access to flexible computing and storage infrastructure, coupled with a software platform(often tightly)
	- Ex: Google’s AppEngine (Python, Java, Go)
- SaaS: Software as a Service
	- You get access to software services, when you need them. Often said to subsume SOA (Service Oriented Architectures)
	- Ex: Google docs, MS Office on demand

**Data-Intensive Computing**
- Computation-Intensive Computing
	- Example areas: MPI-based, High-performance computing, Grids
	- Typically run on supercomputers(e.g., NCSA Blue Waters)
- Data-Intensive
	- Typically store data at datacenters
	- Use compute nodes nearby
	- Compute nodes run computation services
- In data-intensive computing, the focus shifts from computation to the data: CPU utilization no longer the most important resource metric, instead I/O is (disk and/or network)

**New Cloud Programming Paradigms**
- Easy to write and run highly parallel programs in new programming paradigms:
	- Google: MapReduce and Sawzall
	- Amazon: Elastic MapReduce service(pay-as-you-go)
	- Google(MapReduce)
		- Indexing: a chain of 24MapReduce jobs
		- ~200K jobs processing 50PB/month (in 2006)
- Yahoo!(Hadoop + Pig)
	- WebMap: chain of 100 MapReduce jobs
	- 280TB of data, 2500 nodes, 73 hours
- Facebook(Hadoop + Hive)
	- ~300TB total, adding 2TB/day(in 2008)
	- 3K jobs processing 55TB/day
- Similar numbers from other companies, e.g., Yieldex, harmony.com, etc.
- NoSQL: MySQL is an industry standard, but Cassandra is 2400 times faster!

#### 1.6. Introduction to Clouds: Economics of Clouds
- Two Categories of Clouds
	- Private clouds are accessible only to company employees
	- Public clouds provide service to any paying customer
- Singe Site Cloud: To Outsource or Own?
	- Medium-sized organization: wishes to run a service for M months
		- Service requires 128 servers(1024 cores) and 524 TB
		- Same as UIUC CCT cloud site
- `Outsource` (e.g., via AWS): monthly cost
	- S3 costs: $0.12 per GB month. EC2 costs: $0.10 per CPU hour (costs from 2009)
	- Storage = $0.12 x 524 x 1000 = $62 K
	- Total = Storage + CPUs = $62K + $0.10 x 1024 x 24 x 30 = $136 K
- `Own`: monthly cost
	- Storage ~ $349 K / M
	- Total ~ $1555K / M + 7.5K(includes 1 sysadmin / 100 nodes)
		- Using 0.45:0.4:0.15 split for hardware:power:network and 3 year life time of hardware

- Breakdown analysis: more preferable to own if:
	- $349 K / M < $62 K (storage)
	- $1555K / M + 7.5 K < $136K (overall)

- Break even points
	- M > 5.55 months (storage)
	- M > 12 months (overall)

- As a result
	- Startups use clouds a lot
	- Cloud providers benefit monetarily most from storage

- Summary
	- Clouds build on many previous generations of distributed systems
	- Especially the timesharing and data processing industry of the 1960-70s.
	- Need to identify unique aspects of a problem to classify it as a new cloud computing problem
		- Scale, On-demand access, data-intensive, new programming
	- Otherwise, the solutions to your problem may already exist!

### 2. Clouds are Distributed Systems
#### 2.1. A cloud is a Distributed System
- A cloud consists of
	- Hundreds to thousands of machines in a datacenter (server side)
	- Thousands to millions of machines accessing these services (client side)
- Servers communicate amongst one another -> Distributed System
- Clients communicate with servers -> Also a distributed system!
- Clients also communicate with each other
	- In peer-to-peer systems like BitTorrent
	- Also a distributed system!

**Four Features of Clouds = All Distributed Systems Features!**
1. Massive Scale: many servers
2. On-demand nature: access (multiple) servers anywhere
3. Data-Intensive Nature: lots of data => need a cluster (multiple machines) to store
4. New Cloud Programming Paradigms: Hadoop/Mapreduce, NoSQL all need clusters

**Cloud = A Fancy Word for a Distributed System**
- A “cloud” is the latest nickname for a distributed system
- Previous nicknames for “distributed system” have included
	- Peer-to-peer systems
	- Grids
	- Clusters
	- Timeshared computers (Data Processing Industry)
- Nicknames come and go, but the `core concepts` underlying distributed systems stay the same
	- And they are used decide after decade
		- E.g., Lamppost Timestamps were invented in the 1970s, and they are used in almost all distributed/cloud systems today
	- This course is about these distributed systems concepts
- A few years from now, there may be a new nickname for distributed systems
	- The core concepts will remain the same, and they will continue to be used in real systems

#### 2.2. What is a Distributed System?
*A distributed system is a collection of entities, each of which is `autonomous`, `programmable`, `asynchronous` and `failure-prone`, and which communicate through an `unreliable` communication medium*.

Distributed System = Many Processes Sending and Receiving Messages through Unreliable Communication Network

A range of interesting problems for distributed system designers
- P2P systems [Gnutella, Kazaa, BitTorrent]
- Cloud Infrastructures [AWS, Azure, Google Cloud]
- Cloud Storage [Key-value stores, NoSQL, Cassandra]
- Cloud Programming [MapReduce, Storm, Pregel]
- Coordination [Paxos, Leader Election, Snapshots]
- Managing Many Clients and Servers Concurrently [Concurrency Control, Replication Control]
- (and many more that you’ll see in this course!)

Challenges in solving these problems
- **Failure**: no longer the exception, but rather a norm
- **Scalability**: 1000s of machines, Terabytes of data
- **Asynchrony**: clock skew and clock drift
- **Concurrency**: 1000s of machines interacting with each other accessing the same data


### 3. MapReduce
#### 3.1. MapReduce Paradigm
- Terms are borrowed from Functional Language(e.g., Lisp)
- Sample Application: `Wordcout`
- Map:
	-  Parallelly Process a large number of individual records to generate intermediate key/value pairs.

![Map Task](https://lh3.googleusercontent.com/DfWUkmMQ79PNd6tZDsgblL-iHF3qVFJr1hKI5yBDiGP_1274BtvxE8RhZsR9oGrDe93rNP_fR2YexJtw6iWb4ZlX6DVNBoiqPmZNVrNa6WLYGNnDZuRBXDHX8bqtDdqJrJYD0j0IdHiDwZNDd9rV7fscbWLaaVg75RSDJSb9c5uTlwDrqsV-Zod4JALW5ePcGKvpthf_paxOeK9Ahk6-d-IZma2SELKmSBp_5H1c64WU_dI-D91x1ddBUE7tl36ZlrYyKOp-u-PQkIF3wWszZEq7tls7RKaJ0CONDsf0s9uuD4rikXoTqPECkelROgRat3Ott1iT0Q-F4blAuHkR67CrsnUmqcdhSQ0xB_u2UNXGLpwPmAB_5rHDlwq1hJDel4GeoMNcg00e2Z_iNSMMBer11Rxw5Ho5qPn2LYA_4t2etHNMvUgcDI0CZ6ZjUYeFFxTP5gDi4nJ78yPLlQD8KpsHtJffIU7pcRPJlRqNtdix26rBj4vpOhtsdUvo5X6yzUj_RZbYfc2CxPFX3Wxdx9GjIYvIrNCaRrXY37FEUsPdAN6mKr-Z3mJK1gv7_lP2NdHy_ICQwZPA_EkxdGq39tFied4C6gRn51ijaek0CP5xO-16rjTufMNXYky8vH8117P4cWJ9YbtwbyBeCFvFaeqb5oDiy_Ei2lANSPsbMQ=w515-h221-no)

![Two Map Tasks](https://lh3.googleusercontent.com/Zzn05SvIEdGVi_2XrtRDz5y_znvh2fBbBUpif2gDg3-OiAW1f2kEBEgOBXon2j5zfYx44BIzMA-0-cfsQPQlBObbaguZp5HZnC5prLDDZ06U-JS-9kXT458I0SjNdRW_dvlTh8aV5Enlk1THmR9lyUlFcMomAL4UWhMiBVH9JdHvxYaPGSWkN2ZUH24NJXAf0ehDVtSTggcI_igtR9zJ2q4ktj5W12BxmTf6KAvpP8P37xKnO6NdubZDQbjQ7s5izpmXOMU3N8MY1BN3R6HEv6HkLW2Pw9CNhCDfQg21ETyPTTKMMZW5jEw6l_J1-K1U5OiW6ihns6zBSVogPslfkks2eVt68HegruksFs_0OUw6ZIYJ0ifwAF3Qegf4pMJgVduETukuFSv9yiVVskNR4QXDwQWfyyqsqQXIcyQ9QU2eoAHOUdbY6_dfa28oYz50XnnGsq74meNo7X0JovLI0t5bHya1Wo9gGuscMR2WBNdyvwS3zYMNOtBjoofuT4sVAI0-s1_BAlGlmoDrabZhMEIdV69QEVcLdA_-pGC1QwLRdw_T9YhMTNEUOeKnZ3MYzZQxGjiJY6wYHu1HUg_Y7ukj3mBZKW_xuJxlYtsClRR89WF6GPwwUX_-wtA1rq_2jc2APmzoMQ0rcFpP76oqv03kvyKe44Z42vC5wcQXzg=w550-h230-no)

![Many Map Tasks](https://lh3.googleusercontent.com/oIFVIxsAc2O8FUBhHcM53R_CbBjDvh_SuUJ2G_w3UGK1Jw-7vs6GnDlSRzpfeDt-kIplYHviiWvk19FtIjbTUBRQVd0MNkQsk-uw_OwyFPNFHrn1LrsTaQtNSqaRJLj4WE2jWrXiesYd3JHdZp3ZuKFYammv2KnCFgtD2VpA_TyrqmsT76-x9qZ5RlkGDJesQABTCgTzxQx0vCkaBtvl2dBb8ReNI9BeU0f1XUNaadXmYXUxU6x8cxpQGPPXJGy9CG1IXvI8a3CJpaqy9hxqNwvK-qTK0c5WONNF7BVzkOwHxFZvq4qBC8V5gm9gxxmyKBMZoeeRjC-vuYkF77nuU30-0B9PfNSz92i1xaNz0QzcT6sipacAzFmyXdxz4dBdLHriaiX8pZ3VSsHrIBQj8YxRcUWgdxSeAcnfCFyCs5Sjo7WfodDSFoz_Ow_0f7e2NurgmCQUP2jFk7wIRrqUls8cNsFcAZnfxrpnLplgnk-97U7kWK9IThQKvav8ugcFLcgReslCD0dZTZZQjHm3BxcQG9Lg0tcnMGGC2bp3cPG-KX85UlCs0rU5hQZCh9wykDwG80WDTcZb9tUVKK4_o_NORSZR7FFA-mrsz9sW5xjxMWcWLbjmZnT3ds29fYSyECWpgnupHTKQoR6BQ21lQHFnjZnzHewc6tFn62_YXA=w554-h211-no)

- Reduce:
	- Processes and merges all intermediate values associated per key
	- Each key assigned to one Reduce
	- Parallelly Processes and merges all intermediate values by partitioning keys
	- Popular: Hash partitioning, i.e., key is assigned to reduce #= hash(key)% number of reduce servers

![Reduce Task](https://lh3.googleusercontent.com/mWsFpursi24LyePN_HIZ7LGSgLhYgwsDqyFV1-wVtAwszGvPCGs8f-oDjISRGMEqP_kzxM9SmTcB2wiC-gp5ThjbzuKi1a-kGZ5IBUogIMqfXUKqaRtd3XJOs8unXx10PoFCOGVhP4xgFtSqJ5xg5oGQl7cazW_Zn7sUhhnMoDK90sLKcE_ldYaXI9n_cIC3YxECaXVmRwWdPsro1m5ntflm0vth9-XnO8ILIUn-YgeC_jU1b9ucNY9t2pZAy6TpgTaf6ZU3y7LXpEyeJEtHVzYegqjfORaRVlri1_t9OL1O3Aft8AIgSK9w6cLcoQJAtiW6zizkke8OXkHrYuP-BDaJzzdiB_-NlNxZeGsHoIsGLkobJkLyLvJv6W9NQFdNTD3RN4dVpE0hcfDKWi1ofFo9FepvX_I0wZ6Ko0YZa8s8hpUDvJaqMiDKNGYJ1t_mmxwJyybSPBcKlnfIBENUjT2EUkZf27TH0qMHVoZfIWhpGSyz9ihN0pa6CYuEBIwjpMhDZY95vfnd_Qb-geNKFXkgeXvS5BcOK3Taw8Ah_Jy62ylqbWQ81gM726xQboMnuXaYW1ffGqRMB-wKkn9FIPWUXzurLfiwzOBHRaWLKLTvZQ0KaF6f9S9gLb3epaUbNQYzs7qXz8vQi2UBw_pGhVzLrx4ehrTX_M5nNC7zrA=w493-h214-no)

![Two Reduce Tasks](https://lh3.googleusercontent.com/YO_-BhfPsNjjotY8XInGVzHyqEt-r5n4wIuERO2L4eX1D-5cKBJd1A0Uw-XDIh7PRBqwijyQXcN0gj8Y69Bdkh1RXfNTjL58qgez1yCakVbr6Im-1dhHHWK-ooI5HPflgKi2JCULU7RHRFSpZzzzEGLnFQFxck9Gs57-s-ClWQbwTXUIDcbtmoVY3eG28fISvvLYu2H0Ix3zYudDOqaeoZW9T8ulLu8UDnv6QBFfx8qdKx_9cKqEdzjyiWyJ8Ta6JdbEVLiXeSSv2AjpDQBbttNrrDVr4UYZW-J26wX18UrwIXLVR-8Kze0Co1uDYSf4ty7hJ3NbSafsujDNLx4i8xJFprRzXAZGmfjloC9TOsSgKJkcyMnAISLUQZR05sOcrEimTXcsmaGjykh-j05ifeKFPxNYYr_DXVdo0PkfqHoM8KnqVEFV85LelPJJMUlYHre-FO7A416WdYF2QmwcggA1bouufP-mIVmuFAUKeGLdevIw8ZnDb9KmRL03wQPeoIhA1atABp27YBB4i-BHzF8MQkrp9CK6tGFkuBiK41z4JEKPgL_j6lQZ0delBfTGFDHfCNWLNg0l-yYkwn8s2D6JOUQE9IR1Z2UEFxmBX3cfEfcu7LVLGoaiuZ0kaS8_RHSLbCVGuccUKnWDCB63iasqFvcHcc31_rrGLHR05Q=w526-h155-no)


#### 3.2. MapReduce Examples
Distributed Grep
- Input: large set of files
- Output: lines that match pattern
- Map: Emits a line if it matches the supplied pattern
- Reduce: Copies the intermediate data to output

Reverse Web-Link Graph
- Input: Web graph: tuples(a, b) where (page a -> pageb)
- Output: For each page list of pages that link to it
- Map: process web log and for each input <source, target>, it outputs <target, source>
- Reduce: emits <target, list<source>>

Count of URL access frequency
- Input: Log of accessed URLs, e.g., from proxy server
- Output: For each URL, % of total accesses for that URL
- Map: Process web log and outputs <URL, 1>
- Multiple Reducers : Emits [URL, URL_count]
(So far, like Wordcount. But still need %)
- Chain another MapReduce job after above one
- Map: Process <URL, URL_count> and outputs <1, (<URL, URL_count>)>
- 1 Reducer: Sums up URL_count’s to calculate overall_count.
	- Emits multiple <URL, URL_count/overall_count>

Sort
Map task’s output is sorted (e.g., quicksort)
Reduce task’s input is sorted (e.g., mergesort)
- Input: Series of (key, value) pairs
- Output: Sorted <value>s
- Map: <key, value> -> <value, _> (identity)
- Reducer: <key, value> -> <key, value> (identity)
- Partitioning function - partition keys across reducers based on ranges
	- Take data distribution into account to balance reducer tasks

#### 3.3. MapReduce Scheduling
Externally: For user
- Write a Map program (short), write a Reduce program(short)
- Submit job, wait for result
- Need to know nothing about parallel/distributed programming!

Internally: For the Paradigm and Scheduler
- Parallelize Map
- Transfer data from Map to Reduce
- Parallelize Reduce
- Implement Storage for Map input, Map output, Reduce input, and Reduce output

(Ensure that no Reduce starts before all Maps are finished. That is, ensure the ***barrier*** between the Map phase and Reduce phase)

For the cloud:
- Parallelize Map: easy! each map task is independent of the other!
	- All Map output records with same key assigned to same Reduce
- Transfer data from Map to Reduce
	- All Map output records with same key assigned to same Reduce task
	- Use partitioning function, e.g., hash(key) % number of reducers
- Parallelize Reduce: easy! each reduce task is independent of the other!
- Implement Storage for Map input, Map output, Reduce input, and Reduce output.
	- Map input: from distributed file system
	- Map output: to local disk (at Map node); uses local file system
	- Reduce input: from (multiple) remote disks; uses local file systems
	- Reduce output: to distributed file system
* local file system = Linux FS, etc.
* distributed file system = GFS (Google File System), HDFS (Hadoop Distributed File System)


The YARN Scheduler
- Used in Hadoop 2.x +
- YARN = Yet Another Resource Negotiator
- Treats each server as a collection of *containers*
	- Container = some CPU + some memory
- Has 3 main components
	- Global Resource Manager (RM)
		- Scheduling
	- Pre-server Node Manager(NM)
		- Daemon and server-specific functions
	- Per-application (job) Application Master (AM)
		- Container negotiation with RM and NMs
		- Detecting task failures of that job

![How a Job Gets a Container](https://lh3.googleusercontent.com/_ggVQZTdJbYM9gypXn9lHrTL8ZuPSZc0m8XYAlwrZjwWzXjwXw3A2cfV11Zd3bFFHukHOyb2smo48yF6GLUBMB0O8FBIjJhvK4ewck6JXqj4t-7YtNPDwvYIygzwk_disv1n_cG0P-W8BmIk7Tl0R0nzrM6noBYVzV35P5MQ1LV_Wrml1ZUGnCWjs2Q0j-AZDSDEAGqEJMqj5jBQ8oQH0g0pdZGtZ_HrIt4zUxiUIwAJa4Hy2j78zydM_e6WB3bELNWwmYlU2EXqMPRaWz8luLejzmXoDB2wOFuTZD0M3-fgdMijGeHXBQWAc61oA1YlquU4ZHGruG9BLSRwYvdAufhJ0_x6BjTpsMcikGQGpUO8keVgGoEfxC6AssRIEp4wwEaqWTWk-OqKLuvuXzSXx4nhHMPYGYPHbR7WNtuY6ouEdBUWjOkD7h4xXJUVamO0tdCPhxdqgZOBIxsqPpEeqdoRE9N10_wx_7P3m8iSO3I7NK0od5IhYYrbUOOdsslQsZrDoWgB2se_cZywbKH6_UhOsb4EZKTxPOalb9l5AD0S3-9cs5wdR-i6trIRgbwWnIjU2MNFXcl4UBvd13bvkfvGMZk2aduRwmJJAnZk9gxNUgLSnA4vsN_9yreclNl8Ur2rp9XfqKEz7PkUX7I33LpVKd3de3FuD9p9ZbMNzg=w1237-h765-no)

#### 3.4. MapReduce Fault-Tolerance
Fault Tolerance
- Server Failure
	- NM heartbeats to RM
		- If server fails, RM lets all affected Ams know, and Ams take action.
	- NM keeps track of each task running at its server
		- If task fails while in-progress, mark the task as idle and restart it
	- AM heartbeats to RM
		- On failure, RM restarts AM, which then syncs up with its running tasks
- RM Failure
	- Use old checkpoints and bring up secondary RM
- Heartbeats also used to piggyback container requests

Stragglers (slow nodes)
- The slowest machine slows the entire job down (why?)
- Due to Bad Disk, Network Bandwidth, CPU, or Memory
- Keep track of “progress” of each task (%done)
- Perform backup (replicated) execution of straggler task: task considered done when first replica completed. Called `Speculative Execution`.

Locality
- Since cloud has hierarchical topology (e.g., racks)
- GFS/HDFS stores 3 replicas of each of chins (e.g., 64 MB in size)
	- Maybe on different racks, e.g., 2 on a rack, 1 on a different rack
	- Mapreduce attempts to schedule a map task on
		- a machine that contains a replica of corresponding input data, or failing that.
		- on the same rack as a machine containing the input, or failing that.
		- Anywhere

Summary
- Mapreduce uses parallelization + aggregation to schedule applications across clusters
- Need to deal with failure
- Plenty of ongoing research work in scheduling and fault-tolerance for Mapreduce and Hadoop
