# ADHD 검증 웹

## 📌 프로젝트 목적
본 프로젝트는 설문 데이터, CAT(인지 과제) 테스트, 웹캠 행동 분석 데이터를 결합하여
사용자의 ADHD 가능성을 예측하는 AI 시스템을 구현하는 것을 목표로 함.

기존의 단일 설문 기반 판단 방식에서 벗어나,
👉 객관적인 행동·인지 지표를 함께 활용한 다중 모달 ADHD 예측을 지향함.

## 🧠 사용 기술
Python
scikit-learn
pandas / numpy
MediaPipe (웹캠 행동 분석)
FastAPI (백엔드 API)
pickle / joblib (모델 직렬화)

## 구현내용

1️⃣ 개별 모델 학습
CAT 테스트 데이터로 CAT 모델 학습
설문 데이터로 설문 모델 학습
각 모델은 predict_proba() 형태로 ADHD 확률 출력
2️⃣ 웹캠 행동 데이터 처리
실시간 얼굴 랜드마크 추적
Head Pose(Yaw, Pitch, Roll) 계산
고개 돌림 / 자리 이탈 / 유효 프레임 비율을 CSV로 저장
세션 단위 요약 피처 생성
3️⃣ Synthetic Fusion Dataset 생성
기존 CAT 데이터 통계를 기반으로 가상 사용자 500명 생성
각 사용자에 대해:
27개 CAT 피처 생성
CAT 모델 → p_cat 계산
설문 모델 또는 통계 기반 → p_survey 생성
최종적으로 fusion_dataset.csv 구성
4️⃣ 최종 Late Fusion 모델 학습
입력: p_cat, p_survey, 주요 CAT 피처
출력: ADHD 최종 확률
실제 서비스 환경에서 바로 사용 가능한 구조로 설계

## 실행화면
<img width="1930" height="1478" alt="image" src="https://github.com/user-attachments/assets/76ebcef1-4040-45fd-9f42-8eb005af6024" />


## ✍ 느낀 점

이 프로젝트를 통해
단일 모델이 아닌 다중 모델을 결합하는 Late Fusion 구조의 중요성을 이해하게 되었음
단순 설문이 아닌 행동·인지 데이터의 정량화가 ADHD 예측 정확도를 높일 수 있음을 확인함
실제 서비스에 적용 가능한 AI 시스템은
👉 모델 성능뿐만 아니라 데이터 흐름과 구조 설계가 핵심이라는 점을 배움
