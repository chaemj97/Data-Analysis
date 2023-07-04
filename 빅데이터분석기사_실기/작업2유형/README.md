- 더미변수로 변환
pd.get_dummies(df)
카테고리형을 더미로 바꿈

- 구간 나누기
pd.qcut(df['body_mass_g'],5,labels=False)
5개의 구간으로 나누기

- Voting
서로 다른 알고리즘을 가진 분류기가 같은 데이터셋을 기반으로 학습되고 결합하는 것
Hard voting은 다수의 classifier의 예측 결과값을 다수결로 최종 class를 결정

Soft voting은 다수의 classifier의 예측 결과값간 확률을 평균하여 최종 class를 결정

- predict
model.predict(test) : 정수로 반환
model.predict_proba(test) : 특정범주 확률로 표시


# 기억 안날때
help('sklearn.preprocessing')