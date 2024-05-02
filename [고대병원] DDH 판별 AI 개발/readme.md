# 목표 
 DDH 실시간 가이드 및 판별 AI 개발
 DDH 판별에 필요한 5개 Point의 위치 정보 이용

# 제안 방법
 논문의 concept을 참조, 2개의 AI 개발
 5개 point가 존재하는 영역을 검출하는 AI –> Global Detection
 영역 검출 후 정확한 위치의 point를 검출하는 AI –> Local Detection

# 학습 데이터 구성
 DICOM file에서 영상 추출
 추출한 영상을 256x256의 크기로 resize
 ‘labelme’ labeling tool을 이용하여 line annotation 진행
 DDH 판별에 사용되는 점 5개를 line에서 추출
 Iliac line에서 겹치는 영역은 임의로 지정하여 추출
 ![image](https://github.com/sunnnny02/sunny/assets/122530193/2a97df46-3eda-48bd-9145-6cb7226e707a) {: width="50%" height="50%"}
 1번 point : label 1의 왼쪽 point
 2번 point : label 2의 왼쪽 point
 3번 point : label 3의 왼쪽 point
 4번 point : label 3의 오른쪽 point
 5번 point : label 4의 오른쪽 point
 - 최종 생성된 dataset
   256x256 크기의 초음파 영상 2,823장
   5개 point 좌표 값을 저장한 텍스트 파일 2,823개

# 수행 내용 
- 모델 구조
![image](https://github.com/sunnnny02/sunny/assets/122530193/2ad8600d-f077-42b8-957b-55048ff836a8)
 The goal is to detect tumor’s location by conducting a 2 stage detection.
 We utilize the YOLOv8 architecture with inputs sized 256×256 to detect 5 tumor regions. For each input, we predict the label and region of each point.
 Subsequently,  We conduct a local detection to localize the exact points of the tumor based on the results of global detection. In this process, we utilize a Multi-Layer Perceptron(MLP) to predict the two points ; points on tumor’s location.
 The mean IoU of five points obtained from a global detection is 0.85, indicating improved results compared to the previous model.





