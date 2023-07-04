1. 통계적 가설검정의 구성요소
- 귀무가설(null hypothesis) H0 - 기준이 되는 가설(ex. ~차이가 없다)
- 대립가설(alternative hypothesis) H1 - 주장하고 싶은 가설
- 검정통계량(Test statistic)
- 기각역(Rejection region) alpha
- p값 - 귀무가설을 기각할 수 있는 가장 작은 수준의 확률 값
(검정통계량이 alpha의 범위내에 들어가면 귀무가설 기각 / p값이 유의수준보다 작으면 기각)

2. T검정(독립 소표본, 단순 평균)
- 주어진 변수(Y)가 정규 분포를 따를 때, 변수의 단순 평균에 대한 가설 검정을 수행하는 경우
- scipy.stats.ttest_1samp(data,기준값 = ,alternative = )
- 기각 여부 체크
  - critical value 이용
    - scipy.stats.t.ppf(q=alpha,df=자유도)

3. T검정(독립 소표본, 평균 비교)
- 주어진 변수들(Y1,Y2)이 평균은 다르지만 분산이 동일한 정규 분포를 따를 때, 두 변수의 평균 차이에 대한 가설 검정을 수행하는 경우
- scipy.stats.ttest_ind(data1,data2,equal_val = ,alternative = )
  - equal_val : 분산이 같은가?

4. F검정(독립 소표본, 평균 비교)
- 독립 평균 비교는 T검정 아닌 F검정(ANOVA)을 이용 가능
- 2개 이상 집단, 독립, 분산 같음
- scipy.stats.f_oneway(data1,data2...)

5. T검정()
- scipy.stats.ttest_rel(data1,data2,alternative= )

6. 카이제곱 검정
- 범주형 자료의 독립성 검정에 이용
- 귀무가설 : 두 변수가 서로 독립이다.
```
cont_table = pd.crosstab(a['sex'],a['agegrp'])
chi2_test = scipy.stats.chi2_contingency(cont_table)
```

7. 윌콕슨 부호검정
- 두 집단의 분포에 대한 유사도를 검정하는 기법
- 귀무가설 : 두 분포가 유사하다
- scipy.stats.wilcoxon()
```
wilcoxon = scipy.stats.whilcoxon(a['bp_after'],a['bp_before'],alternative = 'less')
```