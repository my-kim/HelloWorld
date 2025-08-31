# ELB (NLB & ALB)

Elastic Load Balancing은 들어오는 애플리케이션 트래픽을 Amazon EC2 인스턴스, 컨테이너, IP 주소, Lambda 함수와 같은 여러 대상에 자동으로 분산시킵니다. Elastic Load Balancing은 단일 가용 영역 또는 여러 가용 영역에서 다양한 애플리케이션 부하를 처리할 수 있습니다. Elastic Load Balancing이 제공하는 세 가지 로드 밸런서는 모두 애플리케이션의 내결함성에 필요한 고가용성, 자동 확장/축소, 강력한 보안을 갖추고 있습니다.

본 랩은 아래와 같은 구성을 통해 NLB와 ALB 구성을 통해 차이점과 구성 방식을 이해하기 위해 아래와 같이 구성합니다.

NLB 랩에서는 새로운 인스턴스 4개를 구성하여 TCP 포트 기반으로 Loadbalancing을 구성하며, ALB는 앞서 구성한 인스턴스를 활용합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7GaoQBR4mddR7VViXj%2Fimage.png?alt=media\&token=de3964dc-745f-49ad-b04c-6ffdb0b743f8)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7GbIsO6dUuDig3rF69%2Fimage.png?alt=media\&token=191ffb99-6840-49db-b1fb-02d8e0ae0ef8)

* 보안그룹 (Security Group) - IMD-PUB-SG
* 네트워크 - IMD-VPC / 각 Public Subnet 별 2개 EC2 인스턴스 / 퍼블릭 IP 자동할당 활성화

sudo yum -y install yum-utils

sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

sudo yum -y install httpd php mysql php-mysql

sudo usermod -a -G apache ec2-user

sudo chown -R ec2-user:apache /var/www

find /var/www -type f -exec sudo chmod 0664 {} \\;

sudo touch /var/www/index.html

sudo systemctl start httpd

sudo systemctl enable httpd

* 보안그룹을 새로 작성합니다. (보안그룹 이름 - NLB-SG : 보안 정책은 22번, 80포트를 허용합니다.)
* 기존 키 페어 또는 새로운 키페어를 생성합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7GfXT6uzQp13CjZSB-%2Fimage.png?alt=media\&token=2e5c1152-afc6-4c1d-a183-5ca9c4c2597b)

* 먼저 NLB 고정 IP 부여를 위한 EIP를 생성합니다. (NLB는 ALB와 다르게 EIP부여가 가능합니다. 필수 조건은 아니므로 생략해도 됩니다.)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7GdVx-UdiCJ2QTkfxJ%2Fimage.png?alt=media\&token=33f3b919-78dc-4686-ae6f-e793b8fe33b3)

* EIP 할당을 위한 Amazon IP 주소풀을 선택하여 고정 IP를 할당 받습니다. 2개의 서브넷에 할당하게 되므로 2번 반복해서 2개를 할당 받습니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7Gdg3Kj78dHvXMKgRr%2Fimage.png?alt=media\&token=a59f6561-ac3b-418d-b775-ed7bf6df608c)

* 2개를 할당 받으면 아래와 같이 2개의 EIP가 생성됩니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7Gfnf05im8aX75gt2N%2Fimage.png?alt=media\&token=9162cebb-15eb-4500-b8fe-2d6aeb38f376)

* NLB 생성을 위해 로드밸런서 생성을 선택합니다.

**EC2 대시보드 - 로드밸런싱 - 로드밸런서 - 로드밸런서 생성 선택 - Netwwork Load Balancer 선택**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7GfvXaT3BsBqD2MnYO%2Fimage.png?alt=media\&token=5d2bf6a2-426a-4d0f-a46a-d212bd02b89a)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7G_30EGxpKKUefnuXY%2F-M7Gg1IXqM3-0JDOK2S_%2Fimage.png?alt=media\&token=f3e078cd-2084-42f1-8984-ae26366de8cc)

* 로드밸런서 구성에서 이름을 선택하고, 체계는 인터넷 연결 (Public Subnet)을 선택합니다. Private 의 경우에는 내부를 선택하면 됩니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVy6zh1Aw1034Wbv_Fi%2Fimage.png?alt=media\&token=270036aa-8641-41c9-a822-77af4f084edb)

* 가용영역 및 서브넷을 선택합니다. 또한 IPv4 주소는 "탄력적 IP 선택"을 선택하고, 미리 할당해 놓은 EIP를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVyAUtiCypY58Gwfg2l%2Fimage.png?alt=media\&token=1e72e677-1dbf-44dd-b23c-c06ae2438571)

가용 영역과 서브넷을 신중하게 선택하십시오. 로드 밸런서를 생성한 후에는 활성화된 서브넷을 비활성화할 수 없지만, 서브넷을 추가로 활성화할 수 있습니다.

* 리스너 및 라우팅에서 대상 그룹을 생성을 선택하고, 대상 그룹을 생성합니다. 생성이 완료되면 다시 생성된 대상 그룹을 찾아서 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyAWJ07CEJILQw48SI%2F-MVyBJBFoTAxTMrZSBWX%2Fimage.png?alt=media\&token=e460bfb1-b4f7-46c6-8390-18067cb103c8)

* 대상 그룹 생성을 선택하면 아래와 같은 화면이 보입니다. 대상 유형 선택에서 인스턴스를 선택하고, 대상 그룹 이름을 선언합니다. 다음 단계를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVy8H4Nx2z3mRRmCrb3%2Fimage.png?alt=media\&token=09814c1f-43cf-4615-90a6-7757d0b10fba)

* 대상 그룹에 포함될 인스턴스를 등록하는 화면이 보이고, 여기에서 앞서 생성한 인스턴스 4개를 선택하고, "아래에 보류 중인 것으로 포함"을 선택하면 대상 그룹에 등록됩니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVy8lxpw_We85mA7Zhk%2Fimage.png?alt=media\&token=bc29908c-64f4-460f-8355-74a69db5dcf9)

* 대상 그룹에 인스턴스들이 등록 된 것을 확인하고, 대상 그룹 생성을 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVy902H0XbgJMono0XL%2Fimage.png?alt=media\&token=b68d85f9-182d-4103-b076-4acbf01dd839)

* 대상 그룹이 정상적으로 등록된 것을 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVy5XyYHg2XBlc11nRF%2F-MVy9BGTm0I2yvqUxK6G%2Fimage.png?alt=media\&token=b560e8fc-04d0-4d73-8605-9c62844c2fc0)

* 이제 다시 로드 밸런서 생성 단계로 전환해서 "생성한 대상그룹을 선택" 합니다. 태그에 키 "Name", 값 "IMD-NLB"를 입력하고, "로드밸런서 생성" 을 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyAWJ07CEJILQw48SI%2F-MVyAkmB-XMQdVSjbTSj%2Fimage.png?alt=media\&token=ee3ab7c5-9bc8-4897-8885-d068592f861b)

* NLB가 대상 그룹에 대한 Healthy 체크를 시작합니다. 대상 그룹 상태를 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyAWJ07CEJILQw48SI%2F-MVyE7DKofkUYNqO2BWj%2Fimage.png?alt=media\&token=18738466-e4da-4afe-a86f-f83fe78e195d)

* 앞서 생성한 EC2 인스턴스(NLB 대상 그룹 인스턴스)에 SSH로 접속해서 아래 Script를 복사합니다.

sudo echo "\<html>\<h2>My Public IP is: $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4/)\</h2>\</html>" >> /var/www/html/index.html

sudo echo "\<html>\<h2>My Private IP is: $(curl -s http://169.254.169.254/latest/meta-data/local-ipv4/)\</h2>\</html>" >> /var/www/html/index.html

sudo echo "\<html>\<h2>My Host Name is: $(curl -s http://169.254.169.254/latest/meta-data/hostname/)\</h2>\</html>" >> /var/www/html/index.html

sudo echo "\<html>\<h2>My instance-id is: $(curl -s http://169.254.169.254/latest/meta-data/instance-id/)\</h2>\</html>" >> /var/www/html/index.html

sudo echo "\<html>\<h2>My instance-type is: $(curl -s http://169.254.169.254/latest/meta-data/instance-type)\</h2>\</html>" >> /var/www/html/index.html

sudo echo "\<html>\<h2>My placement/availability-zone is: $(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)\</h2>\</html>" >> /var/www/html/index.html

* NLB가 대상 그룹에 대한 Healthy 체크가 정상인지 확인합니다.

**EC2 대시보드 - 로드 밸런싱 - 대상 그룹**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyAWJ07CEJILQw48SI%2F-MVyDH9KinqipKlRMuGN%2Fimage.png?alt=media\&token=dbb36401-34dc-4a62-8fec-72e924fd53bc)

* NLB는 서로 다른 리전간의 LB를 속성 편집에서 구성해야 합니다. 비용은 ALB와 다르게 부과 됩니다.
* NLB DNS Name 또는 EIP에 접속하여 결과를 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyIrCCWDsWMAKSeeC1%2F-MVyJi76GrbgdidWRCbX%2Fimage.png?alt=media\&token=33bcc3e3-0939-492e-a255-50409c41c5a9)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyIrCCWDsWMAKSeeC1%2F-MVyJsoq2-8niExO4TXr%2Fimage.png?alt=media\&token=87fe62a8-537a-4346-bc86-72014efb7ecb)

로드 밸런서는 프로토콜, 원본 IP 주소, 원본 포트, 대상 IP 주소, 대상 포트, TCP 시퀀스 번호에 따라 흐름 해시 알고리즘을 사용하여 대상을 선택합니다. 클라이언트로부터의 TCP 연결은 소스 포트와 시퀀스 번호가 서로 다르므로 다른 대상에 라우팅될 수 있습니다. 각 TCP 연결은 연결 수명 동안 하나의 대상에 라우팅됩니다.

따라서 ALB와 같은 결과 처럼 LB가 원하는 결과가 아닐 수 있습니다.

**ALB랩에서는 EC2-Linux에서 생성한 EC2 자원을 그대로 사용합니다.**

* AWS 관리 콘솔에서 **EC2 서비스**를 선택합니다. **"로드밸런싱"-"로드밸런서"를 선택**합니다. 로드밸런서 유형은 **ALB를 선택**합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M6cQQBVUmsL6OGyrTFA%2F-M6cRAfkByyFsGr750LN%2Fimage.png?alt=media\&token=8fed96cb-c61b-492f-8d39-2091db622d01)

* **1단계 로드밸런스 구성을 선택**합니다. **로드밸런서 이름을 생성**합니다. **리스너는 기본 HTTP , 80**을 유지 합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7GpYO7V6vslAyuhLYs%2F-M7Gq4LNd8d1j2o2vkac%2Fimage.png?alt=media\&token=aadadc74-f01a-42ea-9c36-500bad3ceec9)

* **EC2 Computing LAB에서 생성한 보안그룹을 사용**합니다. Public 보안 그룹을 사용합니다. 해당 보안그룹에는 **80 포트가 허용**되어 있어야 합니다

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7GpYO7V6vslAyuhLYs%2F-M7GqDffvekdA6JrWHhE%2Fimage.png?alt=media\&token=c1afebd0-e1c7-4b91-9eb0-da88a5d8f999)

* 라우팅 대상 그룹 (Real Server)를 선택합니다. Real Server 들의 그룹을 정의하고 대상 유형은 인스턴스로 선택합니다. (PUBLIC-01,02)
* 상태 검사는 PUBLIC-01,02에 포함되어 있는 웹서비스 URL을 선택합니다. PUBLIC-01,02에는 "/var/www/html/ec2meta-webpage/index.php" 에서 웹서비스를 제공하고 있습니다. 해당 경로에 대해서 상태 검사를 수행합니다.

/ec2meta-webpage/index.php

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyEiGK4Hm4OiLvqZkC%2F-MVyFxJHgqPUXywgxwZm%2Fimage.png?alt=media\&token=28f64bf4-c26b-4a66-a48e-4eb94176f155)

#### 9. 대상서버 (Real Server)를 등록 <a href="#id-9.-real-server" id="id-9.-real-server"></a>

* 대상서버를 등록합니다. 대상서버는 Public Subnet-A,B에 할당된 서버입니다. (PUBLIC-01, PUBLIC-02) 등록 후 나머지 단계를 완료합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyEiGK4Hm4OiLvqZkC%2F-MVyGQ9mMoLzGU66Lkgj%2Fimage.png?alt=media\&token=ce518aeb-8b09-4fea-b507-255bac06f304)

* 생성된 ALB 의 상태를 확인하고, DNS A 레코드를 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyEiGK4Hm4OiLvqZkC%2F-MVyHvuI3KYTX6FNdqOL%2Fimage.png?alt=media\&token=92eb6d08-9fe6-4ca6-9870-db0d76f2a8ad)

* 대상서버가 **"Healthy" 상태**인지를 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVyIrCCWDsWMAKSeeC1%2F-MVyJ1fstrL3N8Y8ZOw6%2Fimage.png?alt=media\&token=65f657f2-875e-4098-a152-b52c6ac90b3c)

* ELB DNS A레코드 주소로 정상적으로 웹서비스가 제공되는 지 확인합니다. 앞서 ALB 정보에서 제공되는 DNS A 레코드를 복사해서 웹 브라우저 창에 붙여 넣고 확인합니다.

ALB-DNS-A-Record/ec2meta-webpage/index.php

* 웹페이지를 Refresh 할 때 마다 페이지의 정보가 다르게 변경됩니다. 라운드로빈으로 로드밸런싱이 이뤄지기 때문입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7GpYO7V6vslAyuhLYs%2F-M7GqcroWuRAz4oMPADm%2Fimage.png?alt=media\&token=9b2f78a9-fdee-4b2e-80e0-95a89974317f)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7GpYO7V6vslAyuhLYs%2F-M7GqfmFLoKPgv1dL4Cx%2Fimage.png?alt=media\&token=b23b733f-3dd7-40a6-adc3-e80e949926ee)
