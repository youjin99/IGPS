# 신규지역 공공자전거 대여소 위치 결정

**GIS데이터 기반 신규지역 공공자전거 대여소 위치 결정**

# 프로젝트 소개

**서울시 따릉이 데이터를 분석**하여 **이용량에 영향을 미치는 지리정보**(GIS)를 **회귀분석**을 통하여 파악한 뒤 이를 **Multi-MOORA, AHP 방법론**을 사용하여 대여소 위치를 1차적으로 선정한 후 **쏠림현상을 해결**하여 최종 대여소 위치 선정
![캡처4](https://user-images.githubusercontent.com/76585610/143587177-51956e82-22ec-445b-ade0-1bc2eaf53ebc.PNG)

# 사용 데이터

- **서울시**</br>
대여소 정보 : 서울시 공공자전거 대여소(따릉이) 현황 정보</br>
대여이력 : 서울시 공공자전거 대여이력 정보</br>
지역경계 : 모든 읍/면/도 경계에 대한 공간정보 및 속성정보</br>
도로 : 도로의 시점과 종점, 도로명부여의 기본정보</br>
건물 : GIS 건물통합정보</br>
경사도 : 수치표고모델지형의 고도값을 수치로 저장함으로써 지형의 형상을 나타내는 지도</br>
인구 : 서울시 주민등록인구 (연령별/동별) 통계</br>
지하철 : 서울시 지하철 좌표데이터</br>
버스 : 서울시 버스정류소 좌표데이터</br>
공원 : 생활권, 생활서비스 시설(공원) 정보</br>
대학교 : 전국 대학교 위치 정보</br>
- **인천시**</br>
지역 경계 : 모든 읍/면/동 경계에 대한 공간정보 및 속성정보</br>
도로 : 도로의 시점과 종점, 도로명부여의 기본정보</br>
건물 : GIS 건물통합정보</br>
경사도 : 수치표고모델지형의 고도값을 수치로 저장함으로써 지형의 형상을 나타내는 지도</br>
인구 : 서울시 주민등록인구 (연령별/동별) 통계</br>
지하철 : 서울시 지하철 좌표데이터</br>
버스 : 서울시 버스정류소 좌표데이터</br>
공원 : 생활권, 생활서비스 시설(공원) 정보</br>
대학교 : 전국 대학교 위치 정보
</br>

# 문제해결

 **1. 서울시 따릉이 데이터 분석**

![캡처2](https://user-images.githubusercontent.com/76585610/143587031-f7c5f3d3-f97a-405e-9476-af8eb83fc13b.PNG)


- 설명
    
    서울시 따릉이 데이터를 바탕으로 대여소 기준 100m 버퍼를 생성한 후 이를 기준으로 14가지 데이터 정보(도로길이, 지하철, 버스, 인구, 시설물 등) 레이어화하여 시각화 및 분석 진행 
    

 **2. 회귀분석을 통해 이용량에 영향을 미치는 지리정보(GIS) 파악**
- 설명
    
    서울시 각 대여소별 평균이용량을 종속변수로, 각각의 데이터들을 독립변수로 입력하여, 도출되는 베타값을 통해 우선순위 결정 
    

 **3. 배치 알고리즘(AHP, Multimoora)을 사용하여 대여소 개수 및 위치 선정**
- 대여소 개수 설정

| 자치구 | 총주거인구 | 대여소 | 대여소/인구 |
| --- | --- | --- | --- |
| 종로구 | 155,106 | 99 | 0.000638 |
| 중구 | 132,259 | 76 | 0.000575 |
| 용산구 | 240,665 | 67 | 0.000278 |
| ... | ... | ... | ... |
| 광진구 | 355,306 | 74 | 0.000208 |
- 설명
    
    따릉이의 경우 1명 당 평균 대여소 0.000248개
    
    미추홀구의 총 인구는 404,618명이므로
    
    404,618 X 0.000248 = 100.345264개 → 100개의 대여소를 배치 
    
- **AHP**
    
    ![캡처5](https://user-images.githubusercontent.com/76585610/143587229-f97eda84-209f-4686-9f38-699b990bcce6.PNG)

결정된 우선순위를 기반으로 가중치를 도출해내야 했는데 기존 AHP의 방식은 전문가의 의견을 기반으로 하는 방식이었다. 이러한 방식은 기존의 정성적인 방법과 다르지 않다고 생각했다. 그래서 각 변수와 우선순위를 입력하면 가중치를 알려주는 **슈퍼디시젼(Superdecision)** 프로그램을 사용하여 가중치를 도출했다. 
  
- **Multi Moora**
  ![캡처w](https://user-images.githubusercontent.com/76585610/143587257-2c27bac6-d30c-4c43-8fbb-86bcd5e8e1fc.PNG)
    
도출된 가중치를 기반으로 인천시 데이터에 적용하고자 했다. Ratio System, Reference Point Approach, Full Multiplicative Form이라는 세 가지 방법론을 모두 고려하여 **우선순위를 결정해주는 Multi-MOORA(다속성 다기준 의사결정 방법론)**을 사용했다.

- **대여소 배치**

![456](https://user-images.githubusercontent.com/76585610/143587361-e2c9c272-1c7d-4f90-8eb2-b99c73658802.png)

Multi Moora(다속성 다기준 의사결정론)를 사용하여 이용량이 많을 것으로 예상되는 순서로 각 그리드의 순위 결정 후 상위 100개의 그리드에 대여소 배치 

    

**4. 쏠림현상 해결**
- 대여소가 주로 주안1동, 숭의 2동 근처에 많이 쏠리고, 학익동, 문학동에는 대여소가 거의 존재하지 않는 **“쏠림현상”**이 발생했다. 공공자전거 특성 상 수익성도 중요하지만 **공익성도 중요하다고 판단**하여 이를 해결하고자 했다.


- **랭크 순 주변 그리드 8개 제외**

![그림3](https://user-images.githubusercontent.com/76585610/143587376-5976155b-dcf1-4fbe-94e8-598b9352ea99.png)
    
   랭크 순으로 주변 그리드 8개를 순위에서 제외
    
 - **동별 인구수 고려**
![그림4](https://user-images.githubusercontent.com/76585610/143587387-0320f8e6-e639-4a7b-b155-0a5caa7a09eb.png)

    설정한 100대의 대여소 개수를 동별 인구수를 기준으로 나누어 적절히 분배 
    
- **쏠림현상 해결 전 후 사진**

![그림6](https://user-images.githubusercontent.com/76585610/143587563-6851c18e-a2fe-45be-8809-a1a516cac855.png)


![그림7](https://user-images.githubusercontent.com/76585610/143587575-50d99790-62a7-4a65-b4ac-5999cd231df1.png)

쏠림현상 해결 전/후 사진으로 기존에 몰려있던 대여소들이 **비교적 고르게 분포**되어 있는 것을 확인할 수 있다.    

# 예상 이용량 도출


![그림8](https://user-images.githubusercontent.com/76585610/143587716-22ed1238-0894-44f4-ad3c-b4bf4b03771b.png)

- 설명
    
    최종적으로 배치한 예상 대여소 위치와 지리정보를 활용하여 예상 이용량을 도출 
    
    → 미추홀구의 예상 대여량은 약 2300건으로 서울시의 평균 이용량인 약 2100건보다 높은 수치 
    

# 결론 및 기대효과
1. **정량적인 방법을 참고하여 효율적인 위치 선정이 가능**
이 프로젝트에 적용된 시스템을 활용하면 예상 이용량 예측이 가능하다. 따라서 신규 지역 도입 전에 활성화 가능 여부를 판단할 수 있다. 따라서 서비스 변경으로 인해 자전거들이 방치되는 문제 예방 및 안정적인 공유 서비스 유지 가능
2. **공공자전거 시스템 확장 용이**
이 프로젝트의 시스템은 해당 지역에 대한 데이터가 존재하면 얼마든지 시스템을 확장할 수 있다. 즉, 인천시의 미추홀구뿐만 아니라 공공자전거 시스템이 존재하지 않는 지역의 경우에도 적용이 가능하다.
3. **라스트마일 이동수단 선택지 제공**
수년간 라스트마일 이동수단에 대한 관심이 급격하게 늘어나고 있다. 이 프로젝트의 시스템이 도입된다면 대부분 도보로 다녔지만, 선택지를 추가로 제공함으로써 시민들에게 편의를 제공할 수 있다.
