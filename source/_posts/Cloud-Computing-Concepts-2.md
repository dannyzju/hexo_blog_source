---
title: Cloud Computing Concepts Notes 2
date: 2017-03-14 08:23:37
toc: true
categories: tech
tags:
- 学习笔记
- tech
---

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
(To be completed)

## Grids
(To be completed)
