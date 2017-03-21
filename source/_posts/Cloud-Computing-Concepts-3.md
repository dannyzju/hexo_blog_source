---
title: P2P Systems
toc: true
categories: tech
tags:
- 学习笔记
- tech
- P2P Systems
- Cloud Computing Concepts
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

### Gnutella
#### Gnutella
- Eliminate the servers
- Client machines search and retrieve amongst themselves
- Clients act as servers too, called **servants**
- [03/2000] release by AOL, immediately withdrawn, but 88K users by 03/2003
- Original design underwent several modifications.

![Gnutella](https://lh3.googleusercontent.com/E-oSzLcIcVVpqK35ox8bgJQZU3zjNy5KjII_RJTR8BgxYFTE6AfNrEUxLIOt8neXcd7nC8gqq3Rk4oBwwUlfFk7QMN9pM1dVQ2lv47IPfT41vcHh7K_TWt0taRgK8Akst4AMdXAG_jUUrUJmT1Xh4dKpkSzi9CrDf2rM_cAh9QY69bOe_GUyOKRLJbie5t6rgx3GlRSmbdctSZk9zxiYJlN1xuXVWvIAFjZBhu4iTbkfwiLnxcKK2YaZfuVoA_ZesWiH013IY1qD4LGHYN6wH9i7IgfDgx9nh53NZeO3YD4wttMlV29t2B6hQdkzkU6Jq33TPsT4IuUwEep2iUQdPl0RNrOBVxe3ktsbetRIFBfI8hxcLV40Rg-vftCKL44C8fyxkJJ-ZsJaG_fPodNpcTujRq8i7EukE9J6qpk3i8-3ClYTuTWNbT0XMVEz14hZXzO0UDVdm74ukSXmCjTW-EP2ZnrsMFWTzNFP04Z9auPnSN0af2ziNZh2YOwHBEx28VI0jwImzSwU6HAv_OxVL9LBfKQbSzwf6Q8eaNuay9B8aabfgWuIsWC-FRLG8_9GXabh4RuSWSZibvsbwcKxTOEISit4CbGDxTi2xSbF-UigZyS6dl8tsdiGCaP4j0QMBockuc1cp2CA2qZJjxbVfAJCkTdRyC16ljWZo07dEA=w1136-h737-no)

#### Gnutella Search
- Gnutella routes different messages within the overlay graph
- Gnutella protocol has 5 main message types
	- `Query` (Search)
	- `QueryHit` (response to query)
	- `Ping` (to probe network for other peers)
	- `Pong` (reply to pong, contains address of another peer)
	- `Push` (used to initiate file transfer)
- We’ll go into the message structure and protocol now
	- All fields except IP address are in little-endian format
	- Ox12345678 stored as 0x78 in lowest address byte, then 0x56 in next higher address, and so on.

![Gnutella Message Header Format](https://lh3.googleusercontent.com/LRSsbshjeCTQPD269zVh2vqZ3BLohu1StylZ35qPyTGHMMh2loNAMf2439lKocqGJ9fcGvhA42tu7abahe5miRGhJJAdcF4qsftmPYkzEHg6tbl3kRuhdVzQi3MobJTvYxiClf2Kp9IkaaW_LN37i-Yb-r9kEASk2GHHJM78xIzSCH402nX17YYXamRFn9HJAyzPygXwjqpT8rGNzJM17S9kismQI9lMzrVyJ4C_6ENPDzvzOLxz2FKNWNLWIPccrsy_clqIf8i6O04ljmvcJy7KfFEy_QCvFam10h6KNKUPflBIb7JXFol-ELG9QSUSai87TkpM2hZ2cw04pdq-jdj-iGbPNyDOTkTeQqi4Q3tBbeM8_sBGtbQXGPdeQuItodGCRRs87mie-HVSw0vn_KvFqqwHZ8PzecYHof24PY1RpgxawCsm-H7szc4Wp5EoxM5vtbYzhQwmyAniq6ruJlhzCfcAz4qu_b7Hb7au3jXl7L-9H-hj-V3okA1bcUZUMctO9LSGO95Y79GngeSodywmp60HmyNrWMRdoQjF-FDfnA5dp6jzWIPDmb75DVBc3cuv7kCmVInR72MbLodURPem3ryJCKQfg16ZnyXprA5tpM9x_lVr0MSC0p0VxzQbwpl5ZaxSeRLLa_GqoOsTb6eAgsH3PhrDhdErsiCf-g=w1199-h545-no)

![Payload Format in Gnutella Query Message](https://lh3.googleusercontent.com/t5DT0ws6785AzmBtbTxfZ_Evm5Me8GehCp8A64fsfxg6agC2y1W1tSUjt7z7pf5YGsD4fjGvMfvHuwtD_1pJ2-moc3w8eWm5j43_eiOZDvlKfQoNrHx3aTfZbCLFhSEBAbi5U7MHinRGill2qS1KERb7dXEW0DfAOCKvcEPrlyj1-uGGazcHAO4sKTI-0Ns_p7Qz9NGmIVs5IKqAMLCFPlX6btZsSdyoJ0jgLiojFBiugr12W9YOvygzHjO4jJL-C-SEOWN_Diat1Z1FOl8K1A1qpDOmAxXIKTpVvlH8Xy3aF7onZ7QCIBGt51ysVG1iXS44UffoB5dTAJRwkLd5SLPv8f6Sv6k6qJT21LYdCcZGejxf6U1JflMgEYURDllqp24GjmCvOWz5u_7Fm_i8IWUg_Sx9D07kT3XN-gyYkjtJcCvRKnCDp328Zyj_mHjnH8CJ2x3C7bx7Osufp0AQSku5Le9EdHLqFcQ4GYHyWAHqC21MOVuG82zgk0qg3ul8qBwol2xu9LczhN5qqwawtVSpT2FhzwT0yyD8kKsKePS8gzVw1ULH_Nrb6_AqOt6gxypYVYLuUHgEH5U7Fe8VT9SKNCFGQYRv67UTjD3OOm8Cn0iLYm5_-vaUmVopnUR2jRo8nSbn3q3xyzFWhPBOF7z7LFDrh2N1x5TulxPTAA=w1131-h610-no)

![Query](https://lh3.googleusercontent.com/WL2uOCLMOsYsv9N9x5O_nQbFWiDWARQ0OzzXMlKXJoUybULNqltEP8F_Hy3WNZsx-Zh_S8D4xQKKNtDnXZJUlY3uMoJYrvA59qW-tLcuhsTe_bUd2c4otsAojchZwAzoMORqjWQGHLbAwKMVnJ8RZ2oh3knh8xU7m83vES3HpDs7O_MLn2QDmcsn7MbJri3-SyjUq1myzz9Mhd5AB_bqMIaKMc5iMvn_LnUclVdXcAUyKLrrc9ZwODrfaS5Cieh9Owhgoq8tt3vdwkB7bqMGudIsx4eZDIoc20grYpA1XruiDIxS3fpWEKw7xzTqd7N7SgMlfY3ANhL1eAjkIFgVLVqT5mZTP2PuT3ndbyQ6ILKhQOBxDfXLYCTTR0znYEurJLb5fJwQndyTO7swvufZQ1GSeXL7EwK52rbHDb4X0yVhFKLqOYyctQXlSnCXkGPhMGWCZ6_xXWLC1mSzXPrR_02wpexhLHWfuE7sCDmsweKOSA1JZ6JVJUoEjPtBql25XXPJU9U7Mlc2NaLKQ8LvmdKQvus3k_D2h1Gwu1SShBLNfFZotIWFKzTZuez2ZSxAn055WCeoWmvNRMgQ8CckFQZ2OqckljVtIEdwpZVxY3_3Ip5CPYiTuTwpluLTr7Pr_9ERAFUyCXixr472GFJt1bgTXfQeRmREY_jTpIeQGQ=w1161-h733-no)

![Payload Format in Gnutella QueryHit Message](https://lh3.googleusercontent.com/c911jczEQAMunfIYehuINIsTa2wHqstosXDE_dWzalq_mnBlouQ9qixr_1vhIsk6fjdP1IPsW3BYrKYjmf5WyWS8uWoOD-eWo6oBD4DhHpcWeXFergI4BEylp7LBHLZvula6gw955_wnTWiPmuRvHQ6EBR_1v_-4J8cGUXUwFd5veVtrt7n0AUza4BcaroG9hMUVg-u7Yt4LHorWy9Mkyts5NGeEDF6R8zIvKFqY4Q7-uyzrauU5B4KCWNEFWMwhE58-zRIdLibhlSzlnYmMjo9tbEtUaNdzWmsW51tTxZXFdFL7QPGWXZPMUf8QZ2M46YXR1l5giKb6ey0HH78lcyAiwG3O31gvzgUIRNGyFWVtL_7q9_Ibx1vO1y86ZGhstrbDmcc8g4pUvw16t6Oz6ZWD7s4mvgfljLhBAqIfgnZ5sOHAvBiy-EmWnruRNHQ9sPqGx_0WBxScZwPnNdrfnkNgxGvopOAD-oEf98vFSi5cRSMww5mBVYKsOX5DbbBu5roU0GCzVzcz-bw8XbwMNVzmAGieCGFe8KqRJCVZhILZC2XTNJxD771VApTINguhNOROxcISHuU58IQO7vDzVWwar4ndBpboUbsIOyR3UT9T4279_m3n-xcwkoZtg3CB9qvTqABj-CKvRACcHHp8grvzV0EgeW03iaNwDXcyDA=w1199-h593-no)

![QueryHit](https://lh3.googleusercontent.com/Yea7x5cEVn3Hz1emPWPwXXlG_FXayMCiUBcSLKNKfcug4uYQytFUCW4blH_ihu7ICna1lqlFQw8uw3bNf4obpaD78M4TJNy2V5l460Cepdr65VqWflZTgZ5yY05KgIRdunxSAvOUcnr89DsreJ2Ae9LhBH3H_7zjsRpej1NUIYKBSptY5MLkyQRGzI4ZWtnzBudtspCZR9tZyVfJUC-bHTfEg23uZqo8YZEQ3VIAs4SL679Y_UJefozibd54UPy6FoXQfCC23Lc2RN9sFONBzXVIsCcF3jBCa217rkeHkTGAKXV0bsnhsC6Sc0tRLd4LZwy-abX_k9Tee0Og2-HCia5QI3IMIlMO8vLhnreQbkix8XB_0iz-eM558g4aMLHdYyee2wNYOAvMqj-73ZMBwZQTLvamMOkgJXLDXY2FOsXu5QtMtRSDKN7AClIW_mPDm0dl_CCOv8HSKJgmykui-GGVeINBUHyxXM-fTdf6Iv6_-2PbIlC6_Q9PgCwSPxkLXG3xKQNZTkZ2X1nh4_9m4PB5eWeokVzF3Id0cfLiy2WXJ5oV37NXFrpMqTLwkdIXBFbhKMdJU7Uj1FhBJm9Kx01RXXmhtpmaAzUbAquBURHtR1HRF8brlTyhTuZFPRDN722uwXvs44TyW8faBN51LoR9JguppmI_JRky9_UjmQ=w1170-h734-no)

#### Avoiding Excessive Traffic
- To avoid duplicate transmissions, each peer maintains a list of recently received messages
- Query forwarded to all neighbors except peer from which received
- Each Query (identified by DescriptorID) forwarded only once
- QueryHit routed back only to peer from which Query received with same DescriptorID
- For flooded messages, duplicates with same DescriptorID and Payload descriptor are dropped
- QueryHit with DescriptorID for which Query not seen is dropped

#### After Receiving QueryHit Messages
- Requestor chooses “best” QueryHit responder
	- Initiates HTTP request directly to responder’s ip + port
		- GET: get/<File Index>/<File Name>/HTTP/1.0
		- Connection: Keep-Alive
		- Range: bytes=0
		- User-Agent: Gnutella

- Responder then replies with file packets after this message:
	- HTTP 200 OK
	- Server: Gnutella
	- Content-type: application/binary
	- Content-length: 1024

- HTTP is the file transfer protocol. Why?
	- Because it’s standard, well-debugged, and widely used.

- Why the “range” field in the GET request?
	- To support partial file transfers

- What if responder is behind firewall that disallows incoming connections?

#### Dealing With Firewalls — Push
![Dealing With Firewalls](https://lh3.googleusercontent.com/dmLEy0BDI4v-jvB5RwPOcfI-FPtwOKTPNekn5IuiHzmmeNV7F-BgEROc5lmKAcRafXj9Ke_HAiQ8C1jSAj9N-UzVNN5ynX1o8863DYTgwlqXdVrP2-zHhVUVm9CiRyKQKbwukRucefS1WAuyIhReR07tfhO8_QTSPY4YMkkkOAo4MGtnfjR3C_EuCZmMdUmpFPQX78Yq2RUVKdUXlXBjUkL64JJ0D5Vie0XIhxe8B-QBO4VYKoHPSTIAqnt1SUFyqgpmUoN73J8qXdLtC5fBZ5t43Dc3nj2zRP9Ho8cVTga_BO3p_bw1YFkjAIzAE25njMQWfLJGM8AVXb-O1vlHBd7ibDy8NPbJb-b8yVDOMk6KnwIckhi9_rqdTVk5Kx6fd9OGbX-y_gEWBlkwuLKRSZfXEK2TNYAnRoTSWQj05Gi4LHT_AIHtI7e_rgptjlKV-O5Dx0LtXDZzRudG2YC8DyeM_epis5pmiCCAv5YpQkjQRUb1ctHWIjVAQ4kqYnEZq5xY7_lSAs6DCPiPUL1Ul1KaDP9-oiyr-htcSESTF9FKKGSfK9N1jOEqk40EdxEaasKKaIBywaUOVLGUWimcMYi7hxyDJWM-jDIWiwHR4ca7MxNA04WS8TQ7MspttqP2fcKL9k_S79q27S-D804EoVNl35-5nz8ZYonpgd4PDg=w1199-h698-no)

![Push](https://lh3.googleusercontent.com/fl2Y1TR9pGUndWM2tcK4tBGHTipAP45fsusvV51v2yIvbOC4ozmDHO8MZNzOCQnJfYF9qzLRD6aRFWnbXVko20lsfUHbsUSZEFYgeYDjPnUAz1VhMf4pRewMvkpGgEysvpBOvYojmPSq-CfvMMxGC2e78lvTyt99_aDxJiZ5JIE2iSl15HHhaYUfS2tcjOrsUsasmcvK2xqOjQw1rn70yXu5Ut_brqHNnqE_VtPOZZARyVAIM-nxl1eQTe5nfn7OMMQsEJpNzXGhWXcA4Z8SROeXoQQKZ1ZYjD21ku15iiALdebmuGoGDOoQl8moMhH6tETfpYXN-VbZCZgm27CT6ZSVEk1uHb4N3wy-tbmYZk6hqjZoAY_8THjg39dqsKrp6tUIBHT-KlbHtqaDijz3bzD4XfpNOV5amMa3ZkBBki8TNC5k2SMSXiT9EHIrr4fsKM_nKS5p_Tn3U51e9E30G6P0IvVDNCJgryF0eXXPR6X1uEEKngkQ0-j8IVXRdqJCxdbGdQh5DVL7tjhBWA-DQaknLj4DZSVGSPh9ryMjUta6fu363_nki8C7b1V9h1fm_RfKslrVz3ucxBxE4crJImuzAuC7QPcpr62vp6a2EJWRbTpOKOwjKwS5a1I3h7V5t_T8kuMj-deQ5KYTeaqSTZd9QlCsYVpRUrxhMv7moQ=w695-h459-no)
- Responder then sends GET to responder (as before) and file is transferred as explained earlier
- What if requestor is behind firewall too?
	- Gnutella gives up
	- Can you think of an alternative solution?

#### Ping-Pong
![Ping-Pong](https://lh3.googleusercontent.com/y0GASC1IUZFxTcmX0ax2rM6YZ4uKFeBwiVOxDQp8GA4BQUugzv2lanoUKklDahD3NBNLIX7BeRwlZooFWBaVf_W4w2EAC4hnP5J6WUAe2yX-d1Cwv5DcGQkx9XYuNqT__bfjK1mHDSllTZJ5E0MPRZjaJKWDKHZW7KBiS0X-eVDr0auI5eIqQokA5gPfNcEtbnyWbsJzQktceFPBhGCsrWpSRaB06716kGjw1JQGXVd3bJkizskJRq5tmRu6SULzeqWQdzt4FZWCpm7AYDGTRXBMVBbq-QgRj6tIDAj2c2f0xPmWzPMCVa8CMQnJJ70u15nX8KozUo8eQ27WfhtsAycetF-dFaIc3BYtVB4o8JEhWXbLyR30cgVoJc_RuGBM4TD4ScOrM6R2IoukKYMP7cUkGO8GqBk-f8XfmzxqVQNRnvmE92kbWEmuDvNp2IArPQpnGvVMbq57tSwUjPITblwDqphl7sFR-LzlKvERLPfN4E1B-HAiUG2fdSpWLa08rLd3r_2I_OGqxPGXfOBvBtOmmAIWrNIlQLX-xEP1dqufE8i_dxgrLSXyK2I4H_lrI05O9LGz5ggzhRzUq4egt2xYGDaKaA2gASAwcg4-NBrllfZovxX5wuye4oHdxo7GN4nWts8ljSTRLRsA77uiSOwAMQLESTmGdho2Me3vCg=w855-h262-no)

- Peers initiate Ping’s periodically
- Ping’s flooded out like Query’s, Pong’s routed along reverse path like QueryHit’s
- Pong replies used to update set of neighboring peers
	- To keep neighbor lists fresh in spite of peers joining, leaving and failing

#### Gnutella Summary
- No servers
- Peers/servants maintain “neighbors”, this forms an overlay graph
- Peers store their own files
- Queries flooded out, tel restricted
- QueryHit(replies) reverse path routed
- Supports file transfer through firewalls
- Periodic Ping-Pong to continuously refresh neighbor lists
	- List size specified by user at peer: heterogeneity means some peers may have more neighbors
	- Gnutella found to follow `power law` distribution: P(#links = L) ~ L(-k), (k is a constant)

#### Problems
- Ping/Pong constituted 50% traffic
	- Solution: Multiplex, cache and reduce frequency of pings/pongs
- Repeated searches with same keywords
	- Solution: Cache Query, QueryHit messages
- Modem-connected hosts do not have enough bandwidth for passing Gnutella traffic
	- Solution: use a central server to act as proxy for such peers
	- Another solution:
		- FastTrack System (soon)
- Large number of *freeloaders*
	- 70% of users in 2000 were freeloaders
	- Only download files, never upload own files
- Flooding causes excessive traffic
	- Is there some way of maintaining meta-information about peers that leads to more intelligent routing?
		- Structured Peer-to-Peer systems, e.g., Chord System (coming up soon)

### FastTrack and BitTorrent

### Chord

### Failures in Chord

### Pastry

### Kelips

(更新于03/21/2017，预计完成于03/25/2017)
