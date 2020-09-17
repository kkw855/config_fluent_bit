##설치
/etc/yum.repos.d/td-agent-bit.repo 파일을 만들고 아래 내용 추가  
[td-agent-bit]   
name = TD Agent Bit  
baseurl = https://packages.fluentbit.io/centos/7/$basearch/  
gpgcheck=1  
gpgkey=https://packages.fluentbit.io/fluentbit.key   
enabled=1   

$ yum check-update   
$ yum install td-agent-bit   
$ yum service td-agent-bit start   

##시스템 로그 수집 설정
/etc/rsyslog.d/60-fluent-bit.conf 파일 만들고 아래 내용 추가  
OS system 로그를 수집하기 위해서 필요한 설정   
action(type="omfwd" Target="127.0.0.1" Port="5140" Protocol="tcp")   
$ sudo service rsyslog restart   

##설정 적용 위해서 재시작
$ sudo service td-agent-bit restart  
$ sudo service td-agent-bit status -l   