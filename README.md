<div align="center">

# 🎯 MBTI 다국어 번역 및 텍스트 분류 전이학습
### 🧠 Hugging Face NLLB-200을 활용한 교차 언어(Cross-lingual) 파인튜닝

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E.svg?style=for-the-badge&logo=Hugging-Face&logoColor=black)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)

</div>

## 📌 프로젝트 소개
본 프로젝트는 인터넷 게시물 데이터를 기반으로 작성자의 **MBTI 성격 유형을 예측하는 텍스트 분류 전이학습(Transfer Learning)** 파이프라인입니다. 

특히 영문으로만 이루어진 대규모 원본 데이터셋을 한국어 화자 환경에 맞추기 위해, Meta(Facebook)의 고성능 신경망 기계번역 모델인 `NLLB-200`을 도입하여 데이터를 한국어로 일괄 번역한 뒤 학습을 수행하는 창의적인 다국어 처리 접근법을 보여줍니다.

## 📊 데이터셋 및 모델 구성
- **빅데이터 출처**: [MBTI 성격 유형 데이터셋 (Kaggle)](https://www.kaggle.com/datasets/datasnaek/mbti-type) (MBTI 타입 및 유저별 다중 텍스트 포함)
- **기계 번역 모델 (Teacher Model)**: [`facebook/nllb-200-distilled-600M`](https://huggingface.co/facebook/nllb-200-distilled-600M) - No Language Left Behind 오픈소스 모델 활용.

## ✨ 핵심 파이프라인 단계
1. **데이터 스크래빙 및 탐색(EDA)**: MBTI 데이터셋을 적재하고 불균형 분포 및 텍스트 노이즈 구조를 시각적으로 확인합니다.
2. **텍스트 정규화 및 전처리 (Preprocessing)**: 무의미한 URL 파라미터, 이미지 확장자 토큰 등을 정규표현식(`re`)으로 제거하고 문장 단위로 필터링합니다. 
3. **NLLB 기반 대규모 기계번역 (Translation)**: 전처리된 영어 문장을 NLLB-200 모델을 호출하여 고품질의 한국어로 변환합니다. (언어 장벽 극복)
4. **Hugging Face 토크나이징 (Tokenization)**: 사전 학습된 언어 모델의 텍스트 분류(Classification) 토크나이저를 통해 한국어 문장을 텐서로 양자화합니다.
5. **전이학습 (Transfer Learning) 훈련**: 변환된 한국어 데이터 위에서 MBTI 라벨의 손실 함수를 줄여나가는 방향으로 언어 모델 가중치를 파인튜닝(Fine-tuning)합니다.
6. **추론 및 성능 평가 (Inference)**: 새로운 입력 한국어 문장에 대해 훈련된 모델이 MBTI를 확률적으로 추론하고 결과를 반환합니다.

## 🛠️ 기술 스택
* `transformers` (Hugging Face)
* `pandas`, `numpy`
* `re` (Regular Expressions)
* `tqdm` (진행 상태 시각화)

## 🚀 시작하기

이 프로젝트는 **Google Colab (GPU 권장)** 환경에서 실행되도록 최적화되어 있습니다.
1. 환경에 필수 라이브러리를 설치합니다.
   ```bash
   pip install transformers datasets pandas numpy
   ```
2. 프로젝트 노트북 파일을 열고 셀을 순서대로 실행하여 번역 파이프라인 및 분류 모델 학습이 완료되는 과정을 모니터링하세요.

---
*본 프로젝트는 대규모 언어 모델(LLM) 생태계, 다국어 자연어 처리(NLP), 전이학습 방법론에 대한 끊임없는 탐구의 일환으로 [우진(Woojin Choi)](https://github.com/CHUH00)에 의해 개발되었습니다.*
