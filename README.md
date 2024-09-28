# 시계열 데이터 기반 상품 판매량 예측
---
## 프로젝트 개요
- 주제 : 시계열 데이터 기반 상품 판매량 예측
- 학습 과목 : 데이터전처리, 데이터분석, 딥러닝 모델링
- 데이터 출처 : 자체제작
- 중점 사항 : 시계열 데이터 전처리, 딥러닝 모델 구축, 기술 및 비지니스 측면 모델 성능 평가
- 프로젝트 목표 : 각 상품에 대한 판매량 데이터에 대해서 시계열 패턴을 찾은 후 딥러닝 모델을 통해 각 상품의 판매량을 미리 예측하는 서비스를 구현.
---

## 도메인 이해 
![image](https://github.com/user-attachments/assets/82bbdd7c-ee7c-41f2-b76f-efe7a0eb4bed)
![image](https://github.com/user-attachments/assets/94720511-2008-4f01-b85b-8b8c6ecda25b)
![image](https://github.com/user-attachments/assets/2ddd0e97-362d-4961-aa68-acf922286582)

---

## 데이터 소개 

![image](https://github.com/user-attachments/assets/26c60e57-4cd9-47a7-97fd-f7816d6a822e)


## 핵심 사항 

![image](https://github.com/user-attachments/assets/8bb06096-c062-4dba-9394-4ebc3f1d0189)

- **3가지 상품(3번:음료 / 12번:우유 / 42번:농업 제품)에 대한 수요량을 예측하고 재고를 최적화 해야 함**

  ![image](https://github.com/user-attachments/assets/8d2b08bb-a9bc-4d35-8c7e-9010033356ac)

- **시계열 데이터 분석 큰 그림**

![image](https://github.com/user-attachments/assets/a1efd541-2ad4-49b9-a1bb-67fad0ac3cc0)

---
## 데이터 분석 및 전처리
- 대상 매장에서 날짜별 구매고객수

  ![image](https://github.com/user-attachments/assets/b4afcccb-8eb3-46ea-be31-0bb480c2df2d)
1) 매년 5월 7 - 10일 고객구매수 높은편(2014/5/10, 2015/5/9, 2016/5/7)/ 매년 12월 20~25일 고객구매수 높음
2) 미국 어머니날 (2014/5/11 일요일, 2015/5/10 일요일, 2016/5/8 일요일) 하루전날에 높은것을 확인

### 1. Beverage
- 날짜별 상품 판매량
![image](https://github.com/user-attachments/assets/0551dd58-1448-40e2-bd51-871170336cea)

- 요일별 판매량
![image](https://github.com/user-attachments/assets/cfd3acda-0b43-4a8c-a332-c11ede3df67b)

- 시계열 데이터 분해

  ![image](https://github.com/user-attachments/assets/4ef1149c-7a7a-49df-925a-a01ae09701a4)

- **패턴 정리하기**
1) 2016-04-17 -> 판매량이 가장높음 / 대부분 주말에 음료판매량 높음
2) 요일별 판매변화량 높은순  목요일 금요일 -> 리드타임후 판매변화량 높음/ 토요일 일요일 -> 매우낮음

### 2. Milk
- 날짜별 상품 판매량
![image](https://github.com/user-attachments/assets/f957ec61-f450-4eb1-8f3c-1109c8232d45)

- 요일별 판매량
![image](https://github.com/user-attachments/assets/28b0f88e-7df5-45b9-aa0e-5e38e935e1ee)

- 방문 고객수와 상품 판매량 추이 비교

  ![image](https://github.com/user-attachments/assets/694b09c1-2112-4366-8ee2-e9c4c5c4f263)

- 시계열 데이터 분해

  ![image](https://github.com/user-attachments/assets/311d2b35-69fe-49b4-9d8c-f42b362fca93)
- **패턴 정리하기**
1) 상품을 시계열 분해 함수로 분석해보면 1월부터 12월까지는 증가하는 추세를 보이다 1월에는 다시 값이 급감하는 추세를 보이고 1주일의 계절성을 지닌 것으로 보임
2) 연도가 증가할수록 판매량도 증가, 연도마다 12월에 가장 많은 판매량인것을 확인
3) 방문 고객에 따른 상품판매량의 강한 연관성을 보임
4) 주말과 평일을 비교해봤을 때 주말이 평일보다 2배가량 높은 수치를 보임


### 3. Agricultural products
- 날짜별 상품 판매량
![image](https://github.com/user-attachments/assets/30db56e3-a083-4464-8d93-44ba3b3e4879)

- 방문 고객수와 상품 판매량 추이 비교

  ![image](https://github.com/user-attachments/assets/c772fb67-3791-4e6e-9090-6f4262bd90ac)

- 요일별 판매량
![image](https://github.com/user-attachments/assets/46cbc49f-b0ff-42a0-846a-07621fa6a1ff)

- 시계열 데이터 분해

  ![image](https://github.com/user-attachments/assets/adaf17da-d24b-4223-b2cb-65fa11943c6f)
- **패턴 정리하기**
1) 상품을 시계열 분해 함수로 분석해보면 판매량은 계절성을 띈다. 여름철에 증가, 겨울철에 감소
2) 2016년 10월 7일 조지아 주 애틀랜타 시티에 폭발적인 판매량 확인됨 (원인: 비가 왔다는 점 말고는 특이 사항 없음)
3) 월요일부터 일요일까지 판매량이 증가


---
## 모델링
- 스케일링 작업시 ['boarding', 'receipt'] 에는 MinMaxScaler진행 / ['avg_ride_distance', 'avg_rate', 'count_taxi'] 에는 Robust_Scailing(이상치가 있는 feature에서 좋은 결과를 보여줌)진행
1) Linear Regression
![image](https://github.com/user-attachments/assets/11bf271b-0963-412a-84e5-2202f2e81653)
![image](https://github.com/user-attachments/assets/5d4825d4-0692-4ce5-be52-29abe7e1f7c5)


2) Lasso Regression
![image](https://github.com/user-attachments/assets/09ff1240-54a8-4925-84a0-b06245124c0e)
![image](https://github.com/user-attachments/assets/52379464-156f-46e1-b494-36749431c45a)


3) Ridge Regression
![image](https://github.com/user-attachments/assets/7cd18837-5a1b-4dac-84a2-052eee53c100)
![image](https://github.com/user-attachments/assets/2fa3186f-50d8-43a9-a65b-d464c721fa34)


4) ElasticNet
![image](https://github.com/user-attachments/assets/3874277f-ec49-4313-a0fe-ffe6eaa9c21b)
![image](https://github.com/user-attachments/assets/7601b9ce-5f73-4c86-8651-a5376aa279f2)


5) KNN
![image](https://github.com/user-attachments/assets/9072f62f-d8cf-4afc-a9b2-cd5243cf3926)
![image](https://github.com/user-attachments/assets/9263b0c9-d66a-4453-bf30-f6ebcaa84505)


6) Decision Tree
![image](https://github.com/user-attachments/assets/bb526bea-ee42-4ac5-88d4-4d1d6202cf07)
![image](https://github.com/user-attachments/assets/2f755f6a-469c-4c08-8a9e-40afbab060db)


7) Random Forest
![image](https://github.com/user-attachments/assets/2f1420ed-ebda-4407-8a34-876671105041)
![image](https://github.com/user-attachments/assets/26316b26-40da-49eb-bc1c-1539d32f6fab)


8) LightGBM
![image](https://github.com/user-attachments/assets/30c1b8e5-2137-4b4b-8244-6f6462937bc4)
![image](https://github.com/user-attachments/assets/decde94b-6d7b-4001-a6ad-f793e5d5b0eb)


9) XGBoost
![image](https://github.com/user-attachments/assets/60f5c6a8-b5ee-4cb5-9559-270627d4b7e8)
![image](https://github.com/user-attachments/assets/f81d250c-7509-4294-bc52-264f2b9b3b11)


10) Gradient Boosting
![image](https://github.com/user-attachments/assets/7ca32345-5873-433d-9364-383c4245af5b)
![image](https://github.com/user-attachments/assets/786c2d1f-83bd-4238-9a46-6aa07d26a3c3)



### 최종 모델
- **총 10개의 모델을 돌려본 결과 Ridge 모델의 성능이 가장 좋았다.**

  ![image](https://github.com/user-attachments/assets/48813c6b-9312-4c22-82f5-bcefe4297588)



