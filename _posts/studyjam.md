


# 쉘 스크립트 / 쉘 프로그래밍

## 1. 쉘 스크립트 작성시 선수지식
- 개요 
    - 쉘에서 실행되는 종류
    - 앨리어스(alias) / 함수
    - 디스크 내에 존재하는 명령어(ex. /bin/sh)

1. 필수 명령어 :
    - **grep**
        - 옵션들 : -i(대소문자 구분X), -n(라인넘버), -v(제외), -w(정확히 일치), -r(recursive), -A(append, after)
        - 패턴 : *, ^root, root$, [abc], [a-c], [^a]
        - ***주의*** : grep 명령어의 pattern 부분에 변수로 지정하는 경우
            > PATTERN=root
            > grep 'PATTERN' /etc/passwd (X)
            > grep "PATTERN" /etc/passwd (O)
            > 패턴은 큰 따옴표일때만 해석
        - fgrep 고정

    - **sed** : stream editor
        - sed [-n] 'addressCMD' file1
            - address : addr1, addr2
            - CMD : p, d, s
            - -n(not default) : 원래 file1을 한번 출력하는 특성이 있는데 이를 하지 말아라
        - sed [-n] '/pattern/CMD' file1
        - sed [-n] 's/pattern1/pattern2/' file1
            > 이 때 슬래쉬는 다른 걸로 대체 가능함
            - sed -i를 붙이면 파일안에 내용을 편집 가능(원래는 복사본으로 보여주는것)
            - p랑 d 도 있음
    - **awk**
        - C언어에서 쓰는 명령어 다 쓸 수 있음
        - awk 'statement' file1
        - awk '{action}' file1
        - awk 'statement {action}' file1
        - $ > 필드 출력 
            > $0 : 모든 필드
    - 기타 명령어
        - sort
        - cut
        - uniq
        - tee 

2. 쉘의 특성 :
    - 리다이렉트
    - 쉘 기능
    - 변수 
    - 메타 캐릭터
    - 앨리어스 
    - 환경 파일  
     ++
    - 배열, 맵
    - Here Documentation
    - Grouping
    - 조건부 실행
    - 디렉토리 경로/파일 이름
    - 한 번 더 평가 

## 2. 쉘 스크립트 문법
- vscode 설치
- 쉘 프로그래밍 문법
    - 프로그램 작성 및 실행
        - && => 앞이 참이고 뒤도 참이어야 실행
        - ; 그냥 실행
    - 주석
    - 입출력
    - 산술연산
    - 조건문 
        - if fi
    - 반복문
        - for do done
        - while do done
        - until do done
    - 함수
        - 함수 문법 

            ```bash
            # 함수 선언
            fun1() {
                문장
            }
            fun1 #함수 사용
            # 함수 입출력
            fun1() {
                arg1=$1
                arg2=$2

                # 문장

                echo ""
            }
            ```

    - IO redirection
    - ...

## 3. 쉘 프로그래밍
- 실습 
