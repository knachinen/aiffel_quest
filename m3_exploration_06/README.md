![download](https://github.com/knachinen/aiffel_quest/assets/137038897/e9c494b5-156d-491a-9168-ee9a2cf5d649)# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김성진
- 리뷰어 : 최연석


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 1. 자기만의 카메라앱 기능 구현을 완수하였다.
    기본 예시 코드 외에 추가 기능을 추가하여 완수 하였다.
    # 코 위치 - 가로세로 선 표시
    '''
    draw_line(img_face_show, (x,0), (x,img_face_show.shape[0]), (255,255,255), 2)
    draw_line(img_face_show, (0,y), (img_face_show.shape[1], y), (255,255,255), 2)
    '''
    # 투명도 조정
    ```
    img_face_bgr = img_face_org.copy()
    # 스티커 부분 이미지
    sticker_area = img_face_bgr[refined_y:refined_y + img_sticker.shape[0],
                                refined_x:refined_x + img_sticker.shape[1]]
    # 마스킹 이미지
    img_mask = np.where(img_sticker==0, sticker_area, 255).astype(np.uint8)
    ```
    # 이미지 원근 조정
    ```
    M = cv2.getPerspectiveTransform(pts1,pts2)
    img_warp = cv2.warpPerspective(img_side_sticker, M, (cols, rows), cv2.INTER_LINEAR, borderValue=(255, 255, 255))
    ```
  > 2. 스티커 이미지를 정확한 원본 위치에 반영하였다.
    # 최종 이미지 출력
    ```
    img_face_bgr[refined_y:refined_y + img_sticker.shape[0], 
             refined_x:refined_x + img_sticker.shape[1]] = img_merge
    
    img_side_bgr[y_mod:y_mod + img_warp.shape[0], 
             x_mod:x_mod + img_warp.shape[1]] = img_merge
    ```   
  > 3. 카메라 스티커앱을 다양한 원본이미지에 적용했을 때의 문제점을 체계적으로 분석하였다.
    - 얼굴 인식모델이 인식하지 못하는 이미지 외에 여러 이미지들에 스티커가 정확한 위치에 반영 되었다.
    # 잘 안되는 이미지
    ```
    def get_rect_img(img_face, img_sticker)
    ```
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석과 마크다운으로 알아보기 편하였다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 오류 없이 잘 작동하셨다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 다음과 같은 순서로 이해하여 작성 하였다.
  '''
  이미지 불러오기 -> 얼굴 인식 -> 얼굴 모양 인식(코 위치 계산) -> 스티커 이미지(불러오기 및 조절, 벗어난 범위 처리) -> 수정 이미지 출력
  -> 투명도 조정 -> 이미지 원근 조정 -> 수정 이미지 출력 -> 잘 안되는 이미지
  '''
- [O] 코드가 간결한가요?
  > 함수형으로 코드를 작성하였고 주석을 제공하였다.
  # 함수형 코드 작성 예시
  ```
  # 위 과정 전체 반복
  def get_rect_img(img_face, img_sticker):
  ~생략
  ```
  # 주석 예시
  ```
  # 위 과정 전체 반복

  # 얼굴 인식 
  side_rects = detector_hog(img_side_bgr, 1)
  for dlib_rect in side_rects:
      l = dlib_rect.left()
      t = dlib_rect.top()
      r = dlib_rect.right()
      b = dlib_rect.bottom()
      
      cv2.rectangle(img_side_bgr, (l,t), (r,b), 
                    (0,255,0), 2, 
                    lineType=cv2.LINE_AA)
  # 얼굴 모양 인식
  list_landmarks = []
  for side_rect in side_rects:
      points = landmark_predictor(img_side_bgr, side_rect)
      list_points = list(map(lambda p: (p.x, p.y), points.parts()))
      list_landmarks.append(list_points)
      
  # 얼굴 모양 인식된 부분 점으로 표시
  for landmark in list_landmarks:
  ~생략
  ```

# 참고 링크 및 코드 개선
# 인식되지 않는 얼굴에 대해 다양한 얼굴 인식 모델 종류에 대해 링크 첨부
```
https://velog.io/@easttwave/Deep-Learning-%EC%96%BC%EA%B5%B4-%EC%9D%B8%EC%8B%9D-%EB%AA%A8%EB%8D%B8-%EB%B9%84%EA%B5%90-%EC%A1%B0%EC%82%AC
```
