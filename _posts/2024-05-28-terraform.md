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

---

- 용어
    - terraform :  AWS 인프라 리소스를 프로비저닝, 업데이트, 삭제하는 도구 
    - provider : AWS 인프라 리소스를 관리하는데 사용하는 terraform plugin 
    - resource : AWS 인프라 자원

- 테라폼 동작
    - terraform init
        - .terraform을 생성하여 provider, module, 백엔드 설정
    - terraform plan
        - 코드들을 실행하지 않고 시뮬레이션 돌리기
    - terraform apply
        - 만들어놓은 코드들을 적용하는 단계
    - terraform destroy
        - AWS 리소스 삭제

[권장] plan -> apply
[권장] fmt -> validate -> git add 해주기

- 디렉토리 및 파일
    - root module/sub module
    - 파일명 : *.tf

- 순서
    * 의존성 관계에 따라 실행
    1. vpc 생성
    2. public subnet 생성
    3. routing table 생성
    3. routing table <-> public subnet 생성
    4. security group 생성
    5. ec2 생성

1. TERRAFORM 블록
    - 블록 정의 필수아님.
1. PROVIDER 블록
    - 블록 정의 필수(region 정의 필수)
1. RESOURCE 블록
    - 숫자보단 문자, 언더바로 단어 잇기


- 변수 선언 방식
    - description(optional), type(required), default(required)
    - type(변수) = default(값)
    - type X -> any라는 뜻
    - default X -> 사용자 입력


string인 map
ptyon 

terraform에서는 변수를 너무 많이 사용하면 해석이 난해해질 때가 있음. 

문자열 내에서 참조를 하려면 "${문자열}" 형식을 사용한다. 중괄호 안에 참조를 넣을 수 있으며 테라폼은 이를 문자열으로 반환한다.  
> 예  
> resource "aws_security_group" "instance" {  
> &nbsp;&nbsp;name = "instance_${var.server_port}"     
> }  

|입력변수|출력변수|
|-----|-----|
|variable 변수로 정의|output변수로 정의|
|변수로 태그 주는 것, 선언을 해주어야 함|선언하면 실행될 때 자동으로 출력|
|var.이름.변수|`terraform apply` `terraform output`|


태그로 과금 확인하고 어떤 환경에서 쓰는지 확인 가능.   
수많은 리소스에 태그를 같은걸로 주면 태그를 바꿀 때 문제가 됨.

three teir 구조가 머임?

태그를 가지고 검색 가능 -> 많이 쓰는 방법

`git clone https://github.com/smth-hyj.git CODE`

sensitivie = true >> 민감한 값 숨기기

ARGUMENT 종류
- 일반 Argument
- 메타 Argument : 공통적으로 사용할 수 있는 인자값
    - depends_on : 순서 조율
    - count, for_each 
    - provider 
    - lifecycle : resource의 create, update, destrou 해당 동작의 수행 중 원하는 방식으로 변경해야 하는 경우 사용한다
        - create_before_destroy : 해당 리소스가 변경이 불가능한 경우(제약이 걸려있기 때문에), 이런경우 리소스를 삭제하고 업데이트된 리소스를 새로 생성하는 동작을 시행(create_before_destro =  true)
            - ex. S3 스토리지, 대상 그룹(alb 등), 등등
        - prevent_destroy
        - 
        
데이터 소스 

[추가적인 실습]
- default VPC/default Subnet 에 EC2 인스턴스 만들기
- 이 때, Data Source를 사용하여 EC2 인스턴스의 이미지를 조회하여 사용할 수 있도록 설정해야함

> data.aws_ami_instance.id

[중요한 테라폼 페이지](https://developer.hashicorp.com/terraform/language/state/remote-state-data)


ELB 를 테라폼으로 구성
health check 

data로 선언했다는 것은 기존에 선언된것을 쓰겠다는 뜻

```md
for_each = [
    [1, 2, 3] # 리스트 형식
    {k1=v1, k2=v2} # 맵 형식
    (1, 2, 3) # 셋(set) 형식
]
each.key, each.value
자동 변수
```

반드시 알아야하는 코드
1. 개발자를 위한 EC2 인스턴스 생성

```[미니 프로젝트 1]

* provier 설정
* VPC 설정
* Public subnet 설정
* Internet Gateway 설정
* Public Routing 설정
* Public Routing Table Association(Public subnet <-> Public Routing) 설정
* Public Security Group 설정

* AMI Data Source 설정
* SSH Key 생성
* EC2 Instance 생성

* User Data 
	* docker 설치
* 테스트 (SSH Connection 연결 -> docker 실행)```

2. 3-Tier 생성
    - 가장 많이 쓰이는 구조
3. CI/CD 파이프라인 코드 만들기 시간
    - CICD 파이프라인 코드 - EKS 파일 만들기