# Automatic-Data-Collecter
# 자율주행 #인공지능 # 가상 데이터 # 가상 공간 # 3D유니티 #PPO알고리즘  


## 📜 프로젝트 소개 
 - 자율 주행 모델 개발 시, 개발자들은 종종 가상 데이터를 활용합니다. 하지만 이 데이터는 그들의 차량이나 다른 환경과 일치하지 않을때도 있지만, 프로그램의 제한으로 인해 수정이 어려워 대부분 그대로 사용하게 됩니다.
 - 이러한 문제를 해결하기 위해 Automatic-Data-Collecter(ADC)를 개발하였습니다.
 - 이 SW는 사용자가 자신의 차량에 맞게 환경을 쉽게 조정할 수 있도록 설계되었으며, 전방 이미지, 라이다 센서 데이터, 세그멘테이션 정보 등을 자동으로 수집하여 제공합니다.

## ⌚ 개발 기간
* 2023.09 ~2023.10

## 👨🏿‍🤝‍👨🏿 제작 맴버
 - 하태성 : 가상 공간 제작, 자율주행 차량 제작, 데이터 수집 알고리즘 제작(front_image, 차량의 현재 상태, segmentation)
 - 박신영 : 가상 공간 제작, 전반적인 코드 최적화, 데이터 수집 알고리즘 제작(Lidar_sensor_data)

## 🛠 개발 환경
- python
- pytorch
- C#     
- Unity

## 🏆 경남 SW경진대회에서 대상을 수여하였습니다.🎊🎊

# 🎥지금부터 설명을 시작하겠습니다.

![슬라이드1](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/7680f4aa-2c8d-43dd-bf4d-bfbc3d690c45)

![슬라이드2](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/760fd190-1e17-46cc-9053-0981dc8718c7)

![슬라이드3](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/877fbe9b-028a-4cc5-8a3d-2f1544e80d9d)
 - 먼저, RC카의 자율 주행 방식은 크게 두 가지 방법이 있습니다. 왼쪽 예시처럼 차량의 전방 이미지를 활용하여 주행하는 방법과, 오른쪽 예시처럼 Lidar 센서 값을 활용하여 주행하는 방법입니다. 차량이 이러한 데이터를 수집한 후, 인공지능 모델을 통해 분석하고 처리하여 자율 주행이 이루어집니다.

![슬라이드4](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/86888e59-8159-4426-a0b0-50e647d1883c)
 - 이러한 RC카는 두 단계의 과정을 거칩니다. 첫 단계에서는 왼쪽 예시와 같이 학습 공간에서 충분한 학습이 이루어집니다. 이 과정에서 차량은 문제 없이 주행할 수 있을 만큼 충분히 학습됩니다. 그런 다음, 두 번째 단계로 넘어가 오른쪽 예시처럼 테스트 공간에서의 성능을 평가합니다.
 - 하지만 여기에서 주목해야 할 중요한 문제점이 있습니다. 우리의 인공지능 모델은 제한된 학습 공간에서만 학습이 이루어지기 때문에, 다양한 환경과 상황에서의 데이터를 충분히 수집하고 학습하지 못하는 경우가 발생할 수 있습니다. 이로 인해 모델은 학습 공간에서는 원활하게 작동하지만, 실제 테스트 공간에서는 예상보다 성능이 저하될 수 있는 '과적합' 문제가 발생할 수 있습니다.
![슬라이드5](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/bb448a40-b108-4ae8-b83f-7844831dc6c9)
 - 실제로 저희 322팀의 RC카 환경에서도 똑같은 문제를 보여주었는데요. 학습공간에서 완벽하게 학습이 되었지만 다양한 상황과 공간 데이터를 수집하지 못한 모델은 테스트할 때 이상행동을 보여주었습니다.
   
![슬라이드6](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/12a17a25-8057-4fe8-835a-4f7c5006961e)
 - 데이터의 다양성 부족은 인공지능 모델 학습에 큰 문제로 작용합니다. 이를 해결하기 위해, 다양한 데이터 전처리와 증강 방법이 사용되고 있습니다. 예를 들어, 좌측의 이미지에서 볼 수 있듯이, 이미지를 회전시키거나 색을 반전시키는 방법이 있습니다. 이러한 방법들은 모델이 다양한 상황에서도 잘 작동할 수 있도록 도와줍니다.
 - 그러나, 실제로는 이러한 전처리와 증강 방법만으로도 데이터 부족 문제를 완전히 해결하기는 어렵습니다. 이에 대한 해결책으로, 우측의 이미지에서 볼 수 있듯이, 가상 공간을 활용한 방법이 등장하였고, 가상 공간에서는 실제와 유사한 다양한 상황을 모사하여 데이터를 생성할 수 있어, 이를 통해 수집되는 가상 데이터를 학습에 사용함으로써 모델의 성능을 향상시킬 수 있습니다.

![슬라이드7](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/ca61abe3-10a4-4e5e-8fd1-b1aae122dbea)
 - 가상 데이터를 활용한 자율주행 모델 학습 방법에 대해 언급하자면, 특정 프로그램들이 이미 이러한 접근 방식을 사용하고 있습니다. 예를 들어, 왼쪽 이미지에서 볼 수 있는 AWS(아마존 웹 서비스)는 이러한 방법을 적용하고 있습니다. AWS는 자체적으로 제작한 가상 공간에서 자율주행 모델을 학습시키고, 학습된 모델을 실제 트랙에서 테스트하는 방식을 사용하였습니다.
 - 하지만, AWS 프로그램에는 한계가 있습니다. 그것은 이 프로그램이 AWS의 자체 차량과 트랙에서만 사용할 수 있도록 제한되어 있다는 점과 유료화로 되어있는 점입니다. 이로 인해, 다른 사용자나 연구자들이 이 프로그램을 활용하여 모델을 학습시키기에는 제약이 있게 됩니다. 
 - 저희 322팀은 RC카 자율주행 모델의 학습을 개선하고, 더욱 유연하게 적용할 수 있는 방법을 모색하였습니다. 저희의 목표는 기존의 제한된 사용성 문제를 해결하는 것이었습니다. 저희는 누구나 자신의 차량과 트랙에 맞게 수정하고 적용할 수 있는 프로그램을 개발하려 했습니다.
 - 또한, 사용자가 자율주행 모델 학습에 필요한 다양한 유형의 데이터를 자유롭게 수집할 수 있도록 하여, 모델의 학습 과정과 결과를 더욱 풍부하고 정확하게 만드는 것이 우리의 목표였습니다.
![슬라이드8](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/3bef7840-3532-4af0-a605-8241bab581e3)
 - 지금부터 저희 322팀이 제작한 프로그램을 보여드리겠습니다.
![슬라이드9](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/6b31dd5d-a6a8-418d-812b-304a18c85738)

![슬라이드10](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/166c41ff-2ad1-45ae-a00a-b9c1c2362f6d)

![슬라이드11](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/d62b9037-26fc-4417-b82e-967ab20e036e)

![슬라이드12](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/4d0fc01f-739e-4393-a0eb-acb47fdb4d47)

![슬라이드13](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/9da5d938-6515-444d-80dc-25898d4b7d12)

![슬라이드14](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/17c0b318-a988-4d3c-981f-509f57bf6b77)

![슬라이드15](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/f17f5539-d1d8-4f4a-93e1-e19a5b0076a7)

![슬라이드16](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/b4b54a02-5545-44d2-b076-779f05df057c)

![슬라이드17](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/3ebf767d-6bdc-43fd-aa46-dd9e46bef80e)

![슬라이드18](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/b2c6d3cd-b780-4e12-b8e0-6efe228a7249)

![슬라이드19](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/2544e52b-564a-47e4-b7bc-1550773ce36e)

![슬라이드20](https://github.com/gkxotjd12312/Automatic-Data-Collecter/assets/54784059/368f6d6d-f689-44cc-b2ac-88a6bb0a306d)
