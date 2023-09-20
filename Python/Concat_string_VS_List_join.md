# 실험 동기

socket통신을 구현하여 client 에서 서버로 100MB 정도되는 zip파일을 전송하는데 1시간이 넘도록 진행되지 않아 문제를 해결 중에 string concat과 list join의 시간복잡도 관련 문제인 것을 발견

# 실행 환경

- Window 10
- Intel I7-6500U 2.50GHz (4 CPUs), ~2.6GHz
- Python 3.11

# 코드

## 모듈 임포트

```python
import time
```

## String Concat

```python
def string_concat(n):
    s = ''
    for _ in range(n):
				s += 'a'
    return s
```

## List Join

```python
def list_join(n):
    s = []
    for _ in range(n):
        s.append('a')

    return ''.join(s)
```

## 실행 코드

```python
LOOP = 5
sum_time = 0
for i in range(LOOP):
		start = time.time()
		string_concat(10000)
		end = time.time()
		sum_time += end - start
avg_time = sum_time / LOOP
print(avg_time)
```

# 실행시간 비교

## 5회 실행 평균

| n(반복횟수) | String Concat | List Join |
| --- | --- | --- |
| 10,000 | 0.0013 sec | 0.0010 sec |
| 100,000 | 0.0140 sec | 0.0365 sec |
| 1,000,000 | 0.1572 sec | 0.1388 sec |
| 10,000,000 | 7.6225 sec | 1.1618 sec |
| 100,000,000 | 663.9347 sec | 11.0420 sec |
- string concat의 1억 회는 1회 실행

# 결론

1. 메모리 효율성 관련하여 차이점이 생긴다
    - string(문자열)은 불변 객체이다
    - 따라서 string concat은 문자열을 더하기 위해 계속해서 새로운 메모리 공간을 할당 해야 함
2. 1억 회 반복 시 list join이 약 60배 빠르다
