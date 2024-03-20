---
title: Linux 도커(2)
date: 2025-03-19 09:00:00 +09:00
categories: [국비, 도커]
tags: [linux, container, docker, 리눅스, centos]		# TAG는 반드시 소문자로 이루어져야함!
---

# 도커
## 도커 설치
1. 도커 설치 방법의 종류
    1. 도커 데스크탑 설치
    1. 직접 설치하는 방식

2. 직접 설치하는 방식
    - 레포지토리를 사용하여 설치
        
    ```bash
    #1. set up the repository
    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linuxcentos/ docker-ce.repo

    #2. Install Docker Engine
    sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin     docker-compose-plugin

    #3. Start Docker
    sudo systemctl enable --now docker

    ```
    
    - 설치 스크립트를 통해 설치

    ```zsh
    yum -y remove rune

    # or

    curl -fsSL https://get.docker.com -o get-docker.sh # -o 옵션은 현재 불러온 웹 요청을 저장.
    sudo sh get-docker.sh
    # 그냥 sh get-docker.sh를 하면 dockerd-rootless-setuptool.sh install 작업을 수행해줘야함

    systemctl enable --now docker
    ```

