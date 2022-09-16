# 파일 1 전처리
### 서울시 공중화장실 데이터에서 주소를 위도 경도로 변환해주었습니다.
### Geocode라는 구글 어플리케이션을 이용했하였는데 하루 이용량이 1000개의 데이터로 한정되어있어 파일이 여러개라 하나로 합쳐주는 작업을 진행했습니다.

```py
# 위도 경도 데이터 좌표 종합하기
# 파일 불러오기
import pandas as pd
import numpy as np
data1 = pd.read_excel("D:/multi_1/bath0001.xlsx")
data2 = pd.read_excel("D:/multi_1/bath1003.xlsx")
data2_plus = pd.read_excel("D:/multi_1/bath1966_2000.xlsx")
data3 = pd.read_excel("D:/multi_1/bath2001.xlsx")
data4 = pd.read_excel("D:/multi_1/bath3001.xlsx")
data5 = pd.read_excel("D:/multi_1/bath4001.xlsx")
data6 = pd.read_excel("D:/multi_1/bath5001.xlsx")

#data1.head()

# 인덱스 열로 사용하기 위해 숫자 배열 생성
num = np.arange(1,1002)
len(data1["Latitude"])
data1["Num"] = num

# 위도,경도 열만 남기고 다 제외
data1_1 = data1.drop(columns = ["소재지도로명주소"])

#1002번 데이터 누락되어있음. 만들어서 추가
df1 = pd.DataFrame([[37.517755,126.907807,1002]],
                  columns = ['Latitude','Longitude','Num'])
data1_2 = data1_1.append(df1)
data1_3 = data1_2[["Num","Latitude","Longitude"]]

# 최종으로 사용할 1~1002 위도/경도 데이터
# data1_3

# 1966~2000번 데이터 누락됨. 합쳐야함
data2_plus_la = data2_plus["Latitude"]
data2_plus_lo = data2_plus["Longitude"]
data2_plus.rename(columns = {"번호":"Num"},inplace = True)
data2_plus_num = data2_plus["Num"]
data2_plus_1 = pd.DataFrame({"Num":data2_plus_num,"Latitude":data2_plus_la,"Longitude":data2_plus_lo})
# data2_plus_1

# 1003~1965번 데이터
data2_la = data2["Latitude"]
data2_lo = data2["Longitude"]
data2.rename(columns = {"번호":"Num"},inplace = True)
data2_num = data2["Num"]
data2_1 = pd.DataFrame({"Num":data2_num,"Latitude":data2_la,"Longitude":data2_lo})
# data2_1

# 최종적으로 사용할 1003~2000 데이터
data2_2 = data2_1.append(data2_plus_1)
# data2_2

#data3.head()

data3_1 = data3.drop(columns = ["소재지도로명주소"])
data3_1.rename(columns = {"번호":"Num"},inplace = True)

# 최종으로 사용할 2001~3000 위도/경도 데이터
# data3_1

#data4.head()

data4_num = data4["번호"]
data4_lo = data4["Longitude"]
data4_la = data4["Latitude"]
data4_1 = pd.DataFrame({"Num":data4_num,"Latitude":data4_la,"Longitude":data4_lo})

# 최종으로 사용할 3001~4000번 위도/경도 데이터
# data4_1

#data5.tail()

# 인덱스 열로 사용하기 위해 숫자 배열 생성
num = np.arange(4001,5000)

len(data5["Latitude"])
data5["Num"] = num

# 위도,경도 열만 남기고 다 제외
data5_1 = data5.drop(columns = ["위도/경도"])

#5000번 데이터 누락되어있음. 만들어서 추가
df5 = pd.DataFrame([[37.6813890, 127.064322, 5000]],
                  columns = ['Latitude','Longitude','Num'])
data5_2 = data5_1.append(df5)
data5_3 = data5_2[["Num","Latitude","Longitude"]]

# 최종으로 사용할 1~1002 위도/경도 데이터
# data5_3

#data6.head()

data6_la = data6["Latitude"]
data6_lo = data6["Longitude"]
data6.rename(columns = {"번호":"Num"},inplace = True)
data6_num = data6["Num"]
data6_1 = pd.DataFrame({"Num":data6_num,"Latitude":data6_la,"Longitude":data6_lo})

# 최종적으로 사용할 5001~5109 데이터
# data6_1

# 데이터프레임 다 합치기
# 1~5109번 데이터 종합
data_real = data1_3.append(data2_2).append(data3_1).append(data4_1).append(data5_3).append(data6_1)
data_real["Latitude"].fillna(0)
data_real["Longitude"].fillna(0)
data_real_1 = data_real.set_index("Num")

# 1~5109번 위경도 데이터 최종
data_real_1


```