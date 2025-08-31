# VPC

이 랩은 기본 VPC 네트워킹의 다양한 기능을 구성하는 환경입니다. EC2 컴퓨팅 랩을 완료하였다면, Task3 전단계에서 Private EC2 인스턴스와 Bastion Host만 구성하고, Task 3를 진행하면 됩니다.

Amazon Virtual Private Cloud(VPC)를 사용하면 AWS 클라우드에서 논리적으로 격리된 공간을 프로비저닝하여 고객이 정의하는 가상 네트워크에서 AWS 리소스를 시작할 수 있습니다. IP 주소 범위 선택, 서브넷 생성, 라우팅 테이블 및 네트워크 게이트웨이 구성 등 가상 네트워킹 환경을 완벽하게 제어할 수 있습니다. VPC에서 IPv4와 IPv6를 모두 사용하여 리소스와 애플리케이션에 안전하고 쉽게 액세스할 수 있습니다.

Amazon VPC의 네트워크 구성을 손쉽게 사용자 지정할 수 있습니다. 예를 들어, 인터넷에 액세스할 수 있는 웹 서버를 위해 퍼블릭 서브넷을 생성할 수 있습니다. 또한 인터넷 액세스가 없는 프라이빗 서브넷에 데이터베이스나 애플리케이션 서버 같은 백엔드 시스템을 배치할 수 있습니다. 보안 그룹 및 네트워크 액세스 제어 목록을 포함한 다중 보안 계층을 사용하여 각 서브넷에서 Amazon EC2 인스턴스에 대한 액세스를 제어하도록 지원할 수 있습니다.

본 랩은 아래와 같은 구성을 통해 VPC 기반의 네트워킹을 통해 클라우드 자원을 효과적으로 연결, 제어하고 모니터링하는 방법을 익히도록 합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VSimvfblK5NQ9gpc0%2F-M6VTQMcHl71u2K_6WTl%2Fimage.png?alt=media\&token=89f0453d-06fb-471d-afff-6d91c0d5ed5d)

* **System Manager 기반 Session Manager 구성**

EC2-Linux 또는 EC2-Windows 랩을 구성한 경우, Task1을 수행할 필요 없습니다.

* **"AWS Management Console - AWS 서비스"** 에서 **"서비스 찾기"** 창에 VPC를 탐색하고, VPC를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PHh4_CNXHD0kY5p93%2Fimage.png?alt=media\&token=11fd73be-e222-4179-8650-530bbb349f94)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PHqQEjmSxAzewDCzq%2Fimage.png?alt=media\&token=3bd7021b-a9e4-4ef6-889b-c8836aa24fd4)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6K4hZYDLSJ1uAcvM4c%2Fimage.png?alt=media\&token=acdd1cbd-2b28-4b59-b970-27a43e9de0d3)

* **이름 태그** : VPC 이름 태그를 입력합니다.
* **IPv4 CIDR 블록** : VPC에서 사용할 IPv4 주소 대역을 입력합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PHuMOY_AVA7H-OXyG%2Fimage.png?alt=media\&token=18e8203e-6e66-4b3d-9c1c-8f73bd6cf8b2)

* 생성되는 EC2 인스턴스의 DNS Name 서비스 활성화를 위해, **"작업"**&#xC744; 선택하고 **"DNS 호스트 이름 편집"**&#xC744; 선택합니다. **DNS 호스트 이름을 활성화**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PHzf-2pwN9wVZyQZR%2Fimage.png?alt=media\&token=5904199b-f65c-4bcd-8622-a2e45c5032e8)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PI1kB1H0aeW5kWYL2%2Fimage.png?alt=media\&token=9c521c15-955c-47c3-8a8e-98f1a07c9c42)

#### **5.Public ,Private 서브넷 생성.** <a href="#id-5.public-private" id="id-5.public-private"></a>

* 좌측 VPC 대시보드에서 **"가상 프라이빗 클라우드" - "서브넷"** 메뉴를 선택하고, **"서브넷 생성"**&#xC744; 선택합니다.
* 4개의 서브넷을 각각 생성하고, 속성을 정의합니다.

Public 서브넷은 Internet Gateway와 1:1 NAT로 직접 연결 가능한 네트워크 범위를 의미합니다. Private 서브넷은 외부로 직접 노출될 수 없으며, 외부와 연동하기 위해서는 Source NAT를 사용하는 방법으로 NAT 기능을 지원하는 인스턴스 또는 NAT Gateway 등과 같은 서비스를 사용해야 합니다.

| **서브넷 이름 태그** | 가용영역            | **IPv4 CIDR 블록** |
| ------------- | --------------- | ---------------- |
| IMD-PUBLIC-A  | ap-northeast-2a | 10.1.1.0/24      |
| IMD-PUBLIC-B  | ap-northeast-2c | 10.1.2.0/24      |
| IMD-PRIVATE-A | ap-northeast-2a | 10.1.11.0/24     |
| IMD-PRIVATE-B | ap-northeast-2c | 10.1.12.0/24     |

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PI7GbGiJOb8jCRmvb%2Fimage.png?alt=media\&token=2470c78e-04a0-4ac2-99a7-6355eb90ed78)

* 4개의 서브넷이 정상적으로 구성되어 있는지 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIBIidaI5s0FHy_et%2Fimage.png?alt=media\&token=9e49c1bc-a46b-4447-a40c-77b9446ddfb5)

|   |                              |
| - | ---------------------------- |
|   | IMD-PUBLIC-A , IMD-PUBLIC-B  |
|   | IMD-PRIVATE-A, IMD-PRIVATE-B |

* 좌측 VPC 대시보드에서 **"가상 프라이빗 클라우드" - "라우팅 테이블"** 메뉴를 선택하고, **"라우팅 테이블 생성"**&#xC744; 선택합니다.
* 2개의 라우팅 테이블을 각각 생성하고, 속성을 정의합니다.

라우팅 테이블은 서브넷과 연동하여 구성됩니다. 각 서브넷이 목적지로 가기 위한 경로들의 정보를 담고 있습니다. 여러개의 서브넷을 묶어서 연동할 수도 있고, 개별로 구성할 수도 있습니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIHShd-WlKpf7CMuh%2Fimage.png?alt=media\&token=0610e808-76bb-4c48-ba76-6a51bbdacb97)

* 각 라우팅 테이블에 서브넷을 연결합니다. PUBLIC-RT, PRIVATE-RT 모두 구성합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIMRq3AywxJ904JAJ%2Fimage.png?alt=media\&token=c18648b4-f8ee-477a-b275-4e388573b30a)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIPzUjJ7P2IYqLfuZ%2Fimage.png?alt=media\&token=7e44c8bd-060a-4523-b197-c76fae6d7693)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PISPxwHrGSxB0U2gp%2Fimage.png?alt=media\&token=ab286ece-f712-4ebb-90d2-3b47ffc3f6d2)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIVAFN4Ravkw4GXJU%2Fimage.png?alt=media\&token=f5df2552-413e-4805-8d14-3f2d3373f740)

* 좌측 VPC 대시보드에서 **"가상 프라이빗 클라우드" - "인터넷 게이트웨이"** 메뉴를 선택하고, **"인터넷 게이트웨이 생성"**&#xC744; 선택합니다.

인터넷 게이트웨이는 VPC 내부 네트워크가 외부와 연결되는 구성을 담당합니다. 인터넷 게이트웨이는 한개의 VPC에 연결되며, 퍼블릭 서브넷의 인스턴스들과 1:1 NAT를 완전 관리형으로 제공합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KELe0eYjM4ljb0nhl%2Fimage.png?alt=media\&token=cafe7a2f-2f68-4c5a-b88c-a0d39c8c7a24)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PI_XmMBlfrxccWHI2%2Fimage.png?alt=media\&token=9d0ad779-25c8-46b5-939e-c2cbc8648171)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIcWrp5SEdM0jaM5s%2Fimage.png?alt=media\&token=9c2a98f1-bab9-4f66-bf64-2e7d30efa381)

* Public-RT 라우팅 테이블에 인터넷 게이트웨이로 향하는 트래픽을 업데이트하기 위해, "**라우팅 테이블" - "PUBLIC-RT"**&#xB97C; 선택하고 **"라우팅 편집"**&#xC744; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6KnDdNi1Xw4AdNjjfr%2F-M6KskjBCLDRjo2R7WCa%2Fimage.png?alt=media\&token=d620a166-c890-4b6b-978c-4035b8711783)

* **"라우팅 추가"**&#xB97C; 선택하고, "**대상"**&#xC5D0; "**0.0.0.0/0"**, **"생성한 IGW"**&#xB97C; 입력하고 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PFwM4pyfkgFoPnfhr%2F-M6PIm9ts7dnkZGraFR7%2Fimage.png?alt=media\&token=93f06643-fa25-4639-91ed-93935d47d803)

**EC2 Computing 랩을 완료한 경우, Bastion EC2 인스턴스만 생성하고, Task3으로 이동합니다.**

**키 페어는 1회 다운로드 이후, 다시 다운로드 받을 수 없습니다. 키 페어를 통해 EC2 인스턴스에 접속하기 때문에 키페어 다운로드 위치를 반드시 파악해 두고 잘 관리해야 합니다.**

* EC2 대시보드에서 **"네트워크 및 보안" - " 키 페어"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PN5eBjkopnaXrYaNw%2F-M6PNRTM6UvYz_jnMBLE%2Fimage.png?alt=media\&token=25199c90-360f-4e19-aba9-a8f46b37b0cb)

* Mac OS , Linux 계열의 OpenSSH 사용자는 파일형식을 pem을 선택하고, Window OS 계열의 Putty 사용자는 파일형식을 ppk를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PN5eBjkopnaXrYaNw%2F-M6PNWeCUPRePT-aLCsc%2Fimage.png?alt=media\&token=16503299-ed25-479d-84d7-ad632cd4277f)

#### **10. EC2 대시보드에서 인스턴스 시작을 선택.** <a href="#id-10.-ec2" id="id-10.-ec2"></a>

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KFn47SxffJUk3TCx5%2Fimage.png?alt=media\&token=abaf33f2-6d41-40e2-8294-00fc34ae3ee8)

* **Amazon Linux2 AMI(Amazon Machine Image)** 를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KGD3pUJsNO18d_zbM%2Fimage.png?alt=media\&token=66efc91e-cfbf-4597-b47a-4343a9d816b4)

* **인스턴스 유형 - t2.micro** 를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KGQCgRkGXMSk74Uai%2Fimage.png?alt=media\&token=a21754a9-0143-4e46-9732-df72ea4899da)

|   |                                 |
| - | ------------------------------- |
|   |                                 |
|   |                                 |
|   | IMD-PUBLIC-A \| ap-northeast-2a |
|   |                                 |

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KI03hwbHAVphna3Xu%2Fimage.png?alt=media\&token=111f2c16-81fa-4c05-bc32-09879be08033)

sudo yum -y install yum-utils

sudo yum -y install httpd php mysql php-mysql git

sudo systemctl start httpd

sudo systemctl enable httpd

sudo git clone https://github.com/whchoi98/ec2meta-webpage.git

sudo systemctl restart httpd

* 위의 "사용자 데이터 예"를 복사해서 값을 입력합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KISFW75ipHvBKGOKt%2Fimage.png?alt=media\&token=e740f8aa-c839-4190-876d-7d77aa60b214)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KJ3iuHFTkCf4Q8WtP%2Fimage.png?alt=media\&token=336f32ea-733b-455c-9ee7-7c539805ead6)

* AWS에서 제공하는 볼륨 유형들을 확인합니다.
* **키 : IMD-EC2 , 값: PUBLIC-01**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PN5eBjkopnaXrYaNw%2F-M6POLrhj3yqP7BsX4Jx%2Fimage.png?alt=media\&token=4b303bfe-3a34-4bbd-a819-44131330eac2)

* 아래와 같은 값으로 보안 그룹(Security Group)을 구성합니다.

| 유형           | 프로토콜 | 포트범위    | 소스   |
| ------------ | ---- | ------- | ---- |
| SSH          | TCP  | 22      | 위치무관 |
| HTTP         | TCP  | 80      | 위치무관 |
| HTTPS        | TCP  | 443     | 위치무관 |
| 모든 ICMP-IPv4 | ICMP | 0-65535 | 위치무관 |

* 설명 : Security Group for IMD-PUB

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KL3waN-V1j9B-CNbl%2Fimage.png?alt=media\&token=a0741cfe-3f0e-45a8-be87-fe765a484e56)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6JzjpaRV3UoXw5hf__%2F-M6KLN0N-p1E08Owwsk-%2Fimage.png?alt=media\&token=c191ce4a-7ede-4e23-9471-ea81c7ff9a0e)

* **"기존 키 페어 선택"을 선택하고 , 해당 키페어를 선택합니다.**(예. IMD-LAB-PUTTY)
* **"인스턴스 시작"**&#xC744; 선택해서 인스턴스를 생성합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PN5eBjkopnaXrYaNw%2F-M6POkdl-dbyPJDNW8_w%2Fimage.png?alt=media\&token=4f44d369-1e87-4488-a667-81d03f49a8ff)

**위의 과정을 반복하여, 아래표의 인스턴스들을 추가로 생성합니다.**

| EC2 인스턴스 이름 / 태그   | 서브넷           | 서브넷 주소 대역    | 가용영역            | 보안그룹           |
| ------------------ | ------------- | ------------ | --------------- | -------------- |
| IMD-EC2 PUBLIC-01  | IMD-PUBLIC-A  | 10.1.1.0/24  | ap-northeast-2a | IMD-PUB-SG     |
| IMD-EC2 PUBLIC-02  | IMD-PUBLIC-B  | 10.1.2.0/24  | ap-northeast-2c | IMD-PUB-SG     |
| IMD-EC2 PRIVATE-01 | IMD-PRIVATE-A | 10.1.11.0/24 | ap-northeast-2a | IMD-PRI-SG     |
| IMD-EC2 PRIVATE-02 | IMD-PRIVATE-B | 10.1.12.0/24 | ap-northeast-2c | IMD-PRI-SG     |
| BASTION            | IMD-PUBLIC-B  | 10.1.2.0/24  | ap-northeast-2c | IMD-BASTION-SG |

### Task3: NAT Gateway 구성 및 Private 서브넷 연결 <a href="#task3-nat-gateway-private" id="task3-nat-gateway-private"></a>

NAT Gateway는 Private Subnet의 외부 통신을 위한 Source NAT를 제공하는 AWS NAT 완전관리형 서비스 입니다.

* **VPC - 가상 프라이빗 클라우드 - NAT 게이트웨이 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVv7Qk8YFdYgF0hNUZm%2F-MVv7xbtg15KffBa-wyy%2Fimage.png?alt=media\&token=01e38de7-ee80-4ca1-90d6-9be3400865e2)

NAT 게이트웨이 생성 메뉴에서 아래와 같은 값을 입력합니다.

* **탄력적 IP 할당 ID - 탄력적 IP 할당 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVv7Qk8YFdYgF0hNUZm%2F-MVv8PCeivM-3xsVGSEn%2Fimage.png?alt=media\&token=40107519-6b2d-4471-9f81-19045d99db49)

NAT 게이트웨이 생성이 완료되면 다음과 같은 화면을 확인 할 수 있습니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvABoUtHkyGr1vMuyZ%2F-MVvAnvVRJzaEs_U5Dxf%2Fimage.png?alt=media\&token=d6a10d4c-f3bf-4d48-93bf-7e16b633333e)

#### 20. Private Routing Table 구성 <a href="#id-20.-private-routing-table" id="id-20.-private-routing-table"></a>

Private Subnet을 위해서 라우팅 테이블에 NAT 게이트웨이 경로를 추가합니다.

* **VPC - 가상 프라이빗 클라우드 - 라우팅 테이블 - PRIVATE-RT 선택 - 라우팅 탭 - 라우팅 편집 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvABoUtHkyGr1vMuyZ%2F-MVvBHXYbKv8dZmaLmxd%2Fimage.png?alt=media\&token=b5069785-780b-42eb-a818-818bf22bf838)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6PYaeXLRq9Pk09CIA6%2F-M6PZMq_Qq1l-lMfTwzu%2Fimage.png?alt=media\&token=0a9d2bbe-44c5-4c21-9d96-1b303dfff3d8)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvABoUtHkyGr1vMuyZ%2F-MVvBk91Po1-951pCofQ%2Fimage.png?alt=media\&token=d66ceb9e-f166-4e4c-ba7b-6a48c0595878)

**Task4. Private Network 연결을 완료한 이후에는 NAT Gateway를 통해 Private EC2에서 외부망으로 연결이 가능하지 확인 할 수 있습니다.**

### Task4: Private Network 연결. <a href="#task4-private-network" id="task4-private-network"></a>

Private Network은 외부에서 직접 접속이 불가능 하기 때문에 , 여러가지 방법을 통해 접속이 가능합니다.

* AWS 관리 콘솔에서 EC2를 위한 Session Manager 기반으로 접속
* Client 측에서 AWS CLI - Session Manager Plugin을 통한 콘솔 접속
* Public 서브넷에 Bastion Server를 배치하여, SSH Agent Forwarding을 통한 접속
* Public 서브넷에 Bastion Server를 배치하여, SSH Proxy Tunneling을 통한 접속

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6T2w2IDj0HYgsNb_V8%2F-M6T4x9Ie3K9YkWB0NWX%2Fimage.png?alt=media\&token=15c860ae-a12d-47b7-bd88-c91a30ec9a71)

#### 21. Bastion Server 기반 Private EC2 접속 <a href="#id-21.-bastion-server-private-ec2" id="id-21.-bastion-server-private-ec2"></a>

* Private Subnet에 위치한 EC2 인스턴스는 외부에서 직접 연결할 수 없습니다. Bastion Server는 이러한 이슈를 해결하기 위해 Public Subnet에 서버를 설치하고 SSH port를 허용하고, Bastion Server를 통해 내부의 Private EC2에 연결할 수 있습니다. 아래 그림은 외부 SSH Client에서 Private EC2 인스턴스를 Bastion Server를 통해 연결하는 논리적 흐름입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6T5QXQTohkw7VoBwDb%2F-M6TlTTMljaSL0xULp7H%2Fimage.png?alt=media\&token=aec5305a-f561-470a-9f80-2c5aefe6317a)

* **Linux/Mac OS 환경일 경우 (Window 사용자의 경우 생략 합니다.)** 먼저 Linux/Mac OS의 OpenSSH Client를 기반으로 Bastion Host를 통해 접속하는 방법을 살펴봅니다. SSH Client에서 아래와 같은 명령으로 key를 저장합니다.(ssh-add -K는 로컬에 Key를 저장해 두는 명령입니다.)

ssh-add -K "key\_path/key.pem"

* 저장된 Key값을 확인합니다. (ssh-add -L 은 저장된 key값을 보여주는 명령입니다.)
* Bastion Server에 정상적으로 접속이 완료되면 연결을 원하는 Private EC2 인스턴스에 SSH로 접속합니다.

ssh -i "key\_path/IMD-PUB-OPENSSH.pem" ec2-user@PUBLIC\_DNS -A

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UCXvlBscRNGFBQ1E9%2Fimage.png?alt=media\&token=54423518-664f-4e3f-827c-986ca05096d8)

* **Windows 환경의 Putty 사용자일 경우** Windows 환경의 Putty 프로그램에서는 아래와 같이 Bastion Host 접속을 위해 설정합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UBbQiRGkSWy3YxMN9%2Fimage.png?alt=media\&token=8f8df0fa-8268-4230-8f58-f15aa8c818cb)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UC1huqDyyT_AVUYJH%2Fimage.png?alt=media\&token=26edb03d-08cd-4038-ba86-1f86cad66c68)

Linux/Mac OS에서 처럼 로컬에 Key를 임시저장해서, Putty에서 Private key파일을 선택하지 않아도 됩니다.

[Pageant key](https://the.earth.li/~sgtatham/putty/latest/w64/pageant.exe)

프로그램에서 Private Key를 업로드 할 수 있습니다.

* (option- Mac OS /Linux 사용자를 위한 Bastion Tunneling) SSH Tunneling을 통해 접속 할 수 있습니다. Bastion Host로 22번 포트를 연결 한 이후, 별도의 포트 번호로 터널링 하는 방식입니다. 먼저 아래와 같이 터미널에서 백그라운드 또는 포그라운드로 실행하고, 터미널을 닫지 않습니다.

ssh -i “bastion key.pem path” -N -L 22001:"Private EC2 IP" ec2-user@"Bastion IP"

* 새로운 터미널을 생성해서 아래와 같이 위에서 선언한 포트로 접속하면 Private EC2로 접속합니다.

ssh -i "target-key.pem" -p 22001 ec2-user@localhost

* (Option - Window 사용자를 위한 Bastion Tunneling) 앞서 구성한 Bastion 접속을 위한 Putty 구성에서 아래와 같이 추가 구성을 하고, Bastion Host에 접속합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UTyo_O5_VPdUHwSRN%2Fimage.png?alt=media\&token=b53f5b98-dcd5-401e-ac87-ff040fbc9a97)

* **Pagent Key list에 Private pem key를 미리 업로드 해 둡니다.**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvBoK8Fgzs4QMzgtcL%2F-MVvGwizhH3rCCH8gKF2%2Fimage.png?alt=media\&token=8fc1a216-aa7b-4a90-8311-1cf93cdf23bd)

* **Bastion Host 에 먼저 SSH로 접속합니다.**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UUQf0qRHLsyy8VBsd%2Fimage.png?alt=media\&token=397edac5-96bd-4512-b6cc-1fb099355e00)

* 터널링 구성이 완성되었으므로, 이제 다시 Putty 창을 한개 더 열고, 아래와 같이 22번 포트로 접속하면, 터널링으로 내부 접속이 가능해 집니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UUCxVj1f-RhXvudb5%2Fimage.png?alt=media\&token=6a56f3c8-ee0c-4969-8576-21874ca6f1be)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6U9Hy32hbTDI0ljBCC%2F-M6UUYZW1aqnoWZOXSAS%2Fimage.png?alt=media\&token=ad63c629-fa13-4089-a3e3-d8a53fe912eb)

pageant key 가 등록되어, 내부 Private Host로 간편하게 Bastion Host를 통해 접속 가능합니다.

### Task5. VPC Endpoint (Option) <a href="#task5.-vpc-endpoint-option" id="task5.-vpc-endpoint-option"></a>

VPC 엔드포인트를 통해 인터넷 게이트웨이, NAT 디바이스, VPN 연결 또는 AWS Direct Connect 연결을 필요로 하지 않고 AWS PrivateLink 구동 지원 AWS 서비스 및 VPC 엔드포인트 서비스에 비공개로 연결할 수 있습니다. VPC의 인스턴스는 서비스의 리소스와 통신하는 데 퍼블릭 IP 주소를 필요로 하지 않습니다. 랩에서 Private EC2로 연결할 수 있는 방법은 Bastion Host를 통해 연결하거나, VPC Endpoint를 연결하여 Session Manager로 접속하는 방법이 있습니다.

Task5에서는 VPC EndPoint를 통해서 Session Manager로 연결하는 방법을 구성해 봅니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VTZKuTmASFnKKGYXj%2F-M6WwB4E7MeGqfgkHLOI%2Fimage.png?alt=media\&token=3c24c5d8-3b21-4057-aa70-59f4ee813120)

#### 22. Session Manager 연결을 위한 Role 생성 <a href="#id-22.-session-manager-role" id="id-22.-session-manager-role"></a>

* Session Manager를 통한 접속을 위해서는 EC2를 위한 SSM Role이 필요합니다.
* Private Subnet의 Private-01,02 Instance에 IAM Role을 생성해서 연결합니다. **EC2 대시보드**에서 **"Private-01**"을 선택하고, 상단 메뉴 "**작업"-"인스턴스 설정"-"IAM 역할 연결/바꾸기"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q51HvjcSR0DYHeV01%2Fimage.png?alt=media\&token=ef6eb324-2aa2-410e-9a7b-68c152a4b4cd)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q55m8TsiCsHqCEF3x%2Fimage.png?alt=media\&token=e644762c-cd26-4f2d-98b2-b855ec9d2d0b)

* **IAM 대시보드**로 이동하면, 상단의 **"역할 만들기"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q5PS4_d3jIRan0ze5%2Fimage.png?alt=media\&token=6ea31977-14ad-438f-bf51-879b07fd39a3)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q5S2li-GT8cFyq7Wg%2Fimage.png?alt=media\&token=0c6b4350-3584-41e1-8787-7bc819e883dd)

* 정책필터에서 **SSM을 검색**합니다.**"AmazonEC2RoleforSSM"**&#xC744; 선택하고, "**정책생성"**&#xC744; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q5dhDv_PmgtQqHFPY%2Fimage.png?alt=media\&token=320c557a-f353-4e95-9a75-7e24827dddcf)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q5n9ajTH_-WI7q0Ta%2Fimage.png?alt=media\&token=597c45d1-0b22-4337-a567-23a36e8f8daf)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q65kYau9RoXGE5iR2%2Fimage.png?alt=media\&token=e015de04-d529-4f6a-af01-e9ab4b6d9896)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6P_62tL3ozRkrc68ve%2F-M6Q6ElsKaFrmAA7Meri%2Fimage.png?alt=media\&token=f8f1d0aa-7ffa-46d4-849e-dc2370f58cf2)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Q6Heb04x_KFbWgBCW%2F-M6Q6iZ9nP6nxZkesOVE%2Fimage.png?alt=media\&token=9e89e12c-570a-442e-88cc-b8e478b2cd35)

* **Private-02** 인스턴스에도 생성된 IAM 역할을 할당합니다.

SSMRole을 정의하더라도, Private EC2 인스턴스는 외부에서 접속 할 수 없습니다. VPC Endpoint 설정이 완료되면 System Manager의 Session Manager 기능을 통해 연결할 수 있습니다.

* VPC Endpoint설정을 위해서 **"VPC 대시보드" - "가상 프라이빗 클라우드" - "엔드포인트" -"엔트포인트 생성"**&#xC744; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VQsZIcfSAds5N9240%2Fimage.png?alt=media\&token=a1c234f5-e569-4e5a-b6b0-aaa41e0f5b75)

* 서비스를 선택하기 위해 **"서비스 이름" - "ssmmessages"**&#xB97C; 선택합니다. 현재 **사용 중인 VPC**를 선택합니다. 서브넷은 **Private 서브넷 2개 (2개의 가용영역)**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VQvlEKL7C3oh3-hds%2Fimage.png?alt=media\&token=aaa28ebf-4cb5-46a8-92ac-7e718176da66)

* 새로운 **보안그룹(Security Group)을 생성**하고 선택합니다. 보안 정책은 **"HTTPS"를 인바운드 허용**해 줍니다. **"IMD-SSM-SG"** 보안 그룹을 생성하고 **Search 창에서 "IMD-SSM-SG"**&#xB97C; 찾아서 선택합니다.
* 적절한 **태그를 구성**하고, **엔드포인트 생성**을 완료합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VQxnYg3dg3CaRp-pt%2Fimage.png?alt=media\&token=d982d947-a796-4942-9110-7b236bd7dd9d)

* **"VPC 대시보드" - "가상 프라이빗 클라우드" - "엔드포인트"** 에서 **상태-사용가능으로 변경**되었는지 확인합니다. 서브넷 창을 선택하고 **2개의 ENI(Elastic Network Interface)가 생성**된 것을 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VR0LDy5Eg7lk5HpKK%2Fimage.png?alt=media\&token=ea030047-c295-424d-8111-792fc2f549de)

* AWS 서비스에서 **"System Manager"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VR2MLJ_e-jLbmi4hA%2Fimage.png?alt=media\&token=0b17d258-f4fd-4207-b4bc-f21457067acf)

* **"System Manager"**&#xC5D0;서 **"Session Manager"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VR4HJEEriL1LSSxOL%2Fimage.png?alt=media\&token=8c60ad5c-5ecb-4816-8ce1-595793a9e7c1)

세션시작 화면에서 대상 인스턴스가 보이지 않습니다. EC2 인스턴스를 최초에 생성할 때 IAM Role 역할을 정의하지 않고, 생성 이후에 추가했기 때문입니다. **IAM Role을 추가로 연결한 Private 인스턴스들을 재시작**합니다. EC2 인스턴스를 재시작하면 **System Manager - 세션관리자**에서 정상적으로 인스턴스들이 보입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VR6h3BEjncNw4RQ3T%2Fimage.png?alt=media\&token=7d2370a0-0ab6-4eea-905a-fed743f3c4b5)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VR92LKPePtghrsEuw%2Fimage.png?alt=media\&token=c94af00f-a142-4e50-8f99-e2f5b54c3d51)

* 이제 Bastion Host를 경유하지 않고 , VPC Endpoint 서비스와 Session Manager를 통해서 Private 인스턴스들에 직접 연결이 가능합니다. **EC2 대쉬보드**에서 **Private-01, Private-02 인스턴스**를 선택하고 "**인스턴스 연결" - "Session Manager"**&#xB97C; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VRAiFJEJYICz39eHn%2Fimage.png?alt=media\&token=0cdd1c70-e618-4d76-a8a1-5a44a88c9c2d)

* 정상적으로 Private 인스턴스에 연결되는 것을 확인 할 수 있습니다.

Session Manager에 최초 연결될때 , Linux 계정을 확인해 봅니다.**ec2-user**로 로그인 되지 않습니다. IAM-Role에 의해 생성된 **ssm-user** 계정입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6VQjisGkfCypXHO9NX%2F-M6VRE3a3S5c2AFUqg2X%2Fimage.png?alt=media\&token=f546c705-3802-4308-b24c-292c359e0778)

아래에 출력된 결과와 AWS 관리콘솔 - Private-01 인스턴스의 주소를 비교해 봅니다.

curl http://169.254.169.254/latest/meta-data/local-ipv4

* Cloud9에서는 아래와 같이 Session Manager Plugin을 설치하여 접속 할 수 있습니다.

\#session manager plugin 설치

curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/linux\_64bit/session-manager-plugin.rpm" -o "session-manager-plugin.rpm"

sudo yum install -y session-manager-plugin.rpm

git clone https://github.com/whchoi98/useful-shell.git

* Cloud9 터미널에서 아래와 같이 접속 할 수 있습니다.

aws ssm start-session --target {Instance ID}

**보안 그룹**은 인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽 역할을 합니다. VPC에서 인스턴스를 시작할 때 최대 5개의 보안 그룹에 인스턴스를 할당할 수 있습니다. 보안 그룹은 서브넷 수준이 아니라 인스턴스 수준에서 작동하므로 VPC에 있는 서브넷의 각 인스턴스를 서로 다른 보안 그룹 세트에 할당할 수 있습니다.

네트워크 ACL(액세스 제어 목록)은 1개 이상의 서브넷 내부와 외부의 트래픽을 제어하기 위한 방화벽 역할을 하는 VPC를 위한 선택적 보안 계층입니다. 보안 그룹과 비슷한 규칙으로 네트워크 ACL을 설정하여 VPC에 보안 계층을 더 추가할 수 있습니다.

| 보안그룹                                                             | 네트워크 ACL                                                     |
| ---------------------------------------------------------------- | ------------------------------------------------------------ |
| 인스턴스 레벨에서 운영                                                     | 서브넷 레벨에서 운영                                                  |
| 허용 규칙만 지원                                                        | 허용 및 거부 규칙 지원                                                |
| 상태 저장: 규칙에 관계없이 반환 트래픽이 자동 허용됨                                   | 상태 비저장: 반환 트래픽이 규칙에 의해 명시적으로 허용되어야 함                         |
| 트래픽 허용 여부를 결정하기 전에 모든 규칙을 평가                                     | 트래픽 허용 여부를 결정 시 규칙을 번호순으로 처리                                 |
| 인스턴스 시작 시 누군가 보안 그룹을 지정하거나, 나중에 보안 그룹을 인스턴스와 연결하는 경우에만 인스턴스에 적용됨 | 연결된 서브넷의 모든 인스턴스에 자동 적용됨(보안 그룹 규칙이 지나치게 허용적일 경우 추가 보안 계층 제공) |

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yqd6tg-0E4BwNF9sy%2F-M6YsGLmkKD7cEF0Sh-g%2Fimage.png?alt=media\&token=d41fed3f-2cbd-4bc4-ae54-284cc66d50bb)

* NACL (Network Access Control List) 구성을 위해 , **"VPC대시보드" - "보안" - "네트워크 ACL" - " 네트워크 ACL 생성"**&#xC744; 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yh5NfAXxgwZVGwDOD%2F-M6Yh9ZEB9gkm7qsftx6%2Fimage.png?alt=media\&token=cce39276-661a-4472-a8ac-77d0a1788e36)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvL9vw9JWRhBUGLm81%2Fimage.png?alt=media\&token=8ccecabc-cef0-47c6-b509-23ac8e9e1fa9)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvPjbZI_cc4RgfjUXg%2Fimage.png?alt=media\&token=46b87dee-bb58-4894-91e7-9aa7885098f2)

* NACL은 상태비저장 방식으로 트래픽 반환시에도 정책이 필요합니다. 트래픽 반환은 모두 허용하기 위해 **대상을 모두로 정의**하고, **유형도 모두 트래픽을 선택**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvQBn_Kd3IevT_jKBX%2Fimage.png?alt=media\&token=2cb41e59-bf58-4aa5-9d8a-bd9d5c8c92f1)

* **서브넷 연결 편집은 Private-A,B** 모두 적용합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvQJ-XB9PUo7yIXWWD%2Fimage.png?alt=media\&token=c5932c1f-03fa-4c3f-8857-3bd9b35def4b)

* 2개의 콘솔 창을 열어서 트래픽이 어떻게 제어되는지 확인합니다. Public-01, Public-02 인스턴스에서 Private-01 인스턴스로 Ping을 적용해 봅니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvPMRgx0JNlnpS5Xp1%2Fimage.png?alt=media\&token=bea6d19f-526e-4433-96fe-e2d204969130)

**Network ACL은 사용자가 정의하지 않아도 기본 NACL이 인바운드,아웃바운드 모두 허용입니다. 랩에서는 별도의 NACL을 적용해서 서브넷에 적용한 것입니다.**

* 네트워크 ACL 선택 - 서브넷 연결 선택 - 서브넷 연결 편집 선택 - 해제

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvQske21o8VHj5-ayX%2Fimage.png?alt=media\&token=3fa00caa-265b-425d-8788-b410789b6379)

* 네트워크 ACL 선택 - 작업 선택 - 네트워크 ACL 삭제

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVvI9w3fKS27zRuWVwg%2F-MVvRGF5egBJ20qGkdrz%2Fimage.png?alt=media\&token=497a551a-0db6-41a0-94cd-a8baf1132e2b)

#### **25.보안 그룹 - Security Group 구성** <a href="#id-25.-security-group" id="id-25.-security-group"></a>

* 네트워크 ACL을 모두 허용합니다. (인바운드 소스 허용을 0.0.0.0/0 으로 변경합니다.) 또는 규칙 번호를 10번 이전 번호로 만들고 모든 규칙을 허용해도 됩니다. 이것은 Network ACL이 순차적으로 보안규칙을 탐색하고, 곧바로 적용하기 때문입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6YsJFqB3BFzp059HFd%2F-M6Yt6BH3kjZZg6PkSwq%2Fimage.png?alt=media\&token=de0fe23b-6868-4c7f-97f7-4fd2f55dff01)

* **VPC 대시보드 - 보안 - 보안그룹에서 "IMD-PUB-SG(Public subnet을 위한 Security Group)"을 수정**합니다. **인바운드 ICMP 허용을 모두 제거**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6YumI77eYU99T5llrI%2F-M6Ywucz_CMr2qLnNEgu%2Fimage.png?alt=media\&token=b9792709-12bb-4303-810b-b4cea30df416)

* 적용 이후 외부에서 더 이상 ICMP가 허용되지 않습니다. 하지만 내부 Public EC2 에서는 아웃바운드 규칙에서 모두 허용이므로 ICMP가 정상적으로 허용됩니다. 상태저장 방식으로 반환트래픽에 대해서는 제어하지 않기 때문입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6YumI77eYU99T5llrI%2F-M6Yx_AUBsMAAG5ccuTK%2Fimage.png?alt=media\&token=bc81a13d-ddc9-4510-9542-5b42552e3bbd)

외부에서 PING을 계속 적용한 상태에서 , 인바운드 규칙을 제거해도 PING은 정상적으로 허용됩니다. 하지만 PING을 끊고 다시 PING을 시도하면 더 이상 응답하지 않습니다. 이것은 상태저장방식의 특징으로 대부분 보안제품도 동일합니다.

VPC flow log는 VPC 트워크에서 전송되고 수신되는 IP 트래픽에 대한 정보를 수집할 수 있는 기능입니다. 플로우 로그 데이터를 Amazon CloudWatch Logs 및 Amazon S3로 게시할 수 있습니다. 플로우 로그를 생성한 다음 선택된 대상의 데이터를 가져와 확인할 수 있습니다.

VPC flow log는 다음과 같은 여러 작업에 도움이 될 수 있습니다.

* 네트워크 인터페이스를 오가는 트래픽에 대한 분석

VPC Flow log 데이터는 네트워크 트래픽 경로 외부에서 수집되므로 네트워크 처리량이나 지연 시간에 영향을 주지 않습니다. 네트워크 성능에 영향을 주지 않고 VPC Flow log를 생성하거나 삭제할 수 있습니다. 또한 VPC Flow log를 사용하면, CloudWatch Logs 또는 Amazon S3 중 어디로 보내든, CloudWatch Logs 요금이 적용됩니다.

VPC, 서브넷 또는 네트워크 인터페이스에 대한 VPC Flow를 생성할 수 있습니다. 서브넷이나 VPC에 대한 VPC Flow log를 생성할 경우, VPC 또는 서브넷의 각 네트워크 인터페이스가 모니터링됩니다.

모니터링된 네트워크 인터페이스를 위한 VPC Flow log 데이터는 트래픽 Flow 설명하는 필드로 구성된 로그 이벤트인 flow log record로서 기록됩니다.

#### 26. VPC Flow log를 수신할 CloudWatch Log Group을 생성 <a href="#id-26.-vpc-flow-log-cloudwatch-log-group" id="id-26.-vpc-flow-log-cloudwatch-log-group"></a>

* 먼저 VPC Flow log를 수신할 Cloud watch log group을 생성합니다. **AWS 서비스 - CloudWatch - 로그 - 로그그룹 - 로그그룹 생성을 선택**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yz3h6FF63QxRWg7-a%2F-M6Z-KEna2MayXvGS1Bm%2Fimage.png?alt=media\&token=f8528f07-dbe2-47dd-be83-25ff526b73ab)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yz3h6FF63QxRWg7-a%2F-M6Z-ZfmCHx2_zspbR2F%2Fimage.png?alt=media\&token=c2908361-b5d2-4c76-b2a6-720787c2d718)

* 로그그룹이 정상적으로 생성되었는지 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yz3h6FF63QxRWg7-a%2F-M6Z-kIFfI0PwrCc2Q54%2Fimage.png?alt=media\&token=ce1abfcc-2a71-4e50-a49c-ef624484ff33)

* 다시 **VPC 대시보드**로 돌아와, V**PC를 선택하고 플로우 로그 생성**을 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Yz3h6FF63QxRWg7-a%2F-M6Z0Akqli3xMKkNwvke%2Fimage.png?alt=media\&token=3f33eb9e-4dbb-4be9-a249-a1d0b5f5862f)

* Maximum aggregation Interval 을 1분으로 선택합니다. 대상로그 그룹은 앞서 생성한 로그 그룹을 섵개합니다.(IMD-VPCFlow) IAM역할을 "flowlogsRole"을 선택합니다. 만약 없는 경우 생성버튼을 눌러서 생성합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z0J_IXP33Z18oDIVc%2F-M6Z1odUoOpvCthGgtUW%2Fimage.png?alt=media\&token=853ced04-0646-4717-bf23-fa37e17925ae)

* 앞서 IAM Role에 "flowlogsRole"이 없는 경우에만 해당됩니다. 생성 버튼을 누르면 자동으로 IAM 메뉴로 연결됩니다. 별도의 변경없이 생성합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z0J_IXP33Z18oDIVc%2F-M6Z0qzBTtyqjg6QeKIH%2Fimage.png?alt=media\&token=7b276a1a-7128-48dd-8f04-a4a0ac3f137d)

* VPC 플로우 로그가 정상적으로 생성되었는지 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z1qdaKlFknO5NXJGM%2F-M6Z2DBtIcCdjJRHaeQA%2Fimage.png?alt=media\&token=17ce3570-8305-468f-9463-bb314000f4ab)

* **CloudWatch 대시보드**로 이동합니다. **"로그"-"로그그룹"을 선택**하면 최초에 생성한 로그 그룹이 보입니다. **해당 로그 그룹을 선택**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z1qdaKlFknO5NXJGM%2F-M6Z2WcXA8GBi4sB3Wqy%2Fimage.png?alt=media\&token=c1f06afd-5701-4acf-82e3-583db29f95f7)

* 로그그룹에 스트림이 정상적으로 로그들이 쌓이는 것을 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z1qdaKlFknO5NXJGM%2F-M6Z2eN3B-HjhTtYIjJj%2Fimage.png?alt=media\&token=7287f036-7da0-4dba-97ab-80b4e2de5aaa)

* **로그 그룹의 스트림 중에 한개를 선택**해서 내용을 살펴봅니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6Z1qdaKlFknO5NXJGM%2F-M6Z2nVgl3lAyiZKhc9N%2Fimage.png?alt=media\&token=75059d2b-1ede-41cd-90a9-0e48207c897e)

* 상세한 VPC Flow 분석 방법은 아래 URL을 참조합니다.

