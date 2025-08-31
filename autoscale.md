# AutoScale

이 랩은 기본 VPC환경에서 Auto Scaling Group을 생성하고 EC2 자원을 생성하고 축소하는 과정을 포함합니다.. (update : 2021-03-15)

AWS Auto Scaling은 애플리케이션을 모니터링하고 용량을 자동으로 조정하여, 최대한 저렴한 비용으로 안정적이고 예측 가능한 성능을 유지합니다. AWS Auto Scaling을 사용하면 몇 분 만에 손쉽게 여러 서비스 전체에서 여러 리소스에 대해 애플리케이션 규모 조정을 설정할 수 있습니다. 이 서비스는 간단하면서도 강력한 사용자 인터페이스를 제공하므로 이를 사용하여

[Amazon EC2](https://aws.amazon.com/ec2/)

인스턴스와 스팟 플릿,

[Amazon ECS](https://aws.amazon.com/ecs/)

작업,

[Amazon DynamoDB](https://aws.amazon.com/dynamodb/)

테이블 및 인덱스,

[Amazon Aurora](https://aws.amazon.com/aurora/)

복제본 등 리소스에 대한 규모 조정 계획을 수립할 수 있습니다. AWS Auto Scaling을 사용하면 성능과 비용을 최적화하거나 둘 사이의 적절한 균형을 유지하기 위한 권장 사항을 활용해 간단하게 규모를 조정할 수 있습니다. 이미

[Amazon EC2 Auto Scaling](https://aws.amazon.com/ec2/autoscaling/)

을 사용하여 Amazon EC2 인스턴스의 규모를 동적으로 조정하고 있는 경우, 이제 AWS Auto Scaling과 결합하여 다른 AWS 서비스의 추가 리소스를 조정할 수 있습니다. AWS Auto Scaling을 사용하면 항상 적시에 올바른 리소스가 애플리케이션에 할당됩니다.

본 랩은 아래와 같은 구성을 통해 EC2 인스턴스들의 Auto Scaling을 확인하는 데 도움을 드립니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MW6qGIzif_2aEe80OPR%2F-MW6qRzKmLgqC0wUZEWj%2Fimage.png?alt=media\&token=91c5f031-ce4a-469e-901f-72adf9414d6a)

* **Auto Scaling Group 을 통한 EC2 증가와 감소 이**

### Task1. AutoScaling 을 위한 EC2 생성 <a href="#task1.-autoscaling-ec2" id="task1.-autoscaling-ec2"></a>

#### 1. AutoScaling Group을 위한 EC2 인스턴스 생성 <a href="#id-1.-autoscaling-group-ec2" id="id-1.-autoscaling-group-ec2"></a>

* **AMI - Amazon Linux 2 AMI (HVM), SSD Volume Type - ami (64비트 x86)**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuDR5qw7es4mZyY7O2%2F-MVuQaIgHgUhga72U-3Y%2Fimage.png?alt=media\&token=c4a55cfb-ad31-4208-b19a-d1a9146a23d9)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuDR5qw7es4mZyY7O2%2F-MVuQm8Wvg7lScWcNLuc%2Fimage.png?alt=media\&token=75b89f86-e3c7-4068-844d-b2e8485cadfb)

sudo yum -y install yum-utils

sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

sudo yum -y install iotop iperf3 iptraf tcpdump git bash-completion

sudo yum -y install httpd php mysql php-mysql

sudo yum -y install python-pip

sudo yum -y install nethogs iftop lnav nmon tmux wireshark vsftpd ftp stress

sudo systemctl start httpd

sudo systemctl enable httpd

sudo git clone https://github.com/whchoi98/ec2meta-webpage.git

sudo systemctl restart httpd

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuRV6_1oa5Bkgg_2gA%2Fimage.png?alt=media\&token=de81ccac-8726-4072-af5f-d8135a709394)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuR_m8FoUrUAEY6tSv%2Fimage.png?alt=media\&token=051355bc-36dd-45a2-bef7-76eb3a8c7f74)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuRpBurvY2wpYrMMqx%2Fimage.png?alt=media\&token=8c40c7ca-c105-4f41-b448-2b7889d4c3a0)

* **태그 추가 - 키 : Name , 값 : ASG-EC2**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuS3PA2-mIGL6i5Gry%2Fimage.png?alt=media\&token=0b84ac39-cec7-4d9a-9e18-ee18792c49d3)

* **보안 그룹 구성 - 기존 보안 그룹 선택 - IMD-PUB-SG**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuSO2bOqxQLFxd9W6L%2Fimage.png?alt=media\&token=b6996b68-21a4-4bb1-87a0-d1794e1a3696)

* 기존 키 페어 선택 - IMD-PUB-PUTTY

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuSf9bw43jBO1QIZ03%2Fimage.png?alt=media\&token=f081c72b-5ce2-490e-ac3d-459979b12982)

#### 2. 생성된 AutoScale Group 용 인스턴스 확인 <a href="#id-2.-autoscale-group" id="id-2.-autoscale-group"></a>

AutoScale Group 용으로 생성된 인스턴스를 확인합니다. 해당 인스턴스는 AutoScale Group을 위한 인스턴스 템플릿으로 생성할 것입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuQvcTXu9cb33fWf74%2F-MVuT--ly574GunWcMaY%2Fimage.png?alt=media\&token=3fad8474-8773-4c8c-ab8c-61918b1c3b50)

인스턴스 메뉴에서 생성한 인스턴스를 선택 - 작업 - 이미지 및 템플릿 - 인스턴스에서 템플릿 생성을 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVue9jGtXg4BhapXHPD%2F-MVulkc8Y3iwsoip0B0I%2Fimage.png?alt=media\&token=37204802-f062-4cef-b67c-e3a00b9a8492)

**아래에서 처럼 시작 템플릿 이름을 선언하고, 나머지 값은 그대로 사용합니다.**

* **나머지 값은 기본 값을 그대로 사용하고, 시작 템플릿을 선택합니다.**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVunICc4WOblsRLTn09%2F-MVunefHTzP7qF_rPrw8%2Fimage.png?alt=media\&token=bc6ac6ca-2850-4823-85ca-0462c6805d7b)

* 시작 템플릿이 완성되었습니다. 해당 템플릿을 이용해서 Auto Scaling Group을 만들 것입니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuprrfx1Mp5h1r0-03%2F-MVuqpj1BtZCkqCou9QK%2Fimage.png?alt=media\&token=05017950-a146-4854-a641-3f40b603ae60)

### Task2 : Auto Scaling 시작 구성 (Auto Scaling Launch Config) <a href="#task2-auto-scaling-auto-scaling-launch-config" id="task2-auto-scaling-auto-scaling-launch-config"></a>

* **EC2 대시보드 - AutoScaling - Auto Scaling Groups (새로 만들기) 를 선택합니다.**

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuprrfx1Mp5h1r0-03%2F-MVurIcY6QAmiY6diUGg%2Fimage.png?alt=media\&token=f4f687e2-667f-4da9-aa2a-2d71eb31f54b)

* Auto Scaling 그룹 이름을 선언하고, 앞서 생성한 시작 템플릿을 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuprrfx1Mp5h1r0-03%2F-MVurqnN28yaWVER3lH2%2Fimage.png?alt=media\&token=ac4d8809-f974-452d-92c2-13fb6f0f9511)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuprrfx1Mp5h1r0-03%2F-MVusfEdlonX1TJTtmNA%2Fimage.png?alt=media\&token=9decc229-710e-40f7-a904-4af6edb7cd54)

* 서브넷 - AutoScaling Group을 배포할 Subnet 선택

여러개 서브넷에 배포하는 방식은 ELB와 함께 구성합니다. 여기에서는 AutoScaling Group 동작 방식을 보기 위해 구성하는 것입니다.

테스트를 위해서 상태 확인 유예 기간을 10초로 조정하고, 모니터링 Cloudwatch 내에서 그룹 지표 수집 활성화를 선택합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVustCVWoMviQJvsyb7%2F-MVutTORErBwxdmdqeHj%2Fimage.png?alt=media\&token=452a0cc6-b371-4202-afad-e3a03b1cb2d1)

대부분의 경우, 서비스 상태가 된 직후의 Auto Scaling 인스턴스는 웜 업을 거쳐야 상태 확인을 통과할 수 있습니다. Amazon EC2 Auto Scaling은 상태 확인 유예 기간이 끝날 때까지 기다린 후 인스턴스의 상태를 확인합니다. Amazon EC2 상태 확인과 Elastic Load Balancing 상태 확인은 상태 확인 유예 기간이 끝나기 전에 완료될 수 있습니다. 하지만 Amazon EC2 Auto Scaling은 상태 확인 유예 기간이 종료되기 전에는 그러한 상태를 반영하지 않습니다. 인스턴스에 충분한 웜 업 시간을 제공하려면 상태 확인 유예 기간이 애플리케이션의 예상 시작 시간을 포함하도록 해야 합니다. 수명 주기 후크를 추가할 경우 유예 기간은 수명 주기 후크 작업이 완료되고 인스턴스가 `InService` 상태로 전환되기까지 시작되지 않습니다.

상태 확인 유예 기간은 초 단위입니다. 따라서 예를 들어 300초를 지정하면 5분 간격이 생깁니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVustCVWoMviQJvsyb7%2F-MVuvSb8ZjD3Y9WTpybc%2Fimage.png?alt=media\&token=344fb780-62ad-46dc-876c-e5863682cb55)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVustCVWoMviQJvsyb7%2F-MVuvlwBtMcB6rP-Udq3%2Fimage.png?alt=media\&token=29746477-e567-4921-bf7b-13997a6fa678)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVustCVWoMviQJvsyb7%2F-MVuvw_UAhmMTI0WO9Q_%2Fimage.png?alt=media\&token=883a466a-eb48-47ba-bf94-a468f22984cc)

* **AutoScaling 그룹 생성을 완료합니다.**
* 알림 수신을 설정한 이메일에 **SNS 승인요청**이 기다리고 있습니다. 수락하시기 바랍니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVuyWYrwfZWaJ2j9M6o%2Fimage.png?alt=media\&token=a1f00261-74d5-4525-a3bc-1259146b2ab1)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVuybfvnAZ_cmWUtUt_%2Fimage.png?alt=media\&token=a26013d9-14e9-49c4-b7ee-7b9f74019ce1)

잠시 후 아래와 같이 인스턴스가 생성된 것을 확인 할 수 있습니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVuzF4-tcnXUFK8uAOf%2Fimage.png?alt=media\&token=95e1c83b-6ca3-4bc0-88ee-64fdbaf7dd4c)

Auto Scaling 그룹에 생성된 그룹을 선택하고 , 인스턴스 관리 탭을 확인 해 봅니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVuzWiXKi9RqRndhTv1%2Fimage.png?alt=media\&token=84fef1f9-04d9-4546-816c-3343a5f0690a)

* 생성된 각각의 EC2 인스턴스에서 CPU 로드를 생성합니다. 화면을 분할하고 "top" 명령을 통해 CPU Load를 확인합니다.

생성된 EC2 인스턴스에 tmux 가 설치되어 있습니다. 화면 분할을 통해 명령을 top 를 입력해 봅니다.

화면 분할 - ctrl + b , % 화면 이동 - ctrl + b, 이동

sudo stress --cpu 1 --timeout 600

AutoScaling Group에 할당한 인스턴스 타입의 CPU 숫자에 맞추어서 위의 명령을 조정합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-M7CSJey4dJjvrv0Og03%2F-M7DXW2LpCY2NDRCFGaO%2Fimage.png?alt=media\&token=ccdd45f3-d64c-4c74-8622-c8fa5fd425d1)

* EC2 인스턴스의 모니터링에서 Cloudwatch를 통해 1분간 평균 CPU를 확인합니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVv5TcCOi9eSjmH0Gy1%2Fimage.png?alt=media\&token=437e3473-ed62-4f92-a284-ebb351b62a15)

* 수분 뒤에 인스턴스가 증가하는 지 확인합니다. (Auto Scaling 그룹과 EC2 대쉬보드에서 확인)

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVuw-vBcEQOzOVZaS3Y%2F-MVv4pvKMKd3GZKWI5je%2Fimage.png?alt=media\&token=815c4fe0-30a9-452d-8ddd-32c2a64fcaba)

* CPU Stress가 종료된 수분 뒤에 인스턴스가 감소 하는 지 확인합니다. (Auto Scaling 그룹과 EC2 대쉬보드에서 확인)

앞서 생성한 Auto Scaling Group의 SNS가 계속해서 메세지를 통보하게 됩니다.

![](https://1144846305-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6E6esvG0nVqh6wA9AB%2F-MVv9y3H69A79sG2M26v%2F-MVvA9SEvftC58SDNL1l%2Fimage.png?alt=media\&token=0e897f3c-d7b4-4488-bae9-33a9a13996dd)

성공적으로 Auto Scaling 그룹 랩을 마치셨습니다.
