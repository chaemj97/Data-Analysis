- 상관 계수
df[['age','balance']].corr()

- 샤피로 검정
Shapiro-Wilk 검정은 가설검정의 방법으로 데이터가 정규분포를 가지는 지에 대해 검정하는 방법
from scipy.stats import shapiro
shapiro(df)

- 카이제곱 독립성 검정
from scipy.stats import chi2_contingency
observed : 관찰빈도로 pd.crosstab 결과 값을 입력
chi2,p,dof,expected = chi2_contingency(observed)
# return 카이제곱 통계량 값, p-value, 자유도, 테이블의 합계를 기반으로 한 기대빈도

- 결측치가 존재하는 행 모두 지우기
df = df.dropna()

- 리스트형태의 값을 여러 행으로 전개
df.explode()
```
     col1       col2
0   [1, 2]     [a, b]
1      [3]        [c]
2   [4, 5]  [d, e, f]

df.explode('col')

   col1       col2
0     1     [a, b]
0     2     [a, b]
1     3        [c]
2     4  [d, e, f]
2     5  [d, e, f]
```



- datetime.datetime.strptime(aa,'%Y') 은 문자열을 날짜 객체로 변환
- df.dt.strfime('Y')은 날짜 객체를 문자열로 반환
- 한 객체 내에서 열과 열  행과 행의 차이를 출력하는 메서드
  df[].diff()
  기본값 periods=1,axis=0

