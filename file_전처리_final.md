### 24시 화장실 표현을 위해 24시간인 행들 추출하여 Y로 값 대체

```py
import pandas as pd
data = pd.read_excel("D:/multi_1/seoul_toilet_final.xlsx")

# data.head(3)

# 어떤 값들이 있는지 확인
data["Open_Hour"].unique()
# '24시간',"24","상시","00~24","00:00~24:00","00:00~00:00","00:00~24:00 (05:00~24:00  매주월요일)"

#"24시간","24","상시","00~24","00:00~24:00","00:00~00:00","00:00~24:00 (05:00~24:00  매주월요일)"])
data.loc[data["Open_Hour"]=="00:00~24:00 (05:00~24:00  매주월요일)"].count()

data.loc[data["Open_Hour"]=="00:00~24:00 (05:00~24:00  매주월요일)","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="24시간","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="24","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="상시","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="00~24","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="00:00~24:00","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="00:00~00:00","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="상시","Open_Hour"] = "Y"
data.loc[data["Open_Hour"]=="상시","Open_Hour"] = "Y"

data_1 = data.rename(columns = {"Open_Hour":"Open_Always"})

# 파일 저장
#data_1.to_excel("D:/multi_1/seoul_toilet_information.xlsx")
data_1
```