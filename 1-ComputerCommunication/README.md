# 컴퓨터 통신

## 목차
1. [인터넷 통신](#computer-communication)
2. [IP](#ip)
3. [TCP, UDP](#tcp-udp)
4. [PORT](#port)
5. [DNS](#dns)

## Computer-Communication
컴퓨터는 과연 어떻게 내가 보내는 정보를 원하는 컴퓨터로 전송시키는 것일까?


## IP
### IP(Internet Protocol)이란?
Internet은 우리가 아는 그 인터넷이라고 생각하면 쉽다.
Protocol은 규약, 규칙이라고 생각하면 된다.

따라서 IP란 인터넷에서 사용하는 규칙(규약)이다.

즉, 인터넷이라는 네트워크에 속해있는 수많은 컴퓨터들 중 내가 원하는 컴퓨터에게 데이터를 보내기 위한 규칙이다.

간단하게 출발지와 목적지와 메세지 등을 패킷 단위로 전송한다.
목적지를 중간중간에 있는 다른 네트워크 컴퓨터들에게 물어물어 데이터를 전송한다.

### IP의 특징
IP는 크게 2가지 특징을 갖는다.
1. 비연결성
2. 비신뢰성

#### 비연결성
우선 비연결성이란, 정보(데이터)를 보내는 컴퓨터(이하 클라이언트)와 정보를 받는 컴퓨터(서버)가 연결되어 있지 않다는 것이다. 위에서 설명했듯이 이 두 컴퓨터는 직접 연결되어 있지 않고 중간이 여러 컴퓨터들에게 물어물어 길을 찾고 데이터 전송을 부탁하여 목적지 컴퓨터로 전송한다. 이 과정에서 목적지가 없는 지, 혹은 데이터를 받을 수 있는 상태인지는 고려하지 않는다는 것이다.

#### 비신뢰성
두번째로 비신뢰성이란, 이렇게 물어물어 보낸 데이터가 변형이 되었는지, 중간에 사라지진 않았는 지, 순서가 정확한지 등에 대해서는 확인하지 않는 다는 것이다. 

## TCP-UDP
### TCP(Transmission Control Protocol)이란?
TCP는 말 그대로 전송 제어를 위한 규칙이다. 앞서 IP는 비신뢰성과 비연결성으로 인해 데이터 전송에 부족함이 있음을 파악하였다.

이러한 데이터 전송의 단점을 보완하기 위해 사용하는 것이 TCP라고 할 수 있다.

IP에서 출발지 주소(IP address), 도착지 주소, 기타 등등의 데이터가 들어갔다면, TCP에서는 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보 등이 들어간다. 이중 PORT는 뒤에서 다시 보기로 하고 전송 제어와 순서, 검증 정보이 무엇인지 TCP의 특징과 함께 알아보자.

### TCP의 특징
TCP는 다음과 같은 특징을 가진다.
1. 연결지향
2. 데이터 전달 보증
3. 순서 보장

#### 연결지향
우선 연결 지향은 IP의 비연결성을 보완하는 것처럼 보인다. 정확하다. 말 그대로 연결된 이후에 데이터를 보내겠다는 것이다. 그렇다고 실제로 클라이언트와 서버를 연결하는 것은 아니다. 그렇다면 어떻게 연결을 확인할 까?

##### 3-way-handshake
TCP에서는 연결지향을 위해서 3 way handshake라는 행위를 통해서 연결을 한다. 
3 way handshake는 아래와 같이 동작한다.

1. 클라이언트에서 서버로 SYN라는 메세지를 보낸다. SYN은 서버에게 연결을 요청한다는 의미라고 생각하면 된다.
2. 서버는 클라이언트의 SYN에 대한 응답으로 ACK(요청 수락)이라는 메세지를 보내고 추가로 SYN라는 메세지를 보낸다.
3. 클라이언트는 서버가 보낸 ACK 메세지와 SYN 메세지를 받고 ACK 메세지로 응답한다. (ACT 메세지와 함꼐 데이터를 전송할 수도 있다.)

이렇게 3번의 데이터를 주고 받는 행위를 3 way handshake라고 한다. 이 과정을 통해서 서버가 데이터를 받을 수 없는 상황인지를 확인한다. 

#### 데이터 전달 보증
데이터 전달 보증이라는 특징은 TCP에서 클라이언트로부터 서버가 정보를 받게 되면 해당 정보를 받았다는 메세지를 보낸다. 이를 통해서 데이터가 전달 되었음을 보증한다. 만약 이 수신 메세지가 일정 시간 내에 오지 않는다면, 클라이언트는 서버로 다시 메세지를 보낼 수 있을 것이다. 

#### 순서 보장
순서 보장이라는 특징은 TCP 정보 중에 순서라는 데이터가 있기 때문에, 서버가 받은 데이터들의 순서를 확인하고 순서가 맞지 않은 데이터를 받게 되면 클라이언트에게 순서가 맞지 않은 데이터부터 재전송을 요청한다.

예를 들어, 패킷1~3번을 서버에게 전송하였는데, 서버가 패킷1,3을 받았다면 클라이언트로부터 패킷2부터 다시 재전송을 요청한다. 클라이언트는 이 요청에 따라 패킷2,3을 다시 전송한다.

### UDP(User Datagram Protocol)이란?
UDP는 TCP와 같은 계층의 프로토콜로 TCP와 달리 별다른 기능들을 가지고 있지 않다.

PORT에 대한 정보와 Checksum이라는 데이터 변형에 대한 확인 기능만을 가지고 있다. 대신 TCP에 비해 상대적으로 단순하기 때문에 속도가 빠르다는 특징이 있다.

또한 별 다른 기능이 없기 때문에 본인이 원하는 최적화작업을 어플리케이션 레벨에서 추가할 수 있고, 최근 HTTP/3에서 TCP가 아닌 UDP를 선택함으로서 관심을 받고 있다.

## PORT
위에서 클라이언트와 서버의 데이터 전송을 컴퓨터 수준에서 보았다. 하지만 실제로 우리는 한 컴퓨터에서 여러 어플리케이션을 실행하고 있다. 이러한 어플리케이션 각각 데이터를 주고 받는 데 이러한 컴퓨터 내의 어플리케이션이 주고 받는 데이터들을 정확한 어플리케이션에 보내기 위한 것이 PORT이다.

IP address가 하나의 아파트 동이라고 하면, PORT는 아파트 동안의 호수 같은 개념이라고 생각하면 이해가 쉽다.

PORT의 주소는 0~65535(2<sup>16</sup>) 중에 할당이 가능하다. 0~1023은 잘 알려진 포트로 사용하지 않는 것이 좋다. (HTTP : 80, HTTPS : 443)

## DNS
### DNS(Domain Name System)란?
사실 사람이 IP address를 외우고 있는 것은 쉽지 않기 떄문에 우리가 흔히 아는 문자열을 통해서 도메인 명을 만들고 이에 IP를 할당하는 식으로 연결한 것을 DNS라고 한다. 

간단히 우리가 외우기 어려운 주소를 알기 쉬운 문자로 바꿔주는 것과 더불어 IP주소가 변경되더라도 DNS를 통해서 접근하는 사람들은 이를 다시 알 필요가 없이 도메인명으로 들어올 다는 장점도 있다.