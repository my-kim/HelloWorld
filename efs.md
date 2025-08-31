# EFS

Amazon EFS(Amazon Elastic File System)는 AWS 클라우드 서비스와 온프레미스 리소스에서 사용할 수 있는, 간단하고 확장 가능하며 탄력적인 완전관리형 NFS 파일 시스템을 제공합니다. 이 제품은 애플리케이션을 중단하지 않고 온디맨드 방식으로 페타바이트 규모까지 확장하도록 구축되어, 파일을 추가하고 제거할 때 자동으로 확장하고 축소하며 확장 규모에 맞게 용량을 프로비저닝 및 관리할 필요가 없습니다.

Amazon EFS는 Standard 스토리지 클래스 및

[Infrequent Access 스토리지 클래스](https://aws.amazon.com/ko/efs/features/infrequent-access/)

(EFS IA)의 두 가지 스토리지 클래스를 제공합니다. EFS IA에서는 매일 액세스하지 않는 파일에 대해 비용 최적화된 가격/성능을 제공합니다. 파일 시스템에서 EFS 수명 주기 관리를 활성화하기만 하면 선택한 수명 주기 정책에 따라 액세스하지 않은 파일은 EFS IA로 투명하게 자동 이동됩니다. EFS IA 스토리지 클래스 요금은 월별 GB당 0.025 USD에 불과합니다.

워크로드 패턴이 다양하지만, 고객은 일반적으로 80%의 데이터는 자주 액세스하지 않으며(EFS IA에 적합함), 20%는 자주 사용하므로(EFS Standard에 적합함), 월별 GB당 0.08 USD의 저렴한 스토리지 요금을 이용할 수 있습니다. Amazon EFS는 공통 파일 시스템 네임스페이스에서 두 스토리지 클래스 모두의 파일을 투명하게 지원합니다.

Amazon EFS는 수천 개의 Amazon EC2 인스턴스에 대한 병렬 공유 액세스를 대규모로 제공하도록 설계되었으므로, 애플리케이션은 일관되게 낮은 지연 시간을 유지하면서 높은 수준의 집계 처리량과 IOPS를 달성할 수 있습니다.

Amazon EFS는 홈 디렉터리에서 비즈니스 크리티컬 애플리케이션에 이르기까지 다양한 사용 사례에 적합합니다. 고객은 EFS를 사용하여 리프트 앤 시트프 방식으로 기존 엔터프라이드 애플리케이션을 AWS 클라우드로 마이그레이션할 수 있습니다. 기타 사용 사례로, 빅 데이터 분석, 웹 지원 및 콘텐츠 관리, 애플리케이션 개발 및 테스트, 미디어 및 엔터테인먼트 워크플로, 데이터베이스 백업, 컨테이너 스토리지 등이 있습니다.

Amazon EFS는 AZ(가용 영역) 내부와 여러 AZ에 걸쳐 데이터를 저장하여 높은 수준의 가용성과 내구성을 제공하는 지역별 서비스입니다. Amazon EC2 인스턴스는 여러 AZ, 지역 및 VPC에서 파일 시스템에 액세스할 수 있는 반면, 온프레미스 서버는 AWS Direct Connect 또는 AWS VPN을 사용하여 액세스할 수 있습니다.

Amazon EFS는 NFSv4 프로토콜을 통해 기존 파일 권한 모델, 파일 잠금 기능 및 계층적 디렉터리 구조를 사용하여 Amazon EC2 인스턴스 및 온프레미스 서버에서 동시에 이러한 수천 개의 서버 연결에 대한 보안 액세스를 제공합니다. Amazon EC2 인스턴스는 여러 AZ, 리전 및 VPC에서 파일 시스템에 액세스할 수 있는 반면, 온프레미스 서버는 AWS Direct Connect 또는 AWS VPN을 사용하여 액세스할 수 있습니다.

Amazon EFS는 Linux 워크로드에 필요한 처리량, IOPS 및 짧은 지연 시간을 제공하도록 설계되었습니다. 처리량과 IOPS는 파일 시스템 증가에 따라 확장되며, 파일 워크로드의 예측할 수 없는 성능 요구 사항을 지원하기 위해 단기간에 더 높은 처리량 수준으로 급증할 수 있습니다. 가장 수요가 많은 워크로드의 경우 Amazon EFS는 10GB/초 이상의 성능과 500,000보다 많은 IOPS를 지원할 수 있습니다.

Amazon EFS는 애플리케이션을 중단하지 않고 파일을 추가하거나 제거할 때 파일 시스템 스토리지 용량을 자동으로 즉시 확장/축소하여 필요한 만큼 스토리지 용량을 동적으로 제공합니다. 스토리지를 미리 프로비저닝할 필요 없이 간단히 파일 시스템을 생성하고 파일을 추가하면 됩니다.

Amazon EFS는 Linux 워크로드에 대한 공유 파일 시스템 스토리지를 제공하는 완전 관리형 서비스입니다. 이 서비스는 파일 시스템을 빠르게 생성하고 구성할 수 있는 간단한 인터페이스를 제공하며 파일 스토리지 인프라를 자동으로 관리하여 파일 시스템의 기초를 배포, 패치 및 유지 관리하는 복잡성을 제거합니다.

Amazon EFS 스토리지를 사용하면 사용한 만큼만 비용을 지불합니다. 스토리지를 미리 프로비저닝할 필요가 없으며 최소 약정이나 선불 수수료가 없습니다. EFS 수명 주기 관리를 활용하면 액세스 빈도가 낮은 파일을 비용이 최적화된 스토리지 클래스로 자동으로 이동하여 스토리지 비용을 92%까지 절감할 수 있습니다. 또한 AWS 예산을 사용하여 파일 시스템 비용을 모니터링할 수 있습니다.

Amazon EFS에서는 기존 보안 인프라를 사용하여 파일에 안전하게 액세스할 수 있습니다. POSIX 권한,

[Amazon VPC](https://aws.amazon.com/ko/vpc/)

및

[AWS IAM](https://aws.amazon.com/ko/iam/)

을 사용하여 Amazon EFS 파일 시스템에 대한 액세스를 제어합니다. 유휴 데이터와 전송 중인 데이터를 암호화하여 데이터를 보호합니다. 또한 Amazon EFS는 다양한 자격 및 규정 준수 요구 사항을 충족하여 사용자가 규제 요건을 충족할 수 있도록 도와줍니다.

본 랩은 아래와 같은 구성을 통해 EC2에서 EFS로 NFS 마운트를 구성해 보고, S3 의 데이터를 NFS로 복사해 봅니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-WDT7oh03J8exsnWK%2F-MW-ZIyRKCk3IP25kdut%2Fimage.png?alt=media\&token=095d7afb-4511-44fb-912e-b1d7e75b1d29)

#### **1.Security Group (보안그룹) 생성** <a href="#id-1.security-group" id="id-1.security-group"></a>

* VPC - 보안 그룹 - 보안 그룹 생성 메뉴에서 EC2가 EFS로 접근 가능하도록 보안 설정을 합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW--Oy_9w-tKC5Zfx95%2Fimage.png?alt=media\&token=2e2750c5-beaa-49d3-b225-9e06d479e20b)

* AWS 관리 콘솔에서 " EFS " 를 검색하고, 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MVzy2yYKTx1jvCdowa8%2Fimage.png?alt=media\&token=8f8b53bd-3d56-497f-b9fe-47f5fa9b4979)

* **수명주기 관리 - 마지막 액세스 이후 30일 경과**
* **암호화 - 유휴 시 데이터 암호화 활성화 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MVzz5sxxXgiqvMC0ETd%2Fimage.png?alt=media\&token=8da42597-5bfc-46bb-95ce-71cfb42c2c19)

* 탑재 대상 - EFS가 연결될 네트워크를 선택합니다.
  * **가용영역 - ap-northeast-2a, 2c 선택**
  * **서브넷 ID - Private Subnet a,b 선택**
  * **IP 주소 - 10.1.11.201, 10.1.12.201**
  * **보안그룹 - 이전 단계에서 생성한 EFS-SG 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW-0A8__HWEaaHnfFak%2Fimage.png?alt=media\&token=15876b03-61f3-4f48-a22e-1ee86dd9458a)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW-0RYLx1-g-odWske3%2Fimage.png?alt=media\&token=a3a7f5e9-6584-4749-b583-9bfef823679e)

* 파일 시스템 상태가 **사용가능**으로 변경되었는지 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW-0dsBPCu5V_RZPa1M%2Fimage.png?alt=media\&token=8d17a3b4-ad0a-414f-a012-de7976453821)

* Private01,02 인스턴스의 보안 정책에 신규 보안 그룹을 추가합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW-1Tq8DrelCkSb4Sav%2Fimage.png?alt=media\&token=cea70763-0a5f-4e1d-8e32-df96d7b87c3b)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVzNv9hsKc0ExKKpip6%2F-MW-1C5O_QMS33WcJkfz%2Fimage.png?alt=media\&token=38be14eb-e269-4a12-960b-875affa65ddc)

* Bastion Host 에서 Private-01,02로 접속하거나, Session Manager를 통해서 접속합니다.
* 아래 명령을 통해 Private-01,02 인스턴스가 EFS에 마운트 합니다.

sudo yum install -y amazon-efs-utils

sudo mount -t efs fs-36892f56:/ \~/aws-efs/

sudo yum install -y amazon-efs-utils

sudo mount -t efs fs-36892f56:/ \~/aws-efs/

각 Private01,02 EC2에서 아래와 같이 EFS가 마운트 된 것을 확인합니다.

\[ec2-user@ip-10-1-11-101 \~]$ df -h

Filesystem Size Used Avail Use% Mounted on

devtmpfs 482M 0 482M 0% /dev

tmpfs 492M 0 492M 0% /dev/shm

tmpfs 492M 404K 492M 1% /run

tmpfs 492M 0 492M 0% /sys/fs/cgroup

/dev/xvda1 8.0G 1.5G 6.6G 19% /

tmpfs 99M 0 99M 0% /run/user/1000

fs-36892f56.efs.ap-northeast-2.amazonaws.com:/ 8.0E 0 8.0E 0% /home/ec2-user/aws-efs

* VPC - 엔드포인트 - 엔트포인트 생성 에서 S3용 VPC Endpoint Gateway를 구성합니다.
  * AWS 서비스 - 서비스 이름 - S3 검색 - Gateway 타입으로 선택
  * 라우팅 테이블 - Public/Private Routing Table 선

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-HCgFcibZ-LQYSzB6%2F-MW-JCXGNxIq-QxkOYLK%2Fimage.png?alt=media\&token=0aef37d1-a56a-4981-811e-c8d23dedd77b)

* VPC - 라우팅 테이블에서 정상적으로 S3용 라우팅 테이블이 추가 되었는지 확인

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-HCgFcibZ-LQYSzB6%2F-MW-JRYzqxdCYEIQYU9i%2Fimage.png?alt=media\&token=34f7cf66-1428-45ae-ab0c-668ca9b0a76b)

* AWS 관리 콘솔 - IAM 에서 Private-01,02 EC2 인스턴스가 S3에 접근 하도록 권한을 설정해 줍니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-Pm-konc076_gugnd%2F-MW-QmaYEZnNbUkcEHxn%2Fimage.png?alt=media\&token=789bb0df-94d5-49be-b9b5-863cb7169765)

* **역할 만들기 - AWS 서비스 - EC2 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-Pm-konc076_gugnd%2F-MW-Qxz2h_0_p5df6sdd%2Fimage.png?alt=media\&token=829221e3-ab4b-4a5d-9be9-85dd9c96694f)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-UvMqu0KyNEKo47P1%2F-MW-VleQiCt9AExBGqM3%2Fimage.png?alt=media\&token=5e49cea7-67f5-48cb-b3b2-036fa4b3cd0c)

* **역할 이름 - EC2S3Access 를 입력합니다.**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-Pm-konc076_gugnd%2F-MW-RHmMDs7pwH2dakdc%2Fimage.png?alt=media\&token=dbf28608-33a2-4be3-b1d4-0bbb24288abb)

* Private-01,02 EC2에 IAM 정책을 부여합니다.
* EC2 대시보드 - 인스턴스 - Private-01,02 선택 - 작업 - 보안 - IAM역할 수행

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-Pm-konc076_gugnd%2F-MW-RxVievACx4FnUpZ8%2Fimage.png?alt=media\&token=7fef961d-6f0b-43b7-bb31-5a650574f78f)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW-Pm-konc076_gugnd%2F-MW-SI-COmJI-xfMkvxy%2Fimage.png?alt=media\&token=133fcdb4-7ffe-4853-8e51-d3d8091b2b17)

#### 11. EC2에서 S3 파일을 EFS로 Copy <a href="#id-11.-ec2-s3-efs-copy" id="id-11.-ec2-s3-efs-copy"></a>

* Private 01 인스턴스에서 아래와 같이 AWS CLI를 통해서 S3 내용을 확인합니다.

aws s3 ls s3://"s3-bucket-name"

sudo aws s3 cp s3://"S3-bucket-name"/image.png /home/ec2-user/aws-efs

ls /home/ec2-user/aws-efs/

아래와 같이 S3에서 EFS로 정상적으로 Copy 되었는지 확인합니다.

\[ec2-user@ip-10-1-11-101 \~]$ ls /home/ec2-user/aws-efs/

EFS 랩을 정상적으로 완료하셨습니다. !!!
