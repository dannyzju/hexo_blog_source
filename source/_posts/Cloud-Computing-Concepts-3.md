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
#### FastTrack
- Hybrid between Gnutella and Napster
- Takes advantage of “healthier” participants in the system
- Underlying technology in Kazaa, KazaaLite, Grokster
- Proprietary protocol, but some details available
- Like Gnutella, but with some peers designated as `supernodes`

![A FastTrack-Like System](https://lh3.googleusercontent.com/APqwNhTcyx54MT62fS1Es7uE3-vP3wQpO_8RkPfy5x_Hg4R4SpBJYOl_S2HUXvfHXdgs4G4_Sf5f7cfVNUXCSosoxODs1f3_0VZZfn2-zyk4VFhtnXn980hNrXavYyPZaecNr3xRzKsj-hNKr9Av46e7rhro95OfwrmJ6zXL46yHPdJGbndsnjbR1hN-ICwtdSOCozX-HVUALGOu7L-vv7cXm3rAlhBdOtxhnd0I9Pb-iV01dVHjMm9j9yRdIHN9YSOhOfcgX7v6sQPpN0dS206Di1eGG2B-3BNXCAjDOZ5gEspP0vEocO3BIP706q_rkguuNddSq1jUMni7kNWTBWSlyv-RnuPaFlleFuvTGVBtj6mJ6M18KwLOMxEcrwP7hWzSAW-tweuGYUZg2xaiqcnNrgLswabE_7NT2mVB3HOnm33LbFxITrx-cHEi1-rPmGEMk3jsnry15-KWIUbc4BrFhN152UZkGu2pPm9IvFju_Qx7jrvWijK_hHtzlev2Pgd8zE_Hu89qq9D2NwQNDUkzE6r1YB-ZUKuix0uG4nFypUCud_uwcI-3L2rTmfviGqqq1C5ZtWD08f6-G6H5F8q8zEKpg42faVMmeQ6jIj7Ke_UK1iifch_MukWYAvAaV6fI0Dl938qBme7xqt2AxfLPGKEwvPn2ljiKNHOaCA=w824-h496-no)

- A super node stores a directory listing a subset of nearby (<filename, peer pointer>), similar to Napster servers
- Supernode membership changes over time
- Any peer can become (and stay) a supernode, provided it has earned enough *reputation*
	- Kazaalite: participation level (=reputation) of a user between 0 and 1000, initially 10, then affected by length of periods of connectivity and total number of uploads
	- More sophisticated Reputation schemes invented, especially based on economics (See P2PEcon workshop)
- A peer searches by contacting a nearby supernode

![BitTorrent](https://lh3.googleusercontent.com/FZgdQchpi7QmQDH-I6al0PVvKYPdfCUghCGEo2HGQnKZaFZzO50CRHO5PeKXQd6LbFgsuNMI6DHr94sxODjVULnEI_3cHHkPZAZUrCSkQrvbtefFkq8c9TXm9c6DDU0VH_DIhBmH1QhK2PeueV4GSIqDw75Lin7NzKr_WQiS8-7y1JS0LImy-iwqJ8YHgLhrRWY4LFjVOVBDX20J5yv4D11ZTLC0IJEk63GnIMPIgbzX7UGAl0rHJzIBFBUf_GuuMj2HRuLbPQb6qytNeyM3sCD3MYvqJJO2K8L4Su2pRAw5qp06p6iNVoLgJvYZzHFWKBFXBj2JEoknQPuh98ONlkjpj747Q7D9dBwdJyj9e65f9dnsVnWL0HydPSvQje7qviobbRTFmimq5DK6BayUqTnMxLP8E0VsDrupXRAQQxckQQ5J7BdV6nTuW7BSbBgoNHrYdXUCwVRVxl8f0XRHcwdr7rQRp9vi6U5KN1DKrO_Gkw-DOwV5ButB030D4yelinbYZLQlZ5mKD9DDWRNJxoWW7b-QxTKT42tyNlqhNXAkjGPwsXntfieT7cxRN_VRNaaJo02Put--uaX6LvCec9doBEwuaW9NVCmVQuLnlgSHkKy2LRTAFAb6TB90-40oWvrPsvxP73Y7uI-BEecAHQfETLCS2Ok_Jajhg1lfKw=w824-h500-no)

- File split into blocks (32KB - 256 KB)
- Download `Local Rarest First` block policy: prefer early download of blocks that are least replicated among neighbors
	- Exception: New node allowed to pick one random neighbor: helps in bootstrapping
- `Tit for tat` bandwidth usage: Provide blocks to neighbors that provided it the best download rates
	- Incentive for nodes to provide good download rates
	- Seed do the same too
- `Choking`: Limit number of neighbors to which concurrent uploads <= a number(5), i.e., the ”best” neighbors
	- Everyone else chocked
	- Periodically re-evaluate this set (e.g., every 10s)
	- Optimistic uncheck: periodically (e.g., ~30s), unchoke a random neighbor - helps keep unchecked set fresh

### Chord
#### DHT = Distributed Hash Table
- A hash table allows you to insert, lookup and delete objects with keys
- A distributed hash table allows you to do the same in a distributed setting (objects = files)
- Performance Concerns:
	- Loading balancing
	- Fault-tolerance
	- Efficiency of lookups and inserts
	- Locality
- Napster, Gnutella, FastTrack are all DHTs (sort of)
- So is Chord, a structured peer to peer system that we study next

#### Comparative Performance
![Comparative Performance](https://lh3.googleusercontent.com/Q8mF1tb6uR4nCwOFDDvDJZS4eNH78zpW4g93MHEVQ7AWEb9LJuBzexJpoPJbOG3lXeV0kRxtwKz8y_ZX3UVOru1JXr577dL9Sr-CgJAqWQOWA31noCpWp49Iovz4XwQ-r1Q7ZzGt59lUolMHFZe3Gp-LDzTnk5nBRTYJdx63qQbPqA6DaaBdCk-iVUvooYNEn6b83dxH8sfJBeDYQ-yxRN8mfa2VjhcaKA-J70yYnPeTHQArw_lhl_mYItp1r6WBNyMhlVLig_8Hr7QKPjSHqBma23BQmCAcKCw9JcpMPTNFlMYUZy2hPzURL0sopE2ysXtIAH1KNCh56x4NK4NfuXedO1YRjftybt97sJOiX56V9FVlDQdm69Y36fv5cV4TeFS709v19X6qVPoL1XRgKDnHmhOv1Kj9BUExYGlpizN7v9NiappcUN216jlholoL-62YzfCFfvrL3snnINspSVRkv7tH3d_1o9YLiX31MARFTpX36NUQB415oNmNGQroYxHgbY0l1m3x8d50bxi0VadkXMiX74wGi-0x_pxMbNe2C89VzX-vSUX_VTIu9HmQarlPi-54eL0gTYiWLob5s1GNXAxV7IXED8kh6HU3rm1QJh_p6vPVVALuXtyEcFesXCl2R1oc0nfVNTJy0WwNASoz6GPqDXaictow-O2HRg=w1006-h558-no)

#### Chord
- Developers: I. Stoica, D.Karger, F.Kaashoek, H. Balakrishnan, R. Morris, Berkeley and MIT
- Intelligent choice of neighbors to reduce latency and message cost of routing (lookups/inserts)
- Uses Consistent Hashing on node’s (peer’s) address
	- SHA-1(ip_address, port) -> 160 bit string
	- Truncated to m bits
	- Called peer id(number between 0 and 2^m - 1)
	- Not unique but id conflicts very unlikely
	- Can then map peers to one of 2^m logical points on a circle

#### Peer Pointers (1): Successors
![Successors](https://lh3.googleusercontent.com/WT623T_MCVdUxDTx_WV1adLWQLWGxhGao1nTzPnD3gURsPnV4Iw8ib-ghmAG0MGJucDMOpjuT8qnVJBxeUcNaMhn-eM5nS80TFU5CO89qtxDKSLNfhJCXeuzlGarFzRuNFR7YzVry5FkdUGJVqPZnI_MYsYFecgHoEEizntjDrdB5sVaIqV9bNVKcDwJ6gTItYss6PNIla0oE8RthL2LfvbQKdrrFPT-hP4FdEp1DXmSIgdZ2WG6SqmsIJnri-EqdLZEn-uZ4rwEF7Mtez6092zvjok9eaYqol7-BAmJCuxkhDDSm2eh2D3xSQDnGnLjCl4I4-plh5FamYuvO4mIL1J85mD8hi4HALqZxdN90tpn8pypZOahqegX6bSvZ2ZwEHT_OusC529Rs7W-b0Ys0eCtw_yVWh7Sz0EO3W76NVuLCpY8m9CeLMbTvlu6otu6dbaAomvCmb6mC4Ax-BgwRUVbchmBYpWtqu5HJjtvhLrTVnERFOw7fDlySOJEaFv0p8XnEQ9D5G6VI9KdWsdYPVKOg6vhN5nz3gPeEHXbDselbwIg7ATDTy_59QaOqX2LHmDbxMB7vfMIBHL0golwAnGUZhTCsI_kgmmQ14Jb7x09jw0FUGqUAt-WTkX8bGufQiKFc9fIOuEb7HgytQ2OnJznnSXP095oEpPu7d8BaQ=w1005-h575-no)

#### Peer Pointers (2): Finger Tables
![Finger Tables](https://lh3.googleusercontent.com/RMfXjJem5R88pR5LOVEgc4mphhLbb-KE0in0Y0MLnnSYkIQgnvMuCfmlnihBdqkpW_L8hKqIDTJftG3xzKi-m6zS4H9KE-fDNymLTO77u7yGHyeTKU4ySzY6ODj0oRaW7n3ejPI1TxTtNdAwfR-O1Uv_4VIeQrDClOQP-VWHpiQJ-4cX2GG9hebTK8aSyEFUgMJwE3sj-fssGsMyMTBIZkkrhs2JR15tgO7OdsxAnuJRSkAOqnFMfpwt90XDkoMUgjQ8OKBCRQZtRkRhUXfCYPVImt8MOrIO0CMVz9IL08enopedI-HZEz3EyWhKkFwfTUfZmbisgNIIvI6ox4pJ6hESBedJMxGMYQ0bv3A5n19bjv_IVmO0_xQ7S04guoFaEgHbQaX9hG5QM95QGKWdQ6C5u9I3IQQYIUezIv5AiMXYLcIeIW-GStFsX3yJKkOTVhBBHkuXH1Ig0J0Lf8DmFJ9T_9CUI4H_1EBEh0YwBraE83ASEuzXNfSyBqJq7LNd7XsGvuZG_McxhYjSCaNWG4_XfI_P66B0FzWlEa59KpBuGMeItRfUX-LfpSaf9aLaSjV-pcAhmfRHeRqEZGZ3VtmOXZbTmXkxd2x5-oonpH-A7cSJd_VEMedAiRPeWnz99nlZmoWzPKPvCB_onE4UPoArQsOOsBVnOSMIOykWoA=w990-h517-no)

#### What about the files?
- Filenames also mapped using same consistent hash function
	- SHA-1(filename) -> 160 bit using string(key)
	- File is stored at first peer with id greater than or equal to its key (mode 2^m)
- File `cnn.com/index.html` that maps to key K42 is stored at first peer with id greater than 42
	- Note that we are considering a different file-sharing application here: `cooperative web caching`
	- The same discussion applies to any other file sharing application, including that of mp3 files
- Consistent Hashing => with K keys and N peers, each pear stores O(K/N) keys. (i.e., < c.K/N, for some constant c)

#### Search
![Search](https://lh3.googleusercontent.com/q4flxQoXToWb4t--H_gn_He68mofaCISK4p-vrGi0jgsFrNY3xtIzsaACg8I9Rk-wmpim6PJ5LFoaNkMjWifxV2l0ahMDXT0jmBtf_Nr-xSuM4gw-ez-Q8_vo1ex4iWu-nmv539ykuWSJD5u8RE68KLNsB9ZcZR5ElODTgLWa_vqMP0f7iVDMf7L4GtAvsdVFABfblcA3hHG5PtNBt5h_KBxQ6KGmLHFs9QWmigr_bTURI77d4V_9Qw9xRM6RckupzzAXrYGnOwWDmA2VEdgtoKe_RUFY63suVd6O55IZgdw6pxSJWedtnUCZvSE8vnjfpXwi364fyVcKk-caWvT0O-dn_lli9E5YgxXsUKIapQkynXvefm36uShd3QnM_p0CJBP4sh5tQSABDgqrlUHv1UlIrw3cX51E2cobS64XQWewAviPJF6lfcbMzUsFaoMDRacVY_d2_BhmL0o7MnTUuOXYqGUGfqgc7LNJH57Aw3kOU7ZhCd2vBoS0LZjqBfS2X2-I_wMNrvHgCAHtBgfp2rhO-yzOiwNImNvV-uVWK1skjSuCz7xWOdIzuBhnBV4tfDu27UQkMzqSUqI8lMY6_rncRwC3eKkK1CU2z4a23kgwI-SJQyi9uDabihh-CXLX_TTql5Nb3_om3BC09b_bwrHjSVjWhhWbgAw5Np9HA=w1005-h430-no)

#### Analysis
`Search takes O(log(N)) time`

**Proof**
- (Intuition): at each step, distance between query and peer-with-file reduces by a factor of at least 2
- (Intuition): after log(N) forwarding, distance to key is at most (2^m) / (2 ^ log(N)) = (2 ^ m) / N
- Number of node identifiers in a range of (2 ^ m) / N is O(log(N)) with high probability (why? SHA-1! and “Balls and Bins”)
		So using successors in that range will be ok, using another O(log(N)) hops
- O(log(N)) search time holds for file insertions too (in general for routing to any key)
	- “Routing” can thus be used as a building block for
		- All operations: insert, lookup, delete
- O(log(N)) time true only if finger and successor entries correct
- When might these entries be wrong?
	- When you have failures

### Failures in Chord
#### Search Under Peer Failures
![Search Under Peer Failures](https://lh3.googleusercontent.com/qKpwgq3yOFazF2YkC3KlZa-DhA43KxSQrOWSgGg8a0ZFgs1-u1iJZ3AbBYiQqUjF1LZGtOoL3HG_YT_PtNqX8mJsWBtd8eliU6HzIgMcj3V1D1bjmnLHbYvZXw57IIZ6SpSktVjvvwJBQaGNfbCQQw79EvU5bFga0SaSkE9ALUVTIlVYqdi1Syy_0EoTnx5khdzrwgt33cnmb-AVJlE44wKmfQCqsBurl9l0kdaajOkgIE3-aE6nViyTuA5Bla1K8dIr68UmxIKm3kN6yzY_NdTOb6LNWhetGPKHldTZUuN-TYu6MHOE97uKsPUtsE8ZW6p8JQOp-ZugSRwZIPYHDqAiqJlCdRMh6-lWoyJ7m5r2h4LMfQp9I2ZrgeelHaiplhzsMCTFfVZM4uYDYBX0j14pErxHmd5d1nY5MYAxFY_KKkCO7W0JuykFEk--0duBlRQ6L3_pB5ayJvqtBzwS_BoyU_kK4PalzphazYfV4gpRUc3a-KrWHAzwoZvLicCeBPBFgYfousF3bXTiKuG_JrQsoO2OVMZDNv6XBNrdmMSxpIDtsh_erXMkApboeotwtxxS2DMinGzNcn1atbp8gbU-hdu8s1ACzeEOB_i_0dDphqEtE2cWR2_A4ubX40wCvFERLp0IvCUnFBkqsTMpNZuk3WKFFM-77SZRvGmi1A=w774-h472-no)

`One solution: maintain r multiple successor entries in case of failure, use successor entries.`

![Search Under Peer Failures 2](https://lh3.googleusercontent.com/hELVxi5XY2h-3Cw6fHVeZvKG__temY7lJrFUQcm4jd0zQF6JeM8A73lXIs7ANpVH-T2s2blF1GQpIuXHd2_NQdc9xHyoAVErpic2Kvpu890B3iUkMiJi8uTxOxh570PL49he0h1QbFTUdF-UMMYXvN9HKADK8SNdn4hoouf0WEZAIlb8W6G1RQYOX3zH26ButO5I38zJRSYqaPnOg7SucXFvIye3xuNlp3K4hvC1eMGJtcts93xB_-WlVyw_Y6GE-QdS54pU-DOitXKl0SQqm-gEgWeOw9wgAH3MU6-4YeU93_wcp0xo1Lzxs4a5iIVmTac4FVoW2oR9B23kJWnwUSD9GaGlE3lyH44xZK2COk_26KRD7TI71PlIQ-r6jTKtPMUtCRL8wc2ax7_kTX2aWoH6bAS5Qd-GVLZ9ETs8kkfXFh0KGmhFmGNqQ8bsKIcdV3LV2CNUAX4ASYCpek55unLzApucUW_p4t_8ReGbc6pDKTsqUgWGyxqSBMKC0c30FDbMtxcKO7hyZHMUVe7VmwSJYGY4n58RSLjVCj-NmsZKU7PL-SLn-YUB-YAGPoQyFhyVfOJPh52vyLaHY1QF6pGwIHl5McoFnQOTQ2WQTcSdHDFkx-xbsEHtKArXcN0mWLuy8HTVkiF8XMHJ_DkE8muWeZjvJfUp0EYdWNKCAA=w773-h458-no)

![Search Under Peer Failures 3](https://lh3.googleusercontent.com/Bg9E7h2kb7E5BaSAl-NYr61NGzJ6bXTMud6uB8bM6x6urzXHSQ1B7hcGQ8AEoYFK69Gmu5WHawEmuchvRCiQWlyaCoLg81DCGGd3QDp0P91GKLsRO2gpJ-TApbpvcdI_yEW7FcIOPGeJsupdL1FDmfZeejqYc0lCpC37rLL8cnl-aYW_veUAAKXtW8sOXuzyD6P68RVfju5r7ilyKYJCG8DhVPS_1lM42J_4ZSm-6P1W00HxksUKM6zn-Vhnhw-_M3-zAr1rXiTIjo5pDc57MPhXch9J-D5Hy5O6RgY29rLHvopf7-rpF7hlLnVB1XxCkIQA0IUg5pbyqtUAu-rBo2CN7TkBoAoudiE-F5NNPIU2ZDcsxKATTnl8TKu2bFRSK9UZVo2hPv1HK6AMufXFodAevwLUJktlrBraH1pTHretl-Lq4dG0lsVm8cgnhSuliM92Exx8BzU7fq_aS12Uw44FJfAG_gXY4DcP8Ga6Ktz2ZYJZhOQPEbuEyq_6bhH4QxxZeCFsQ0EB5WoICV1oiYB8HDBZOovkYsuaX-Iyb9iU0p1rC3Qo8DE32w5bfBodvyvDTGzbvc_CCT_Cg9zjRrryLdqyQJDzaCWxB0zz5kaRYMRaaxYvoCol_aEqpQtE0BjeGEULYdFuJh5ihRtX-xk5u-n3pJc9zNg_8oXHCg=w372-h207-no)

![Search Under Peer Failures 4](https://lh3.googleusercontent.com/7Z2y7Mv2SmncJND1eXX6NiZlUyujHSZjl3_FI3u65RLisUEhFGRhuIsh1_0DMFr_y0TOIL8BwI2EHLhxFlfxTesXb82cH3R_sgOgnqLJjDWNmu3_-QyVQy_B9p9yeJqCPQApBIX_BLW59_maSrAkECSpFG6HexVvTq7soZtvwPslaVAGFuqNNlf6g_rL3h8oi15ccS_qU4r2IC4gJvBEfUuApDz-DEK5ZSNrGGMkSctbQNn5ycj53gGH27XVw6VeetXR8TSs5U33e7wzEXhN9K5dAzesMz-kkfFcGC-6cuWhFWTjaJ-BJ1nYWaZ6JgB64S2pc0D7OjfHZDSJ8DolmjQwyBdDo40mFIUXgKkgM4_5QLTzkd3T3-ARIHedE601RtF_cUr-8dXpGHsoYNbI6Q-ltSsEdpsb62b_qz8tc63VZWr1AneY-SIqGav-FF0UaY-onYuZ5qJQMSIkoY1MvcxG47fGGDnhQCrZRHcH3h_9477AI-ZTbIxv1fLAXeWL7SDgc19GwEyI6x1Q_lQro2q4Gzc-dxLTQ8uyfWj-FPo_TyPp_4kNxdbrYui33aCzBSGp6y7SY2iLm4PpcjgRUaHLIY2hL_Fszo6sbse425MQ0h2qegpHqgJXvlvi7iQVvNJxSOQNAgu3iMllrLeRcGa1ZuPlb8m6Ip0LD2tiqw=w773-h443-no)

`One solution: replicate file/key at r successors and predecessors`

![Search Under Peer Failures 5](https://lh3.googleusercontent.com/fCrDcjBZLDvqRY4-BdjWxKlxbKazX7wl_kaOWgN2pO618eT3zY4uRKqT_iZWOFyBbJc2dnjvD6AA7_HnxBI5TvQ9xXDsCUoNo4_EVwm_jZIFiKpoE3ncuVXeNXmyP9O2wRKJx1xI3XYlRD5WsyE4fKPSOV-i_z5vfKwmzPuOWziHW9mhmcKRZhmIR0A8gcSaRUo9TNvxB-GqzJzl0KDD4KA75bBtqAvDYP9yprmmxnzIzWqdwYXwFQ5VFYWcwiaX3KxuusO9HtkO4X3LOEgMPMdTszBml9DgxK57MAfh0teZ5tnlHcj9Opb7lpMN_27CLqzWPaDI13VvBVqZH-aRL9Ncyb8oFUx9YH6hh3MybEjNfKyqbDIJ7--D5mgTTNCOlpsZ4kVMKaIz7_HXeZLa10jMHuFJ21x4JR55_b7R8NjFijZCnP2bV0EEC9Y5RGSamHqHT4AvT7_y1wu5V_Z2YvZ8fq80PKsfIMgN4OxBWjJeXMf3_l8c8Qut0601HXeSFBiXMpt4AZfYL6lkb_Jv6DpfUNQUlWsj4aY4CKuuOhTMroCYE2K3QBC0O7RSYntYe95g3AvCSuwzvCKivAFCKHA5J98KzSWySD3ydmc83rWHZQZVkBEQ3gJ_2EfANjVas3sTbkcadIbO_tSsgGH0pOm6ph-01HIpWuxmsHdIog=w774-h443-no)

#### Need to Deal with Dynamic Changes
- Peers fail
- New peers join
- Peers leave
	- P2P systems have a high rate of churn (node join, leave and failure)
		- 25% per hour in Overnet(eDonkey)
		- 100% per hour in Gnutella
		- Lower in managed clusters
		- Common feature in all distributed systems, including wide-area (e.g., PlanetLab), clusters (e.g., Emulab), clouds (e.g., AWS), etc.

So, all the time, need to update successors and fingers, and copy keys.

#### New Peers Joining
![New Peers Joining](https://lh3.googleusercontent.com/jcNJUPI5iLuGObCyRzDY1MgpcMrv-uJwX_uJsry0EKo-rntC9dJnJTMFtt7oLtlgfAduL3-cElzpgs_zyqSW2c3g7-4FEnCQMZg2ulXmlEccftogOZ7kCSiKgoJp441lGplWNtSq6jsNyCx5sXGHtIOHED2NGWJZAo1c71I0JhTOhO16XN6LduanhF6Bjfv3F9aldRbKEJd9o6ret1qzwqfQwCBZZ9ZR280dlNL1VOi6GCF8w4pcBWETPJq05h5EpbJWqKng1Eq_gRv7ES-o-FT0TaaKaXi83_HZQGg9ykz84LzN0Oep958oUPzzSHep28NxO3ZFyjQFBl2lSCflpRPhxiOiCK3NfaVRlzCEdAo6rPW_yjrU2WPKSEQC4Ywi0UB25yfjyV52UgXjxN1NRoUzu4mhT-1kCW-QQy5j_marRss_3zdDr2554t8-6Y1jnIbhKEiNynqiEN_H9VqfqHUJSstBlg5J6T711eBMjgBOapDITYOsV4_vU5_86X5W5Qw7WyjIBV1kRsgdAyie1SGanVEuGU8Eg6K7DUSJ5v5_wOVYtIb3UFHTkw4-m3ZOKmqh9IN1n0CUDuEAqtUx3I45Eo3BtHOH-h1GKiy2x0_4GF63rxHWrZ54sdS8s-VfenAL8NBTL-0DWgXfPmHSZRRPOLSGi39DfEECAlarOg=w774-h496-no)

![New Peers Joining2](https://lh3.googleusercontent.com/p5YBAqg8u_2YgNOtjghPjqU7kbfBhY9nbxoj81_WZ5EmLDTEM3nGyQalWfPw2oH8YjSTQF81U4UprThaLoLsr0IQFOof9h3kuzej5nP1aTW25TqSxkW9HoHcn2rTarkgOb2pq57Zxjt9Sj31A0n2pwzeyI8YJz6A8nWWNOFyKDAVCHPwrjU8aoffGRYMbK5Ph-lL32RNV19TI6fsnByIVR5MekOsDRGi_IFUlfFlN6vlEGasqY0m7ZiX1qCeusf-Zfu8Y9G-ERtlwOE1MMPBc3RlcNAXrE3n3ZxhKttlrMmtoyUADBzEoeuze2i4S6nOnNh0jx2AMRINGH_JU9ULvgf8C-Rpx7EEoioemoXZgsHiGu2CmA9WvpfonpZlQJOUMSeS6tIo4g9pRnMrQtCwQUknk-Pb-x1H2Eq2ph496Qz7T9k_8zqUVuISKjK_WrYBljQFainVjpNiUpY-2V7pBQ02I9vxxZJ6cZBZMZ3eeJ3wKi_z5r1PHxQ3FFDQU1wHBUFtDzG0Dr_l71axtmrzQdOchCaXFOEwbbQVpKK-u_oj40TzKshg8J-uYpf7YrFWQ47jT54Pob37ZGDXjeQBvw74mPXacWeq2k-5oeAZB6oyqHFC3CgjrbV2_cybkEOpLtzyYBz44utXG55Q6zUEtsIgY2tcvRs-NXSRKJb5ug=w773-h481-no)

- A new peer affects O(log(N)) other finger entries in the system, on average[why?]
- Number of messages per peer join = O(log(N) * log(N))
- Similar set of operations for dealing with peers leaving
	- For dealing with failures, also need failure detectors (we’ll see these elsewhere in the course!)


#### Stabilization Protocol
- Concurrent peer joins, leaves, failures might cause loopiness of pointers, and failure of lookups
	- Chord peers periodically run a stabilization algorithm that checks and updates pointers and keys
	- Ensures non-looniness of fingers, eventual success of lookups and O(log(N)) lookups w.h.p.
	- Each stylization round at a peer involves a constant number of messages
	- Strong stability takes O(N^2) stabilization rounds
	- For more see [TechReport on Chord webpage]

#### Churn
- When nodes are constantly joining, leaving, failing
	- Significant effect to consider: traces from the Overset system show hourly peer turnover rates (churn) could be 25-100% of total number of nodes in system
	- Leads to excessive (unnecessary) key copying (remember that keys are replicated)
	- Stabilization algorithm may need to consume more bandwidth to keep up
	- Main issue is that files are replicated, while it might be sufficient to replicate only metal information about files
	- Alternatives
		- Introduce a level of indirection (any p2p system)
		- Replicate metadata more, e.g., Kelps (later in this lecture series)

#### Virtual Nodes
- Hash can get non-uniform -> Bad load balancing
	- Treat each node as multiple virtual nodes behaving independently
	- Each joins the system
	- Reduces variance of load imbalance

#### Wrap-up Notes
- Virtual Ring and Consistent Hashing used in Cassandra, Riak, Voldemort, DynamoDB , and other key-value stores
- Current status of Chord project:
	- File systems (CFS, Ivy) built on top of Chord
	- DNS lookup service built on top of Chord
	- Internet Indirection Infrastructure (I3) project at UCB
	- Spawned research on many interesting issues about p2p systems

### Pastry
#### Pastry
- Designed by Anthony Rowstron (Microsoft Research) and Peter Druschel (Rice University)
- Assigns ids to nodes, just like Chord (using a virtual ring)
- `Leaf Set` - Each node knows its successor(s) and predecessor(s)

#### Pastry Neighbors
- `Routing tables` based prefix matching
	- Think of a hypercube
- Routing is thus based on prefix matching, and is thus log(N)
	- And hops are short (in the underlying network)

#### Pastry Routing
- Consider a peer with id 01110100101. It maintains a neighbor peer with an id matching each of the following prefixes (* = starting bit differing from this peer’s corresponding bit)；
	- *
	- 0*
	- 01*
	- 011*
	- …0111010010*

- When it needs to route to a peer, say 01110111001, it starts by forwarding to a neighbor with the largest matching prefix, i.e., 011101*

#### Pastry Locality
- For each prefix, say 011*, among all potential neighbors with a matching prefix, the neighbor with the shortest round-trip-time is selected
- Since shorter prefixes have many more candidates (spread out throughout the Internet), the neighbors for shorter prefixes are likely to be closer than the neighbors for longer prefixes
- Thus, in the prefix routing, early hops are short and later hops are longer
- Yet overall “stretch”, compared to direct Internet path, stays short

#### Summary of Chord and Pastry
- Chord and Pastry protocols
	- More structured than Gnutella
	- Balck box lookup algorithms
	- Churn handling can get complex
	- O(log(N)) memory and lookup cost
		- O(log(N)) lookup hops may be high
		- Can we reduce the number of hops?

### Kelips
#### Kelips - A 1 Hop Lookup DHT
![Kelips](https://lh3.googleusercontent.com/nQBrB7OpWiWRNfSWgWmLoguYYXdQfRoPlk5dg4ld3alwUUqMwJWdkzJt-Ilh1hYWmIBAhH1D2D4-wIp-BQtYJ4X2TY8dSW7IEJGsY6mX7l81Qmgr6h1KXq5AHuuSKU9dY9Tbg9l5KOS9bslaFVOQjrB8d3aSwRq9RQlgyzcU4fgv7EGUTINgJAd0o9TqnMLobI3PuGpyfHSNdg_RjG6ShDRJgPr0Pqmg7E0UGW62UDwZqMchwnf1nWnTLEKc3U27j7vcQWo3476UlYS5TL6yRUwRRh-irKj7ECB8J7CCDFCNUE1VzPhlqJpbpFfZCYyAPBq_UjO9ydtmeO0RjaXyps9qSZRLLdq1q4nZO50dmHuBgVeK-Gdzh6dYzyATWZWEoL1CMwfc1x3jq-pDIKqiQIfIxhRZfzBfPO_VLpB1QKOzejtNGaIVerCbFHWLVFwYPeJa21EWGXOsHdh5wyw1e9NLQkfD0CNPTDXc1LrFCb8qHZ575LtLof7Ws91IeWcsiGxn-vdl9wr-CUOkgr9i3erngUOxwZSL8AiUZCQh8bzQeEf26W7dJSDVbyyMPKw-8yO6D8xT7qm2cme0iUErHucZsqKxTVk9GX09ZgYpEHUh7y-cy1qOa1Q88cWgNyM0jNoiNIanU1LUhEyeAWb85UUIq680GMx8Oj5u4yNHiA=w773-h485-no)

- File can be stored at any (few) node(s)
- Decouple file replication/location (outside Kelips) from file querying (in Kelips)
- Each filename hashed to a group
	- All nodes in the group replicate pointer information, i.e., <filename, file location>
	- Affinity group does not store files
- Lookup
	- Find file affinity group
	- Go to your contact for the file affinity group
	- Failing that try another of your neighbors to find a contact
- Lookup = 1 hop (or a few)
	- Memory cost O(N^(1/2))
	- 1.93 MB for 100K nodes, 10M files
	- Fits in RAM of most workstations/laptops today (COSTS machines)

- Membership lists
	- Gossip-based membership
	- Within each affinity group
	- And also across affinity groups
	- O(log(N)) dissemination time

- File metadata
	- Needs to be periodically refreshed from source node
	- Times out

![Kelip](https://lh3.googleusercontent.com/ar6rT0PG-tFxrdSSnWiKsxS82MLrhrMg7XX-KceL6YSRyr5WcXQBo-daxuHYXdF3Ol7jCFmJgW0XDn-MZYestCAW2OttxAzD2SBtHoOMVngWgGRtBw6I4vQB6ZYQP-ervSHpv5Ye3nJuZFnb4IBJ8Akm9brEkY_p8KrPQGXMCE1TE_UlY5q2odY7FBB07vQLdZWFbuOJFYFhH7pa44WWBvYIZxvGhsPY6xkcjcoCwFJVHzb6LlX5xCoszL3mgm0U05fp98g6GV1RWiG_P6_YTrC1E2nMEQwFie6wrf9pP-nLuHw4B8loN55deDllRoO6i7k399UQIk47RA5NsiMDTRqJy2C0RDdQnLkwO-isvlqHJpye65KYpsGJHydzgZboC7TpKt4HSzoZEe6T5efx6gWB0UGdhBOUnssKeKQjS2D1ULivhA9Pdv0NdArbdKHoEG8ligJXPO04kvzfuPUTc_8FWzFQ0qs4zEdiakatD_rWGBd8Cu4MDI-HzKrD0xlBtrSnDWX7R0WidcvEZSujr5va6g-lDMmHo8Reozqif3OnbTcRUCp-ErChHXHkFp2gIbKRmap1CYdrjw-psiIFd9Jg496r4-giI1-NJKeki9Obn4cpDHUIAQxSdYKuwe1UcMaH_aFz54G3Uxlb8GDYmyT2Xn6IB4Adp-MjgjEy0A=w685-h762-no)

#### Chord vs. Pastry vs. Kelips
- Range of tradeoffs available
	- Memory vs. lookup cost vs. background bandwidth (to keep neighbors fresh)

#### What We Have Studied
- Widely-deployed P2P Systems
	- Napster
	- Gnutella
	- Fasttrack (Kazaa, Kazzalite, Grokster)
	- BitTorrent
- P2P Systems with Provable Properties
	- Chord
	- Pastry
	- Kelips
