## Ubuntu 16.04 설치하기
### 1. Ubuntu 부팅 USB 만들기
#### ISO파일 다운로드
- 비어있는 USB준비
- [KAIST FTP](http://ftp.kaist.ac.kr/)에 접속하여 ubuntu-cd/16.04 다운로드

#### Rufus
1. [Rufus](https://rufus.ie)에 접속하여 Rufus를 다운로드
2. USB를 연결 후 실행
3. 부트 선택 - 디스크 또는 ISO 이미지, 선택박스를 누르고 위에서 다운받은 ISO파일 지정
4. 파티션 방식 - MBR, 대상 시스템 - BIOS(또는 UEFI-CSM)
5. [ISO 이미지 모드로 쓰기]를 선택
6. 복사가 완료되면 종료 후 USB로 부팅 (BIOS로 들어가서 부팅)

### 2. Ubuntu install
1. 설치 언어 목록에서 English 선택 (한글로 하면 이후에 불편함이 있어서 영어로하는 것을 권장)
2. 설치 중 업데이트와 소프트웨어 설치는 선택사항
3. 디스크 전체를 Ubuntu로 설치할 것이기 때문에 [디스크를 지우고 Ubuntu 설치]를 선택 (듀얼부팅을 하고싶다면 [듀얼부팅 참고](https://pythonkim.tistory.com/70))
4. 이후 Seoul과 English 키보드를 설정하고 진행
5. 사용자 정보를 입력 후 설치 후 재부팅
