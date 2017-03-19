---
title: Gossip, Membership, and Grids
date: 2017-03-14 08:23:37
toc: true
categories: tech
tags:
- 学习笔记
- tech
---

Class notes 2 for Cloud Computing Concepts by Indranil Gupta @ Coursera

(更新于 03/19/2017)

This chapter mainly introduces the following two building blocks for distributed system (in the cloud)
- Gossip or Epidemic Protocols
- Failure detection and Membership Protocols

## Gossip
### Multicast Problem
What is multicast?
- Sending information to other nodes in the group;
- Opposed to broadcast, multicast is more restricted and only sends info to a particular group of nodes, instead of everyone.

What are the requirements for multicast protocol?
- Fault tolerance
- Scalability

![Fault-Tolerance and Scalability](https://lh3.googleusercontent.com/L_7hHFT-OEtwK3K6GAUqBGWVo3ND1lFM--mUzCCy4-iTYq78jDX_7HkAAK4-b4kQttoshXc9T1QTsUQcO0dp1gDatZPXMo50tIHIZCIH9p7-0WF2zGMZpJK7vZk9XFMfErhccaeQtvYEgc1r8IB_ah68oFqv7-gIvlqOtKCHGgAsOcp1IS4N7xbx9RPxEJZ84hBAjoPX7hdHtjLIA6-e5spMtx8oBmmAU7DuCqJGuVhtoG_L6mXUkvWd_S9wqhd4PiNtpT8kxJ92MoyK1EtxiFqFsFm0TqUzkss_EnlfAZkDxeG9FPSwxDqj13CifzooL5cHfYXxpCptv16uVUYg1rMo2ul6EdXxGDX9Zpd1v_O_x0sTAmZfXgu0RjF4cQBMQ8I0_X68FKkFkGWNsW6rfk7KnJRepiGhq19CE-Ncf-TRDwKxDJ4FAjTVLQh31cU_Eu8Y77kePgZYk4ZmlAX0mmsmVfYwyxfP3HreYJnPWH2z29jU2Mer0ChsY2FYJKLNBcG11Pi5pEzAybRdUnSoJ_13V1a5zt53gIlwQiiktK2ZWSUC-nIr5q4eK0UKxnoOFBsOVawgpQ-41n07oAT8PI_FlvApJm_DIaPob7i3-yTdhRhl2dbyZJhnaD7xzIExhOtt1FEB4Nn_PYJnhGQ_zJuTZ4Q6h4SlgqyhqQrv3Q=w969-h509-no)

One of the simplest ways of doing multicast is a centralized approach.
![Centralized Multicast Protocol](https://lh3.googleusercontent.com/iGKGaDBr6k3b0lN5284Yh6zFnl6mH0ixIYZvq9uun3xY71FsTWOXapeRhExf3z4jVTOinKWEgDkpBoe71QbU16b_oMP-q6Opzd9mkyaznd-9rzNIcljp9UKG1EuqH8IUtEc1SVGUmsEmrZkT_WBkSXk0mjb66UNjDAaMutXJiAoU_w8kvTusuHG1rWth-FrkxHq5DJPiMDGeMMJgTeSbwiRvL7KEZUWU79G9BNdVbNu9RP53WATxL_e6bOOfqqxGkzQowEbsPU8gPZdNbTiQpCar_IOt43TtHJmBgqMeDZZCqmgeXW-WUqfIkiNyiB5wUztlflE5rlz_7tOQwOvLbVzMksY8chJjTIwIt9AmsK4vhl4hdpNLB8Wn0z5W96awlNfyYlEUpSaCuPBoc7g8bfGTBMLZvZlPmlwnkUy4UuXjMTjQsQK0Qa2urNahOqTMtU7_NOfO_uJSLfYpNt7PszecpkFCj9GSNbxnxZlTFhhpvC-TqHxcYnm5ptCu0dyyMVAqnQWywb8XGWe3sdVHR8iwwB4WtrISehy0mWeT09qWwdkba-U1Ux4dX1YgzwJ7r91-fTVvhZ0j5VdKl3CtiR54pwKzYpGn8qtle7sfYyFjY6Wod8BvPUUfV3gCke9CoWPfpsTvZpyCgsWdUgtSC-rmQRNWNTI5BqtfsmiAyg=w934-h491-no)

Problems with centralized approach:
- Fault tolerance: if senders fails, all rest fails;
- Overhead is high, O(N) time complexity.

A better approach, Tree-Based Multicast Protocols
![Tree-Based Multicast Protocol](https://lh3.googleusercontent.com/a-zPrhEuMA4jMnaYOGfg3dMgB6DnsPoUk0yn2dZ_kBlldDFj8cwRf2t6CZ-SXgoFKusheiHq3nHJq8enf2EwIdjUSFDsJfhKuHYB7k2ot19jPunVAaHjKs9FDvfuveaYrm0sfUzcJBvbZme7g6em6eQwSb9Hf1icCOiTORD5xMu1BEWqt_hz80YDniukw4Fc-4IMPDy-L5bAfuAAsERi0UCpzEUhKDP_d3n70Eph6NximkNKFdwNB_UTLkuA7mjVfsyVMbQgArUxhwWO03rYLwSQ_tsPdXeYxo4YyNvvwWakHpwBcDLnTXbOG0dpGnuPJlyRvNwHfEwUJAwI-tdWOI-orHHcNvy0FjXb-rGaFO49Hke1tpfYAKwadAQttDvkxbeRM3YXDN3zX6GeKWo4Et9NbASsRRV1tBXyk9Ztu3YC9VmhHR399-SkfUb0cOCD8KC_ktFl2oXktg7gsPXXam9_FWG7p4oJgZZq_hLdAOSV7EcGP0VnKb7mo1_81rjb6lmRM6xaFLouAnfb6IpdnR_bBL2H-lk0-bIkt5ndY_aVwZmkq0HhbdJN3-3YBDCDTsXdknyr6NbfajxNDXuELg_d6p-g2iBPFC67qcnW3Iwr-gix7vZ8cs75waEfZxh1uh_rnpmfr8whwBRhjJx85SROUloi1DiHaqaEMwndHw=w1086-h604-no)

Tree-Based Multicast Protocols
- Build a spanning tree among the processes of the multicast group
- Using spanning tree to disseminate multicasts(Latency reduced to O(log(N)))
- Use either acknowledgements (ACKs) or negative acknowledgements (NAK) to repair multicasts not received
- SRM (Scalable Reliable Multicast)
	- Use NAKs
	- But adds random delays, and uses exponential back off to avoid NAK storms
- RMTP (Reliable Multicast Transport Protocol)
	- Use ACKs
	- But ACKs only sent to designated receivers, which then re-transimit missing multicasts
- These protocols still cause an O(N) ACK/NAK overhead

### The Gossip Protocol
A gossip protocol is a style of computer-to-computer communication protocol inspired by the form of gossip seen in social networks.

Periodically, a sender will select b random nodes from the group, and sends them copies of the gossip. B is a gossip parameter, and typically is a very small number, e.g., 2.

![Gossip Protocol](https://lh3.googleusercontent.com/EbrnuPa6Uyoyf8UFdii-RaYIS3Sq3cSDN6aRPKiRJYRNw1KX0e1oObPHv4xlAJ1piYE00V5Nz-GvN_kFbF8GIwpKsD5_fFhr0aoVL3EAZ4QmZgu53eMYXAi9Cj48TBki7eHrb6iKdPaNYkdAqO31RTi6-2epDYdN5_dWy2Wbet82CIIWVSK-d_H87V_u7q4YZR9t9emQZSDQIkzBmctkzwduBwbzH30mMf_CYSAyduXs38LtqQ8LyukG469CxWUNar4rSlovLAUEGrckrHAB6qj1CbtQlTypZiS7KDT_2tZDdob1pxMPE0G1ciq7E5tUkSxgFL3M3Qh1k0ziMZgRY-NQMJN-JdKuX7PKe_CDp2gRX03xK1dz02JLM_EN1R6DR7nIdkNvwVlfDBz5cGBtF89p4_KawaGb4XDMidUzpfv30liynnFB-GRu1QjhzzUVT6JuNHVmiJz_V-N_W5KvQmAkhBp8jcZCAAVQwxtNR8QVEx7wCvsgbGMlcU41Pmj0FzJqEZSZRZhDB7iUjq1T3lbCl-DBTpVh-7OBJvzfyvagQkvYDVSyth4vhe3hcSMS7Ro9ZtcEBsnMgKv5dOBjwMeOVqUfRIZgnV3tToiv4Lb4w8L-GOjJd2CzIKZtaHiiBZY0boWJ6_3Kqfv350pa_Xcruqp4QTsCKL3zuxTp4w=w690-h415-no)

- “Push” Gossip:
	- Once you have a multicast message, you start gossiping about it.
	- Multiple messages? Gossip a random subset of them, or recently-received ones, or higher priority ones.
- “Pull” Gossip:
	- Periodically poll a few randomly selected processes for new multicast messages that you haven’t received
	- Get those messages
- Hybrid variant: Push-Pull
	- As the name suggests

### Gossip Analysis
Claims of the simple Push protocol
- Is lightweight in large groups
- Spreads a multicast quickly
- Is highly fault-tolerant

From old mathematical branch of Epidemiology
- Population of (n + 1) individuals mixing homogeneously
- Contact rate between any individual pair is β
- At any time, each individual is either uninfected (numbering x) or infected (numbering y)
- Then, x0 = n, y0 = 1, and at all times x + y = n + 1
- Infected-uninfected contact turns latter infected, and it stays infected.

![Analysis](https://lh3.googleusercontent.com/NpSovr4yV8-wykhh47j8mcgef9GOfHY_75tUxslOq3evkiDrarZbGwK4JpEo2dZXmL4vYR5gn33yuhMgwLX5uYHQdirtn7y08sa40FaFEmkXFJdAMWcDAsK-1IYOZmop-O7cpx9MomEAbatE6jX4Xifh1b1Xb-vZqEt7SUTvinHs6wu_3hRrvmMMbe_Qrk6E6_nJmNZ7mZ1zJX04IQ22i-55fPFbaKi4ToDlkH9tDGwM-kurVc1I5wklWXTjOB8k78n0EdffUG_UNxxtNq8qH-3OlM-_S14ibMZvGt7hPCU0qKlR5oYECBA3zbPj4cDYVsYpzKIyDimE4zoN4BvYXN5eOR5az5NDgr-0J-hmNeYOP9SrDaMv7592_kZTpiLc-lrQDc9MXxQHrL8oC7mFRBk533r8yXQCph5Ez02Wjx-7DzflLGzyQjxdECSJS9OVk7RpTdtKHvEn79lBvgcdogHzI1seqmnTmp_CMfP7jf1SBDcAScmkst6ZRSIthA3_37l5V5bqrqz5NGceVRsrnySqsZguJUyCtm_ZpXavjlOQ4ltRMd78JgcqphQWz0gKF80iVzCYXFjgeGMOuCgaRyrMP72JJuYQa2xIVNBMrpYFxPo7RPqAHPthY36t4DYDMB7PFmA6NH9rQaxI9d195mrF7GEpUA6dbwqkB9AqYw=w1504-h644-no)

xy represents all possible infected-uninfected pairs.

![Analysis 2](https://lh3.googleusercontent.com/CwP-Z-ArAtD8P7SSnsOsvnXeerZbagIEpUWwMAlD_0VlwT97n-wo4F6ukD3q8zkt-adBoc4YBm6rRMGknJGbZNDNGQY_DudDW5XoIQUOJ0QpGO_sSxsNtRd5bBIVELuHa3FdhwqVj_EY0gPmMZxVubddQCmrzFLdLp1PBrBwtW1ekIXNpjbShAdlbZJjC_cvSWHeTwURFppogOdYaD_V8EhucYad85YZMqRlEA-iHXXwJwN2SJfjPnv3DUTxDYyHkqIKv6gIm7NEOcDqyJOKGLz3buCWgvYqjdHPmR9NiBcT18eoJ-Vnl8sv8UtVC6ZbWZ33QYlGjx8lygIwjG6Fu5fWSQnEcDctyUw0aRf5z829w3Kr5KlvchExYhre-QfZvEaQseHXKuYo1DTUmMeTVUF2s-EhPt53d15gShk-FNEiZjZNF-VuhpCobBeatR3ocOpDcGv7sb_fRW2MLyQVlmwCfo804rMnxu939CpQwMO_pCS9_f4uYI7WYsssUG0C4jj45or2OrZAZjyOtKg5qhrkbmUJGe9mQp8zk-fQ-Iw21MV1HL0nEylnie91VluRC190gU_L_cqltXaN64lZKVqOy11R9gNpTVp_ODXucJcA1fV00ILyyo856CYRx0plo6hc2F9dfLD2BvzT0M6jJcZ-dZGUkGYR2GytZhg9kg=w1387-h603-no)

- Log(N) is not constant in theory
- But pragmatically, it is a very slow growing number
- Base 2
	- Log(1000) ~ 10
	- Log(1M) ~ 20
	- Log(1B) ~ 30
	- Log(all IPv4 address) = 32

![Analysis 3](https://lh3.googleusercontent.com/4kNgYoaJajllNlsq9oq_Uw2JP3wdj3WXBymX4oh_rkr_nyO6YsMcWBmiDkK8zGsTOHPIKN9yU0XkmpAAEyWCRjtmIh4HeY-CEOO-aJzR352ZAA7mQd-TWRkuw53QCi2KrWxMUshYcYLYwXLQUpKncnOkW4kvH9z0DKdfid4npnSEGARY5jVfRgbpS5yKJpf9XCVWk7vk0BcN-OwFFXM6mbx3htfP1J2q3QW6RXoxJWJ69HxHwlb4NNA0CYmT4AFsaENvfoAXF2kEhesI6Ndr0_Y0tlDX12ahA8u6AcaYQ0jTQPpLs7fl7-245W1I5utaTq3KiOdrhB9XkJ7AMjYuuWklj6c5oFwhI-5xEhd0j2Xaige5QkaVIcyG-dF_fGpg2Oh-3QcJq-LNa5OLSy4jHQqrTh7_Unwo8rXvN3cJtWWqGR9gi43yxvGhM41HnoJbao2tJME5NY3tNGkJRh2kRJ03NgdydYmmce5pro--R3aIj0BZxJGDIuzlCNNgY3QDhQMTxQwl4NdqZgMmoQw5ZAqNE2xBjby_yZl2hOxjBxq4iu8eUD5443lqhWAV7SSwXVJcdce16uZs6kUigxvGksn-Sy3btZp3B2ZWCf0oX_ItXljyoQeJfkmkJKvYEKdbXi-99w-IgOdXGujCHEfTLAKNFmndbvM5Ox0kKed4cw=w1161-h525-no)

**Fault-Tolerance**
- Packet loss
	- 50% packet loss: analyze with b replaced with b/2
	- To achieve same reliability as 0% packet loss, take twice as many rounds
- Node failure
	- 50% of nodes fail: analyze with n replaced with n/2 and b replaced with b/2
	- Same as above

`With failures, it is possible, but improbable that the epidemic will die out quickly.`

**Pull Gossip: Analysis**
![Pull Gossip](https://lh3.googleusercontent.com/-bS_pDxZcAn2KdGdGlI-fhesApSpI0m4IbxMoxi5uAFAu6q2lkIw8MUsbrRhpzFocmWIea-ZawHbcug-D8nfClxzs-82ZBK9e7HAGg9UzPg-RgH_IKyaWN-SPsjORVOQkaqq_Fot1FEfhnSyYP_Ecu4Df7DmNmy9ivGB08G36nA0PKReExwz0ncdx_gMLnDNuWzyE8JHJ_8lX0FeYhEoPDN9LwD9qWHvLXjmXUXhPUIE_o5sDC2xx_-jwb-G-9NdltWa2sG3rFr0dFz1PbwjL7ySdPzG_ZvL62g6UW2HXA9fSHnlxMB6GgBWPOrjPN12brrU8J_IW5_C1uWMb2oU4apmQI8xe-aLYZUEscnN-x59pmYD6m8aQSUnA2YvSK9ApZX3lCP069Qadc_qTFm_TQ5mnNgtSJt2ezDymV191oyke-csSeF6rx00WIMVqIrApeeFFEy4cBcVExsdBgTngVBUAqmEv19DpyAp9fsSOLWUDi7sM7eyL64fWTibR6r-EOZRgDxcNC-lo5fjxOCbTAPSpMLXAHaqWdTLsE_BuLhpfto5GsNrsr5l3TlByEYu5LIaRxFPWlwQDoLXDyyMeQflwCD1zQt97S6LeR54375RhdJXqZmU8i3cZuMATIhyn1pX8Ihe9zY9mVtbiSBHInTO9GyFKE4ofwYVkTL8Qg=w1039-h620-no)

![Pull Gossip 2](https://lh3.googleusercontent.com/YdpmtEundS6HNVvq3IX8DGRvgw-mx0xsSkCBLVl5IlxjDmQsFadWYjaYlpkbwhLOG8zK2SSkhnglKCMUY3ejAs7YLajdQsaa7WEkE67l6xRRi2xZVd2o6Ixq_rl1J3lQsJdM1BL1HRlmWyAEupW2TVEhNNPfEZLZS0KjnuwPB_2Jkzusbo-H8IwvIcN-PjZ-fjlttMCOMwDE6hQtlp7LoGRYuyMRMTcSvWBKp8UDKGI16oh0Pjsb7ibIXnrnHRIoE88Z2MzjGKHLUAcDVXEGd6Iy21o-F9Gp4cdjScKp7sat_rQBXGmzqZlbdqf1QdOBaQlIs52X4huWhKBlLZAeH-opmZi6hcIhMgo0PmCGMdRTUviNIWeY3fc5K3wi-dfuN4GDBJlErR8Oy2kcriborK0M9LcLkhkO1P4waWPh2C7-yu1RFQ9OLLihH2FXFXtfWjsGMi8cqdPClWylL6BDz1FA9fOkyDM7uOXm8vrbqbeMaX96zt6bIJV2Cn4NHF76wu73IS-jl9r6xYsw7H7Fd0D3FmnyvnWZLfn40vALco3GpNNmFnVS2nk7FEtjEWJr7fshWW_tM8sm0XdrRrdJ2_TRagx61Ws93nNQJ7dOe-ssDIso4rS5HQU35z7L0cRcFKKyN2Erspvdf63tzC-w7Z6YkNIW30D_jGHo0uuYhA=w1034-h634-no)


### Gossip Implementations
Some Implementations:
- Clearinghouse and Bayou projects: email and database transactions
- refDBMS system [PODC ’87]
- Binodal Multicast [ACM TOCS ’99]
- Sensor networks [Li Li et al, Infocom ’02, and PBBF, ICDCS ’05]
- AWS EC2 and S3 Cloud (rumored). [‘00s]
- Cassandra key-value store (and others) use gossip for maintaining membership lists
- Usenet NNTP (Network News Transport Protocol) [’79]

NNTP Inter-Server Protocol
- Each client uploads and downloads news posts from a news server
- Server retains news posts for a while, transmits them lazily, deletes them after a while.
![NNTP Inter-Server Protocol](https://lh3.googleusercontent.com/Jxz9cSmiucf1j2CQMPfZ3CKVZF1oGZvI02y2rOblcAeiI1DBn5Plo_q6fl28SlPmImdV63VdEy1xjlnmc6FWpio90Le63iO579tQpwoBpliH5PJ22rsnAcBVbImas_kf3yoL1s1Vwd_tH7-YVYgwYwp8NybAGo604LTuXHMLNM1thfFn4-u0TkQBSv030O5PtKRJsohTWeFDrYOpxMJ0Y2AMU-lcx1f5cZdeYv_6mgJEDM4Uppyee8OkhbGAhbpKKL1Fx7qyhNOXAC0BcpsGo_1lMA6pNnHuoWeDaVWeIg88Ism3ZAvazxWLamEiOI9KDUd_kLwDmkq82wnez7d_yyQSvqkHuxeHvvrSRrHScFeCKdgA2O7okDPuX8P7AVErMSbYam34dqF-LfFBF5wClsk6LwF2doTz0vol2jAZGghXjG4NjfwcvMymd227EoWIxOjDFtqUDjp5yTyT4zgb2hG3tJkfX8NxpnJvhI-tyBfvynrGEYKFu82zLsOhpBDmOI-EOBl-KSRxzeU-xpprKfGMGhPtxrk3ZvnaZEbGYUAYp-oPRsfODxTVSKookhWckbelnpnAqfq3TjQhXm6epWj9xYpIC6tQYkbfRaXinT4k_PqaEpV8ehopGLRveGxyJwWCxzBTb5Fuh8TiwGhTJmXvsbiXPV6LyI6w5gW3-Q=w1552-h531-no)

Summary
- Multicast is an important problem
- Tree-based multicast protocols
- When concerned about scale and fault-tolerance, gossip is an attractive solution
- Also known as epidemics
- Fast, reliable, fault-tolerant, scalable, topology-aware.

## Membership
### What is Group Membership List?
**Failures are the norm**
- Say, the rate of failure of one machine (OS/Disk/motherboard/network, etc.) is once every 10 years (120 months) on average.
- When you have 120 servers in the DC, the mean time to failure (MTTF) of the next machine is 1 month.
- When you have 12,000 servers in the DC, the MTTF is about once every 7.2 hours!

**Group Membership Service (Membership Protocol**)
![Group Membership Service](https://lh3.googleusercontent.com/0lSZMTpCdbfukb0W2qy3gVf93baG9mzQrBll_VjXTJ8Td_8yQZSSRL80-L-aHLLSSmZonepBXLwEkdCbXA0MDcIxxCq-Mbb-0mpkWD8QZNhIgEbjud-Y3IdecPryk27KJpTiXyq0gPyTu5ci2HGcsRaZgW2mKlRdqfDjjEvVyabxcsQriV563lVAyUgIBHf9qEQOkn1oxcbT4Q_XLrysHJ-QXbaK1R2RlpmMjt4VFoRSgvrGkqsLmonJMcC8Plt0ganAs_lFdGqls_dSHJysDpsCqOWJpquRUhCAJDixwnAfzC_-h0hFcKxd4vLVaI2Vw1br7Wd7IpIulpbX7HKlHGY8BTOGVCwUUPUw3wQMcAQ15fk0X5_wJqN3rCxwjADA93D1tWhS14SxsmtJjLQ2kJaQXm-WHtGybPfxuyJbL5XpLTkuhyJBrFGJx1heuUmnTVuEwUEid_s5FI2_AzsT_ryvWYl-Xx4WIEYw1e1XcPrEm1MgzXu5N6x1yOdej6eT6bH1-caw6swkIJQeev6adPOYsBbjSpenN_FIykb6u3YdTEuiiHR1jDjT1HmJlenHVE8fGRkN1Qi1oJV6eI_snPiNMIeu1pnusz7LDVkO89W0EuSUDqZDYN4lrZqzmxY78LzRfs0UsJBd0uNwXRHsbeJpMP8hSr8OiVbvO8cbPQ=w990-h328-no)
- In each application process *pi*, there is a membership list that maintains a list of most, or all of non-faulty processes.
- The membership list is a *Almost-Complete list(weakly consistent)*
- Two sum-protocols
	- Failure detector: a mechanism that detects failures.
	- Dissemination: disseminates information about these failures after detection to other processes in the system.

**The flow of failure detection and dissemination**
![Failure Detection and Dissemination](https://lh3.googleusercontent.com/yI2nCBtceXUVH4jDI2ZojE4T4O4GBT2mNztSehJsaG252JhtlSC8VF7WPA3gn5dKGJh155coxkHXX6i7pr7JkVC1ehMLs0fJFxGI2QN7_IhwBH366sSNWgopjOc7NSJD6rLwnhdY13bn8mtzyDkNiqPHqlEvbc0dk5rYzECxZl0xf2PvxVIqrtoAWhZzPDMwMT11mgCMWMR7j3O7ltxMuhGxfPe4t_0SoUZTE3DexPbogQjIaaEP95Fy7fuWU5UBaf_lCCzdDRSz5gNAIszcmlYETvllFZgSqQrCH5-06ZUkTEMrN-AIx-TO2G_7wslInPNNQmZPaqONMICDJMTWbDF9gn3WlINMR7wIpvclg-GYA2W8ZQ9JHy9pucm_J2mk7qco7GaXwbmq8t_5KdS42eGfUA92EwuIVZrEqcMmHsGmxAQ1u9R22YAi4U2SivrMLDWZD_JjNTSo2WLtV_f08xOKtI5nEEU6TQEJzoybpjmbBQivFSd3Fy4K38Dggf-r-WGgym8jHI8ek12VhqK2nNDTSDmiQb8qITIfPLa_e5zutFKlip-lkuX-hWmohDU5ZqpTtA0FJCbHg1GWvwFrtOF0RK9iF6RAV3J4hFSWEPZsyDmnkSi6SnQOQYHyjf601EWPJDJ7K2IPg6XSOODs7NTKkqlcpBxLaGy4wCYe6Q=w990-h566-no)


### Failure Detectors
**Distributed Failure Detectors: Desirable Properties**
- Completeness: each failure is detected
- Accuracy: there is no mistaken detection
- Speed: Time to first detection of a failure
- Scale:
	- Equal Load on each member
	- Network Message Load

`Completeness` and `Accuracy` are impossible together in lossy networks [Chandra and Toueg], if possible, then can solve consensus!

In real world, `Completeness` is always guaranteed, and `Accurary` is partial/probabilistic guaranteed(almost 100%, but not exactly). Because when you have a failure, you definitely want to be able to detect it, recover from it, and make your data consistent again. You don’t want to miss any failures. However, if you mistakenly detect a failure, it’s fine for you to ask that poor and victim process to leave the system and rejoin again, perhaps at a different identifier. The overhead of doing that is less than if you do the reverse.

Here are three failure detection protocols.
#### Centralized Heartbeating
![Centralized Heartbeating](https://lh3.googleusercontent.com/EnWz7E6gfc_ozDudBKkrKqduZGC2TohywwywXXts03hWhUsJNzzowXd6sLQpw33VeLIhI-JaaOCUt959lcIHMG8FMPiaiFLngZWghn73zWZNYBfkjjxFw7qN1Yjq83C2znsnHfBH0OnfzOVm2AaWZ1cop__B8quvavAjd4sba7oqafZ1oI9X1zlHMJ655wDE5tK7RvV81Dy7PjbeFNjxW7JRRCOvbAnm8JIl06faSQJxq7-jBg_hUkyyOI4VS4CeiGMr6g-ICkX6UBKh7GIDaa5hAdah9x_b8F3wVBLRoX3VOv0HSHC-n-vStKENbNwH7XanKeLPaOVZ-sozSxICB4UQIi9Pa0KGDJhM98M2xkhKwM_YGgRRJiuJ5i1nVuNs7dULF_rvx0HVQ74Fd9xpHhsDj23s6P7b6xEh3pv8Z9lFuH5kabGt-cSD_gYgi5q254CgzR0NZ6sNqOoxlhzdEgLhUzpAaPVdN5LWPBr3vsQMuyxT2lgsbJ4uZGg-nTH3BVS9b0pS5QfUJXfIWgSzikM4sDKzDoQmIns3f8s1Ojhk0sfYqD7BGxAalz8w3ChqrI2bkAlFA10on_piugYsLC--JgpgKGzqfVS4jd7B1nFVJ9mb-WbcUfJMb9i7-LHrAHJuv7NcSWjvxrhLf3ipoMLVpTAD34Ck7mZf181Qbw=w1249-h522-no)

Cons:
- When *pj* fails, there is no guarantee about who detects its failure
- Overloaded, hotspot issue.

#### Ring Heartbeating
![Ring Heartbeating](https://lh3.googleusercontent.com/3Tqbd9Ph6sWH0mIl1CsWUm7xze3dP4EszbEJ8oZDwd9nV-QzFOD3hdPV9cUk9VA-zpQmhiHl2Cye84rg8YogXdwC4SOoHo-5IlMAxYWrSudRcfTqefhmC9PxYGvJ1MMdyZZf2YI7LdOm5mje9OhbjGhtJQHFu6kvD_p4ZVaLrwbjhjaoL3_Be2MjMXevSyRwoNd7OiIL0yzyeDUuLzrRwqjdJYXuaZhvbP3_RoL6I47APMc8i5_A0I4GwoR7fJgstSRUyKlE7ppyKTB2KumeLA79c_IeU5ra7CR9UdQ2nMDw10pmINTyfnWe48c98Lj9uCDpiAKp1Z8GlZBuN0R4Kk9EacwRnwQEVSfJBJ4JTXt-XmGqK3iAbMWaHPSV7bIxyNe31SpcU0Keu_hfMuDB9tXUA6Ai3hVALsFYMFO4AaYmnmLnep_Pg_xFTmo4nCuxK3xoYBTu645eKN15dym0Q7B4tpx4Pb-NH3AhcwKEDLMu7u5pEdxS91XLYJkdHRTpvree1Jy24ieopHqovPW32Fv1yOs3m4k-RDahljnuaq3vRRY3Kz--KEm0UomCtmxtcGVyGjAT7YKzq_QD7hTwg-fY7OQ5inZzykzhXWce5EEdTEywGQ950bPzSvfDrJWG9vZjjdbhe8TK-vxN4EkRaClA8IeDS7eyO9H9OHmogw=w1249-h517-no)

Pros:
- Avoid a hot spot, better than the centralized approach;
Cons:
- Might still have some failures undetected when you have multiple failures, e.g., both pi’s neighbors fail
- Repairing the ring is also another overhead.


#### All-to-All Heartbeating
![All-to-All Heartbeating](https://lh3.googleusercontent.com/KfoZUNOg4xYnr1fwebulo6X80KmEf1aobujAP_VP0pJBTWbFHuMyuXpNjsVun9-reIbeJNPSNfFCW5AuqKR7EpI-tvdt7lFmRLWWlFqBlHVKKwhtGd2Mno-yMpQ6wEUhFNb9wWgvihMS1g4Vv6uTx03q59wZYe0vyUv2s6gSG95mjBIl6YB-FfPGbuMDFmhOHPLnjMUSQvYzizHYzeZPrdIpkGNP9SDWpqBx8C409qwEnxj3oBUJQqmMp56B83qd11kNl5KVLkw1u4lCl6r_Z6cCGjs1LjRLYG6Qh3f-x7y6t-9NFiX4AhduPtSN2aBOsSw_YKJXxx5OdAxpJusYMYmkvzJK37UmTSgxzBCJ83JX5LQuewhmKZXFeFNwBZM5wf_q-tEU7ah9wKVgOsxVSRF2izskO3pBn5SepggfwSefboVu3uYi4wCdGUW8Fu38EMpiSSrdb6RJgG8zcFvyBqx2WHDD1zqihDHfMPL4_g7PAFVwVTZ5bCZhRTEXxGuTpsZ5dhlQqdqzueqBvh58aj-iXUtQUamWUnbZVQNB6TsdW4HWSiA2WIYLcoINCI34FNSdYdKx7kWYim4aObiChUr3nFWpaYkczpJd3G-3jPqNKbq6UwLopjnVT3lWf0GDXseHZljyp6ptEkI2U7cNqiwm_d-8IaTbxILV7_yBlQ=w1249-h578-no)
Each process pi sends out heartbeat to all the other processes in the system.
Pros:
- Equal load per member, well distributed across all. (The load looks high, but tactually be not so bad)
- The protocol is complete, if pi fails, as long as there is at least one other non-faulty process in the group it will detect pi as having failed.


### Gossip-Style Membership

![Gossip-style Heartbeating 1](https://lh3.googleusercontent.com/-I-ViG1FQQVya5UK1Wm8Dd5M6zAF1-OZb1tBpY-0zOc5XcpHpwri_11qQ6xWXz8DS02haSQEobVSjXxpNY9tC0KXgdisn4-N_fdJL6HEO9kQK8Q_Ykf_f2UgXUjgz-IUhQ-Z0foqxJo1Xd0YzxIqy5is0VUhttbf76nquNVyRGElmORxu4nZeObEPyE1sJgb5i-88OQss0qOfSPDBxnGDcjOU6sg8GIu_XlFZ9ycw-JnEs96disdl8PKzgDp7pHo93o_yeamQ08ih8GGl1vsIyjUhgBoqO5x90qXBbQEgTbKHmPhbdIB-P3SZyZ59szOG0CaJvh1K5prQz0yxKrfyJvfg2c0a_y89Y7VqKlFJ0W5PlOmA3vj1exObJwQj9-KuHv6M2WhuE0EVbPxw0QK2EqSRoELKmKCiTlPwOk4rXDkkVZqmvhIAp8g6KVNus8HbcfNUZt-0Q28Cjl43AkqipDuh8SqIFEByv6cjqEGzCdFyd9RXPJJPS0Sqns5MpmAjMc-TMGlsT9kvqY09GEBVmIWcLNBruR5u2RRWodDrXhIYFa1lN4WbJpp9dGMRpAzCvu1OuUyNsXHYzctJ2TM5hFDzIW4ubvt4FKd4CwkrbCu9-1g0oL14WOvY261qtymXBY9dr5xcvw6GXGgK0Dg9CViGR-3MAgWdInZrsoTfQ=w1105-h466-no)

![Gossip-style Heartbeating 2](https://lh3.googleusercontent.com/3epbIenhHzsTU_UBrTeQuTDTckh3Aq_N8dQTQxGFlq08K5n0a6cH4MhfeI0DEo5Vu9BgcdafEUYNwmP5gW6S-vFuL3A6In7yJFPgZWpfNmwkVtbi8OShgp7gFZ8PsUY3zjqkccm_fzMP6h7AP96La4mTbaTxx54sHSQgD1M2aKtxKt3m0SU89aZFake6jNGe0wdMhEBjxqH1ZF5rxqhG4-f6Jq66CmuMuQLxk3ufUWSNohctvooXfUd1JXfwk6bXb49xaqX91sX-QH36oeZQMTE14VttxWihbfQAbW_YCuikSFR0fsckdCcmtTwF_K4q9kEFKj5iaRuqWxV6RVerQJKK2gvt7iQ6XquB7aE6JowhlaIBvt2zatzQeQKPKsUog93qx6BZ3sLLBqj6gqH6TxqvTok2tZh0ff7PM72FOuIBqR61NNuCj4K0RUriWHz43SHe5JMQznebAU3tMec2SpnmQgNyMnY3Y5GWcBO0WnWkpXO62g9ajnyzlcxuCQ8z5ATOdE0GO7yT23vODTbmny2QH0pBrXzhHUx4gcOghjF0elqCMN9-N_-peTVc3pyUXzv-Av1ZNN8He2S8iH5natrZw8oh_7xrU1LeU7eJGJmOHzZv3LuVwJNyRtxQQybBhRdSC_T3y3SE0xAgWnb6g4L5fY8hdpQ5bh4n1gFHkw=w1105-h463-no)

Gossip-style Failure Detection
- If the heartbeat has not increased for more than T(fail) seconds, the member is considered failed.
- And after T(cleanup) seconds, it will delete the member from the list.
- Why two different timeouts?
	- If you delete the member right away where an entry might never go away.
	- For instance, if process 2 has an entry just failed, and deletes it. Then process 1 may have the same entry not failed yet, and sends it to process 2, the process 2 may consider it as a new entry and add it back with the new local time. With the ping pong behavior of gossip, this entry may never go away from the system.

### Which is the best failure detector?
Optimal is derived from the main properties:
- Completeness: Guarantee always
- Accuracy: Probability PM(T)
- Speed: T time units
	- Time to first detection of a failure
- Scale:
	- Equal Load on each member
	- Network Message Load

#### All-to-all Heartbeating Load Analysis
![All—to-All Heartbeating Load Analysis](https://lh3.googleusercontent.com/O-l6oxNOi0qQM_vMdfRIIBc43dX-8h1yR8J4lijgl256f3jxLasA-2343VzE8kb9FX9FhVaAC8GGL3qQ3HByo15_8n27mXzYH7ciKhsloVS9o3oKld5aOHJA3E6vHe9-jD4o7a8inaKzbBIWGkF1iza-YZC-MluM1Mg1RUhd85ML2P1m0JOFooSl4qd9U9brBrqQmSrhXYhDbw3otRUbMphY7MnCdVJQh_qdJPNu43oAZQuTRW1zkhROlufqPa4ZpFZsBcJDGfMCvv7uKHDNh8YRXdbGYgAZirUGKdRGshrdR_gvjx6PsEn_KaxhdnPXzOIuVgyA0_cW5BGJW-hMky5-wLLwKZsZvnKXtmmEX27fsCEvmxLrDkAFSFEsZPIaJ-oeeZD3tLuYZoNfIRb0q8irc8d_waqEk6YYVvtB-YSCAIoqgsxTeQ6c873PXU3Yp2dgA6mO2a_vqOEB-ZSPu0Mct78Y00Mn-UBs5Q0VaopDmu1Vwqyy6ZZmyFICTVQGMzhcoenrNNM-uyOLFv2wfSHIprWN8GL6N5SFW8RhBTDWcmkrrFOGPosPKGxcdSmdsF1mdkJalqPVhBsSJD7vy1g0hp-IkvLG6kXEJCxO12BsbbfkZ4KXLgCVtppmvA7GVwOTeNBb2Z0DX-D-I-lqaKP_fwyvgl78943v2DcFUQ=w828-h347-no)

#### Gossip Heartbeating Load Analysis
![Gossip Heartibeating Load Analysis](https://lh3.googleusercontent.com/7voCt5CxStRmleomYLpCH7Droe4bi-imoFLTXDzsyd528Q0LubHAZF_kciHF6PPCIHo4Tu66G8pT7VGNVqJhvgwtPYfNy5Jd5JfZn9InszpkOWnQLt7Tiwc7ntm3-8C8L58SV47L4zFLfyvNZeiNGU_1ZteWTJbt9IwfTtwsdnuc3qfhuAjqhmkdJXqEV7Xh7pqA6BRofFkTya7bgVoTzdnOwOGR5wRXkZ7EAeuPL-FrHT0ZkxY2pM2KekZuOkPu7JspDDm9LiFCUMwoQ5GoQbCRrhUvcShxlqKkQm4pw2ATwBJYvfGLJPnPoCvX8pMKqWimdQpsDrHtL-PHmSb5IS4FLN82nQYAhQ0799_7q-KbJKrW2U1JI7NIMtQR1JJrt9x7NLwQcSFosioznCj_niI1IAiMNTR35FM2VBj9w2pdHa_oGMA4ajpLVUulluy5RNDoFTQ4Hh-UzXFyRjVX_jK1Z8jWkHVYDtQ38x8jwDsft9xO3x1QCVCjw-Frkl6KflBIYYrHDL31XyDrCcPMgnlei3Y3UEtQdZlsOi15b80MsQ4U5M0li7PLp9kwvkQlwCJ3zVbObGXVUsfhmeK988xd-l9HHeSiU3fuDQ07UoNpBBZy56YQbFIOWOVy9att60UguJ2kW7_CpKQvxvSsvYp9mzuO0fH01faTm7L6tA=w828-h347-no)

**Conclusion**: Gossip-based heartbeating protocol has a higher load than the all-to-all heartbeating, it’s because gossip is trying to get a slightly better accuracy by using more messages.

#### What’s the best/optimal we can do?
**Worst Case Load**
![Worst Case Load](https://lh3.googleusercontent.com/rhAw6FGaWhUHR1bYYNA1A2IBkbZFCZdLAQb8cvrl9JtVZLyOUkrcS3JgiKuZOkSiWqw4l9T-bOc9f7I39xQZH1V5QzOwYjbTnt1m74yJeheqtZGbpELByIqEtlVgSroRnrsgtqC8pPOP2yHnKn32u8NN6vCHqK-HCeQqCogyWurv6li4K7KI9n_C-ICKpvjJMa3nVBi6K1vKnNsTj8jeSmT6FfZj2MBWSW76nIw9nhp97pgyDC8THe6wngbvn_yjhhOZb7d3FmKtJ2t7apG7Ib7j1bMFoyTKFJcBBp2sqKOIXEZqK_kc69d6Hpu_byZs9vhHT4wgL-VqEMhMn_UtEKKOtChJ580Sjaos8Ziv3lwIGjplS-vm-dchTOMHSRw_kSxMxyWvcSxckbc_WTepyN7HU-23xPeX3mU3MAtECNHeOkH3Ox31aCP87VFcpj77SFqL8ymx6SX-RvAZl_yOKKFpzcv_IzD2gziItCzWCP9cV_nH_WjlwoQQXS0U3wuhzluK50xqwzsOpvQy9VjZXpsJOtvm8qk9r65EYln3CkTl-QsV1wgnlgWnKtsSG2JGFL5I6NKIj7ODQnpCYF2jl2BWOd5z7rLVstZkryKYswtE_bMcI5ad_2OO9-hB1lFM5BjKG2GrGUZq5XjaeCIGEe3qCDap5j5Y604lzuJR-w=w828-h355-no)

**Optimal Case Load**
![Optimal Case Load](https://lh3.googleusercontent.com/U4Onb3oayMfPRSjA2Os49lp9gQkW9b45PmC9jzUzwr6upIJHvRCj1ySLEd7XGQOHU5Xa-vmJizsVBq0YnyDhTUc1zu6jMryWXEFkM6On7HAMJO_eODifxPaJadgiv7yghk56I9ip50PEau5IMJiBSkpdqOKTUFpX_IsBQ7A2IzvUpJKZOoiGMLOHVTr3ceMvgWwAiF9GD3xxC1vTnRp_vvZoXvCUgfd-69DY2Rd_a6hqJr5CkBm8PD78StVpJhf9yBxuR4fVgdSwAJZNvGoJyvDJNgvYB3GjtCXvnZeSd8Pji_vNJE7cSr5lCm6UdQsQzdThV3EX1oBN7EfKXZjIo6Y7AhrwbCmFUtiFkVfuqEj12vXhYRNDJL5Va3e3O-scxfC65OgOTPYQ5qL7RCtzfb0xDvh-Xvlw7eiLRC0AtjpSfNO7F_grtZbAKMljteDsz28QFoExJgCfkh8Otfuqa2VJkvPGDAqEGaKOduFdOx95oKs7k6qQnb7mPp1NbAFVCpyiopCMOr9wRhu2wuRBGQcJptgrql__fb2be1PWnYe12sOKTm-FVQCvHCsLx3w6cZ746uztJWQuyq4-JreVcBpoIV8QxjJHcf3f2mAJCmIStIPZf3Q8N8eUezw9jDdNC9DAlcTXgutxOyGc-H8APsSgQ9dXwWRmYqYh8cxAbQ=w828-h543-no)


### Another Probabilistic Failure Detector
#### SWIM Failure Detector Protocol
![SWIM Failure Detector Protocol](https://lh3.googleusercontent.com/39oV7t3ZOD7xAumWYGetDu7SLu93znYs7Bzk4MLKXjoFhMFbIh1G8SnLnaRR0v9YdzKiYcXLNCCFtvzvMOKiVb7SS5uud4s5daHSErLCvSvJz354MK5JGG_mlyeMsTdt4ShVIdTzhqm5TUFnOGiL7RItVMiORZ4sZsq-wIJ4upHT7awNxUXhXqZfhdYwksYakTok9rRl0K7qZY1wna2PbnxBI0_JgIHFG8LJeR7070gkLYrX71ueswXl1g_H7OQkfUq7AJrOdj1hJbh8jt8e3phNwUlGCEsEjJi9SC3pZRedcS8lWEUWCbZo8gHqXXALBY9hXUD7tOsPjYR6WO8FW6NcyZOIxPczBb4Y__lkuPujiCxHymoGCTmeIXj2YqsyQf_I6BtXQu-2LHVzHg8n-deCdQ2bmJUJHIzTclYYrPBboJ1WrkqvB6gIJS8-L_WvRPdw9LwUmKITnnjs71BNNM8Srlb6xGUhg97FqxJjbmQsVGFy09vOlokCZvPXbTyRVvHHZTWD_mEyCq1pyM2w8TB7ei0p8tZp13CRfE9360uiTj6wPT_wp2HONXV9Txlzs3aryGlJB7YkeXSyHBKMgdZ-enOH6ZC00OJ06fsEheWnAW1syuWNUyoLRxq3iMV0VLA6Pd4rvcC9R9yIXi9_yWKjTvV2afzLLZALfOGKCw=w761-h318-no)

#### SWIM Versus Heartbeating
![SWIM vs Heartbeating](https://lh3.googleusercontent.com/Bepw0l52MMlCi1Zw5dwuFeyPjVwI7jDTeFYUlvgAw8UJBF6BDhx0y7CUCrf8OvJOvQAaF4vvGYyochL-KF8jCtkPljv9YAQ6hBWUyW4Zaa_7dN2sQR1k9K-j59e1G-7-zlTqKHN1dOKnEOwmks_mrqdwmy4Xvf0HW3VZ9SzdhhjdnAdlgD0Nwt9OSaf6PjprzQl4iDL4L9BZkulWX66W2YwMtCmBYlket9zF0kHhnzKFtchDWzF37afKQMmPeKvKJtzBlr47VnOkalTKUO3n6YxkUumaVkrVhzFssFmFub6Sd8FukZ9_g8DpwL7Vfh6rUgz08Ex3eY1TqALU1YmYatQoFKEzCM22cIa6CCHfeLLN5db_-SSspLWJsBcd7au_OR-dTlM0eJxsoDEhYX9-WDWBgiZjclIpyefZXn0aE7PBOMMnHPGSinQfRMyrgUpcTmIG1A27DJPhNuUmS7cxFO2l0q_rpv9lNwY9lsR9aw9kKBAJJaCMwigONm5ID5FN2f15N9sSp7xsWpnqU7j0EJoxrtzBCWP9BDS24-e-Lqo9dr-11nYM04jeg-SV2UpPX3sLvkox-7ZgKMwNLXYhGEUMkVvrhidMz1B2zQjHrNnLePxtqdIlWehR01VaMKnnsrTfJoeoPjXl2PHj8V7JwuWyGoQNwJA0CkC7IVj54Q=w891-h377-no)

#### SWIM Failure Detector
![SWIM Failure Detector](https://lh3.googleusercontent.com/N4gLqzn3s3qV1FwRC4vV3jpR7vtGzwrHPIVhbyRMBER_yaC2To8Dgfzs9TwcR8lqwuifNgrnJDIpD5O7beNNIKIwzrlI3x11L2V2tw8pwcmJy_fB2BgmRy-igoDQ4OjHmJIaXwq_AQZ_TUobkNuJUSrQ7nDmV-tyFvi9UtN9coN8MNLns0flOXOa9wix_Rx3BDt7mLRx8mB50rkBMCt6jBcdDCEIF0fr_fsM8JyG0an509gEHlHlOI5LOTGlT2DDuKbd3FLJajuGDco8B0ZDPHTp5uSRjCMln-n-e9q4FT86n_5J9_kBTvhW6CjeEiEhmKLWR_oxDXauMrGJpWltkTZRJ50ov5GRKyGP6Ok_yC9U30OizjaNAZdsp7qYBM9xu6-iAnITHkMtQlEkKlbbcGS9-v6x86NQdwdoirWBQsKtaY70Jr5qZNxKWoKbAB0bRkGkDC1vePMoKl9kWcWmKiBvc8sBXVC16eyDj_6ezFg2qgw32VG2ekP9M4teiK_fojha_UfedfXGkevtJynAEoidYy6vmucK4DTzHI5chvz4cc6YA_jT23mJjPbWX5DqEfkFLXfZ6JfqNu8ers2MuwPqEHv7vwesbJFQwA7U8SpNSsNt94oCKMKvta6sQ-I5gNNyjn1TdURS-MZaBiXJvUOOrJSLiQ4Ll1NjfIwoNA=w891-h594-no)

**Accuracy, Load**
- PM(T) is exponential in -K. Also depends on pml (and pf)
- See paper

L/L* < 28, E[L]/L* for up to 15% loss rates

**Detection Time**
- Prob. of being pinged in T’ = 1 - (1 - 1/N)^(N - 1) = 1 - e^(-1)
- E[T] = T’ e / (e - 1)
- Completeness: Any alive member detects failure
	- Eventually, every other non-faulty process that has this failed process in this list, will pick it as a pinged target.
	- By using a trick, within worst case O(N) protocol periods

**Time-Bounded Completeness**
- Key: select each membership element once as a ping target in a traversal
	- Round-robin pinging
	- Random permutation of list after each traversal
- Each failure is detected in worst case 2N-1 (local) protocol periods
- Preserves FD properties

### Dissemination and suspicion
![Dissemination](https://lh3.googleusercontent.com/dogZe4DEAHoMWXOaQ7r7iOAh3BtnyZCd4VFI2JBZVDMerUNatygWo1ua7BIWOQrL0GrzCMDKGbNDswBY6-pyT2FcwwAXHSnJ-Ccsq-ZsiSBDF9OykA0EXU1QA5yiwOHX1abCfGtf5T4-MNgkBjPuukd_5A6mo2cO23lFvTygdWw5vVGoz9SRXNqiMzwi26uYzgeSMBROxggLPkcvDdrZSpjkFm0XeWvKDZgvLd3vRtwf5p30UM-_PUfwo_P0UlS1pNF3THzqWiIIJYyOg_4eo6-T76yrCMYUz75Vn6nD1yo04MNTEkX5nGD1pIjRyrp8rSePS5WxrEuGBLaY9LNHaMNES69VvkjNRYSx8jaT_3SljH_KzSJ6XFYRS6beP6sKz_QSyq0QlfZ7KoWuWj-46_2WKYROTTgbNDf79jZKfGNXzIKCUcB6G8WcN9dQqazdsE8F1pH8TBd0D9GMoOAY-WfnmtJB6cOiwCCLUQs8IYLDrWMnFj4AubJJkntUZXYCoYb8bquQBFXiggphKzAv0H8CSbCVgXl8tlo6T3befhuIhvrQkyui0VE64OM4cCBfx48NKjymRrrwWcqWo-AhPkAJwpBwaj5rWE7nxGShkUMfR_yoTpn5Tkq-swPOc3A5bg6de4m-ceKwx0jymf7yiWxeTOYHcxEH3k1UPN9a3Q=w868-h518-no)

#### Dissemination Options
- Multicast (Hardware / IP)
	- Unreliable
	- Multiple simultaneous multicasts

- Point-to-point (TCP / UDP)
	- Expensive

- Zero extra messages: Piggyback on Failure Detector messages
	- Infection-style Dissemination

**SWIM Failure Detector Protocol**

#### Infection-Style Dissemination
- Epidemic style dissemination
	- After λlog(N) protocol periods, N^(-(2λ - 2)) processes would not have heard about an update
- Maintain a buffer of recently joined/evicted processes
	- Piggyback from this buffer
	- Prefer recent updates
- Buffer elements are garbage collected after a while
	- After λlog(N) protocol periods, this defines weak consistency

#### Suspicion Mechanism
- False detections, due to:
	- Perturbed processes
	- Packet losses, e.g., from congestion

- Indirect pinging may not solve the problem
	- e.g., correlated message losses near pinged host

- Key: **suspect** a process before **declaring** it as failed in the group

![Suspicion Mechasnism](https://lh3.googleusercontent.com/m_pzGtPdmyCiYLM6B_Xj_hxgCgZ2MxBHsJcOW5WHuFc5xNCplSRZUvxbPfjS2Wcw5t_mvOhyxsvzTUK4xDR7SPuPYozaQ8JJnR65UUc8LClsIyFD1fHElwaOVJO_TPkdKpbibhM4C0ACwwXVtTzeDvTYl4RVacnwAZLzmzyRQtLsalPpbvMwPRze5ki_v1o1wQ5n5YcG7MguXFzYO_ylL225iCHmVw-9I48ewd1e7GGAr7ucoS_S04Vz3tz7eyaF8lyqmcurqpU7gj4edPutsbknIteyu0eqLttWQBu2m_5B4zMrCTqXQ_H2DADuIrxj92r5Ho01WMDtLjP150LtFCL8qZ5iJ3TGUl01BYSANnAsjqaH1XNgSqIsStg0rQLPq_TFwxHqQqCq3hLF1mnqPBPZFwE5v0jwd0SeIWHrM-ImlOdvMDhaNuJcMGn94aFp-v-vvv5fZTu0qniZZ0rvJ8YGvNlRoE5JZAJlghdWbZxBnx0bWnUq3t2awAqFnF5EI-pvEZTi9Tk-osRFafzVpTHYY7Ar5EvIMaceVjjfpzj0_nfNmDLPwL9TepVExfDlpIkmCYySfsXni7yS3DTumvKBQFO6bbNqV4iQHiW0tWs4e74o7DDw1sjkU-GnM6QLA1FpYRECvSWH0RF_M78C9235-dUWBLYtlF6K5oziiA=w868-h362-no)

- Distinguish multiple suspicions of a process
	- Pre-process incarnation number
	- Inc # for pi can be incremented only by pi
		- Typically Pi does this when it receives a suspect Pi message.
	- Somewhat similar to DSDV (a routing protocol that is used in ad hoc networks)
- Higher inc# notifications over-ride lower inc#’s
- Within an inc#: (Suspect inc #) > (Alive, int #)
- (Failed, inc #) overrides everything else


#### Wrap Up
- Failures the norm, not the exception in datacenter
- Every distributed system uses a failure detector
- Many distributed systems use a member ship service
- Ring failure detection underlies
	- IBM SP2 and many other similar clusters/machines
- Gossip-style failure detection underlies
	- Amazon EC2/S2 (rumored!)

## Grids
### Grid Applications
#### Example: Rapid Atmospheric Modeling System, ColoState U
- Hurricane Georges, 17 days in Sept 1998
	- “RAMS modeled the mesoscale convective complex that dropped so much rain, in good agreement with recorded data”
	- Used 5 km spacing instead of the usual 10 km
	- Ran on 256+ processors
- Computation-intensive computing (or HPC = High Performance Computing)
- `Can one run such a program without access to a supercomputer?`

#### Distributed Computing Resources
![Distributed Computing Resources](https://lh3.googleusercontent.com/wJkApIlpQHJxeKok6fK9Xl81M0QegAwkNUJ2sS1bw6Xxhh61ZoJbhOFqz273BvHSWR8SrA2wsa1w8uN8x3gPLbwzgEBto0ZKeWmz7u5vTAHxEqB6P3XTxGRoS5h5qUPDQDjXSW2eUsyaqUi5zyBmKYnwtwcmCPH4Jzw_iIzFh2HIfwwECkGuf5hHVcJmuCHVq01leDK4gyzBY-czPGgB6KrbQegDCUrrXZe1kFejRsD5nmHQxph54oOMUVwUarKHJwJ6IaaCskLtUJm2XS-G-RgMTG58Ujy2c9s6q3uBoAlfuOuhff-4IsDIAlFiiivEeWRXW9jwRW5XVyv_5_jqZvoUsq1p7L9wVqsm1Tt9fiEqNvduRZAjdXiD30omU30OR-ocO3eXVHs17n1SnfUcRb9nHJ2SgwcWlNqSCDhftzCMzZaUEflkm0PhNLwMjpLsvZs6RnEavR6l6A4Qq3CcS-VRtXyI7yEmvtc03ZzHg_aHVPAW3Ngk7j6f2kOhp97Tsicu5J7X-UwFRvBIiZwQDrUbbvg8OkBaoYSCPQCOFcc_4S2VS_VwDLrz-OEYpCpDZuLW7tX9d408E49zkE7bxFmII6BX_R2dhc5vedvdBs736Wgq99x7HHwQEk0kFLf47OzL1oN4H69dxl9Fyxq0fDHMw6g2Z0ZBt2v0Y45hRg=w868-h507-no)

For example, at certain times of the day, the work stations/clusters at Madison, MIT and NCSA are free and available for running your application.

#### An Application Coded by a Physicist/Biologist/Meteorologist

![An Application Coded by a Physicist/Biologist/Meteorologist 1](https://lh3.googleusercontent.com/dh74d-bz_NYQwpp2T1GOQ1VpLk6wIkUVvF79tWzuXVt5hdOkaX3G2gxCSFlweNepdCV4cyrQanqdgYrsDynQvgrG7uhRQv3Ih6fbxgIcjwTIxY5EgEfeAC8nCMANtmoffV3nbamqnvjwoTWuhjDaTNiQV6uWTJUw6qeZCCnLaFPNEnaucwDJkuWV_fSx5kD4Fxq2OXkXk1-hlE8QbUY0hL_xQbkmzdcAOtgBkW0lv6F2F7EZ-B8ONVkOxOgeSkLlvQC-xaRIKZJzSwOF0kJS-cyEmuMlaRGR9WzZ5rvb-lhw-PsWH-m6DhwJlI2kukokLW8G_55qlatD5fcGck1mK1IcDsrbxkcqozweZurI3gHX6HKByQpJP5BmeU60kN5SlzEq-jMLAplgHI6M0KFj4KIXUJr7XcydZ1a8ur9wAYRbX2rjm7U03GNVUHmiU-yXlcEIzTnS5w0T8uUyQ6sQqjKvtj3ZtwSJddkLnRZvasIBQO4FDf1TFeq3DoDVjdk3jV97m1hgcC0W6goMUwMJ1-LGoKCedV6sFdA89pW1AE9ToQyNHNaCleYt100hWbvlBwkXCuvRc-D6zP5hQ8OtlTTcqQIkMdaf2kpsIvi_YMgf4Lm-KAnLppV5wI8bLwgj_KojAm9nJ8nqlRBJl1HlQhJTT5geMtC1aKR1uXHwIQ=w868-h511-no)

![An Application Coded by a Physicist/Biologist/Meteorologist 2](https://lh3.googleusercontent.com/hd1V_S85bk2M_PTHJ8TZH3WKHDC33DjlJs6FiqqCyhfZne_iDB1UnKjRm4U9PQfOXy-P_KlVNN4uYU9QQaIOkCH0CMh_AstBLXm8m3Ku1XFy6EgyKip1lQ61oIeXzfGxoiSR4KlcEu7saiPpV0L7mbVp2rot3piDunQ4XVHLWHbEmNUxt_nMIz_ZL1mwhVUu4dTcd7nCsuxCbqw_lhznsPByxwSdb5b3n60L3D9FNWWrXPaClzk5hvdBHRM2nN1GurPEFvFCqdnpgaMC1jmS7AOmDBA76X_IIqA46qQOeAVCRZf3x-FB4WwP5Dw7c0JOa3ZhKxddTmHscI3Fj2VOSRbazxAa0G0bnG3HIWVT30Edd3F6cjYV7uExD8JL5IeD3zk7Soyf6-bXqh-GeYoGnYyDo5HPfZAgQ8EIf1DyKxppmbT25wQlUeBup1mzhIsWXoBlsrnL7Omrc04rBDM6pZtDOIV46axBTEQQ7LSwH8I9Dtd0NRafYVT2vevLgJ1fDOIbLBqr-qI1QNzYyilsxLTc_7PlDHGCeoMTuwIJAsolx2_nd1ufcfVYE9UUo1eFzkjM0xn9cSDJqQR2Z6X8ofTJex7uZ33Sf8KIfR324aUMpj4RDSJcWukPrexwh44FUXqCpD1z6XHtitzn5MC_kSA-9TWc0sqTYu_K7EXKJg=w868-h525-no)

So how do we schedule the jobs?

### Grid Infrastructure
#### Scheduling Problem: 2-level Scheduling Infrastructure
![2-level Scheduling Infrastructure](https://lh3.googleusercontent.com/hd1V_S85bk2M_PTHJ8TZH3WKHDC33DjlJs6FiqqCyhfZne_iDB1UnKjRm4U9PQfOXy-P_KlVNN4uYU9QQaIOkCH0CMh_AstBLXm8m3Ku1XFy6EgyKip1lQ61oIeXzfGxoiSR4KlcEu7saiPpV0L7mbVp2rot3piDunQ4XVHLWHbEmNUxt_nMIz_ZL1mwhVUu4dTcd7nCsuxCbqw_lhznsPByxwSdb5b3n60L3D9FNWWrXPaClzk5hvdBHRM2nN1GurPEFvFCqdnpgaMC1jmS7AOmDBA76X_IIqA46qQOeAVCRZf3x-FB4WwP5Dw7c0JOa3ZhKxddTmHscI3Fj2VOSRbazxAa0G0bnG3HIWVT30Edd3F6cjYV7uExD8JL5IeD3zk7Soyf6-bXqh-GeYoGnYyDo5HPfZAgQ8EIf1DyKxppmbT25wQlUeBup1mzhIsWXoBlsrnL7Omrc04rBDM6pZtDOIV46axBTEQQ7LSwH8I9Dtd0NRafYVT2vevLgJ1fDOIbLBqr-qI1QNzYyilsxLTc_7PlDHGCeoMTuwIJAsolx2_nd1ufcfVYE9UUo1eFzkjM0xn9cSDJqQR2Z6X8ofTJex7uZ33Sf8KIfR324aUMpj4RDSJcWukPrexwh44FUXqCpD1z6XHtitzn5MC_kSA-9TWc0sqTYu_K7EXKJg=w868-h525-no)

#### Intra-Site Protocol
![Intra-Site Protocol](https://lh3.googleusercontent.com/Xjjdwmlt_bwtGLd42uGRk_3XMgUwnNjQfqaac0MdE564asUIsqzMuncrnCF_teqeI1xwbqEhMyssSPIBbmknnb6BSIwrse2B04XEqlCOy35KVn9DUvub_k0zoH0slsvXsHDjutXe0w6Q3ar8HZmAV6EsWthtHTiP61O8A9YEhI3sWN3Jo-12zjPEx7M0VTIb3Omu2neAa9D0E2Vt6n1fPaZWXE2aJEtsgeVo_FwyOOUSMvJnPFoc6kVnPZpHzSiUQ4Dl1htmS2shHBv1KxIOvjl9Xr1rxD7nZM9K0bj_aU97nTQsPpw-gt5mnBlmGkgjbuTV08PpMJTUliroONq-Ktmk0fRAKRRLrT4V5yugoQgxJ0kTYtkI3bXLFDf7okslSPv5Zmhe_Y1Gk9PDW1jSPYqwKxylHOR0Xzs_JJQutVDNGawSGL8Jy5zam4963RfzsgB1GoO4r_3wPoGWLsGR9mrpIFz-kDeiZFP7mukB5jPLIyTwN2sc5_A96MvQDhbzFv4MwDzNnmB_eqRXoS65eJZELzgBhOGGFU-vMb34cPRfSmd3YLdyO0QWNKL7p2_i_-kxHygI_TLUWYRZRUYHQ9Fo-hjOphubjlsrzIosBNBAd3w7ALpAiGcjpM8QT-bPfD-isSzzvTMIJDaf-2DWkrp1tqCFun3Qsa1Bf02oPw=w868-h528-no)

**Condor (Now HTCondor**)
- High-throughput computing system from U. Wisconsin Madison
- Belongs to a class of Cycle-scavenging systems

**Such systems**
- Run on a lot of workstations
- When workstation is free, ask site’s central server (or Globus) for tasks
- If user hits a keystroke or mouse click, stop task
	- Either kill task or ask server to reschedule task
- Can also run on dedicated machines

#### Inter-Site Protocol
![Inter-Site Protocol](https://lh3.googleusercontent.com/LXBWXvc2VBfFCN5J11ybV4Bd1yMt8qnw17t7fOwS4fA7nLFdP9sWws0jyvAtkPVv2bzjPenMnb4I3EpryDB3Q7lZheqIo_Uf7XPyAFQ9dycfpl4T-bqJB8KgLvTwM7rX5Br8fIVz5qnCVAPjGf0BXNKp9mm_Jfj-YS3FYIT9yj9Tv4QqmneuBErMFaa7EArFmeeb3Ie0gqUA8dqC78YgI3o55sLBiMrKGq9Aysj14KpFCkY6BIhadH0pOI8Jf3c8SDxpGwVurLTqM1OLX480QlkHbGe5KrXXt-ZqcS4B82bs0oOe5Iq21YJtgzu3ufmE4jMMgXA9zsMEPsRgn4PiWiwxY9wvrR9dV-fFxb4XrD9OnyJT02hJQcCVHKPnqMmDv5dDRN1e5xoARBksm50B-6wqQ4nUWom95OXAW3Yo8exa6er6bQLW8suPjdmaH1pAVtiNT2jcYtrcT6bB-iEiQTGMEi6EnLRMfDGCCVvnrfhmf_DUtMBNEKvco_qFnykNq1QLVh9RFjxoUYI3KqNelHBAfHPKI79-2QSIskURiE_t3DKJGNSJCcl94QtH2oHbQpYiFrGeqAwLNJW_hMYotj4HNaJQvS0EfVKEbmgjboE-ryEsvDEbV4HFdZBoLTNuaXHpZrHxVsodybEWLxmcG6YoKkn6k_Yq_3w588MCqQ=w868-h527-no)

**Globus**
- Globus Alliance involves universities, national US research labs, and some companies
- Standardized several things, especially software tools
- Separately but related: Open Grid Forum
- Globus Alliance has developed the Globus Toolkit

#### Security Issues
- Important in Grids because they are federated, i.e., no single entity controls the entire infrastructure
- `Singe sign-on`: collective job set should require once-only user authentication
- `Mapping to local security mechanisms`: some sites use Kerberos, others using Unix
- `Delegation`: credentials to access resources inherited by subcomputations, e.g., job 0 to job1
- `Community authorization`: e.g., third-party authentication

- These are also important in clouds, but less so because clouds are typically run under a central control
- In clouds the focus is on failures, scale, on-demand nature

#### Summary
- Grid computing focuses on computation-intensive computing (HPC)
- Though often federated, architecture and key concepts have a lot in common with that of clouds
- Are Grids/HPC converging towards clouds?
	- E.g., Compare OpenStack and Globus
