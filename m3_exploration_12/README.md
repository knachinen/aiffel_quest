# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 최연석


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > Step, 상세 내용 별로 주석이 달려있어 이해하기 쉬웠습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 그 외 오류가 발생할 부분은 발견하지 못했습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
- [X] 코드가 간결한가요?
  > markdown을 활용 하여 코드가 구분하기 쉬웠습니다.

# 예시
# 전처리를 순서대로 처리 하였고 알맞은 주석을 달았습니다.
'''
# 데이터 전처리 함수
def preprocess_sentence(sentence, remove_stopwords=True):
    sentence = sentence.lower() # 텍스트 소문자화
    sentence = BeautifulSoup(sentence, "lxml").text # <br />, <a href = ...> 등의 html 태그 제거
    sentence = re.sub(r'\([^)]*\)', '', sentence) # 괄호로 닫힌 문자열 (...) 제거 Ex) my husband (and myself!) for => my husband for
    sentence = re.sub('"','', sentence) # 쌍따옴표 " 제거
    sentence = ' '.join([contractions[t] if t in contractions else t for t in sentence.split(" ")]) # 약어 정규화
    sentence = re.sub(r"'s\b","", sentence) # 소유격 제거. Ex) roland's -> roland
    sentence = re.sub("[^a-zA-Z]", " ", sentence) # 영어 외 문자(숫자, 특수문자 등) 공백으로 변환
    sentence = re.sub('[m]{2,}', 'mm', sentence) # m이 3개 이상이면 2개로 변경. Ex) ummmmmmm yeah -> umm yeah

    # 불용어 제거 (Text)
    if remove_stopwords:
        tokens = ' '.join(word for word in sentence.split() if not word in stopwords.words('english') if len(word) > 1)
    # 불용어 미제거 (Summary)
    else:
        tokens = ' '.join(word for word in sentence.split() if len(word) > 1)
    return tokens
'''
# summa를 이용하여 Extractive, Abstractive 요약간 비교가 잘 되엇습니다.
'''
for i in range(0, 6):
    text = seq2text(encoder_input_test[i])
    print("- 토큰화된 원문: \n{}\n".format(text))
    print("- 실제 요약: \n{}\n".format(seq2headlines(decoder_input_test[i])))
    print("\n- 예측 요약: \n{}\n".format(decode_sequence(encoder_input_test[i].reshape(1, text_max_len))))
    print("- 원문: \n{}\n".format(text_original_test[i]))
    print("- 'SUMMARIZE' 요약: \n{}\n".format(summarize(text_original_test[i], ratio=0.4)))

data_org['text'].iloc[0]
print(summarize(data_org['text'].iloc[0], ratio=0.4))
print(summarize(data_org['text'].iloc[0], words=20))    
'''
# loss를 시각화 하여 잘 분석하였습니다.
'''
plt.plot(history.history['loss'], label='train')
plt.plot(history.history['val_loss'], label='test')
plt.legend()
plt.show()
'''

# 참고 링크 및 코드 개선
```python
```
