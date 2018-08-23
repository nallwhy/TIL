# Teraform & Ansible

## Ops

1. Infra provisioning: 네트워크/디스크/서버 등을 배치 - Terraform
2. Configuration management(=CM): OS 설치, Apache, MySQL 등 설치 - Ansible

## Cloud 에도 남아있는 문제

- 클릭 방식: 자동화가 안됨
- API 방식: 반복 실행시 문제가 생김. 실행할 때마다 계속 생김

## IaC(Infrastructure as Code)

서버의 최종 상태를 코드로 표현
Diff -> API

## IaC tools

- Aws Cloud Formation: 극악의 사용성
- Terraform: 전용 언어를 사용하여 간결. 모든 클라우드에 사용 가능.

## 수동 CM 단점

- Scalability
- OS 에 따라 다른 명령어

## 자체 Script 단점

- 무조건적인 실행: no diff
- 재사용 어려움: 몇달 뒤에 새 서버 셋업시 정확히 모두 기억 가능한가?

## Ansible

- Scalability: SSH 병렬 연결
- Package module 을 사용해서 동일 명령어 사용
- Diff 사용
- yml 로 세팅 저장해서 재사용 쉬움

### 주요 개념

- Task: module 하나 실행.
- Role: task 목록.
- Playbook: Server -> Role. ex) build -> elixir, blockchain -> docker

### 주요 파일

- hosts: tree 형태의 서버 목록
- playbook: *.yml
