---
title: Terraform 기초 과정 (1)
date: 2024-05-24 09:00:00 +09:00
categories: [국비, terraform]
tags: [linux, cloud, 테라폼, terraform]		# TAG는 반드시 소문자로 이루어져야함!
---

## 테라폼 개요

- IaC (Infrastructure as Code)
    - 인프라를 코드로 관리
    - 코드를 넣으면 그림으로 인프라 구조를 보여주는 것도 있음

- 코드형 인프라
    - 코드를 작성 및 실행하여 인프라를 생성, 배포, 수정, 정리하는 것
    - 코드 == 인프라
    - ex. Ansible, Terraform
        - 앤서블과 테라폼을 섞어쓰는게 좋다.
    - 종류
        - 애드혹 스크립트 : Shell 스크립트(Bash), Ruby, Python, Perl
            - 소규모의 일회성 관리에 적합
        - 구성관리 : Ansible, 셰프, 퍼핏, 솔트 스택
            - 역등성 보장
        - 서버 템플릿 : Packer(이미지 빌더), Docker(컨테이너), Vagrant
            - 불변 인프라로 전환하기 위한 핵심 요소
        - 오케스트레이션 : Kubernetes, Docker Swarm...
        - 프로비전 : Terraform
            - 재사용성, 문서화 보장

- Terrform 동작(다음장에서 더 자세히 설명)
    - Refresh (클라우드환경과 실제 환경의 Sync를 맞추는 동작)
    - Plan (현재 상태에서 최종 상태를 확인하는것)
    - Apply (현재 상태 파악)
    - Destory (삭제)

&nbsp;    

![구성관리vs프로비저닝](https://cdn.itdaily.kr/news/photo/202110/204606_205168_410.jpg)

구성 관리 vs 프로비저닝 비교


- 가변 인프라 vs 불변 인프라
    - 가변 인프라 : Ansible 
    - 불변 인프라 : Terraform

- 절차적 언어 vs 선언적 언어
    - 절차적 언어 : Ansible
        - 하나씩 점검(기존것도 점검)
        - 마지막 상태 정보를 기록하지 않아서 느림
        - 초기 인프라 구축에 유리
    - 선언적 언어 : Terraform
        - 마지막 상태 정보를 기점으로 작동


```markdown
## Terraform + Ansible
+--------+
| App    | 	 <-----   Ansible
+--------+	 <----+
| Server |		|
+--------+		+-- Terraform
| Infra  | 	   	|
+--------+	 <----+

## Terraform + Packer
+--------+
| VM     | 	 <-----   Packer/vagrant
+--------+	 <----+
| Server |		|
+--------+		+-- Terraform
| Infra  | 	    |
+--------+	 <----+

## Terraform + Packer + Docker
+----------+
| Container| 	 <-----   Docker/kubernetes
+----------+
| VM       |	 <-----   Packer/vagrant
+----------+	 <----+
| Server   |		|
+----------+		+-- Terraform
| Infra    |	    |
+----------+	 <----+
```


## Terraform 


[중요] 테라폼 코드 작성 시 반드시 필요한 사이트  
https://developer.hashicorp.com/terraform/language  
https://registry.terraform.io/providers/hashicorp/aws/latest/docs  

block 인수 value

terraform plan : 시뮬레이션 작업을 하는 것
(+) 추가
(-) 삭제
(~) 수정

.gitignore 