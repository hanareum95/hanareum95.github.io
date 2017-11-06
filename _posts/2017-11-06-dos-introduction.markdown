---
layout: post
title:  "[dos]introduction"
subtitle:   "[dos]introduction"
categories: Study
tags: OperatingSystem
comments: true
---

##### Motivation
- Resource sharing
-- ex) file server

- Computation speedup 
-- load sharing
-- ex) 천문학, 일기예보 등 큰 계산

- Reliabilty 
-- detect and recover from site failure, function transfer, reintegrate failed site
-- 한쪽에서 문제가 생겼을 때를 위한 backup

_ _ _
##### Examples of Distributed Systems
- Internet
- Automatic Teller Machines
- POS System
- Intranets( 내부망 )
- Mobile and ubiquitous computing
_ _ _
##### Characteristics of Distributed Systems
- Resource sharing
-- naming : 자원의 식별자를 모든 시스템에서 알 수 있는 이름으로 할당
-- coordination of concurrent accesses : 동시에 여러 개가 각자의 공간을 할당해달라고 요청했을 때 resource manager가 충돌이 일어나지 않도록 관리
-- provision of access transparency

- Concurrency(parallelism)

- No global clocks
-- 동기화 문제가 발생

- Independent/Dependent failures
1) Detecting failures : 사용자가 느끼기 전에 찾기
-- checksum, message loss detection by timer
2) Masking failures : 2차적인 문제가 생기지 않도록 격리
-- recovery from replicated data, retransmission 
3) Toleratingfailures : 장애 발생했을 경우 문제가 생기지 않도록 

- Fault tolerance
-- Hardware redundancy
 - 	Hot standby : main과 backup이 같이 동작

 -- Software recovery
 - Roll back of processing by Check-pointing
 - Recovery of permanent data
	
- Redundancy

- Heterogeneity : OS 위에 한 계층을 더 둠으로써 heterogeneity를 해결

- Openness ( OSI7 layer에서 layer간 interface 존재하는 것과 비슷한 개념 )

- Security
- Scalability
_ _ _
##### Design Issues

- Access transparency
	: local과 remote 리소스를 동일하게 접근할 수 있다.

- Location transparency
	: IP가 바뀌었더라도 똑같이 접근할 수 있다. 

- Concurrency transparency
- Relication transparency
	: backup 만들어서 여러 대 운영

- Failure transparency
	: Failure가 발생하지 않은 것 처럼

- Mobile transparency
- Performance transparency
- Scaling transparency
	: 규모가 늘어나도 같은 방식으로

