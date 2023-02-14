---
title: "AI SUMMER - Speech Synthesis[1]"
excerpt: "Speech synthesis: A review of the best text to speech architectures with Deep Learning"

categories:
  - NLP
tags:
  - [NLP, Audio, Speech, Speech_Synthesis]

permalink: /NLP/Speech-Synthesis-1/

toc: true
toc_sticky: true

date: 2023-02-09
last_modified_at: 2023-02-09
---

## AI SUMMER
[AI Summer]("https://theaisummer.com/")는 AI를 공부하고자하는  AI 관련 연구가 적었던 AI Winter과 대비되는 현재, AI에 대해서 배울 수 있도록 초보자를 위한 AI부터 Advanced 과정까지 다양한 레벨의 AI 교육 자료들이 준비되어있다.

## Advanced Deep Leaarning
Advanced Depp Learning의 Topics 중 [Audio](https://theaisummer.com/topics/audio/) 를 공부하며 공부한 것들을 정리하려고 한다. 

# Speech synthesis: A review of the best text to speech architectures with Deep Learning

음성합성이란? Text, 입술 움직임 등 음성이 아닌 modality에서 음성을 생성하는 작업. 
ex. TTS(Text To Speech)는 자연어(text)를 음성으로 변환

음성합성에는 다양한 접근 방식이 존재하며, 가장 대표적인 것은 concatenation synthesis와 parametric synthesis이다.

## Concatenation synthesis
Concatenation synthesis는 미리 녹음된 음성 세그먼트(speech segments)의 연결을 기반으로 한다.
segments는 전체 문장, 단어, 음절 등이 될 수 있다.
일반적으로 waveforms(.wav 파일) 또는 spectrograms 파일로 저장된다.
음성 세그먼트는 미리 녹음된 음성 파일에서 음성인식 기술을 활용하여 다양한 segments들을 얻을 수 있다.

segments를 획득한 다음 음향 속성(acoustic properties)에 따라 레이블을 지정한다. 
Run time에서, 데이터베이스에서 후보 단위의 최상의 체인을 결정하여 원하는 시퀀스가 생성된다.(unit selection)
즉, 데이터베이스의 다양한 segments들을 합성하여 체인을 만들고, 여러 개의 후보 체인들 중 최상의 체인을 결정하여 원하는 시퀀스가 생성된다.

## Statistical Parametric Synthesis
parametric synthesis는 음성(voice)을 수정하기 위해 function과 set of parameters를 사용한다.
![post main image](/assets/images/posts_img/Speech-Synthesis/statistical-parametric-speech-synthesis.png)
[Statistical Parametric Synthesis 논문](https://www.sciencedirect.com/science/article/abs/pii/S0167639309000648)

Statistical Parametric Synthesis는 일반적으로 training과 synthesis, 두 파트로 구성된다. 

훈련하는 동안, spectrum(성대), fundamental frequency(음성 소스) 등과 같은 오디오 샘플을 특성화하는 파라미터 세트를 추출한다. 그런 다음, statistical model을 통해 해당 파라미터들을 추정(estimate)한다.
지금까지 최고의 결과를 제공하는 것으로 입증된 모델을 HMM(Hidden Markov Model)이다.

합성하는 동안 HMM은 대상 텍스트 시퀀스에서 파라미터 세트를 생성한다. 이 파라미터는 최종 음성 파형을 합성하는데 사용된다.

### Statistical parametric synthesis의 장점
- DB에 오디오 샘플을 저장할 필요가 없다.
- Language independence
- 음성 특성에 대한 유연성

하지만, 대부분의 경우 합성된 음성의 품질이 좋지 않다.
따라서 Deep Learning 기반 방법이 사용된다.
이에 대하여 이야기 하기 전에, 음성 합성 모델의 평가 방법에 대해 먼저 알아보고자 한다.

## Speech synthesis evaluation
Mean Opinion Score(MOS)는 생성된 음성(speech)의 품질을 평가하는 데 가장 자주 사용되는 방법이다.
MOS의 범위는 0~5까지이며, 실제 사람의 음성은 4.5~4.8 사이이다.

MOS는 한 그룹의 사람들이 조용한 방에 안자 생성된 샘플ㅇ르 듣고 점수를 매기는 것을 의미한다.
즉, 모든 "사람들의 의견"의 평균이다.

## Speech Synthesis with Deep Learning
주어진 input text sequence 를 Y, target speech를 X라고 하면, 다음과 같이 나타낼 수 있다.
$$ 
X = argmaxP(X|Y,θ)
$$

여기서 θ는 모델의 파라미터이다.

일반적인 모델은 먼저 input text를 acoustic feature generator에 통과시킨다. acoustic feature generator는 fundamental frequency 혹은 spectrogram같은 acoustic features를 생성하는 역할을 한다. 

최종 speech segment를 생성하기 위해서, 보통 Neural vocoder가 사용된다.

## WaveNet
WaveNet은 acoustic features 대신 raw waveform을 사용하여 처음으로 성공한 모델이다. WaveNet은 1초에 16,000개의 샘플을 생성할 수 있다.

WaveNet의 핵심은 autoregressive model이다. autoregressive 모델은 각 샘플이 이전 샘플에 의존한다. 수학적으로 이것은 다음과 같이 표현할 수 있다.

$$
P_θ(x) = \displaystyle\Pi_{t=1}^Tp(x_t|x_1,...,x_{t-1})
$$

본질적으로, weveform의 joining probability를 이전 time steps의 조건부확률의 곱으로 factorize(분해)한다.

이러한 autoregressive models를 구축하기 위해 논문의 저자는 확장된(dilated) convolutions를 가진 fully convolutional neural network를 사용했다.
WaveNet은 PixelCNN과 PixelRNN에서 영감을 받았다.


![post main image](/assets/images/posts_img/Speech-Synthesis/FCNN_with_dilated_conv.gif)
[Source: WaveNet: A generative model for raw audio](https://www.deepmind.com/)

위 이미지와 같이 각 convolutional layer에는 dilation factor(팽창 계수)가 있다. 
WaveNet은 훈련단계에서는 실제 사람의 녹음파일을 사용했다.
훈련 이후 최종 샘플링은 확률 분포$$p_θ(x)$$를 계산하여 수행된다.
각 timestep에서:
- distrivution 에서 값(value)를 샘플링한다.
- value 를 input에 다시 공급하면, 모델이 새로운 예측을 생성한다.
- 이 절차를 한 번에 한 단계씩 계속하여 전체 음성 파형을 생성한다.

WaveNet은 모든 간단한 샘플에 대해 이 작업을 계속해서 수행해야하므로, 추론이 매우 느려지고, 계산 비용이 많이 들 수 있다는 단점이 있다.

## Fast WaveNet


