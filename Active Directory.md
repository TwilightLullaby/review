Active Directory 목차
=======
1.Active Directory의 개념 및 관련 용어의 이해    
2.Active Directory의 도메인 서비스 환경 구축 실습     
3.도메인 컨트롤러 구성 실습               
4.Active Directory 설정 및 통합 관리 실습     
> 목차는 총 4가지 단계로 구성되어 있다

* * *
* * *

Active Directory개념
=======
> Active Directory는 회사 직원들이 계정 정보,회사에서 강제하고 하는 정책들(ex)패스워드를 일주일마다 변경, 5분동안 안움직이면 화면보호기가 켜지든가 등등..)일종의 데이터베이스이다       
+ 기본적으로 암호화 되어있어 보안성이 뛰어나다 
+ 네트워크 자원에 접근하기 쉽다   
+ 네트워크 자원은 사용자 계정,프린터,등등 주변기기를 말한다         
## 요약 : 중앙의 데이터베이스 기준으로 저장해놓고 그 기준으로 바뀌는것(본사 컴퓨터가 규칙을추가하면 나머지 컴퓨터들도 적용)
아래의 사진은 액티브 디렉토리의 개념을 그림으로 표현했다   
![image](https://user-images.githubusercontent.com/76859458/112260378-24d37200-8cad-11eb-9093-46eca935db1f.png)

Acitive Directory 도메인서비스
=======
> 컴퓨터,사용자 기타 주변장치에 대한 정보를 네트워크상 저장하면 Active Directory 도메인 서비스는 이러한 정보들을 관리자가 통합하여 관리하게 된다. 이렇게하면 사용자는 네트워크에 편리하게 자원들을 공유할수있으며 공동으로 작업도 가능해진다 Active Directory 도메인 서비스를 사용하기 위해서는 기본적으로 DNS서버를 설치해야한다    
+ 네트워크 자원은 위에 서술되어있다        
+ 도메인 서비스를 이용하기위에는 도메인 서버를 설치해야한다 후에 설명할거다    
## 요약 : Active Directory 핵심 개념인 관리자가 관리하는 기능을 만들기위해서는 도메인 서비스가 필요하다

DNS
==
+ DNS는 도메인네임서버를 일컫는다       
+ 인터넷의 서버들은 ip로 구성되어있다 인간이 ip를 외우기 힘드니 인간의 언어로 바꾼거다 ex)www.naver.com    
+ DNS가 왜 지금 나오냐면 4개의 가상머신 만든것중에 퍼스트를 DNS서버로 둘 것 이기 때문이다                 
+ 기존의 4개 서버는 8.8.8.8(구글)DNS를 사용했다 하지만 퍼스트의 DNS서버를 이용해 인터넷 연결을 할것이다      
## 요약 : 도메인 ex)www.naver.com 인간의 언어를 ip로 바꿔서 인터넷에 접속하게 해주는것 (정방향)


도메인
==
+ 도메인은 맨 뒤에 숨어진 .(루트 도메인)이 숨겨져있다
+ 그래서 www.naver.com. 이렇게 . 하나 더있다
+ 읽을때 .(루트도메인)->com->naver->www 이렇게 읽는다
![image](https://user-images.githubusercontent.com/76859458/112264597-759a9900-8cb4-11eb-9674-f5c204564920.png)
## 요약1 : ip에 이름 붙인것 도메인은 뒤에서부터 읽는다 (역방향)
## 요약2 : 도메인은 하나의 범위다

단어
=====
![image](https://user-images.githubusercontent.com/76859458/112397144-dbcefc80-8d44-11eb-85c2-fcf32ab9f96c.png)     

트리와 포리스트
-------
+ 도메인의 집합
+ 트리가 모이면 포리스트(포레스트)
+ 도메인<트리<포트리스
* * *
### 요약 : 도메인이 모이면 트리 ,트리가 모여서 포리스트
* * *
사이트
-------
+ 도메인이 논리적인 범주라면, 사이트는(Site)는 물리적인 범주
+ 서울 본사와 일본 사무실은 같은 도메인인지만 사실은 상당히 떨어져있다
+ 그러므로 서울 본사와 일본 사무실은 같은 도메인이지만 별도의 사이트로 구성된다
### 요약 : 서울본사와 일본 사무실은 같은 도메인일지라도 물리적으로 멀리 떨어져있으므로 별도의 사이트로 구성된다      
* * *
트러스트
-------
+ 한마디로 신뢰
+ 포리스트안에서는 양방향전이 트러스트(Trust)를 갖는다 
### 요약 : 트러스트는 신뢰할수있는가에 대한 의미이다 ex)트러스트를 갖는다 = 신뢰를 갖는다
* * *
조직 구성 단위
-------
+ 조직 구성 단위(Organizational Unit, OU)
+ 한 도메인 안에서 세부적인 단위로 나누는 것을 말한다
+ 서울 본사를 관리부,회계부,기술부 등의 부서를 나눈다면 "부서"에 해당되는걸 조직 구성 단위라고함
### 요약 : 단위 그냥 분리? 위에 3번쨰 설명 예시를 보면 이해가감

도메인 컨트롤러
----
+ 로그인,이용권한 확인,새로운 사용자 등록,암호 변경등을 처리하는 기능을 하는 서버 컴퓨터를 도메인 컨트롤러(Domain Conoralr)
### 요약 : 어드민 권한이 가지는 액티브 디렉터리의 핵심기능임
* * *

읽기전용 도메인 컨트롤러
----
+ 도메인컨트롤러 하위호환
+ Active Directory와 관련된 데이터를 전송 받아서 저장한후 사용
+ 스스로 데이터를 추가하거나 변경하지는 못함
### 요약 : 유저들이 쓰는것 도메인 컨트롤러의 엄청 하위호환


* * *

글로벌 카탈로그
-------
+ Active Directory 트러스트 내의 도메인들의 포함된 정보를 수집하여 저장되는 저장소를 Global Cartlog(GC)라고한다
+ 예를들어 이름,로그인아이디,비밀번호 등의 정보가 입력된다
### 요약 : 데이터 저장하는것(비밀번호,아이디 등등)





* * *
* * *
윈도우 서버 변경 방법
==========
### 윈7서버 : 서버관리자>도구>컴퓨터관리>로컬사용자및 그룹>사용자>어드미니스트레이트>오른쪽 클릭 암호설정     
![image](https://user-images.githubusercontent.com/76859458/112742986-5fe7e500-8fce-11eb-859a-ee24395fbf5c.png)

### 윈10:서버관리자 없으므로 실행창에서 명령어 입력 compmgmt.msc = 윈도우키누르고 컴퓨터 관리 클릭        
![image](https://user-images.githubusercontent.com/76859458/112742994-6fffc480-8fce-11eb-802d-c9ecd0e61cd9.png)

* * *
Active Directory설치
=====
+ 1.서버 관리자    
+ 2.관리    
+ 3.역할 및 기능추가  
+ + ![image](https://user-images.githubusercontent.com/76859458/112743129-92dea880-8fcf-11eb-9522-7a0c4a66fc45.png) 
+ 4.시작하기 전
+ 5.설치 유형
+ 6.서버선택
+ 7.도메인서버
+ 8.기능추가
+ 9.ADDS에서
+ 10.확인에서 필요한경우 자동으로 ~를 체크한후 설치 클릭
+ 11.서버관리자 알림을 클릭하고 이 서버를 도메인 컨트롤러로 승격을 클릭한다
+ 12.새프리스트를 추가합니다
+ 13.루트 도메인이름을 yonsai,.com를 입력
+ 14.도메인 컨트롤러 옵션에서 DNS 서버,GC(글로벌 카탈로그) 비밀번호 Yons@i602
+ 15.DNS옵션 아무것도 누르지말고 다음 누른후 잠시 대기하기
+ 16.netbios도메인 이름에 자동으로 yonsai로 입력
+ 17.검토옵션
+ 18.필수구성요소확인에서 검증작업 마치기(경고 몇개뜨는데 무시하자)
+ 19.연사이 어드미니스티레이터는 yonsai도메인의 natbios이다

설치 사진버전
----
![image](https://user-images.githubusercontent.com/76859458/112743155-d6391700-8fcf-11eb-9780-1a7c1bc993c1.png)                 
![image](https://user-images.githubusercontent.com/76859458/112743159-d9340780-8fcf-11eb-958f-0f675ba9f618.png)                    
![image](https://user-images.githubusercontent.com/76859458/112743163-e0f3ac00-8fcf-11eb-9a42-fed480b438b2.png)            
![image](https://user-images.githubusercontent.com/76859458/112743186-139da480-8fd0-11eb-9d1c-cf2cacc1d336.png)            
![image](https://user-images.githubusercontent.com/76859458/112743193-18625880-8fd0-11eb-8f5e-4ac1550b00fc.png)              
* * *


도메인에 컴퓨터 등록하기   
====
+ 1.ncpa.cpl가서 DNS서버 주소를 변경한다 192.168.111.10(퍼스트)로 바꾸자
+ 2.스크롤락오른쪽키+윈도우 누르면 아래의 이미지가 나온다
+ + ![image](https://user-images.githubusercontent.com/76859458/112752537-80379400-900e-11eb-8bf6-e6b4b7818874.png)
+ 3.아래처럼 DNS서버를 바꾸자
+ + ![image](https://user-images.githubusercontent.com/76859458/112752571-a52c0700-900e-11eb-8d53-b52a874227d3.png)

* * *

second.yonsai.com 도메인 구성하기
===========
+ 1.도메인 서버를 설치한다(퍼스트와 동일)
+ 2.서버  관리자에서 알림을 클릭 이 서버를 도메인 컨트롤러 승격을 클릭한다.
+ 3.배포 구성에서 기존 포리스트에 새 도메인을 추가합니다를 선택
+ 4.부모 도메인 이름은 yonsai.com 새 도메인 이름은 second로 입력
+ 5.변경을 클릭해서 yonsai.com의 도메인 관리자인 administrator@yonsai.com/  Yons@i602 을 입력
+ 6.도메인 컨트롤러 옵션에서 windows sever 2016만 사용할 것이므로 '도메인 기능 수준'체크
+ 7.windows sever t머시기 프리뷰로 한다 또 기본으로 설정된 DNS 서버의 체크를 끄고 GC만 설치되도록한다
+ + 끄는 이유는 도메인서비스 세컨드 한개 서버만 이용하기때문 막 20개서버 이용하면 체크해야함
+ 8.DSRM의 비밀번호는 Yons@i602로 지정 한다(AD DS 복구하는 비밀번호)
+ 9.경로에서 풀더위치도 그대로 두고 다음
+ 10.경고 무시하고 설치
![image](https://user-images.githubusercontent.com/76859458/112753232-b3c7ed80-9011-11eb-8b49-0d6c81ca3cc6.png)    
![image](https://user-images.githubusercontent.com/76859458/112753239-bfb3af80-9011-11eb-9053-b7ae4da6c631.png)        




* * *


THIRD를 yonsai.com도메인에 추가하기
=====
+ 1.액티브 디렉토리 설치
+ 2.서버관리자 알림을 클릭하고 이 서버를 도메인 컨트롤러로 승격을 클릭한다
+ 3.배포 구성에서 기존 도메인에 도메인 컨트롤러를 추가
+ 4.도메인 이름은 yonsai.com으로 변경
+ 5.변경 클릭 yonsai의 도메인 관리자인 administrator@yonsai.com/ Yon@i602를 입력
+ 6.RODC옵션 에서 써드를 관리할 사용자를 지정 한다
+ 7.선택을 클릭 사용자 또는 그룹 고급을 클릭 지금 찾기를 클릭
+ 8.administrator관리자를 더블 클릭한다 확인을 클릭하면 위임된 관리자 계정이 완성
+ 9.선택->고급->지금찾기->어드민
![image](https://user-images.githubusercontent.com/76859458/112986966-20bbbe80-919d-11eb-8fe0-1d7c933406c3.png)
![image](https://user-images.githubusercontent.com/76859458/112986984-26190900-919d-11eb-8f91-86f5b652f273.png)
![image](https://user-images.githubusercontent.com/76859458/112986999-2d401700-919d-11eb-80ef-d98e8bea0cd2.png)

* * *
Active Directory 관리설정
=====
![image](https://user-images.githubusercontent.com/76859458/112987615-e43c9280-919d-11eb-89b1-e8a98b8b3849.png)
![image](https://user-images.githubusercontent.com/76859458/112987666-f28aae80-919d-11eb-8b9c-13210da583cc.png)

* * *
second에서 first의 c드라이브를 사용할 수 있도록 설정
======
+ 1.퍼스트에서 원격 데스크톱 연결 키기
+ 2.자세히 누르고 사진처럼 하면 된다
\\first\도메인사용자풀더$

* * *
tip
=====

+ 아이피를 도메인 역방향
+ 도메인을 아이피로 정방향 
+ eksrhfaaa@naver.com에서 naver.com은 도메인 eksrhfaaa 아이디 @<-이 기능은 아이디와 도메인 구별하기위해 있는거다
+ 1.hird\administrator->써드의 관리자 계정
+ 2.administrator@yonsai.com -> first의 관리자 계정
+ 3.administrator@second.second.yonsai.com -) second의 관리자계정
+ 4.![image](https://user-images.githubusercontent.com/76859458/112989699-26ff6a00-91a0-11eb-827a-b3e373a801fb.png)
+ 5.![image](https://user-images.githubusercontent.com/76859458/112989862-54e4ae80-91a0-11eb-9d6d-808f9a7e0a1a.png)

* * *
* * *


중요(시험에 나올 것들)
======
+ 기본적인 도메인 로그온 이름:YONSAI\thisuser
+ UPN : thisUser@yonsai.com
+ 자동으로 주소 받는걸 DHCP라고 한다(DHCP는 Dynamic Host Configuration Protocol의 약자)
+ nslookup= 도메인주소를 아이피 주소로 바꿔주는 중요한 명령어
+ ncpa.cpl->네트워크연결(제어판)
+ 스냅샷=게임으로 비유하면 세이브=백업
+ 서버관리자->로컬서버 ide보안강화 사용안함하면 가상머신에 파일이나 풀더 옮길수있음
+ administrator@yonsai=UPN=윈도우같은 운영체제로할려면 이메일형식처럼해야함@붙여서=앞에는 아이디 @뒤에는도메인 이메일도 같은형식=UPN
+ AGDLP항목 ★★ 시험 100%
+ windows sever에서 제공하는 기본 그룹 개념확인하기
+ 조직구성단위(OU)와 그룹의 차이점 문서 확인
> 생성한 그룹 정책(GPO)이 적용되는 시점은 다음과 같다
> > 사용자가 로그온할 떄
> > 컴퓨터 재부팅 했을때
> > 사용자가 강제로 직접 그룹 정책을 받아 올때(명령어 : gpupdate /force) ★★
> > 정책을 받아오는 주기적인 시간이 되었을 때
> 윈도우 서버 2019 설치
> > 주소 변화 기술로 사설아이피를 공인아이피를 사설아이피로 변경 선택 (NAT)
+ $는 숨김풀더





* * *
* * *
액티브 디렉터리설치
도메인 컴퓨터 등록하기
세컨드 도메인 구성하기
써드 구현하기
액티브 디렉터리 관리 설정하기 무조건
액티브 디렉터리 사용자 계정 만들기
(2가지방법)
조직구성단위ou
조직구성단위를 cmd로 낸다
액티브 디렉터리 그룹 안냄
AGDLP 구현하기 이거 무조건나옴
그룹정책 구성과 운영 무조건냄
서버보안강화 무조건나옴

액티브 디렉터리 서버는 잘안나오지만 
그룹정책 무조건 나옴
서버보안강화
윈도우에서 기본으로 제공하는거 이거 안냄
ftp 제외
