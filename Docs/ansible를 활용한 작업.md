# Ansible 작업 예시

* uptime확인하기

[]()

    ansible all -i inventory.ini -m shell -a "uptime"
    shell을 이용해서 shell 명령어를 입력한다. -a 옵션은 argument옵션으로 보낼 명령어를 입력한다.

* 디스크 용량 확인하기

[]()

    ansible all -i inventory.ini -m shell -a "df -h"

* 메모리 상태 확인하기

[]()

    ansible all -i inventory.ini -m shell -a "free -h"

* 새로운 유저 만들기

[]()

    ansible all -i inventory.ini --key-file="/etc/ansible/awskey.pem" -m user -a "name=jmjang password=1234" -become
    엔서블에는 유저 생성을 도와주는 user 모듈이 있다.
    이 경우 암호를 그대로 보냈기 떄문에 복호화를 거치지 않아 해당 비밀 번호로 로그인 할 수 없습니다.
    로그인까지 가능하게 하는 방법은 추후에 다뤄 봅니다.

* 파일 전송하기

[]()

    ansible all -m copy -a "src=./jmjang.txt dest=/tmp/" --key-file="/etc/ansible/awskey.pem"
    파일을 전송합니다.

* 서비스 설치

[]()

    ansible all -m yum -a "name=httpd state=present" --key-file="/etc/ansible/awskey.pem" --become
    yum 모듈이 ansible_python_interpreter의 버전이 파이썬 3이상일 경우 작동이 되지 않고 dnf 모듈을 사용하라고 나옵니다. 현재는 파이썬2 버전대에서 위의 명령어를 이용해서 httpd 를 설치했습니다.
    yum과 마찬가지로 apt 모듈도 존재합니다.


