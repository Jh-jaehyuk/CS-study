### Overfitting 에 대처하는 방법

1. Early Stopping (조기 종료)

학습 과정에서 파리미터값을 부여해 training loss는 계속 낮아지더라도 validation loss는 올라가는 시점을 Overfitting으로 간주하여 학습을 종료하는 방법
즉, 모델이 학습 데이터에서 더 이상 성능이 향상되 않는 시점에서 학습을 멈춰서 오버피팅을 방지하는 방법이다.
   
![image](https://github.com/user-attachments/assets/d236d486-2493-4cbf-b685-ea4d76798036)

2. Cross-validation (교차 검증)

데이터를 여러 번 나누서 학습하고 평가하여 모델이 학습 데이터에 과적합되었는지 여부를 확인한다.<br>

아래 이미지는 k-flod(K번 나누고 각각의 학습 모델의 성능을 비교하여 평균 값으로 처리)라는 기법을 사용해 교차 검증을 진행 하는데 
- 장점은 데이터셋을 나눠서 검증을 하다보니 K개의 성능 결과를 통합하여 하나의 결과를 도출하기 때문에 보다 일반화된 모델 성능 평가 가능하다
- 단점은 너무 오랜 시간이 걸린다는 문제가 있다

![image](https://github.com/user-attachments/assets/0409349f-8019-4a7a-9be4-47463191c8eb)

3. Data Augmentation (데이터 증강):

학습 데이터의 양을 인위적으로 늘려, 모델이 더 다양한 데이터를 학습하도록 한다.<br>

예를 들어, 이미지 데이터를 회전하거나 확대하여 더 많은 학습 데이터를 만들어서 데이터셋을 증강 시킨다.<br>

하지만, task에 맞기 않는 잘못된 기법을 사용하면 오히려 성능이 떨어질 수 있다. 

![image](https://github.com/user-attachments/assets/a092bb88-f549-4804-8040-c0e3a90b9685)

4. Regularization (정규화):

- L1/L2 정규화: 모델의 가중치에 패널티를 부과하여, 지나치게 복잡한 모델이 되는 것을 방지합니다.
- Dropout: 학습 과정에서 ㅏ## Overfitting 에 대처하는 방법

정규화에서 L1/L2 와 Dropout은 자세한 설명이 필요해서 다음에 알아보는 시간을 가지겠습니다.

Overfitting에 대처하는 방법은 다양하게 되어 있는데 위의 기법이 아닌 모델 앙상블이라던지 STOME 방식이라던지 다양하지만

task에 맞춰 적절한 기법을 사용해 모델의 성능을 높여보자 !
