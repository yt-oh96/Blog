# 1.Image data handling

### %matplotlib inline
Rich output : 도표와 같은 그림, 소리, 애니메이션과 같은 결과물

이와같은 Rich output에 대한 IPython에서 제공하는 표현방식이다.

%matplotlib inline의 역할은 notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게 해주는 것이다.

### plt.rcParams["figure.figsize"] = (8,6)

matplotlib.pylab의 rcParams 설정을 활용하면 차트의 크기, 선의 색, 두께 등 기본값을 설정 할 수 있다.

항목|설명 
-----------|-----------
"figure.figsize" | figure의 크기 (가로,세로)
"lines.linewidth" | 선의 두께    
"lines.color"| 선의 색
"axes.grid" | 차트 내 grid 표시 여부  

### 이미지
컬러 이미지에서 opencv의 경우 bgr의 채널을 갖고, matplotlib의 경우 rgb의 채널을 갖기 때문에 채널 순서를 적절히 변형해주어야한다.         

이미지 데이터는 numpy array인 ndarray로 이루어져있다. opencv는 unsigned char(8bit)를 각 요소의 기본 데이터 타입으로 처리한다.

# 2. Face detection and recognition
### haar cascade
2001년 Viola, Jones가 제안한 방법으로 Haar like feature에 기반한 알고리즘으로 구성되어있다. 

cascade란 하나의 검출기로 물체를 찾는 것이 아닌 여러 개의 검출기를 순차적으로 적용하되 순차적으로 점점 더 어려운 검출기를 적용하는 방법이다. 

시간이 많이 걸리는 강력한 검출기는 초기 단순 검출기를 통과한 후보에만 적용되기 때문에 전체적으로 검출속도를 향상 시킬 수 있다.

<img src="/images/haar.png" width="400" height="200">

위의 그림과 같은 사각형들을 사진에 겹쳐 놓은 후, 명암을 이용한 패턴으로 사람의 얼굴인지 아닌지를 판단한다. 

밝은 영역에 속한 픽셀값들의 평균과 어두운 영역에 속한 픽셀값들의 평균의 차이가 threshold를 넘으면 사람 얼굴에 대한 Haar like feature가 존재하는 것이다. 
