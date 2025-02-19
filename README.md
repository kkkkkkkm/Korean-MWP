<div align="center">
 
# Korean-MWP
MDPI Mathematics: [Synthetic Data Generator for Solving Korean Arithmetic Word Problem](https://www.mdpi.com/2227-7390/10/19/3525) 
</div>

---

**한국어 문장형 수학문제 풀이**

 본 과정에서는 대량의 한국어 데이터 수집을 위해 한국어 기반의 문장형 수학 데이터 생성기를 구현하고, 자연어 도메인의 모델뿐만 아니라 다른 도메인의 모델을 활용하여 자연어 이해능력을 향상시킬 풀이수식 생성모델의 탐구를 목적으로 한다. 
 
 수학문제 풀이모델은 기계 번역 구조를 기반하며 Seq2Seq, Transoformer뿐만 아니라 음성인식에서 사용되는 Conformer 모델을 활용하여 각 모델 기반의 문제 풀이모델의 성능을 비교하고, 추가적인 실험을 통해 생성된 데이터의 유효성을 확인한다. 


## 한국어 문장형 수학문제 데이터 생성기

데이터 생성기는 문제 유형과 어휘적 데이터 변환 방식으로 이루어져 있으며 다음 그림과 같다.

<p align="center">
<img src = https://github.com/kkkkkkkm/Korean-MWP/blob/main/imgs/%EA%B7%B8%EB%A6%BC4.png >

</p>


각 문제 유형은 다음과 같은 세부 유형들이 존재한다. 

</br>
</br>


<img src = https://github.com/kkkkkkkm/Korean-MWP/blob/main/imgs/%EA%B7%B8%EB%A6%BC5.png width = "100%" height = "100%">

</br>


**코드상 구현**


데이터 생성기는 다음과 같은 방식으로 구현된다.


- 정보 변환과 연산자 변환을 위해 문제에 들어갈 명사 혹은 연산자 단어를 담은 리스트 선언


![그림1](https://github.com/kkkkkkkm/Korean-MWP/assets/69561492/45e7625b-b3bf-47db-ac6f-e837b045ec8f)

</br>

 
- 접사 변환과 문장 순서 변환이 적용된 문제 프레임들을 담은 리스트 선언, 여기서 문제 프레임은 명사와 피연산자가 비워진 상태로 존재

</br>

![그림2](https://github.com/kkkkkkkm/Korean-MWP/assets/69561492/7168e56b-cbd2-4f4c-bcb1-3e89f7433625)

</br>

- 랜덤 알고리즘을 통해 피연산자와 각 리스트에서 값 선택, 이후 선택된 문제 프레임의 빈 슬롯에 값이 채워져 문제와 수식 생성 

</br>

![그림3](https://github.com/kkkkkkkm/Korean-MWP/assets/69561492/440c9c2d-bc80-4a31-b88b-53eaef9032f4)

</br>

---

## 한국어 문장형 수학문제 풀이모델 

**풀이모델에 활용된 세 가지 구조**

* Seq2Seq 구조: </br>
RNN 기반 인코더와 디코더로 이루어진 구조 입력 시퀀스를 다른 도메인의 시퀀스로 출력
<img src = https://github.com/kkkkkkkm/Korean-MWP/blob/main/imgs/%EC%A0%80%EB%84%90%20attention%202.png width = "100%" height = "100%">


* Transformer 구조: <br>
기존 RNN layer를 Attention으로 대체하여 RNN이 가진 기울기 소실과 GPU 병렬 계산의 어려움을 해소

<img src = https://github.com/kkkkkkkm/Korean-MWP/blob/main/imgs/%EA%B7%B8%EB%A6%BC6.png width = "100%" height = "100%">



* Conformer 구조: <br>
음성 인식에서 SOTA를 기록한 모델로, CNN의 지역적 특징 포착 능력과 Transformer의 전역적 특징 포착 능력을 융합한 모델
본 논문에서는 Conformer 모델이 음성과 같이 순차적인 특성을 가지고 있는 자연어에서 단어의 의미와 문맥의 의미를 효과적으로 융합할 수 있을 것이라 사료하여 채택

<img src = https://github.com/kkkkkkkm/Korean-MWP/blob/main/imgs/%EA%B7%B8%EB%A6%BC7.png width = "100%" height = "100%">

