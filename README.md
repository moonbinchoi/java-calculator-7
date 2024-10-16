# java-calculator-precourse

## 기능 목록

---
### 문자열 입력
- `camp.nextstep.edu.missionutils.Console` API를 사용해 사용자의 입력을 받는다.

### 구분자 추출
- 기본 구분자 `,`, `:` 인식  
    ```text
    덧셈할 문자열을 입력해 주세요.
    1,2:3
    결과 : 6
    ```
- 커스텀 구분자 인식
    - 문자열 앞부분의 `//`와 `\n` 사이에 위치하는 문자를 커스텀 구분자로 사용
        ```text
        덧셈할 문자열을 입력해 주세요.
        //?
        1:2?3,4
        결과 : 10
        ```
    - 여러개의 커스텀 구분자 인식
        ```text
        덧셈할 문자열을 입력해 주세요.
        //?
        //e
        1:2?3e4
        결과 : 10
        ```
> 예외: 커스텀 구분자에 `//`이 포함될 경우 커스텀 구분자로 인식할 수 없음.

### 피연산자 추출
- 피연산자는 정수 양수여야 한다.
    - `.`도 커스텀 구분자로 사용가능하기 때문

### 입력 오류 검사
- `2.`, `3.`의 예외는 입력 오류로 간주한다.
- `2.`, `3.`에서 정의되지 않은 모든 문자열은 입력 오류로 간주한다.
- 입력 오류가 발생하였을 경우 `IllegalArgumentException`을 발생시킨 후 종료한다.
#### 예외 발생 기준
| 원인                                         | 예외 종류                      | 메시지                                              |
|--------------------------------------------|----------------------------|--------------------------------------------------|
| 빈 문자열이 입력되었을 경우                            | `IllegalArgumentException` | "빈 문자열은 입력할 수 없습니다."                             |
| 커스텀 구분자에 `//`이 포함되었을 경우                    | `IllegalArgumentException` | "커스텀 구분자에 `CUSTOM_DELIMITER_PREFIX`는 포함할 수 없습니다." |
| 커스텀 구분자가 숫자로만 이루어 졌을 경우                    | `IllegalArgumentException` | "커스텀 구분자는 숫자로만 이루어져서는 안됩니다: `delimiter`"         |
| 피연산자가 숫자로만 이루어지지 않았거나,<br/>수식에서 구분자를 찾지 못했을 경우 | `IllegalArgumentException` | "올바르지 않은 피연산자입니다: `operand`"                     |
### 덧셈 연산
- 수식에서 추출한 모든 피연산자들을 한번에 덧셈하여 출력한다.
  - `System.out.println()`으로 결과를 출력한다.