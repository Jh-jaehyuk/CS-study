## 소개

이 문서는 컴퓨터에서 부동 소수점 연산의 정확도 문제에 대한 이해를 돕기 위한 것입니다. 예를 들어, `0.1 + 1.1 == 1.2`와 같은 계산이 상식적으로 `True`가 되어야 하지만, 실제로는 `False`가 나오는 이유를 설명합니다.

## 컴퓨터의 숫자 저장 방식

컴퓨터는 숫자를 2진법으로 변환하여 저장합니다. 예를 들어, 10진수 `5`는 2진수로 `101`, `15`는 `1111`로 저장됩니다. 숫자가 커질수록 더 많은 비트를 사용하게 되며, 예를 들어 16비트는 -32768부터 32767까지의 값을 표현할 수 있습니다.

### 소수 저장 방식

소수는 정수 부분과 소수 부분으로 나누어 저장됩니다. 소수를 저장하는 방법에는 두 가지 주요 방식이 있습니다.

#### 1. 고정 소수점 방식

- **구성**: 전체 숫자를 32비트로 나누어 저장합니다.
  - 첫 번째 비트는 부호
  - 다음 15비트는 정수 부분
  - 나머지 비트는 소수 부분
- **예시**: `21.45`는 `0 10101 101101`로 저장됩니다.

#### 2. 부동 소수점 방식

부동 소수점 방식은 고정 소수점 방식과 유사하지만, 소수점을 왼쪽으로 이동시켜 저장합니다. 부동 소수점 저장 방식은 **IEEE 754** 규약을 따릅니다.

| 자료형  | 크기  | 부호  | 지수  | 가수  |
|---------|-------|-------|-------|-------|
| float   | 32bit | 1bit  | 8bit  | 23bit |
| double  | 64bit | 1bit  | 11bit | 52bit |

- **예시**: `25.12`를 이진법으로 저장하는 과정:
  1. **부호 비트**: `0` (양수)
  2. **정수 부분**: `11001` (25의 이진 표현)
  3. **소수 부분 변환**: 0.12를 이진법으로 변환
     - 0.12 × 2 = 0.24 → `0`
     - 0.24 × 2 = 0.48 → `0`
     - 0.48 × 2 = 0.96 → `0`
     - 0.96 × 2 = 1.92 → `1`
     - 0.92 × 2 = 1.84 → `1`
     - (이하 반복)
     - 최종 결과: `11001.0001111010111...`
  4. **정규화**: `1.10010001111010111 * 2^4`
  5. **지수 부분**: 4에 127을 더해 저장 (`1000 0100`)
  6. **가수 부분**: `11001001...`을 저장

따라서, 최종 저장 방식은 `0 (부호) 1000 0100 (지수) 11001001.... (가수)`가 됩니다.

> **참고**: 지수 부분에 127을 더하는 이유는 음수 지수 표현을 위해서입니다. 127을 더해 0~127은 음수, 128~255는 양수로 구분합니다.

## 왜 `0.1 + 1.1 != 1.2`일까?

컴퓨터는 `0.1`과 `1.1`을 정확히 이진법으로 표현할 수 없으며, 이 값들은 무한 소수로 변환됩니다. 컴퓨터 메모리는 한정된 공간을 사용하므로, 이러한 소수는 잘려 저장되고, 이로 인해 오차가 발생합니다. 따라서 `0.1 + 1.1`의 결과는 실제로 `1.2`와 정확히 일치하지 않아 `False`가 됩니다.

## 부동 소수점 오차를 피하는 방법

부동 소수점 연산에서 발생하는 오차를 줄이기 위한 방법들은 다음과 같습니다:

1. **정수로 저장하기**: 소수 부분을 제거하고, 예를 들어 `2.3`을 `2300`으로 저장합니다.
2. **반올림 사용**: 소수를 반올림하여 정수로 변환 후 저장합니다.
3. **더블(double) 사용**: 더 큰 메모리 공간을 할당하여(`float` 대신 `double` 사용) 오차를 줄입니다. 그러나 이 방법도 오차를 완전히 제거하지는 못합니다.
4. **BigDecimal 사용**: 소수 자릿수가 매우 많은 경우, `BigDecimal` 클래스를 사용하여 정확도를 높입니다. 이 방법은 기본 자료형보다 느리며 사용이 불편할 수 있지만, 오버플로우 및 언더플로우 문제를 해결할 수 있습니다.
