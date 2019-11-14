# Project-"Lip_Reading"

## Korean lip reading for a hearing-impaired person
----

 이 주제를 선정한 이유는 청각 장애인들은 자막이나 수화로 영상을 시청해야하는데 실시간으로 음성을 자막으로 볼 수 없고, 또한 수화로 해주는 방송 또한 적기 때문에 생각해보게 된 주제이다. 최종적인 목표로는 real time으로 영상의 입모양을 해석하여 text로 보여주는 것이다. 
 
 첫 번째로 진행하여야 할 작업은 입을 인식하는 작업이다. 그렇기 때문에 얼굴 인식에 관련하여 공부를 진행하였다.
 
### 얼굴 인식
----
  얼굴 인식의 Step는 4개로 구성되어있다. 우리는 이 과정을 <mark>Highlight</mark>로 표시한 부분으로 변형하여 Project를 진행 할 것이다.
  
  1. 사진 안에 있는 모든 얼굴을 찾아야한다.
 
  -> <mark>영상에는 한명의 얼굴만이 나온다고 한정하여 진행할 것이므로 한명의 얼굴(입)만을 찾으면 된다.</mark>
  
  2. 얼굴의 각도, 방향, 조명등이 좋지 않은 상황이여도 인식을 해야한다.

  -> <mark>정면의 영상, 같은 조명 등 좋은 상황으로 환경을 한정하여 진행한다.</mark>
  
  3. 눈의 크기, 얼굴의 길이 등 다른 사람들과 구분하는데 사용하는 얼굴의 고유한 특징들을 찾아 낼 수 있어야한다.

  -> <mark>얼굴의 특징은 찾아내되 필요한 부분은 입의 모양이므로 단어를 말할 때 입의 모양의 특징을 찾아야한다.</mark>
  
  
  4. 얼굴의 고유한 특징을 기존의 알고 있는 모든 사람들과 비교하여 그 사람의 이름을 결정해야한다

  -> <mark>입의 특징을 비교하여 어떤 단어를 말하고 있는 것인지를 알아내야한다.</mark>

#### Step 1 얼굴 찾기
<img src="/images/step1_1.png" width="200" height="200">


 얼굴을 인식할때 컬러정보는 필요없기 때문에 흑백 사진으로 변환을 해준다.
 
 
 <img src="/images/step1_2.png" width="300" height="100">
 
 그 후 인접 픽셀과 비교하여 어두워지는 방향을 나타내는 화살표를 그려준다.
 
  <img src="/images/step1_3.png" width="300" height="300">
  
 이미지의 모든 픽셀에 대해 이 작업을 해주면 모든 픽셀이 위와 같은 화살표로 바뀌게 된다.
 

#### Step 2 얼굴 위치교정, 투영
교정과 투영은 얼굴이 다른 방향을 보고있을 경우를 해결해 주기 위해 적용해주는 기법이다. 이를 해결하기 위해서 landmark라 부르는 특정 포인트를 찾아내게 된다. 기계 학습 알고리즘을 훈련시켜 이러한 포인트들을 찾을 수 있도록 한다.
 
->우리의 Project에서는 정면을 바라보는 얼굴로 한정해주었기 때문에 이 단계에서는 다음 단계를 위한 landmark만 찾게 해주면 된다.
<img src="/images/step2.png" width="200" height="200">

dlib를 이용하여 이 과정을 수행 할 수 있다.


~~~
landmark_predictor = dlib.shape_predictor('/Users/a/workspace/shape_predictor_68_face_landmarks.dat')
~~~

#### Step 3 얼굴 인코딩
Deep Convolutional Neural Network를 훈련시켜 각 얼굴에 대해 128개의 측정값을 생성하도록 한다. (128D encoding vector)

-> 이 부분에서 우리는 입술의 landmark를 뽑고 그 값들을 인코딩하여 작업을 수행해줘야 할 것 같다. 48번부터 68번까지가 입술에 해당하는 landmark이므로 입술의 landmark는 아래와 같이 구할 수 있다.

~~~
for i in range(48, 68):
        coords[i] = (landmarks.part(i).x, landmarks.part(i).y)
~~~

#### Step 4 인코딩에서 사람의 이름 찾기
원래 이 Step에서는 해당하는 사람의 이름을 찾게된다. 하지만 우리는 해당하는 단어를 찾아야하므로 인코딩과 단어가 매칭되게끔 하는 것이 최종 과제일 것이다.

<img src="/images/step4.png" width="250" height="200">

----

현재까지의 진행 상태로는 얼굴을 인식하고 그 중에서 입술 부분의 랜드마크를 뽑아주고, 사각형을 쳐주는 부분까지 진행되었다.

입에만 사각형을 쳐주는 부분이 살짝 잘 안되었었는데 아래와 같이 해결하였다.

~~~
      landmarks = landmark_predictor(frame_gray, face)
            landmarks = land2coords(landmarks)
            landmark=landmarks;
            landmark = np.swapaxes(landmark,0,1)
            xy = landmark[landmark!=0];
            min_x = min(xy[:20]);
            max_x = max(xy[:20]);
            min_y = min(xy[21:]);
            max_y = max(xy[21:]);
            
            cv2.rectangle(frame, (min_x,min_y), (max_x, max_y), (120,160,230),2)
~~~

<img src="/images/re.png" width="250" height="250">