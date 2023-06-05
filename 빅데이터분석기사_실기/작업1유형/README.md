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