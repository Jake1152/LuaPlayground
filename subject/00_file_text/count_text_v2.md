# 문제
## 추가사항
- [v] main() 함수에 외부 호출 가능하도록 변경
- [v] 테이블을 초기화 하는 것이 아닌 바로 쓰는 식으로 변경
- [] 파일 읽을 때, moses사용
- [] 현재 위치로 lua 파일 실행하면 안되는 이유 파악

## 기존

tutorial
#1)
입력받은 텍스트파일의 라인 수와 각각의 캐릭터 수를 세는 스크립트
filename:   count_text.lua
execute:    luajit count_text.lua  ../input.txt
output:
lines:  64
characters:
    A:  8
    B:  12
    D:  2
    E:  13
    ...
    ...
    ...
    Z:  1
- 입력받은 텍스트파일의 라인 수와 각각의 알파벳 캐릭터 수를 표시.
- 숫자가 0개인 캐릭터는 표기할 필요없음.
- 입력파일이 없거나 인자가 생략되었을시 gracefully하게 입력 오류를 표기  (일반적인 리눅스 command line utuility 처럼)

#  문제이해
- 텍스트 파일을 입력 받아서 라인 수와, 캐릭터 수를 센다
- 숫자가 0개인 캐릭터는 표기할 필요가 없다.
- 입력파일이 없거나 인자가 생략 되었을 시, gracefully하게 입력 오류를 표기한다.

# 고려사항
- 필요한 것
  - 자료구조, 실행 파일에 인자 전달, 텍스트 파일 읽어들이기
  - 예외처리, 오류 검증

- 자료구조 선정
  - 알파벳 별로 테이블에 담는다?
    - python dict 같은 것이 있는가?
    - 내부 자료구조는 어떻게 되는가?
    - 속도는 어떻게 되는가?
    - 성능 측정 방법
    - 여러 자료구조를 테스트 해본다.
- 실행 파일에 인자 전달
- 인자 검증
  - 인자가 들어왔는가?
  - 인자가 몇 개 들어왔는지
    뒤에 인자는 무시할 것인지, 에러로 처리할 것인지 UB로 할 것인가?
    - 사용자 편의성을 생각할 때, 2개 이상의 인자는 무시해도 된다 싶다. 
  - 읽을 수 있는 파일인가? 바이너리 파일도 상관없는가?
- 텍스트 파일 읽어들이기
- 한 줄씩 읽는 방법
  - 라인 수 세기
- 한 글자씩 읽기
- 캐릭터에는 알파벳만 포함되는가?
- printable한 값들이면 전부 포함인가?


# 문제해결방법

1. 실행 파일에 인자 전달
2. 인자 검증, 입력 값이 있는가?