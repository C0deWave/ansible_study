# ansible 설치해보기

## 목표:

    ansible를 설치해보고 node에 Ping 날려보기

----

실습은 AWS 인스턴스를 3개를 만들어서 진행해 보았습니다.

### 서버 환경: 

* 인스턴스 개수: 3개 (1개의 노드에만 ansible설치)
* OS: Amazon Linux 2 AMI (HVM) - Kernel 5.10

----

* 엔서블을 설치한다는 것은 엔서블 코어를 설치하는 것을 말합니다.

### 엔서블 코어란?

    엔서블을 동작한는데 필요한 최소한의 패키지 모음

엔서블은 agent가 필요하지 않기 때문에 관리서버 1대에만 엔서블 코어를 설치합니다.

----

기본 저장소에는 ansible가 없기 때문에 엑스트라 저장소인 epel저장소를 추가합니다.

앤서블 저장소 추가

    sudo amazon-linux-extras install epel

엔서블 설치

    sudo yum install ansible

엔서블의 설치가 완료되면 

    ansible --version 
    
을 눌러서 설치가 잘 되었는지 확인합니다.

ansible all -m ping -k 를 해도 제공된 호스트 리스트가 없다는 명령이 나오는 것을 확인할 수 있습니다.

호스트 리스트를 추가하기 위한 명령어

    vi /etc/ansible/hosts

아래에 접근할 인스턴스의 ip를 입력합니다.

그후 다시 

    ansible all -m ping

을 하면 퍼블릭 키 교환을 할것인지 묻는 내용이 나옵니다. yes를 눌러서 known_host에 기록합니다.

aws의 경우는 pem 키파일을 통해서 인증을 진행합니다.

따라서 접근하기 위해서는 pem 키 파일을 가지고 이를 이용해서 인증을 진행해야 합니다.

먼저 ansible 폴더로 이동합니다.

    cd /etc/ansible

해당 폴더에서 인증을 위한 인벤토리 파일을 만들어 줍니다.

    vi inventory.ini

    #### 아래는 내용 ####
    #### 변수를 이용해 파이썬 3버전 지정 => 위험 차단 ####
    [ansible]
    ansible2 ansible_user=ec2-user ansible_host=<<호스트 IP>> ansible_ssh_private_key_file=<<키파일 위치>>
    ansible3 ansible_user=ec2-user ansible_host=<<호스트 IP>> ansible_ssh_private_key_file=<<키파일 위치>>

    [ansible:vars]
    ansible_python_interpreter=/usr/bin/python3

그후에 해당 이름을 통해서 인증을 진행해 봅니다.

    ansible -m ping all -i inventory.ini

핑이 잘 가는 것을 볼 수 있습니다.

![](https://raw.githubusercontent.com/C0deWave/ansible_study/a03596d526cd55897e3f4908492db9f1523f3950/Res/ansible%EC%84%A4%EC%B9%98.png)