### NAT/PAT에 대해 설명해주세요

네트워크 주소 변환을 뜻하는데 IP 고갈 문제들에 대응하기 위해 나온 전략이었음. 보안 강화에 사용되고, IP 변환을 통해 원래 통신할 수 없던 같은 IP끼리 통신을 가능하게 함

NAT 테이블을 통해 공인 IP로 변환해서 외부와 통신할 수 있다.

### GSLB 동작 방식에 대해 설명해주세요

1. 사용자 DNS 질의
2. LDNS ⇒ NS 서버 찾기 위해 root 부터 순차 질의
3. DNS에 질의
4. DNS가 GSLB에 위임했으므로 GSLB 응답
5. 다시 GSLB에 질의
6. GSLB에서 헬스 체크 → 결과 응답
7. GSLB에서 받은 결괏값을 LDNS가 사용자에 최종 응답

### DHCP 릴레이 과정을 설명해주세요

1. DHCP Discover(클라이언트 → 릴레이 에이전트)
    
    브로드 캐스트
    
2. DHCP Discover(릴레이 에이전트 → DHCP 서버)
    
    출발지(릴레이 에이전트 IP), 목적지(DHCP 서버 IP) 재작성. 유니캐스트.
    
    출발지에 쓰이는 IP는 서버 방향 인터페이스 IP, DHCP 메시지 내 IP는 클라이언트 내부 인터페이스 IP 주소. 즉, 둘이 다르다.
    
3. DHCP Offer(DHCP 서버 → 릴레이 에이전트)
    
    역시 유니캐스트
    
4. DHCP Offer(릴레이 에이전트 → 클라이언트)
    
    DHCP Server Indentifier만 실제 DHCP 서버 IP주소에서 `에이전트 외부 인터페이스 IP`로 변경
    
5. DHCP Request(클라이언트 → 릴레이 에이전트)
    
    브로드캐스트
    
6. DHCP Request(릴레이 에이전트 → DHCP 서버)
    
    유니캐스트
    
7. DHCP ACK(DHCP 서버 → 릴레이 에이전트)
    
    유니캐스트
    
8. DHCP ACK(릴레이 에이전트 → 클라이언트)
    
    브로드캐스트