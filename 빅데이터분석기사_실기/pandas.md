인덱스 : df.iloc[]
레이블 명 : df.loc[]

index를 0부터 정렬 : df.reset_index(drop=True)

float로 type 변환 : df[].astype('float')

a 컬럼 값에 따라 오름차순으로 정렬 : df.sort_values('a')
내림차순 : ascending = False

a 단어 포함 : df[].str.contains('a')

item_name를 기준으로 중복행이 있으면 제거하되 첫번째 케이스만 남기기 : a.drop_duplicates('item_name')
마지막 케이스만 남기기 : a.drop_duplicates('item_name',keep='last')

N으로 시작하는 데이터 : df[].str.startswith('N')

NaN 값 무시 계산 : df.groupby().count()
NaN 값 포함 계산(빈도수) : df.groupby().size()

groupby를 사용하면 기본으로 그룹 라벨이 index가 됩니다.
index를 사용하고 싶은 않은 경우에는 as_index=False 를 설정하면 됩니다.

판다스에서 인식할 수 있는 datetime64타입으로 변경 : pd.to_datetime(df['Yr_Mo_Dy'])
년도 : df['Yr_Mo_Dy'].dt.year
요일 영어로 : df.dt.day_name()

결측치 채우기
1. 이전 값으로 채우기 df.fillna(method='ffill')
2. 다음 값으로 채우기 df.fillna(method='bfill')

Timestamp를 Period변환
df['Yr_Mo_Dy'].dt.to_period('D') # 1일의 기간
df['Yr_Mo_Dy'].dt.to_period('M') # 1개월 기간
df['Yr_Mo_Dy'].dt.to_period('A') # 1년의 기간

1차 차분 : df.diff(period=1)

규칙적으로 연산(이동평균 등) : df.rolling(7)
매일 7일간의 평균 알고 싶을 떄 사용

pivot메서드는 데이터의 열을 기준으로 피벗테이블로 변환시키는 메서드 입니다.
df.pivot(index=None, columns=None, values=None)

원본 df 수정 : inplace=Ture

Datetime Index를 원하는 주기로 나누어주는 메서드 :df.resample('W')

pivot은 데이터 재구조화만 가능
pivot_table은 재구조화뿐만 아니라 결측치를 대체하거나 집계 가능 : .pivot_table(..., fill_value = ,aggfunc=['sum','mean'])

인덱스 컬럼 제거 : pd.read_csv(url,index_col= 0)

컬럼 타입에 따라 선택 : df.select_dtypes(exclude='',include='')