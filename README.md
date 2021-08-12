# Image forgery detection

## Research Keyword
> Watch your Up-Convolution: CNN Based Generative Deep Neural Networks are Failing to Reproduce Spectral Distributions (CVPR 2020)
> https://openaccess.thecvf.com/content_CVPR_2020/html/Durall_Watch_Your_Up-Convolution_CNN_Based_Generative_Deep_Neural_Networks_Are_CVPR_2020_paper.html

- [Watch your Up-Convolution 정리](https://github.com/Sang-Yeong/Research/blob/master/watch_your_up_conv.pdf)
- [Azimuth Integral 구현](https://github.com/Sang-Yeong/Research/blob/master/Azimuth_integral.ipynb)
- Idea
	- GAN, AE 와 같은 생성석 신경망; Up-Convolution 기법 사용
		- 보간을 이용한 up-conv
		- 전치된 conv
    - Up-Conv이 **스펙트럼 왜곡을 유발**한다는 사실 발견 --> 딥페이크 검출기 제안
    - 스펙트럼 왜곡을 보정할 수 있는 Spectral Reularization 제안
    	- --> GAN 모델 안정화 & 시각적 출력 품질 향상

<img src='./git_assets/watch_your_up_conv.JPG' width=700>

- Keyword
	1. Sampling method
	2. Frequency domain
	3. Fourier Transform
	4. Azimuth Integral


## Related Work
#### hand crafted method
[hand crafted method 논문 정리](https://github.com/Sang-Yeong/Research/blob/master/hand_crafted_image_forgery_detction.pdf)

> Exposing digital forgeries by detecting traces of resampling(IEEE Transactions on Signal Processing 2005)
> https://ieeexplore.ieee.org/document/1381775

- Idea
	- 이미지 위조 --> 이미지의 기본 통계 변화 분석
	- 이웃 픽셀과의 상관성을 갖는 주기적 samples를 찾음으로써 detect가능

- Resampling signals
<img src='./git_assets/resampling_singals.JPG' width=700>

- Resampling Images
<img src='./git_assets/resampling_images.JPG' width=700>



---
[Mahdian and Saic's method]

> Blind Authentication Using Periodic Properties of Interpolation(IEEE Transactions on Information Forensics and Security 2008)
> https://ieeexplore.ieee.org/document/4540058

- [Blind Authentication Using Periodic Properties of Interpolation 구현](https://github.com/Sang-Yeong/Research/blob/master/mahdian_estimator.ipynb)

- Idea: interpolated signals & their derivatives ← 감지 가능한 **특정 주기 속성** 존재
- Method
	1. ROI selection
	2. Signal derivative computation
	3. Radon Transformation
	4. Search for periodicity; autocovariance, fft
<img src='./git_assets/mahdian_estimator.JPG' width=700>


---

> Effective Estimation of Image Rotation Angle Using Spectral Method (IEEE Signal Processing Letters 2014)
> https://ieeexplore.ieee.org/document/6805599
> https://github.com/ChenglongChen/image-rotation-angle-estimation


- Idea
	- 이미지 회전 각도를 추정하는 blind and effective method 제안
	- 2차 통계의 2차원 스펙트럼을 사용하여 회전된 이미지의 숨겨진 주기성을 활용하여 작동


- 연구 실험결과 확인
<img src='./git_assets/estimate_angle.JPG' width=600>


---
[Vázquez-Padín et al.'s method]
> Two-dimensional statistical test for the presence of almost cyclostationarity on images (2010 IEEE International Conference on Image Processing)
> https://ieeexplore.ieee.org/document/5652513

- scaling
	- 1.05 ~ 2.25 (0.05차이로 구성)
	- interpolation filter: Lanczos-3 kernel(truncated sinc)
	- correct 성공률 측정 기준
	- 40개의 이미지로 test → avg
	- Laplacian operator를 이미지에 적용하고 method 사용


- rotation
	- -89 ~ -1 (2.5차이로 구성)
	- interpolation filter: bicubic
	- 성공률 측정 기준
		- our method
		- Mahdian and Saic; 해당 스펙트럼 피크의 위치에서만 각도를 결정할 수 있기 때문




#### end-to-end model
[ManTra-net]
> ManTra-Net: Manipulation Tracing Network for Detection and Localization of Image Forgeries With Anomalous Features
> https://ieeexplore.ieee.org/document/8953774

<img src='./git_assets/mantra-net.JPG' width=700>

- preprocessing and postprocessing 없이 detection and localization를 모두 수행하는 end-to-end network
- 385가지 유형의 조작 구별가능
- **BayarConv2D**
	> Constrained Convolutional Neural Networks: A New Approach Towards General Purpose Image Manipulation Detection (IEEE Transactions on Information Forensics and Security 2018)
- **SRMConv2D**
	> Learning Rich Features for Image Manipulation Detection(CVPR 2018)
