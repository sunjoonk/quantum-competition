# 퀀텀 AI 경진대회

안녕하세요. 퀀텀 AI 경진대회에 참가한 '칸쵸' 팀의 최고 점수 획득 모델 코드입니다.

이 리포지토리는 FashionMNIST 데이터셋의 클래스 0(T-shirt/top)과 6(Shirt)을 분류하기 위해 고안된 하이브리드 양자-고전 신경망(Hybrid QNN-CNN) 모델의 학습 및 평가 코드를 포함합니다.

## 모델 아키텍처

* **Classic Part (CNN)**: 3개의 Conv2d 레이어, BatchNorm, MaxPool, Dropout으로 구성된 피처 추출기
* **Quantum Part (QNN)**: 6 큐비트($wires=6$), 3 레이어($layers=3$)의 양자 회로. `qml.AngleEmbedding`으로 데이터를 인코딩하고 `qml.RX`, `qml.CNOT`, `qml.RZ` 게이트로 구성된 Variational Circuit을 사용합니다.
* **Classic Part (MLP)**: 양자 회로의 측정값($PauliZ$)을 입력받아 최종 분류(2-class)를 수행하는 2개의 Linear 레이어

## 주요 스펙

* **총 학습 파라미터**: 28,082
* **양자 회로 (QNN) 스펙**:
    * 큐비트 수: 6 (제한 8)
    * 회로 깊이: (원본 코드로 확인 필요, 제한 30)
    * 학습 가능 Q-파라미터: 30 (제한 60)

## 재현 결과

제출된 `best_model.pth` 모델 가중치를 사용하여 평가를 재현할 수 있습니다.

* **Accuracy (Class 0 vs 6)**: **90.6500%**

## 사용 방법

1.  리포지토리 클론:
    ```bash
    git clone [리포지토리 URL]
    cd Quantum_AI_Project
    ```

2.  의존성 설치:
    ```bash
    pip install -r requirements.txt
    ```

3.  Jupyter Notebook 실행:
    `quantum.ipynb` 노트북을 열고 '처음부터 모두 실행'을 진행합니다.

    노트북은 리포지토리에 포함된 `best_model.pth` 파일을 자동으로 로드하여 평가를 수행하고 90.65%의 정확도를 출력합니다.
