## 왜 Linux를 사용해야 할까?
- 우리에게 익숙한 Mac OS, Window OS를 놔두고 왜 굳이 Linux를 사용해야 할까?

### 보안성
- Linux는 다른 어떤 OS보다 안정적이고 안전한 시스템이다. 
- Linux와 Unix 기반 OS는 많은 개발자(오픈소스이기도 하고, 오래되기도 했음)가 지속적으로 코드를 검토하고 있기 때문에 결함이 적다.
  - Linux에서 발생되는 버그는 다른 OS에 비해 빠르게 수정되는 경향이 있음
- 오픈소스이기 때문에 소스코드를 확인할 수 있어 안전하다


### 무료
- Mac, Window도 서버로 활용은 가능하나 유료인 반면, Linux는 완전 무료 정책으로 이를 제공함

### 개발자 친화적
- Linux의 package manager는 다른 어떤 OS보다 강력하다. 
  - Linux에 소프트웨어를 설치하는 것은 윈도우에 비해 훨씬 쉬움
    - 그냥 터미널 창에 다음과 같이 입력하기만 하면 됨
    `sudo apt-get install <software-name>`
  - 이는 개발자들의 작업 흐름을 매우 향상시킬 수 있음
- 리눅스에서는 소프트웨어를 설치하고 나서 재부팅을 안 해도 됨  
  - 윈도우에서 소프트에어를 설치한 후 이를 작동시키려면 대부분의 경우 컴퓨터를 재부팅 해야하는 상황이 발생한다.

### 미리 설치된 다양한 프로그래밍 툴
- Linux에는 많은 유용한 프로그래밍 툴들이 설치되어 제공된다.
  - `grep`, `wget`, `cron`, ...
  - SSH에 대한 툴들도 설치되어 있어 서버를 신속하게 관리하는 데 도움이 된다.
- 다양한 Linux 배포판이 있으므로, 사용자는 자신이 원하는 툴들을 내장한 Linux 배포판을 찾아서 다운받아 사용할 수 있다.

### 시스템 업데이트
- Linux 사용자는 언제든지 시스템을 업데이트 하거나 하지 않을 수 있다.
  - Window나 Mac에서는 가끔 시스템 업데이트를 강제하곤 한다.
- Linux에서 진행되는 시스템 업데이트는 매우 빠른 속도를 자랑한다.
  - window에선 매우 느림

### 개인정보 보호
- window는 항상 사용자 데이터를 수집한다.
  - 사용자에게 허락을 받는다 해도 뭔가 찝찝할 수 있음...
- 반면 Linux는 (프로그래밍 지식이 충분하다면)시스템에서 전송되는 모든 것을 확인할 수 있다.
  - 내가 따로 확인하지 않더라도 많은 사용자들이(오픈소스) 문제를 일으킬 소스코드가 있는지 항상 감시하고 있으므로 걱정하지 않아도 됨
  
### 작업 자동화
- 작업을 자동화할 수 있다.
  - 윈도우에선 bash 쉘 스크립팅이 기본적으로 제공되지 않음
  - Linux에는 `sh`, `bash`, `zsh` 등 다양한 쉘이 있으며, 이는 프로그래머들에게 효율성을 가져다 준다.
  
### 휴대성
- Linux는 portable OS이다. 
  - Portability는 한 시스템 아키텍처에서 다른 시스템 아키텍처로 코드 이동이 쉽다는 것을 의미한다.
  
### 커스터마이징(자율성)
- Linux에선 무언가 마음에 들지 않다면, 마음대로 제거하거나 수정할 수 있다.
  - 다른 OS는 이정도의 자율성을 주지 않는다.

### 낮은 하드웨어 요구사항
- Windows 기반 시스템들은 (오래 전에 비해)높은 하드웨어 성능을 요구한다. 따라서 오래된 하드웨어에서는 최신 Windows가 작동되지 않는 경우가 발생한다.
- 반면 Linux는 매우 낮은 성능을 가진 하드웨어에도 설치가 가능하다.

### 시스템 성능
- Linux기반 PC는 Windows보다 훨씬 빠르다.
  - Linux는 경량화된 시스템인 반면 Windows는 불필요한 소프트웨어가 많이 포함되어 있음
- Linux는 Windows보다 읽기 및 쓰기 작업 속도가 빠르다.
  - Linux에선 파일 시스템이 잘 조직화되어 있음(파일들이 서로 더 가까운 chunk(영역)에 위치함)
  - 따라서 대부분의 클라우드 시스템은 Linux를 사용한다
    - MS Azure 포함 😏

### Linux는 거의 모든 곳에서 실행할 수 있다.
- 슈퍼컴퓨터, 스마트 TV, 자율 주행 자동차, 핵 잠수함, [etc..](https://www.omgubuntu.co.uk/2016/08/25-awesome-unexpected-things-powered-linux) 등 Linux는 다양한 곳에서 실행이 가능하다

### 의미있는 오류메세지
- 윈도우의 블루스크린에서 말하는 오류메세지는 아무런 도움이 되지 않는다🤨
- 반면 Linux는 오류의 원인을 알려주는 정확한 오류 로그를 제공한다

## 결론
- 무료다 🤑


## 참고자료
- [13 Reasons Why Linux Is Better Than Windows](https://medium.com/swlh/13-reasons-why-linux-is-better-than-windows-6fa304454ae)
- [Ten reasons why We Should Use Linux](https://www.opensourceforu.com/2020/03/reasons-to-use-linux/)
- [25 Awesome Things Powered By Linux](https://www.omgubuntu.co.uk/2016/08/25-awesome-unexpected-things-powered-linux)