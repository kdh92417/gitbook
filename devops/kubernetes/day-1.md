# Day 1



## 12. ETCD For Beginners

> ETCD is a distributed reliable key-value store that is **Simple, Secure & Fast**

## Key-Value 저장소는 무엇인가?

> 문서나 페이지의 형태로 정보를 저장

* 개인에 관한 모든 정보가 분산되어 해당 파일에 저장
* 어떤 형식이나 구조로든 저장될 수 있다.
* 한 파일의 변화는 다른 파일에 영향을 주지 않는다.
* 복잡해지면 `JSON` or `YAML` 같은 데이터 포맷을 사용

## ETCD를 어떻게 사용하는가?

````
```
# RUN ETCD Service
./etcd

# Set Value in VERSOIN 2
./etcdctl set key1 value1

# Get Value in VERSOIN 2
./etcdctl get key1
>> value1
````

### ETCD Version

* 현재 버전이 3까지 나왔고, 중간의 버전 2와 버전3 사이에서 API 버전이 바껴, etcdctl 명령어도 많이 바뀌었다.
* etcdctl 명령어는 버전2와 버전3에 동시 작동하도록 구성돼 있다.

```
# 밑의 명령어를 통해 ETCD 버전을 체크, ETCD V2
./etcdctl --version
>> etcdctl version: 3.3.11  # ETCD 유틸리티 버전
>> API version: 2  # ETCD API 버전

# 해당 명령어를 통해 V2 명령어 정보를 알 수 있다.
./etcdctl

# 새로운 ETCD 버전에선는 API 버전이 V3로 설정된다.
# API V3 로 설정
export ETCDCTL_API=3

# version 명령어로 버전 체크(API V2 와는 다르게옵션이 아님)
./etcdctl version
>> etcdctl version: 3.3.11  
>> API version: 3.3

# Set Value in VERSOIN 3
./etcdctl put key1 value1

# Get Value in VERSOIN 3
./etcdctl get key1
>> value1
```



## 13. ETCD in Kubernetes

> 챕터 12에서 ETCD는 Key-Value 형태의 저장소라는 것을 알게되었고, 이러한 ETCD가 쿠버네티스에서 어떤 역할을 하는 지 알아보자

### 클러스터에대한 정보를 저장

밑의 상세정보에대한 내용을 ETCD에 저장하고, 클러스터에대한 정보에 변화를 줄때(Pods가 추가되거나 Nodes가 추가되거나 등..) ETCD 서버에 반영되고, ETCD 서버에 해당 정보가 반영되어야 변화가 완료된 것으로 간주된다.

* Nodes
* Pods
* Configs
* Secrets
* Accounts
* Roles
* Bindings
* Others



* 쿠버네티스에는 2가지 배포유형이 있다.
  * 처음부터 배포하는 것
  * kubeadm 을 이용하여 배포하는 것
* 해당 코스에는 처음에는 kubeadm을 이용해서 배포하고 나중에 처음부터 셋업하는 과정을 경험하게된다.
* 2가지 방법의 차이점을 아는 것이 좋다.
* 클러스터를 스크래치에서 셋업하는 경우 ETCD의 바이너리를 직접 다운로드하여 마스터노드에 배포한다.

```
wget -q --https-only \ "https://github.com/coreos/etcd/releases/download/v3.3.9/etcd-v3.3.9-linux-amd64.tar.gz"
```





## 14 ETCD - Commands (Optional)

> ETCDCTL은 ETCD 서버와 상호작용할 때 사용되는 CLI 도구ㅇ이다.

* ETCDCTL은 API 버전 2 와 3 두가지 버전을 지원
* 기본적으로 API 버전 2를 사용
* API 버전 2와 3는 서로다른 명령어 세트를 가지고 있다.
  * etcdctl backup(V2) -> etcdctl snapshot save(V3)
  * etcdctl cluster-health(V2) -> etcdctl endpoint health(V3)
  * etcdctl mk(V2)
  * etcdctl mkdir(V2)
  * etcdctl set(V2) -> etcdctl put(V3)



### ETCDCTL API 버전 3로 설정

ETCDCTL\_API 환경변수를 사용하여 API 버전을 설정해야됨(설정하지않으면 기본 V2로 설정)

또한, 인증을 위해 인증서 파일의 경로를 지정해야됨



인증서 파일은 `etcd-master 에서 다음 경로에서 사용할 수 있다.`

* \--cacert /etc/kubernetes/pki/etcd/ca.crt
* \--cert /etc/kubernetes/pki/etcd/server.crt
* \--key /etc/kubernetes/pki/etcd/server.key



**ETCDCTL V3로 설정 예시 명령어**

```
kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt --key /etc/kubernetes/pki/etcd/server.key"
```





## Kube-API Server



