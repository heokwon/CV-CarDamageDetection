# CV-CarDamageDetection
### Team - CODEnter
* 윤소미, 장주찬, 전규원, 한정현, 허 권   
[PPT](https://github.com/heokwon/CV-CarDamageDetection/blob/main/car%20damage.pdf)
<br><br>
## Introduction
* Semantic Segmentation을 이용한 자동차 파손부위 탐지   

* 사람이 직접 파손부위를 하나하나 검수해야 하는 부담을 덜 수 있고, 회사 입장에서도  
인적,시간적 자원 절약 측면에서 좋을 것이라 생각하여 진행하게 된 프로젝트   

* 사진이나 영상 속 객체를 pixel단위로 탐지하여 object detection보다 세부적으로   
detecting이 가능한 Semantic Segmentation을 선택
<br><br>
## Dataset
* AI-hub에 socar dataset이 올라오기 이전   

* 구글링을 통하여 segmentation annotation이 포함된 차량파손이미지 수집   

* via tool - 부족한 데이터셋 보충, 좀 더 세밀한 mask를 통해 성능개선을 기대      
차량 파손 이미지 COCOdataset을 사용, via tool을 사용하여 이미지에 polygon을 직접 달아줌으로써   
mask의 좌표를 생성 후 annotation.json 파일 생성   
2명의 팀원이서 1일동안 총 400장의 데이터셋 생성   

* 차량 파손 부위가 아닌 파손 "형태"를 detecting하는 작업으로, 차량 이외에도 스크래치나 이격과   
같은 파손형태 데이터셋도 사용   

* Augmentation - Pytorch의 albumentation을 사용하여 offline으로 데이터증식 진행   
HorizontaFlip, VerticalFlip, Blur, OpticalDistortion, Resize, RandomRotate90   

* Binary 와 Multi 로 진행   
Binary Label : background - 0 , damaged - 1   
Multi Label : background - 0 , scratch - 1 , dent - 2 , spacing - 3 , broken - 4
<br><br>
## Models
* Semantic Segmentation에서 가장 많이 쓰이는 모델 선정   

* DeepLabV3   
reference를 git clone하여 하이퍼파라미터 변경 및 inference추가   
pre-trained model에 fine-tuning   

* Unet   
reference를 git clone하여 하이퍼파라미터 변경 및 inference추가
논문내용을 직접 구현하여 사용
<br><br>
## Env and Requirements
* Google Colab, VScode, AWS
* Pytorch, Pillow, OpenCV, Numpy, Matplotlib, via, albumentation, Weights and Biases
<br><br>
## Progress
* 데이터셋 구축 - 구글링, via프로그램사용하여 직접만들기   

* 데이터셋 정제   
annotation info가 담겨있는 json파일을 이용하여 polygon2mask진행   
확장자를 jpg에서 png로 바꾸기   
binary형태의 데이터셋에서 class별로 array값을 다르게 부여햐여 multi dataset구축   
unet에서 사용하기 위해 img형식의 mask.png를 array로 바꿔 mask.npy로 변경   
split-folders를 사용하여 폴더안의 파일들을 train-set과 valid-set으로 나눔   

* 데이터셋 증식   
albumentation을 이용하여 오프라인에서 augmentation진행   
HorizontaFlip, VerticalFlip, Blur, OpticalDistortion, Resize, RandomRotate90   

* DeepLabV3 & Unet Reference 찾기   

* DeepLabV3 Reference 튜닝, 최적의 hyperparameter찾기, pre-trained 모델에 fine-tuning 시키기   

* Weights and Biases를 연동하여 train-log 관리   

* Unet 논문 및 유투브 참고하여 직접구현 후 학습 진행   

* Label별로 학습시킨 후 ensemble 시도
<br><br>
## Referecne
* via tool : https://www.robots.ox.ac.uk/~vgg/software/via/via-1.0.6.html
* DeepLabV3 : https://github.com/msminhas93/DeepLabv3FineTuning.git
* Unet : [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://arxiv.org/abs/1505.04597)   
* albumentation : https://albumentations.ai/
