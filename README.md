# Lecture-Recommendation-NLP

연세대학교 강의계획서와 에브리타임의 강의평을 바탕으로 강의 추천 서비스 구현


## Install

1. 설치해야 하는 라이브러리
    - Selenium
    - konlpy
    - re
    - pickle
    - keras
    - sklearn
    - gensim
    - torch
    - tqdm
    - SentenceTransformer
    
2. 설치해야 하는 프로그램
    - Chromedriver : [https://chromedriver.chromium.org/downloads](https://chromedriver.chromium.org/downloads) 에서 다운로드
        
        (chrome://version/ 에서 버전 확인 후 다운로드)
        

## Crawling

연세대학교 에브리타임 사이트에서 강의평과 강의계획서 데이터를 크롤링해오는 코드입니다. ([https://everytime.kr/](https://everytime.kr/), ID 및 비밀번호 필요)

crawling_review.ipynb, crawling syllabus.ipynb는 각각 응용통계학과의 강의평들과 상경대학의 강의계획서들을 예시로 한 코드입니다.

Selenium과 Chromedriver를 설치해야만 크롤링이 가능합니다.

크롤러가 반복문을 수행할 때 시간이 다소 오래 걸릴 수 있습니다.

## 라벨링 자동화

labeling_w2v.ipynb 파일은 아래의 내용을 포함합니다.

- 개별 강의평 word2vec 학습
- 강의 특징 항목별 관련 단어 추출: word2vec에서 유사도 높은 top n 단어 내에서 명사 위주 선정
- 강의평별 관련 단어 유무 파악 후 관련성 표시(Y)
- 최종 라벨링: -1(관련 없음)/ 1(긍정적)/ 0(부정적)/ 0.5(애매)
    - reviews_label.csv : 최종 개별 강의평 라벨 데이터
    

## 1D CNN

1D_CNN.ipynb 파일은 아래의 내용을 포함합니다.

- 정수 인코딩 과정
- 1D CNN 모델링
- model을 통한 예측

프로젝트 진행 시에 사용한 정수인코딩된 데이터, tokenizer pickle, CNN 모델들은 1D CNN 폴더에 따로 업로드하였습니다.

## KoBERT

강의평 예측기 with KoBERT.ipynb 파일은 아래의 내용을 포함합니다.

- KoBERT 파일 불러오기
- 데이터 전처리 및 형태 변환
- 토큰화(순서 임베딩 등) 작업 및 학습 모델 설립
- Train & Test - 강의평 예측 봇

강의평 추천시스템 with KoBERT.ipynb 파일은 위 파일과 같은 맥락으로 흘러갑니다.

- 차이점 : 5개의 모델을 섞어서 결과값을 내야해 다섯 번의 Train/Test 작업이 일어남.

## Word2Vec/Doc2Vec + NN

Word2Vec/Doc2Vec + NN 파일은 아래의 내용을 포함합니다.

- preprocess_tokenize.ipynb : 강의평 데이터 토큰화
    - reviewtokenized.csv 생성
- preprocess_w2v.ipynb : 토큰화된 강의평 데이터를 사용하여 word2vec 모델 적용/각각의 강의평에 대해 word2vec 적용한 것과 동일 강의에 대한 강의평 합친 것에 word2vec 적용한 것
    - w2vnormver.csv/w2vaggver.csv
- preprocess_d2v.ipynb : 토큰화된 강의평 데이터를 사용하여 doc2vec 모델 적용
    - d2v.normver.csv
- NN.ipynb : 각각의 벡터화 시킨 데이터를 사용하여 Neural Network 사용하여 각각의 기준에 대한 예측값 예측하는 모델.

## **SentenceBERT**

SentenceBERT.ipynb 파일은 아래의 내용을 포함합니다.

- 강의계획서 데이터 불러오기
- 데이터 전처리 및 형태 변환
- 토큰화 및 Bag of Word
- CountVectorizer을 이용한 n-gram 추출
- SBERT로 문서와 가장 유사한 5개의 키워드 추출
- SBERT에 Max Sum Similarity를 적용하여 각 키워드들간의 유사도는 낮지만 문서와의 유사도는 높은 5개의 키워드 추출

## TF-IDF

TF-IDF.ipynb 파일은 아래의 내용을 포함합니다.

- 강의계획서 데이터 불러오기
- 데이터 전처리 및 형태 변환
- 토큰화 및 Bag of Word
- 각 강의개요에 포함되어있는 단어들의 TF-IDF 데이터프레임 생성
- 키워드를 입력하면 강의개요에 해당 키워드를 포함하는 강의들을 추출

## Reference

- 딥 러닝을 이용한 자연어처리 입문 : [https://wikidocs.net/book/2155](https://wikidocs.net/book/2155)
- Convolutional layers : Deras Documentation : [https://keras.io/ko/layers/convolutional/](https://keras.io/ko/layers/convolutional/)
