# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 최연석


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
> 네 기능별로 분류하여 코드를 작성 하여 이해하기 쉬웠습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
> 오류 없이 잘 구동 가능했습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
> 데이터 호출, 전처리, 확인, 정규화, 학습, 모델링, 예측값 생성등 순서대로 작성하였습니다.
> voting을 사용하여 성능을 향상하였습니다.
  ```
  gb = XGBRegressor(learning_rate=0.024, max_depth=8, n_estimators=1000, random_state=random_state)
  lgbm0 = LGBMRegressor(boosting='goss', learning_rate=0.015, max_depth=7, n_estimators=1600, random_state=random_state, boost_from_average=False)
  lgbm1 = LGBMRegressor(boosting='gbdt', learning_rate=0.015, max_depth=13, n_estimators=1400, random_state=random_state, boost_from_average=False)
  lgbm2 = LGBMRegressor(boosting='goss', learning_rate=0.015, max_depth=7, n_estimators=1400, random_state=random_state, boost_from_average=False)
  lgbm3 = LGBMRegressor(boosting='gbdt', learning_rate=0.015, max_depth=11, n_estimators=1400, random_state=random_state, boost_from_average=False)

  # voting regressor
  vr = VotingRegressor(estimators=[('xgb', xgb), ('lgbm0', lgbm0), ('lgbm1', lgbm1), ('lgbm2', lgbm2), ('lgbm3', lgbm3)])
  ```
- [X] 코드가 간결한가요?
> 간결하고 반복되는 사항 없이 잘 구현하였습니다.
> 함수를 이용하여 정리를 가독성이 높았습니다.
```
def save_submission(model, test, model_name, error):

    # 테스트 데이터셋으로 예측
    prediction = model.predict(test)
    prediction = np.expm1(prediction)
    
    # csv 파일 생성
    data_dir = './data'
    submission_path = join(data_dir, 'sample_submission.csv')
    submission = pd.read_csv(submission_path)
    submission['price'] = prediction
    submission_csv_path = '{}/submission_{}_{}.csv'.format(data_dir, model_name, error)
    submission.to_csv(submission_csv_path, index=False)
    print(submission_csv_path)

save_submission(vr, Xt, 'vr', error='rmse_105376')
```
# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
```

# 참고 링크 및 코드 개선
```python
```
