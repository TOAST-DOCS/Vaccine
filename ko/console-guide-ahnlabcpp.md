## Security > Vaccine > 콘솔 사용 가이드 > AhnLab(AhnLab CPP)

여기에서는 Vaccine Agent 활성화 및 비활성화 절차와 서비스 사용법을 설명합니다.

## 보안 그룹(Security Group) 설정

백신 서버와 통신하려면 보안 그룹에 아래 내용을 추가합니다.

| 방향 | 포트 | 리전 | CIDR |
| --- | --- | --- | ---- |
| Egress | 4119, 4120, 4122 | 한국(판교), 한국(평촌) | 114.110.144.39/32 |

## Vaccine Agent 활성화 절차

인스턴스의 이미지 OS에 따라 백신 설치 스크립트를 불러옵니다.

![vaccine_01_ko_2021_06.png](https://static.toastoven.net/prod_vaccine/vaccine_01_ko_2021_06.png)

### Linux 계열 Agent

1\. 설치 스크립트를 복사하려면 **클립보드 복사**를 클릭합니다.

2\. 설치 대상 인스턴스 터미널에 접속합니다.

3\. 관리자 권한으로 Agent 스크립트를 생성하고 실행합니다.

* vi 편집기 등으로 스크립트를 생성합니다.
* 생성한 스크립트 파일의 권한을 변경합니다.
* 파일을 실행합니다.
```
[root@vaccine-test ~]# cd ~
[root@vaccine-test ~]# vi agent.sh
[root@vaccine-test ~]# chmod 744 agent.sh
[root@vaccine-test ~]# ./agent.sh
/tmp/DownloadInstallAgentPackage: OK
Downloading agent package ...
curl https://114.110.144.39:4119/software/agent/RedHat_EL7/x86_64/ -o /tmp/agent.rpm --insecure --silent
Installing agent package ...
Preparing...                          ################################# [100%]
Updating / installing...
   1:ds_agent-10.0.0-2775.el7         ################################# [100%]
Starting ds_agent (via systemctl):  [  OK  ]
HTTP Status: 200 - OK
Activation will be re-attempted 30 time(s) in case of failure
dsa_control
HTTP Status: 200 - OK
Response:
Attempting to connect to https://114.110.144.39:4120/
SSL handshake completed successfully - initiating command session.
Connected with (NONE) to peer at 114.110.144.39
Received a 'GetHostInfo' command from the manager.
Received a 'GetHostInfo' command from the manager.
Received a 'SetDSMCert' command from the manager.
Received a 'SetAgentCredentials' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetInterfaces' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetAgentStatus' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetHostMetaData' command from the manager.
Received a 'SetSecurityConfiguration' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetAgentStatus' command from the manager.
Command session completed.
[root@vaccine-test ~]#
```

### Windows 계열 Agent

1\. 콘솔 스크립트를 복사합니다.

2\. 설치 대상 인스턴스 터미널에 접속합니다.

3\. 관리자 권한으로 Agent 스크립트를 생성하고 실행합니다.

* 메모장과 같은 텍스트 에디터로 스크립트 파일을 생성합니다.
* 관리자 권한으로 **명령 프롬프트**(cmd) 창을 활성화합니다.
* powershell -file "파일 경로/파일명" 형태로 실행합니다.
```
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Users\Administrator>powershell -file "agent.ps1"


    디렉터리: C:\Users\Administrator\AppData\Roaming\Trend Micro\Deep Security Agent


Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----      2018-06-05   오후 2:37            installer
기록이 시작되었습니다. 출력 파일은 C:\Users\Administrator\AppData\Roaming\Trend Micro\Deep Security Agent\installer\dsa_deploy.log입니다.
오후 2:37:23 - DSA download started
오후 2:37:23 - Download Deep Security Agent Package
https://114.110.144.39:4119/software/agent/Windows/x86_64/
오후 2:37:24 - Downloaded File Size:
13897728
오후 2:37:24 - DSA install started
오후 2:37:24 - Installer Exit Code:
0
오후 2:37:32 - DSA activation started
HTTP Status: 200 - OK
Activation will be re-attempted 30 time(s) in case of failure
dsa_control
HTTP Status: 200 - OK
Response:
Attempting to connect to https://114.110.144.39:4120/
SSL handshake completed successfully - initiating command session.
Connected with AES256-SHA256 to peer at 114.110.144.39
Received a 'GetHostInfo' command from the manager.
Received a 'GetHostInfo' command from the manager.
Received a 'SetDSMCert' command from the manager.
Received a 'SetAgentCredentials' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetInterfaces' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetAgentStatus' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetHostMetaData' command from the manager.
Received a 'SetSecurityConfiguration' command from the manager.
Received a 'GetAgentEvents' command from the manager.
Received a 'GetAgentStatus' command from the manager.
Command session completed.
기록이 중지되었습니다. 출력 파일은 C:\Users\Administrator\AppData\Roaming\Trend Micro\Deep Security Agent\installer\dsa_deploy.log입니다.
오후 2:38:29 - DSA Deployment Finished

C:\Users\Administrator>
```
### 사용 시작

![vaccine_02_ko_20210628.png](https://static.toastoven.net/prod_vaccine/vaccine_02_ko_20210628.png)

새로고침을 클릭하면 현황 목록에 설치된 Agent 정보가 표시됩니다.
**사용시작** 버튼을 클릭하면 서비스 사용이 시작됩니다.

## Vaccine Agent 비활성화 절차

![vaccine_03_ko_210628.png](https://static.toastoven.net/prod_vaccine/vaccine_03_ko_210628.png)

1\. 웹 콘솔 사용 중지

* **사용종료** 버튼을 클릭하여 백신 사용을 중지합니다.
### Linux 계열 Agent
* 인스턴스에 접속하여 Vaccine Agent를 삭제합니다.
    * CentOS: rpm -e ds_agent 실행
    * Debian/Ubuntu: apt-get remove ds-agent 실행

### Windows 계열 Agent
* 인스턴스에 접속하여 Vaccine Agent를 삭제합니다.
    * 프로그램 및 기능 메뉴에서 **Trend Micro Deep Security Agent**를 삭제합니다.

## Vaccine 서비스 사용법
