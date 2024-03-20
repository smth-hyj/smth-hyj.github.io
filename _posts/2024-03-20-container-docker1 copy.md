---
title: Linux 도커(1)
date: 2025-03-20 09:00:00 +09:00
categories: [국비, 도커]
tags: [linux, container, docker, 리눅스, centos]		# TAG는 반드시 소문자로 이루어져야함!
---

# 도커
## 선수지식

![](https://mermaid.ink/img/pako:eNptks9L40AUx_-V4Z1ja6qtdc4ietAVurCw5DKYUQNNUtIprFsKLZsuZXVPrVClEQV_RPEQbQ9K6z_UmfkfnDQr2m7fYSaZz_f73szjVWHXNSlgYJZNi5ZDDQepYBYrUiQbAx6MxFnE2z0RdBFvP4rz63F_hDa_IhE8y44f85j06_K0k3jFcCDboTxuInnaHT-9IoyE3-NPfoI_B0bjqC5-NXj4LI4u5nExDGXzWAQD7rfmcXkSilY3IRvpbx8l-d9IuaQfqeIjtU2bVeLXDr_siVFdqUSzO4s_Px0lsDCV_j7kv-sqA--czHq3F5hFPcSjO3EUzEJ-24rv1XiIq6u2vPjiz9V_l5v0i988TFhC45a_6_-9SSm_OAs7HrWtMp3XnU1CyukdQgrpglrmKdbVOWhgU88mlqnmoBqrDGAH1KYGYPVp0j1SKTIDDKempKTC3MKhswuYeRWqQaVkEkbXLLLvERvwHimW1WmJON9dd-ofcBV-AF7U4BCwrudSuXx2OacvZ7IreT2Tr2nwc-JYTK0msaLnM0uZ7JKuATUt5npbyahOJrb2BoItDuU?type=png)

- 온프로미스 vs 클라우드
    - 온프로미스 
        - 인프라 환경 구축을 직접 다 하는 것(물리적이든 아니든)
    - 클라우드
        - 인프라 환경 구축을 가상화하여 하는 것

- CLOUD 가상화
    - network
    - server
    - service
    - storage

컨테이너(MSA: micro service architecture)

- 클라우드 서비스 모델
    - IaaS(Intrastructure as a Service)
    - PaaS(Platform as a Service)
    - SaaS(Service as a Service)
    - FaaS(Function as a Service)
- 클라우드 배포 유형
    - 프라이빗 클라우드(Private Cloud)
    - 퍼블릭 클라우드(Public Cloud)
    - 하이브리드 클라우드(Hybrid Cloud)
    - 멀티 클라우드(Multi Cloud) :

하드웨어와 네트워크 구조

OSI 7 Layer & TCP/IP 5 Layer
- OSI 7 Layer
    - OSI 참조 모델(OSI Reference Model, OSI 7 Layer)은 국제 표준화 기구 ISO가 책정한 컴퓨터의 통신 기능을 계층 구조로 나눈 개념 모델이다. 
    - 계층화 함으로써 다양한 기술들의 상호연결성을 확보한다.

|ISO OSI 7 Layer| TCP/IP 5 Layer|
|-------|-------|
|7계층  Application Layer|5계층  Application Layer|
|6계층  Presentation Layer|5계층  Application Layer|
|5계층  Session Layer|5계층  Application Layer|
|4계층 Transport Layer|4계층  Transport Layer|
|3계층  Network Layer|3계층  Internet Layer|
|2계층  Data Link Layer|2계층  Network Interface Layer|
|1계층  Physical Layer|1계층  Physical Layer|

RDBMS/SQL

- NoSQL
    - Key Value Store(KVS)
        - 키: 값1 / 값1:값2 형식
        - ex. Redis, Memchached
    - Document Database
        - ex. MongoDB
    - Column-Family
        - 컬럼이 엄청 많음
        - ex. HBase, Cassandra

- 시스템 감시 툴
    - Datadog
    - Zabbix
    - Prometheus
    - Fluentd + InfluxDB + Grafana

### 인프라 구성 관리 기초 지식

Iac(Terraform, Ansible, ...)

CI/CD

## 컨테이너
1. 컨테이너란
    - 호스트 OS상에 논리적인 구획을 만들고, 애플리케이션을 작동시키기 위해 필요한 모든것 (lib, cmd, ...)을 모아서 마치 별도의 서버인것 처럼 사용할 수 있는 기술이다.
2. 컨테이너 기술들의 종류
    1. Docker
    2. LXC
    3. LXD
    4. ...

## 도커
[도커 참고 사이트01](https://docs.docker.com)
- 도커란
    - 컨테이너 기술의 하나로 애플리케이션을 개발, 제공, 실행하기 위한 개방형 플랫폼이다.

- 도커 기능
    - build
    - ship/share
    - run

- 도커 에디션
    - Docker CE(Community Edition)
    - Docker EE(Enterprise Edition)
    
- 도커 구성요소들
    - Docker Engine:
    - Docker Object:
    - Docker Registry:
    - Docker Compose:
    - Docker Swarm:(쿠버네티스로 대체할 예정)

- 도커 기반 기술
    - Chroot
    - namespace
    - cgroups  
++
    - network(bridge)
    - storage(Overlay FS2)
