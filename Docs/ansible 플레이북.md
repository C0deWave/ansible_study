# Ansible playbook

### ansible playbook이란? 

- 작업내용을 파일로 만들어서 여러가지 반복적인 작업을 효율적으로 단축할 수 있습니다.
- 여러 작업의 단계를 검증하면서 진행할 수 있습니다.
- 이러한 작업의 정의목록을 ansible playbook이라고 합니다.
- yaml 형식으로 작성합니다.(띄어쓰기 주의!)
- 멱등성을 가집니다.

[]()

    멱등성: 연산을 여러번 적용하더라도 결과가 달라지지 않는 성질
    예제) 한번 추가된 사용자를 또 추가할 경우 중복되어 에러가 나타날 수 있다.
    => playbook은 멱등성을 가져서 이미 있는 경우 자동으로 넘어간다.
    => 즉 여러번 실행할 경우 변경이 되지 않는다.   

---

### 사용 예시

    다수의 서버에 웹서비스를 설치 및 가동해야 할 경우

---

### 사용 방법

- 먼저 .yml을 가진 yaml파일을 만들어 줍니다.
- tab을 이용하지 않고 띄어쓰기를 이용해서 구분합니다.
- ansible특정 파일에 내용 추가하기
~~~
    ---
    - name: Ansible_node
    hosts: localhost

    tasks:
        - name: Add ansible hosts
        blockinfile:
            path: /etc/ansible/tests
            block: |
                [test]
                1.1.1.1
~~~
- ansible 웹 서버 설치후 실행하기
~~~
---
- hosts: nginx
  remote_user: ec2-user
  tasks:
      - name: install epel-release
        shell: amazon-linux-extras install -y epel
      - name: install nginx web server
        yum: name=nginx state=present
      - name: Start nginx web server
        service: name=nginx state=started
      - name: firewall down
        shell: systemctl stop firewalld 
~~~
- 실행 명령어: ansible-playbook nginx_playbook.yml --key-file="/etc/ansible/awskey.pem" --become

---

## 실행샷

한번 실행을 해서 두번째에는 다시 실행이 되지 않는 것을 볼 수 있습니다.

![실행이미지](https://raw.githubusercontent.com/C0deWave/ansible_study/b38cc79a25e4bb3cb45be174bca2584a712ced50/Res/ansible%ED%94%8C%EB%A0%88%EC%9D%B4%EB%B6%81%20%ED%85%8C%EC%8A%A4%ED%8A%B8.png)

![결과이미지](https://raw.githubusercontent.com/C0deWave/ansible_study/b38cc79a25e4bb3cb45be174bca2584a712ced50/Res/ansible%20%ED%94%8C%EB%A0%88%EC%9D%B4%EB%B6%81%20%EA%B2%B0%EA%B3%BC.png)