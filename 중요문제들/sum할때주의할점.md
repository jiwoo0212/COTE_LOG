두 리스트간 빼고 더할때 sum은 계속 sum을 하지말고 sum인자를 따로 두고 sum 함수 중복사용 막기
[참고](https://github.com/jiwoo0212/COTE_LOG/blob/main/%EB%AC%B8%EC%A0%9C%EB%93%A4/%EB%91%90%20%ED%81%90%20%ED%95%A9%20%EA%B0%99%EA%B2%8C%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)
```python
sum1 = sum(lst1)
sum2 = sum(lst2)

while True:
  sum1 -= 1
  sum2 += 1
```
