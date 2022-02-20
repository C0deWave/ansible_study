# Ansible 구성 파일 및 옵션 알아보기

### 엔서블 실행시 참조하는 주요 파일

* /etc/ansible/ansible.cfg

      ansible의 각종 설정을 건들리 수 있습니다.

* /etc/ansible/hosts

      Ansible이 접속하는 호스트 들에 관한 정보가 있습니다.

### 앤서블 실행시 자주 이용하는 옵션 값

    -i (--inventory-file) : 적용될 호스트들에 대한 파일
    hosts 에 등록된 파일 중에서 일부 호스트에 대해 적용
    인벤토리 파일이 필요함 (ex. inventory.ini)
    
    명령어 예제
        ansible all -i intentory.ini -m ping
    
    all 대신에 그룹명으로도 호스트 특정 가능
        ansible nginx -m ping

[]()

    -m (--module-name) : 모듈을 선택
    -m ping의 경우 일반적인 ping가 아닌 파이썬 모듈을 활용한 ping이다.
    내장 모듈에서 직접 호출해서 실행
    ansible nginx -m ping -k
    
[]()
    
    -k (--ask-pass) : 패스워드를 물어보도록 설정
    ssh로 접속시 암호 입력에 사용된다.

[]()  
    
    -K (--ask-become-pass) : 권리자로 권한상승
    sudo 패스워드를 입력한다.

[]()

    --list-hosts : 적용되는 호스트들을 확인
    맨 뒤에 붙여서 해당 명령어를 받았을 때 실행될 호스트 목록을 알아볼 수 있다.
