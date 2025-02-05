# 사전 준비 사항

## 사전 요구 사항 (필요 설치 파일)
---
- WSL(WSL2)
- Docker Desktop(Kind)
- Git
- Chocolatey
- Kubectl
- 구축파일(.yaml)

본 프로젝트의 작업은 Windows 바탕화면에서 진행됩니다.<br>
Docker Desktop 설치 후 설정에서 kubenetes 해제 필요(기본 설정)

<img src="/DevSecOps.Full-Project/img/2-1.png" alt="Docker Desktop 설정" width="500">
<br><br><br>

## 사전 요구 사항 설치
---

Window PowerShell 관리자 권한으로 실행

###### **1) WSL(Windows Subsystem for Linux) 설치** 
Windows에서 Linux 환경을 구축할 수 있게 해주는 핵심 기능을 한다.
```md
# WSL 설치
1. dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
2. dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
# WSL2 기본 버전으로 설정
3. wsl --set-default-version 2
```

###### **2) Chocolatey 설치**
Chocolatey는 Windows용 패키지 관리자 도구이다.
```md
# Chocolatey 패키지 관리자 설치
1. Set-ExecutionPolicy Bypass -Scope Process -Force
2. [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
3. iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

###### **3) Git 설치**
Github 및 Jenkins를 통한 자동화 핵심 기능을 한다.
```md
# Git 기본 패키지 설치
1. choco install git -y
```

###### **4) Docker Desktop, kubectl 및 kind 설치**
Kind(Kubernetes IN Docker)는 Docker 컨테이너를 사용하여 Kubernetes 클러스터를 쉽게 배포하고 관리할 수 있게 해주는 도구이다.
```md
# Docker Desktop 설치
1. choco install docker-desktop -y
# kubectl과 kind 설치
2. choco install kubernetes-cli -y
3. choco install kind -y
```