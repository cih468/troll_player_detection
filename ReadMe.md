# League of Legend Data Analysis

# AFK Player Detection in Match_data
- 게임을 포기하는 플레이어 탐지 모델 생성



## PPT 파일 

- [PPT](troll_player_detection.pptx)

## 데이터 수집

- https://developer.riotgames.com/
- Rest API 사용



## Task Definition

- AFK란? Away From KeyBoard 의 약자로, 게임을 중간에 완전히 포기하고 이길 의지가 없는 유저를 말합니다. 이번 프로젝트에서는 AFK를 통해 게임을 망치는 Troll player를 detect 합니다.

- 아이템을 판매하거나, 특정 아이템들을 여러 개 구매하며, 게임을 포기하는 유저들을 아이템 선택을 이용하여 찾고, 그들의 특성을 (k/d/a, gold 획득량, 레벨) 들을 이용하여 detection 하는 모델을 만드는 것을 목표로 하였습니다.

  

![img](https://lh5.googleusercontent.com/y3iK0V5iV4U-ZxxghwPnDCm_MGSlH2XG0sueLDaEEF2VN5zS0bo0nbmhNwxU8xOCUDRn67bVZUqrw441GVcXp4isJ8xSbSbLQFKM-OvZXuYr0OVWaAsPIycFLlR1qPU_3y5aAHQrLAzIDYiOiQ)

<image 출처 : op.gg>



## Troll Detection 분석 방법

- 특정 아이템 중복 구매 유저 -> Troll 유저일 가능성이 높다고 판단
- 특정 아이템 중복 구매 유저들의 k/d/a , gold, level 정보를 통해 Troll 유저의 특성 추출
- 앞의 Feature를 이용하여 아이템을 중복 구매하지 않은 Troll Detecting Model 생성(NN 모델)



## **AFK 유저와** 일반 유저의 통계적 차이 비교

- 원기회복의 구슬, 요정의 부적, 사파이어 수정,루비 수정 을 6개 구매한 유저들과 , 초시계, 부러진 초시계를 2개 이상 구매한 유저들을 afk 유저로 판단
- Kill , Death, Assist , Level , Gold 값을 Feature 로 , 해당 유저들의 Feature 데이터들 시각화
- ![img](https://lh3.googleusercontent.com/ykjxsjOK8Dvp07kW7YpQY4m5wNlit3G_PqAc9Tvrx89Dsh2O4V1NzPvWP1su_9DtiiYlxcHV2zF8M3E4wNPFBm4At5VoohGPMcaQAIeZCSgN5wJlnptWZuDci05C_bS4Cbuerw8Ol5TsI0U6wA)

- ![img](https://lh5.googleusercontent.com/RwqIJy_MlqnQ6JTMWpOeV7hEypR6GUhU2ygzE9dLdXK7rXTs7atUDpZm01EIAgCNO0TfPJ0SohICsTyTyRuhqlTMlsNwFbb_cOuOPn2XrtSPkiub8lKhF0oiyXrytMoBrAqU44zAnJf7Ga070w)



## 챔피언별 Data Standard Normalization

- 전체 데이터로 트롤 플레이어를 구분하기에는 각 챔피언별 특징이 크게 작용하여 AFK Detecting Feature로 사용하기에 적합하지 않을 것으로 예상됩니다.
- 각각의 5개의 피쳐에 챔피언별로 평균과 분산을 구해 Standard Normalization 을 진행하였습니다.
- 데이터가 더욱 충분하다면, 포지션 별 – 챔피언 별 통계치를 이용한다면 더욱 좋은 결과를 얻을 수 있을 것으로 보입니다.
- ![img](https://lh5.googleusercontent.com/TDL2fSAiNBL4C6kTiBf5MtY9XIZrGF2N30kjR3q7DoMHlaQzmw55pYnsmB2LAnTvHAlTk7UJlMoM7oNb4JbFUobTtYga2D_KwdyHwQeU3xQsmM2Xms1jEPMAxykUtB2rJq-Ea51CvMjWU_FI-w)

## Result Validation결과 검증

- 실제 아이템으로 afk 플레이가 아니라고 구분한 데이터 중 , 모델이 afk 플레이로 판단한 데이터들입니다.빨간 박스에 보이는 것처럼 아이템을 전부 혹은 거의 다 판매한 유저들이 보입니다.
- 빨간 박스에 보이는 것처럼 아이템을 전부 혹은 거의 다 판매한 유저들이 보입니다.

![image-20210615124548102](C:\Users\OPGG\AppData\Roaming\Typora\typora-user-images\image-20210615124548102.png)



## AFK 유저 탐지 서비스

- 오른쪽과 같이 AFK 플레이 비율을 opgg 사이트의 “여러명의 소환사 이름으로 요약 검색 기능”에 추가적으로 넣어주는 서비스에 활용 할 수 있을 것으로 보입니다. 

- 최근 플레이칸에는 AFK 플레이에 기존의 ‘ACE’,’MVP’처럼 ‘AFK’마크를 달아주어 AFK 플레이를 쉽게 알아 볼 수 있도록 해주고, 연패 연승을 표시해주는 부분에 최근 플레이 중 AFK 비율을 표시해주는 방향으로 추가가 가능합니다.

- 이렇게 솔랭에서 매칭된 팀원들이 AFK 유저라는 것을 쉽게 알아 볼 수 있게 해주면, 플레이어들의 닷지 / 인게임에서의 판단에 큰 도움을 줄 수 있을 것이라 생각합니다.

- ![img](https://lh6.googleusercontent.com/EM_BaDr61ItRGgcvPYQfxRp0HQzc94mqJzPEmirhwij6yND5aey1ct2R7G4ARiOXmM7vmMHT1bj7wrX9yCs7IEHr6lHthdZqL8r8yTwAltxjfyxfj8Oy8pg2mJTq8SETKkF9yg22fK3KgJrFTA)

  <image 출처 : op.gg>