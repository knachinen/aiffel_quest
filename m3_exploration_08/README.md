# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 서희원


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [o] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > Word2Vec 부분을 완성하지 못하혔습니다.
  
- [x] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네 주석을 상세히 적어주셔서 이해하기 쉬웠습니다.
  ```python
  def words_to_indices(texts):
    # 0: '<PAD>' ; 패딩용 단어
    # 1: '<BOS>' ; 문장의 시작지점
    # 2: '<UNK>' ; 사전에 없는(Unknown) 단어

    index = 3  # Start indexing from 1 (0 can be used for padding or reserved for special tokens)

    indices = []
    for word in texts:
        if word not in word_index:
            word_index[word] = index
            index += 1
        indices.append(word_index[word])

    return indices
  ```
- [x] 코드가 에러를 유발할 가능성이 없나요?
  > 네 마지막 Word2Vec 부분을 제외하면 모두 잘작동합니다.
- [x] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 konlpy 가 작동하지 않아 새로운 모듈을 찾아 개발하신걸로 보면 아주 잘 이해하신 것 같습니다.
- [x] 코드가 간결한가요?
  > 네

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
```

# 참고 링크 및 코드 개선
```python
```
