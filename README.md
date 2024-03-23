# ImageToCartoon
This program makes your photo as a cartoon material
***
당신의 추억을 만화처럼 만들어 저장할 수 있습니다!

사용 예시:
![ex](https://github.com/Jung-H-C/ImageToCartoon/assets/101037538/80a6dacd-0866-47d7-873f-f86aa03033dd)
이러한 사진들을
![image](https://github.com/Jung-H-C/ImageToCartoon/assets/101037538/d9c62d4c-97d6-4a0c-b1f4-869643c75d72)

이런 식으로 바꿔줍니다!

# 코드 설명
![image](https://github.com/Jung-H-C/ImageToCartoon/assets/101037538/3b38b50f-8f69-49a3-becf-80181aae030c)
<br/>
프로그램의 메인 뼈대는 이와 같습니다.
등장하는 함수를 소개해드리겠습니다:
- check_size
- cartoonize

# check_size 함수
![image](https://github.com/Jung-H-C/ImageToCartoon/assets/101037538/3dc5a8aa-cbaf-43c4-a9eb-169d0d8c6b88)
<br/>
이 함수는 입력 image file의 size가 너무 큰 경우를 대비하여
파일의 height과 width의 합이 일정 크기가 넘어가게 되면 size를 같은 비율로 점점 줄여나가며
threshold 보다 작은 값을 만족할 때까지 반복합니다.

# cartoonize 함수
![image](https://github.com/Jung-H-C/ImageToCartoon/assets/101037538/e46ca631-d78d-4a97-a7c0-34a12d6538bb)
<br/>
이 함수는 입력 image file을 cartoon화 시키는 작업을 합니다.
다음 과정을 거칩니다:
1. image를 BGR에서 Gray Scale로 변환합니다. (흑백 cartoon 느낌 부여)
2. image를 bilateralFilter를 거쳐 블러 처리 해줍니다. (noise를 제거하는 역할)
3. image속 사물의 테두리를 강조하기 위해 Canny함수를 거쳐줍니다. (인물, 사물 강조 역할)

***
# 만화 같은 느낌이 잘 표현된 경우:
<img src="/sunny_day.jpg" width="30%" height="30%">
<img src="/sunny_day_30_60.PNG">

<br/>
다음 사진과 같은 경우 인물과 배경 등이 테두리 만으로도 선명하게 표현되어 cartoon의 느낌을 잘 전달 해줍니다.

# 아쉬운 경우:
<img src="/blurry_photo.jpg" width="30%" height="30%">
<img src="/blurry_photo_30_60_limit.PNG">
  
<br/>
다음 사진처럼 흔들린 경우는 객체의 테두리가 모호하여 cartoon느낌이 잘 표현되지 않은 경우입니다.
밑에서 다시 서술할 예정이지만 cv.Canny의 임계값을 여러 방면으로 조정해보았으나 애초에 흔들린 사진의 경우는 잘 표현되지 못했습니다.

# 알고리즘 한계:
우선 cvtColor메서드로 BGR2GRAY 변환을 해주었기 때문에 컬러의 경우 아예 표현할 수 없는 부분이 아쉬웠습니다.
예전 고전cartoon의 흑백 느낌을 살리려는 취지였지만 테두리만을 강조하게 되면서 black or white가 되었고
흔들린 사진의 경우 threshold1, threshold2 값을 여러 방면으로 고쳐보았지만 일정 수준 이상의 개선은 불가했습니다.
나중에 새로운 알고리즘으로 발전시킨다면 흑백후 Canny로 테두리를 강조하는 대신 sharpening kernel을 사용하여 디테일을 살려보고 싶습니다.








