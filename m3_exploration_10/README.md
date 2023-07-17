# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 신유진


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 문제해결 뿐만 아니라 여러 사진들을 대상으로 피사체들이 잘 아웃포커싱 되었는지, 거리기반인지 대상기반인지등 여러가지 실험까지 진행함
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 이해됨, 직관적이고 간결하다
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 없다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 코드의 흐름을 이해했고 이를 변형해 함수를 만들었다.
- [X] 코드가 간결한가요?
  > 자동화하는 함수로 인해 코드가 간결하고 직관적이다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

```함수를 만들어 자동화하는 과정이 간결하고 직관적이다. 
def get_shallow_focus(img_path=img_path):
    # 이미지 파일 열기
    img_orig = cv2.imread(img_path)
    # segmentation model 만들기
    segvalues, output = model.segmentAsPascalvoc(img_path)
        
    #seg_color = (128,128,192)
    seg_color = (0,0,0)
    # rgb 칼라에 mapping
    seg_map = np.all(output==seg_color, axis=-1)

    # 배경을 blur처리 후, concat
    img_mask = seg_map.astype(np.uint8) * 255
    img_orig_blur = cv2.blur(img_orig, (20,20))
    img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)
    img_bg_mask = cv2.bitwise_not(img_mask_color)
    img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
    img_thre = np.where(img_mask_color<10, img_orig, 0)
    img_concat = np.where(img_mask_color<10, img_orig, img_orig_blur)

    # 이미지를 작업한데로 출력
    img_list = [cv2.cvtColor(img_orig, cv2.COLOR_BGR2RGB), 
                output, seg_map, img_mask, # 0, 1, 2, 3
                cv2.cvtColor(img_orig_blur, cv2.COLOR_BGR2RGB), # 4
                img_mask_color, # 5
                img_bg_mask, img_bg_blur,  # 6, 7
                cv2.cvtColor(img_bg_blur, cv2.COLOR_BGR2RGB),  # 8
                cv2.cvtColor(img_thre, cv2.COLOR_BGR2RGB), # 9
                cv2.cvtColor(img_concat, cv2.COLOR_BGR2RGB)]  # 10
    
    return img_list
```

# 참고 링크 및 코드 개선
```python
  코드의 간결성에 감탄하고 갑니다👍👍
  구글에 검색해 봤으나 노드에 나와있는 링크만큼 자세한 설명을 못찾아 어쩔 수 없이 노드의 링크들을 첨부하겠습니다.
  - 아웃포커싱하는 법 (https://m.blog.naver.com/typs6301/222172333739)
  - 얕은 피사계 심도 촬영의 이해 (https://www.adobe.com/kr/creativecloud/photography/discover/shallow-depth-of-field.html)
  - 3D 이미지 센서 (https://news.skhynix.co.kr/post/next-gen-3d)
  - Ego Motion(https://sites.google.com/view/struct2depth)
  - uDepth (https://ai.googleblog.com/2020/04/udepth-real-time-3d-depth-sensing-on.html)
```
