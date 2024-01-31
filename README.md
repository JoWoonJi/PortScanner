# PortScanner

# 기획보고서

### 1. 서론

- **배경**: 컴퓨터에 익숙하지 않은 사람들은 포트가 무엇인지 포트가 열려있다는 것의 위험성에 대해 알지 못한다. 열려있으면 안되는 포트를 알려주는 포트스캐너를 만들면 수요가 있을 것이라고 예상된다.
- **목적**: 본 프로젝트는 서비스 포트 스캐너를 통해 네트워크의 보안 상태를 평가하고, 보안 취약점을 식별하여 사용자에게 알려주는 것을 목적으로 한다.

### 2. 이론적 배경

- **소켓 프로그래밍**: 네트워크 통신을 위한 소켓의 사용 방법 및 원리 설명
- **TCP/IP 프로토콜**: 인터넷 통신의 기반이 되는 프로토콜 스택에 대한 설명
- **멀티스레딩 및 비동기 프로그래밍**: 동시성 프로그래밍의 개념과 이를 통한 효율성 증대 방법론 소개

### 3. 설계

- **구조 설계**: 스캐너의 전체적인 구조 및 각 구성 요소의 역할 설명.
- **프로세스 흐름**: 스캐닝 과정의 단계별 흐름도(flow chart) 제시.
- **기술 스택**: 프로젝트에 사용된 프로그래밍 언어, 라이브러리, 도구 설명.

### 4. 구현

- **스캐닝 알고리즘**: 포트 스캐닝을 위한 알고리즘 구현 설명.
- **멀티스레딩 구현**: 병렬 스캐닝을 위한 멀티스레딩 구현 방법론 및 코드 예시.
- **결과 처리 및 출력**: 스캔 결과를 처리하고 사용자에게 표시하는 방법 설명.

### 5. 테스트 및 검증

- **테스트 계획**: 단위 테스트, 통합 테스트, 성능 테스트 계획 설명.
- **테스트 결과**: 테스트 시나리오 및 결과 요약.

### 6. 결론 및 향후 계획

- **프로젝트 요약**: 주요 결과 및 달성된 목표 요약.
- **향후 계획**: 기능 개선, 성능 최적화, 새로운 기능 추가에 대한 계획.


# 요구사항 명세서

### **요구 사항 명세서**

- **목적**: 네트워크 상의 기기에 대해 열려 있는 포트를 식별하고, 해당 포트를 통해 제공되는 서비스 정보를 수집
- **입력**: 스캔 대상의 IP 주소 혹은 도메인, 스캔할 포트 범위(예: 1-65535).
- **출력**: 열려 있는 포트 목록, 각 포트와 관련된 서비스 정보.
- **기능성 요구 사항**:
    - TCP와 UDP 포트 스캔 기능
    - 타임아웃 설정 기능
    - 멀티스레딩을 통한 병렬 스캐닝
    - 한눈에 알아보기 쉬운 결과 출력
- **비기능성 요구 사항**:
    - 확장성: 새로운 스캔 기법 추가 용이성
    - 성능: 대규모 네트워크에서도 빠른 스캔 속도 유지
    - 안정성: 네트워크 오류나 예외 상황에 대한 견고한 예외 처리


# Flow chart

1. **시작**: 사용자가 스캐너를 시작하고, 스캔 대상의 IP 주소(혹은 도메인)와 포트 범위를 입력.
2. **입력 검증**: 입력된 IP 주소와 포트 범위의 유효성을 검사. 유효하지 않은 경우, 오류 메시지를 표시하고 사용자에게 다시 입력을 요청.
3. **스캔 설정 초기화**: 스캔에 필요한 설정을 초기화. 여기에는 타임아웃, 스캔 모드(TCP/UDP), 멀티스레딩 설정 등이 포함.
4. **스캐닝 시작**: 설정된 포트 범위에 대해 스캔을 시작. 멀티스레딩을 사용하는 경우, 각 스레드는 지정된 범위 내의 서로 다른 포트를 스캔.
5. **포트 스캔**: 각 포트에 대해 다음 단계를 반복:
    - **소켓 연결 시도**: 지정된 포트에 대해 소켓 연결을 시도.
    - **응답 확인**: 소켓 연결이 성공했는지 확인. 연결 성공 시, 해당 포트는 "열림"으로 표시되고, 실패 시 "닫힘"으로 표시.
    - **서비스 식별**: 연결이 성공한 포트에 대해, 해당 포트를 통해 제공되는 서비스를 식별. (옵션에 따라)
6. **스캔 결과 처리**: 모든 포트에 대한 스캔이 완료되면, 결과를 처리. 이 단계에서는 열린 포트와 해당 서비스 정보를 정리하여 사용자에게 표시.
7. **결과 출력**: 스캔 결과를 사용자에게 친화적인 형태(예: 표, 목록)로 출력. 열린 포트, 해당 서비스, 스캔 시간 등의 정보를 포함.
8. **종료**: 사용자가 결과를 검토한 후, 프로그램을 종료.


# Reference Docs

<aside>
💡 2024-01-25에 업데이트 된 Port에 관한 IANA의 공식 문서
    https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml?=&skey=-2&page=1

**External Links**

- [RFC1700](http://www.rfc-editor.org/rfc/rfc1700.txt): Last RFC containing assigned numbers (obsoleted by IANA list).
- [RFC3232](http://www.rfc-editor.org/rfc/rfc3232.txt): States that RFC1700 is obsoleted by the IANA list.
- [IANA list of assigned numbers](http://www.iana.org/numbers): Official lists of assigned numbers and the like.
</aside>

### **1. TCP/IP 및 네트워크 프로토콜**

- **"TCP/IP Illustrated, Volume 1: The Protocols" by W. Richard Stevens**: TCP/IP 프로토콜 스택에 대한 심층적인 이해를 제공하는 고전적인 참조서
- **RFC 793 (Transmission Control Protocol)**: TCP에 대한 기술적 세부 사항과 프로토콜 작동 방식을 설명하는 표준 문서
- **RFC 768 (User Datagram Protocol)**: UDP에 대한 세부 사항을 다루며, 무연결성 통신의 작동 방식을 설명

### **2. 소켓 프로그래밍**

- **"Unix Network Programming, Volume 1: The Sockets Networking API" by W. Richard Stevens**: 소켓 API를 사용한 네트워크 프로그래밍에 대한 가이드
- **"Beej's Guide to Network Programming"**: 초보자에게 친숙한 언어로 소켓 프로그래밍의 기초를 설명하는 자료

### **3. 멀티스레딩 및 비동기 프로그래밍**

- **"Concurrency in C# Cookbook" by Stephen Cleary**: C#을 사용하는 개발자에게 비동기 프로그래밍 패턴과 멀티스레딩 기법을 소개
- **"Java Concurrency in Practice" by Brian Goetz**: Java 프로그래머를 위한 동시성 프로그래밍에 대한 안내서

### **4. 보안 및 포트 스캐닝**

- **"Nmap Network Scanning" by Gordon Lyon (Fyodor)**: Nmap, 가장 널리 사용되는 오픈 소스 네트워크 스캐너의 창시자에 의해 쓰여진 책. 포트 스캐닝 기술과 네트워크 보안 평가 방법에 대한 심층적인 정보를 제공
- **OWASP Testing Guide**: 웹 애플리케이션 보안 테스트에 관한 실질적인 지침을 제공하는 오픈 웹 애플리케이션 보안 프로젝트(OWASP) 문서

### **5. 추가 리소스**

- **ChatGPT**
- **공식 프로그래밍 언어 문서**: Python, Java, C#, 등 프로젝트에 사용되는 프로그래밍 언어의 공식 문서

- **GitHub 및 Stack Overflow**: 코드 예제, 라이브러리, 프레임워크, 개발 중 발생하는 특정 문제에 대한 해결책을 찾기 위한 온라인 커뮤니티
- **"The Art of Port Scanning" by Fyodor**: 포트 스캐닝의 기술과 윤리에 대한 논문


# 소켓의 모든 것

### **소켓의 유래**

- **용어의 유래**: "소켓"이라는 용어는 전기 소켓에서 차용된 것으로 추정됩니다. 전기 소켓이 전기 장치를 전원에 연결하는 접점 역할을 하는 것처럼, 네트워크 소켓은 네트워크 상의 두 프로그램이 데이터를 주고받을 수 있는 가상의 연결 점을 제공합니다.

### **기원과 역사**

- **ARPANET과 TCP/IP**: 소켓의 개념은 **1970년대** 초 ARPANET의 발전과 함께 등장했습니다. ARPANET은 미국 국방부의 연구 네트워크였으며, 인터넷의 전신으로 볼 수 있습니다. 이 시기에 Vinton Cerf와 Robert Kahn은 TCP/IP 프로토콜을 개발했으며, 이는 네트워크 간의 통신을 가능하게 하는 핵심 기술이 되었습니다. TCP/IP 프로토콜 스택의 개발은 소켓 프로그래밍 모델의 기반이 되었습니다.
- **BSD 소켓**: 소켓 프로그래밍 모델은 **1980년대** 초 BSD UNIX에서 크게 발전했습니다. 4.2BSD UNIX 릴리즈는 소켓 API를 포함하고 있었으며, 이는 네트워크 애플리케이션 개발을 위한 표준 인터페이스로 자리잡았습니다. BSD 소켓 API는 TCP/IP 네트워킹을 위한 프로그래밍 인터페이스를 제공했으며, 오늘날에도 여전히 사용되고 있습니다.
- **Winsock**: **1990년대** 초, 마이크로소프트와 다른 회사들은 Windows 운영 체제를 위한 소켓 API 버전인 Winsock(Windows Sockets)을 개발했습니다. Winsock은 BSD 소켓 API에 기반을 둔 것으로, Windows 기반 애플리케이션에서 네트워크 통신을 가능하게 했습니다.

### **소켓의 주요 역할:**

1. **통신 채널 제공**: 소켓은 네트워크 상의 두 엔드포인트 간에 통신 채널을 생성합니다. 이 채널을 통해 데이터 패킷을 안전하게 송수신할 수 있습니다.
2. **데이터 교환**: 소켓은 서로 다른 네트워크 장치 간, 또는 동일한 장치 내의 프로세스 간에 데이터를 교환할 수 있는 메커니즘을 제공합니다.
3. **프로토콜 추상화**: 소켓 API는 TCP, UDP와 같은 다양한 네트워크 프로토콜을 추상화하여 애플리케이션 개발자가 손쉽게 네트워크 통신 기능을 구현할 수 있게 해줍니다.
4. **연결 관리**: TCP 소켓의 경우, 연결 설정, 데이터 전송, 연결 종료와 같은 연결 지향적 통신을 관리합니다. UDP 소켓의 경우에는 비연결 지향적 통신을 지원합니다.

### **소켓이 없다면:**

1. **통신 복잡성 증가**: 소켓이 없다면, 애플리케이션 개발자는 네트워크 프로토콜의 모든 세부 사항을 직접 관리해야 합니다. 이는 네트워크 통신을 구현하는 과정을 복잡하게 만들고, 오류 발생 가능성을 높일 수 있습니다.
2. **표준화 부족**: 소켓 API는 네트워크 통신을 위한 표준화된 인터페이스를 제공합니다. 소켓이 없으면 각 애플리케이션 또는 시스템마다 고유한 통신 메커니즘이 필요하게 되어 호환성과 재사용성이 크게 저하될 수 있습니다.
3. **개발 및 유지보수 어려움**: 소켓 API를 사용하면 네트워크 통신 기능을 비교적 쉽게 구현하고 유지보수할 수 있습니다. 소켓이 없다면 이러한 작업이 훨씬 더 어려워지고 시간이 많이 소요될 것입니다.
4. **애플리케이션 간의 통신 제한**: 소켓이 제공하는 통신 채널이 없다면, 분산 시스템, 클라이언트-서버 애플리케이션, P2P 애플리케이션과 같은 네트워크 기반의 다양한 애플리케이션이 제대로 작동할 수 없을 것입니다.

에코서버로 간단한 소켓통신 구현

에코 서버는 클라이언트로부터 받은 메시지를 그대로 돌려보내는 간단한 서비스

### **TCP 에코 서버**

```python

import socket

def echo_server(host, port):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.bind((host, port))
        s.listen()
        print(f"Server is listening on {host}:{port}")

        conn, addr = s.accept()
        with conn:
            print(f"Connected by {addr}")
            while True:
                data = conn.recv(1024)
                if not data:
                    break
                conn.sendall(data)

if __name__ == "__main__":
    HOST = '127.0.0.1'  # 서버의 주소
    PORT = 65432        # 서버가 통신할 포트

    echo_server(HOST, PORT)

```

### **TCP 에코 클라이언트**
```python

import socket

def echo_client(host, port):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(b'Hello, server')
        data = s.recv(1024)

    print(f"Received from server: {data!r}")

if __name__ == "__main__":
    HOST = '127.0.0.1'  # 서버의 주소
    PORT = 65432        # 서버가 리스닝하는 포트

    echo_client(HOST, PORT)

```

# TCP / IP 프로토콜의 모든 것

**TCP/IP는 "Transmission Control Protocol/Internet Protocol"의 약자**

TCP/IP 프로토콜은 1960년대 후반 미국 국방부의 연구 기관인 ARPA(Advanced Research Projects Agency, 후에 DARPA로 명칭 변경)에서 시작되었습니다. 당시의 목표는 분산된 네트워크에서 정보를 효율적으로 전송하고, 여러 네트워크 간의 상호 연결성을 제공하여 통신 네트워크의 신뢰성을 향상시키는 것이었습니다.  

당시 미국 국방성 산하의 고등 연구 계획국(ARPA)에서는 ARPANET이라는 최초의 패킷 교환 네트워크를 개발하고 있었습니다. TCP/IP는 ARPANET을 포함한 여러 네트워크를 서로 연결하기 위해 개발되었습니다.

- **개발**: Vinton Cerf와 Robert Kahn이 TCP/IP의 초기 버전을 개발했습니다. 이들은 데이터가 네트워크 간에 어떻게 전송될 수 있는지에 대한 기본 원칙을 제시했습니다.
- **표준화**: 1983년 1월 1일, ARPANET은 공식적으로 TCP/IP 프로토콜을 채택했습니다. 이 날짜는 종종 "인터넷의 탄생일"로 간주됩니다.

### **초기 개발 (1960년대 후반 - 1970년대)**

- **ARPANET**: TCP/IP의 직접적인 전신은 ARPANET 프로젝트로, 이는 세계 최초의 작동하는 패킷 교환 네트워크였습니다. 1969년에 구축된 ARPANET은 연구 기관들 간의 데이터 공유를 가능하게 했습니다.
- **NCP**: ARPANET의 초기 통신 규약은 네트워크 제어 프로그램(Network Control Program, NCP)이었으나, 이는 여러 네트워크 간의 상호 연결과 데이터의 신뢰성 있는 전송에는 한계가 있었습니다.

### **TCP/IP의 탄생 (1970년대 중반 - 1980년대 초)**

- **Vint Cerf와 Robert Kahn**: TCP/IP 프로토콜의 개발은 Vint Cerf와 Robert Kahn에 의해 주도되었습니다. 그들은 분산 네트워크에서 데이터를 신뢰성 있게 전송할 수 있는 방법을 고안했습니다.
- **TCP/IP의 등장**: 초기에는 전송 제어 프로토콜(Transmission Control Protocol, TCP)만이 개발되었으나, 나중에 인터넷 프로토콜(Internet Protocol, IP)이 추가되어 TCP/IP가 완성되었습니다. TCP는 데이터 전송의 신뢰성을 담당하고, IP는 데이터 패킷의 라우팅을 담당합니다.
- **1983년 전환**: 1983년 1월 1일, ARPANET은 NCP에서 TCP/IP로 공식적으로 전환되었으며, 이는 인터넷 프로토콜의 표준이 되었습니다.

### **TCP/IP의 발전과 확산 (1980년대 - 현재)**

- **인터넷의 확장**: TCP/IP 프로토콜의 표준화와 개방성은 전 세계적으로 다양한 네트워크의 상호 연결을 가능하게 했으며, 이는 인터넷의 급속한 성장과 발전을 촉진했습니다.
- **기술 발전**: 이후 TCP/IP는 지속적으로 발전하여 다양한 인터넷 기술과 서비스의 기반이 되었습니다. 오늘날, TCP/IP는 전 세계 데이터 통신의 핵심 프로토콜로 자리 잡고 있으며, 인터넷의 발전과 함께 계속해서 진화하고 있습니다.

# **TCP / IP 프로토콜의 로우레벨적 구현**

TCP/IP 프로토콜에서의 3-way handshake 과정을 직접 구현하는 것은 파이썬의 표준 라이브러리만으로는 불가능합니다. 이는 운영 체제의 네트워크 스택이 자동으로 처리하는 과정이기 때문입니다. 그러나, 우리는 낮은 수준의 네트워크 접근을 허용하는 **`socket`** 라이브러리의 기능을 사용하여 SYN 스캔(일종의 TCP 스캔 방법 중 하나)을 시뮬레이션함으로써 3-way handshake의 초기 단계를 시각화할 수 있습니다. 이 방법은 종종 네트워크 스캔이나 보안 테스트에서 사용되며, 주의 깊게 사용해야 합니다.

### **SYN 스캔 (SYN Scan)**

SYN 스캔은 TCP 3-way handshake의 첫 번째 단계인 SYN 패킷을 대상 서버에 보내 응답을 확인함으로써 특정 포트가 열려 있는지를 판단하는 기법입니다. 대상이 SYN-ACK로 응답하면 포트가 열려 있다고 간주하고, RST(Reset) 패킷으로 응답하면 포트가 닫혀 있다고 간주합니다.

아래의 예제 코드는 Python에서 낮은 수준의 소켓을 사용하여 SYN 스캔을 시뮬레이션하는 방법을 보여줍니다. 이 코드는 **`root`** 권한이 필요하거나 관련 권한이 설정되어 있어야 합니다. 또한, 목적지 주소가 실제 통신이 가능한 대상이어야 하며, 네트워크 보안 정책을 위반하지 않도록 주의해야 합니다.

```python

import socket
import struct

def create_ip_header(src_ip, dst_ip):
    # IP 헤더 구성
    ip_ihl = 5
    ip_ver = 4
    ip_tos = 0
    ip_tot_len = 0  # 커널이 채움
    ip_id = 54321
    ip_frag_off = 0
    ip_ttl = 255
    ip_proto = socket.IPPROTO_TCP
    ip_check = 0  # 커널이 채움
    ip_saddr = socket.inet_aton(src_ip)
    ip_daddr = socket.inet_aton(dst_ip)
    ip_ihl_ver = (ip_ver << 4) + ip_ihl

    ip_header = struct.pack('!BBHHHBBH4s4s', ip_ihl_ver, ip_tos, ip_tot_len, ip_id, ip_frag_off, ip_ttl, ip_proto, ip_check, ip_saddr, ip_daddr)

    return ip_header

def create_tcp_syn_header(src_port, dst_port):
    # TCP 헤더 구성
    tcp_seq = 0
    tcp_ack_seq = 0
    tcp_doff = 5  # 4 bit 필드, TCP 헤더 크기
    tcp_fin = 0
    tcp_syn = 1
    tcp_rst = 0
    tcp_psh = 0
    tcp_ack = 0
    tcp_urg = 0
    tcp_window = socket.htons(5840)  # 최대 허용 창 크기
    tcp_check = 0
    tcp_urg_ptr = 0
    tcp_offset_res = (tcp_doff << 4) + 0
    tcp_flags = tcp_fin + (tcp_syn << 1) + (tcp_rst << 2) + (tcp_psh << 3) + (tcp_ack << 4) + (tcp_urg << 5)

    tcp_header = struct.pack('!HHLLBBHHH', src_port, dst_port, tcp_seq, tcp_ack_seq, tcp_offset_res, tcp_flags, tcp_window, tcp_check, tcp_urg_ptr)

    return tcp_header

def syn_scan(src_ip, dst_ip, dst_port):
    # 소켓 생성
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_TCP)
    except Exception as e:
        print("Socket creation error: ", e)
        return

    # 소켓 옵션 설정
    s.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)

    # IP 헤더 생성
    ip_header = create_ip_header(src_ip, dst_ip)

    # TCP SYN 헤더 생성
    tcp_header = create_tcp_syn_header(12345, dst_port)  # 임의의 소스 포트

    # 패킷 전송
    packet = ip_header + tcp_header
    s.sendto(packet, (dst_ip, 0))

    # 응답 수신 (참고: 실제 환경에서는 여기에 더 많은 로직이 필요할 수 있습니다)
    data = s.recv(1024)
    print("Received:", data)

    s.close()

# 사용 예
# 'src_ip'에는 자신의 IP 주소를, 'dst_ip'에는 스캔하고자 하는 대상의 IP 주소를 입력해야 합니다.
# 'dst_port'는 스캔하고자 하는 대상의 포트 번호입니다.
# 이 코드는 네트워크 상에서 실제 트래픽을 생성하므로 사용에 주의해야 하며, 스캔 대상의 허가를 받아야 합니다.
syn_scan('192.168.1.100', '192.168.1.101', 80)

```

**중요**: 이 코드는 네트워크 스캔이나 테스트 목적으로만 사용해야 하며, 권한이 없는 네트워크나 시스템에 대해 사용해서는 안 됩니다. 무단 사용은 불법이며 윤리적 해킹 원칙을 준수해야 합니다. 또한, 실제 네트워크 환경에서는 방화벽, IDS/IPS 시스템 등이 SYN 스캔을 탐지하고 차단할 수 있습니다.

### '!BBHHHBBH4s4s' 이 기상천외한 문자는 무엇인가?

**`'!HHLLBBHHH'`**는 파이썬의 **`struct.pack`** 함수에서 사용하는 포맷 문자열입니다. 이 문자열은 **`struct`** 모듈을 사용하여 바이트 객체로 패킹하기 전에 데이터의 형식을 지정하는 데 사용됩니다. 이 포맷 문자열은 다양한 타입의 데이터를 하나의 바이트 스트림으로 패킹할 때, 각 데이터의 타입과 순서를 정의합니다.

포맷 문자열의 각 문자는 데이터 타입을 나타내며, 그 앞의 숫자는 해당 타입의 배열 길이(개수)를 의미합니다. **`'!HHLLBBHHH'`**에서 각 문자의 의미는 다음과 같습니다:

- **`'!'`**: 네트워크('>') 바이트 순서를 의미합니다. 이는 큰 숫자에서 가장 중요한 바이트(Most Significant Byte, MSB)가 먼저 오도록 지정합니다. 네트워크 바이트 순서는 일반적으로 네트워크 통신 프로토콜에서 사용되는 바이트 순서입니다.
- **`'H'`**: unsigned short (C 타입의 **`unsigned short`**)를 의미하며, 파이썬에서는 2바이트(16비트)의 크기를 갖습니다.
- **`'L'`**: unsigned long (C 타입의 **`unsigned long`**)을 의미하며, 파이썬에서는 4바이트(32비트)의 크기를 갖습니다.
- **`'B'`**: unsigned char (C 타입의 **`unsigned char`**)을 의미하며, 파이썬에서는 1바이트(8비트)의 크기를 갖습니다.

따라서, **`'!HHLLBBHHH'`** 포맷 문자열은 다음과 같은 구조의 데이터를 패킹하도록 지정합니다:

- 2바이트 unsigned short
- 2바이트 unsigned short
- 4바이트 unsigned long
- 4바이트 unsigned long
- 1바이트 unsigned char
- 1바이트 unsigned char
- 2바이트 unsigned short
- 2바이트 unsigned short
- 2바이트 unsigned short

이 포맷은 일반적으로 네트워크 프로토콜의 헤더를 구성할 때 사용되며, 예를 들어 TCP 헤더를 구성하는 데 사용될 수 있습니다. 각 필드는 TCP 헤더 내의 특정 세그먼트(예: 포트 번호, 시퀀스 번호, 플래그 등)를 나타냅니다.

# TCP 3-way handshake의 시뮬레이션적 구현

운영 체제의 TCP/IP 스택이 이 과정을 자동으로 처리하기 때문에 파이썬으로 구현이 불필요하지만 배움의 목적으로 외부 라이브러리 scapy를 이용해서 예시적으로 구현

**`scapy`**는 강력한 패킷 조작 도구로, 네트워크 프로토콜을 다루고, 패킷을 생성, 전송, 분석하는 등의 작업을 수행

pip install scapy 필요.

```python

from scapy.all import *

# 대상 호스트 및 포트 설정
target_host = "192.168.1.101"
target_port = 80

# 1단계: SYN 패킷 전송
ip = IP(dst=target_host)
syn = TCP(sport=RandShort(), dport=target_port, flags="S")
syn_ack = sr1(ip/syn, timeout=1)  # SYN 패킷 전송 후 SYN-ACK 응답 기다림

# 2단계: SYN-ACK 응답 확인
if syn_ack is None:
    print("No response from target")
elif syn_ack.haslayer(TCP):
    if syn_ack[TCP].flags == 'SA':  # SYN과 ACK 플래그가 설정된 경우
        print("SYN-ACK received. Proceeding to ACK...")

        # 3단계: ACK 패킷 전송으로 연결 확립
        ack = TCP(sport=syn_ack[TCP].dport, dport=target_port, flags="A", seq=syn_ack[TCP].ack, ack=syn_ack[TCP].seq + 1)
        send(ip/ack)
        print("TCP connection established with", target_host)

        # 이 시점부터 데이터 전송이 가능합니다.
        # 예: HTTP GET 요청 전송 등

        # 연결 종료 과정 (선택적)
        # fin = TCP(sport=syn_ack[TCP].dport, dport=target_port, flags="FA", seq=ack.ack, ack=ack.seq + 1)
        # send(ip/fin)
        # fin_ack = sr1(ip/fin, timeout=1)
        # if fin_ack and fin_ack[TCP].flags == "FA":
        #     last_ack = TCP(sport=syn_ack[TCP].dport, dport=target_port, flags="A", seq=fin_ack[TCP].ack, ack=fin_ack[TCP].seq + 1)
        #     send(ip/last_ack)
        #     print("TCP connection closed")
    else:
        print("Unexpected flags in received packet:", syn_ack[TCP].flags)
else:
    print("Received unexpected packet type")

```
