# EC2

**0. EC2 이해를 위한 선결조건**
- 클라우드 컴퓨팅이란 무엇인가? <br/>
: 인터넷을 통해 호스팅한 서비스를 제공하는 것의 총체를 의미한다. 클라우드 컴퓨팅을 이용하면 정보를 인터넷에 연결된 다른 컴퓨터로 처리할 수 있다.<br/> 

[출처 1](https://searchcloudcomputing.techtarget.com/definition/cloud-computing), [출처 2](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C_%EC%BB%B4%ED%93%A8%ED%8C%85)   

- Infrastructures as a Service (IaaS) <br/>
: 인터넷 상에서 가상화된 컴퓨팅 자원을 제공하는 클라우드 컴퓨팅의 한 형태를 뜻한다.<br/> 

[출처](https://searchcloudcomputing.techtarget.com/definition/Infrastructure-as-a-Service-IaaS)

**1. EC2 소개**

<p>
Amazon Web Services (AWS) 클라우드에서 제공하는 확장식 컴퓨팅으로, IaaS에 해당한다. 
</p>

**2. EC2 특징**
- Amazon Machine Image (AMI), 인스턴스 개념 존재. <br/>
: 소프트웨어 구성이 기재된 템플릿인 AMI가 존재하며, 이를 통해 가상 컴퓨팅 환경인 인스턴스를 시작할 수 있다.
- 다양한 유형 존재.<br/>
: 유형에 따라 CPU, 메모리, 스토리지, 네트워킹 용량의 구성이 다르다. 
- 두 가지 스토리지 사용.<br/>
: 임시 데이터를 저장하는 인스턴스 스토어 볼륨과 영구 스토리지 볼륨인 Amazon Elastic Block Store (EBS)를 사용할 수 있다.
- 고정 IP 주소 제공. <br/>
: 탄력적 IP 주소(Elastic IP, EIP)라는 동적 클라우드 컴퓨팅을 위한 고정 IPv4 주소를 제공해 매번 링크를 새로 딸 필요가 없다.
- 태그 기능 제공. <br/>
: 태그로써 사용자가 생성하여 Amazon EC2 리소스에 메타데이터를 할당할 수 있다.
- 다양한 보안 기능 제공. <br/>
: 키페어로 인스턴스 로그인 정보를 보호하며, 보안 그룹을 설정해 인스턴스에 연결할 수 있는 프로토콜, 포트, 소스 IP 범위 지정하는 방화벽 기능이 존재한다.
- Virtual Private Clouds (VPC) 존재. <br/>
: VPN과 같은 기능으로, 이를 통해 고객의 네트워크, AWS 내 다른 서비스와 통신할 수 있다.
- 자동화 가능. <br/>
: Amazon CLI, boto3 (Python)으로 자동화가 가능하다.

**3. EC2 활용 사례** [출처](https://aws.amazon.com/ko/solutions/case-studies/amore-pacific/) 
- 아모레퍼시픽은 글로벌 서비스에 Amazon EC2 등의 서비스를 활용해 초기 투자비와 운영비를 절약하고 있다.
> "글로벌 서비스를 위해 미국, 유럽, 아시아 등 전 세계에 구축된 리전의 가용성과 안전성을 고려하여 AWS 클라우드를 도입하기로 결정했습니다. 사용한 자원에 대해서만 비용을 지불하는 과금 구조가 TCO 및 운영 비용 절감이라는 아모레퍼시픽의 계획과 부합했기 때문입니다. 아모레퍼시픽은 현재 Amazon EC2와 Amazon RDS, Amazon S3, Elastic Load Balancing 등으로 인프라를 구축해 사용하고 있습니다. ... (후략)"

<img src="https://d1.awsstatic.com/logos/customers/Amore-Architecture.3046f5af2665ade5ba2e87611f107a3fedfca9ed.png">
 


