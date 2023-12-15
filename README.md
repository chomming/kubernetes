# 진행 과정
ALB --> 대상 그룹 --> Node --> Pod

# Cluster
node들의 집합

# Deployment
ReplicaSet의 상위 개념
</br>
AWS의 EC2(인스턴스)와 동일
</br>
pod와 ReplicaSet에 대한 배포 관리
</br>
kubectl apply -f deployment.yaml로 생성 가능

# ReplicaSet
동일한 여러 pod가 동시에 실행될 수 있도록 관리

# Service
pod의 논리적 집합
</br>
AWS의 대상 그룹과 동일
</br>
종류
- ClusterIP : cluster 내부에서만 접근 가능한 IP
- NodePort : Port 번호를 통해 외부에서 접근 가능
- LoadBalancer : 외부의 LoadBalancer 사용
- ExternalName  : kube-dns component로 DNS 이용

# Ingress
외부 요청을 어떻게 처리할 것인지 정의
- 어디로 가세요
AWS의 ALB와 동일
</br>
담당
- 특정 경로로 들어온 요청을 어떤 서비스로 전달할지 정의하는 라우팅 규칙
- 가상 호스트 기반의 요청 처리
- SSL/TLS 보안 연결 처리
[ingress.yaml](https://github.com/chomming/kubernetes/blob/main/ingress.yaml)

# Role
권한 모음

# ClusterRole
Cluster 단위로 접근 권한 제어를 위해 사용됨

# ServiceAccount
kubernetes cluster 내에서 실행되는 pod가 API 서버와 상호 작용할 수 있도록 권한을 부여하는 데 사용되는 자격증명

# Node
가상머신
</br>
master node
- kubernetes cluster 관리 시스템
- 구성요소
  - kube-apiserver : kubernetes의 중심이 되는 요소
  - kube-scheduler : kubernetes의 pod/service 등을 node에 할당
  - kube-controller : kubernetes의 controller 생산 및 배포 관리
    - controller : cluster의 상태 관찰 --> 필요한 경우에 생산/변경 요청
worker node
- 개발자가 정의한 container가 실행되는 노드
- 구성요소
  - kubelet
    - pod를 생성하기 위해 container runtime에 요청
    - object의 상태 모니터링 및 체크 --> kube-apiserver에 전달
  - kube-proxy
    - 각 노드에서 실행됨
    - 각 서비스에게 도달하는 데 사용됨
    - node에 오는 트래픽을 적절히 라우팅해줌
  - container runtime : container 실행 구성요소

# Pod
kubernetes에서 사용하는 container application의 기본 단위(가장 작은 배포 단위)
</br>
고유의 cluster IP를 가짐

# DaemonSet
cluster 전체 node에 특정 pod를 실행할 때 사용하는 controller

# Secret
비밀번호, OAuth 토큰, ssh 키와 같은 민감 정보들을 저장하는 용도로 사용됨
</br>
container 안에 저장하지 않고, 별도로 보관 --> pod 실행 시 설정을 통해 container에 제공해줌

# Namespace
단일 클러스터 내에서 환경 격리
