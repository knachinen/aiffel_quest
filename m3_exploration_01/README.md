# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 손정민


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 파라미터에 대한 설명과 변수 내용에 대한 설명이 주석으로 잘 달려 있었다. 또한 과정마다 어떤 의도로 작성하였는지 주석이 달려있어 이해하기 쉬웠다.
- [ ] 코드가 에러를 유발할 가능성이 없나요?
  > project 1의 fit 함수에서 매개변수로 'learning_rate'라는 이름을 사용하고 함수 내부에서는 'LEARNING_RATE'라는 이름을 사용하여 실행이 되지 않았다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 특히 project1의 y 데이터를 정규화한 부분에서 분석 데이터에 대한 이해도가 높다고 생각했다. 이외에도 전반적으로 코드를 이해하고 작성한 것처럼 보였다.
- [X] 코드가 간결한가요?
  > project 1의 model, train_test_split, loss, mse 등 과정을 모두 함수로 작성하였으며, 변수명도 특성을 알 수 있는 이름이었다. 또한 코드 내부에서 공백을 이용하여 보기 쉽게 구분하였다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# Project 1 주석 기록
def custom_train_test_split(X, y, test_size=0.2, random_state=None):
    """
    학습/검증 데이터 분리

    파라미터:
    - X: 피쳐 행렬
    - y: 타겟 
    - test_size: 테스트 데이터 비율 (default: 0.2).
    - random_state: 랜덤 씨드 (default: None).

    리턴:
    - X_train, X_test: 학습/검증 데이터 행렬.
    - y_train, y_test: 학습/검증 타겟.
    """
    
    # 랜덤 씨드 설정되었을 경우
    if random_state is not None:
        np.random.seed(random_state)

    # 검증 데이터 샘플 수
    num_test_samples = int(test_size * X.shape[0])

    # 랜덤 인덱스 값
    indices = np.random.permutation(X.shape[0])

    # 랜덤 인덱스를 학습/검증 셋으로 분리
    test_indices = indices[:num_test_samples]
    train_indices = indices[num_test_samples:]

    # 랜덤 인덱스로 학습/검증 데이터 분리
    X_train, X_test = X[train_indices], X[test_indices]
    y_train, y_test = y[train_indices], y[test_indices]

    return X_train, X_test, y_train, y_test
```
```python
#project1 오류 발생 부분
def fit(X, y, learning_rate=0.1):
    
    # 초기화
    losses = []
    w = np.random.rand(X.shape[1])
    b = np.random.rand()
    
    # 학습: epoch 1~999
    for i in range(1, 1000):
        dw, db = gradient(X, w, b, y)
        w -= LEARNING_RATE * dw
        b -= LEARNING_RATE * db
        L = loss(X, w, b, y)
        losses.append(L)
        if i % 100 == 0:
            print(f'iteration {i} : Loss {L:0.4f}')
        
    return w, b, losses
```
```python
#project 1 y 정규화

# y 데이터의 min, max
min_val = y.min()
max_val = y.max()

# min-max 정규화
normalized_y = (y - min_val) / (max_val - min_val)
```

# 참고 링크 및 코드 개선
```python
#project2 컬럼 선별

# holiday 분포 불균형하니... 드롭?
# casual, registered 드롭
drop_label = ["holiday", "casual", "registered"]
#drop_label = ["casual", "registered"]
train.drop(drop_label, axis=1, inplace=True)
train.head(3)

# 컬럼 선별에서 countplot은 단순히 데이터의 개수를 표시하기 때문에 barplot이나 pointplot을 이용해서 
# count 결정에 유의미한 영향을 주는지 판단하는 과정이 있었어도 좋았을 것 같습니다. 
# 또 corr()를 통해 상관관계 분석을 해봤을 때 month와 season, temp와 atemp의 상관관계가 
# 1에 근접하게 나오기 때문에 둘 중 하나를 선택하는 것이 좋았을 것 같습니다.
```
```python
for i in range(1, 1000):
  dw, db = gradient(X, w, b, y)
  w -= LEARNING_RATE * dw
  b -= LEARNING_RATE * db
  L = loss(X, w, b, y)
  losses.append(L)
    if i % 100 == 0:
      print(f'iteration {i} : Loss {L:0.4f}')

# project 1의 학습을 돌리는 과정에서 range를 1000으로 설정하여 900까지의 결과만 표시되었습니다. 
# 아래쪽에서 100번마다 표시하게 되어있기 때문에 1001로 수정한다면 1000번의 값까지 print될 수 있을 것 같습니다.
```
