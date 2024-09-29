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

- **데이터 전처리**

  ![image](https://github.com/user-attachments/assets/40b07f1d-d716-4e49-b9bc-9c7663ca0f26)
1) df['Lead_Qty'] -> 추후 target 변수
2) 요일 변수와 주말여부 변수 추가

---
## 모델링
- **LSTM 모델링 , CNN 모델링 두가지로 진행(각각 세가지 상품에 대해)**
### LSTM 모델링
1) Beverage

   ![image](https://github.com/user-attachments/assets/1762937b-56e0-43f2-bf9c-e5e95a2201a0)
   ![image](https://github.com/user-attachments/assets/181f9912-cb42-412e-8ee5-58d1f8a5e77e)

2) Milk

   ![image](https://github.com/user-attachments/assets/525384b4-2b54-4df1-a3c9-e34336c136f5)
   ![image](https://github.com/user-attachments/assets/d88fed4d-1fe4-47b7-b71d-de3ca2974d26)


3) Agricultural products

   ![image](https://github.com/user-attachments/assets/d42a94dd-44bc-41a2-aee5-d0fdcee1ad96)
   ![image](https://github.com/user-attachments/assets/d3af6100-f0b2-474d-9495-cd7dcd4b2c61)
---
### CNN 모델링
1) Beverage

   ![image](https://github.com/user-attachments/assets/8dafe4df-040f-4f06-8d44-31c4554f30d4)
   ![image](https://github.com/user-attachments/assets/691c24ab-c9a7-4e6a-804f-30ba4f13273e)


2) Milk

   ![image](https://github.com/user-attachments/assets/2462bc42-cca7-4188-ad05-2303fb089095)
   ![image](https://github.com/user-attachments/assets/8332781f-1783-4f3f-94dc-a4d64cb9d269)

3) Agricultural products

   ![image](https://github.com/user-attachments/assets/ac14f801-e9e6-4d2b-9ba4-a05920b8adb0)
   ![image](https://github.com/user-attachments/assets/b62c1b1c-ae24-4a4a-9bc5-f9486811b115)



### 최종 모델 (직접 파이프라인 함수를 작성하여 재고손실율을 확인)
- Beverage

  ![image](https://github.com/user-attachments/assets/e621d4da-2e0a-4b2e-979d-405b87826f8a)

- Milk

  ![image](https://github.com/user-attachments/assets/09b88a5f-b75c-4c59-bc58-55a2b797a094)

- Agricultural products

  ![image](https://github.com/user-attachments/assets/fab0acec-c205-4edf-8207-93f176587a60)







