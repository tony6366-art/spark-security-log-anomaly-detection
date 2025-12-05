Big Data Processing + Cyber Security Fusion Project
(Korea University Information Security Graduate School Portfolio)
📘 프로젝트 개요 (Overview)
이 프로젝트는 Apache Spark를 기반으로 대규모 보안 로그(Security Logs)를 처리하고,
비지도 학습 기반(K-Means) 이상 탐지(Anomaly Detection) 기법을 활용하여
비정상적인 네트워크 트래픽 패턴을 탐지하는 시스템을 구현한 것입니다.
이 프로젝트는 다음 두 분야를 융합하는 것을 목표로 합니다:
빅데이터 프로세싱(Big Data Processing)
사이버 보안(Security Log Analytics)
실제 방화벽/웹 서버 로그 구조를 모방한 데이터셋을 생성한 뒤,
Spark ML 파이프라인으로 전처리 → 특징 추출 → 클러스터링 → 이상치 선별까지 전체 흐름을 구현했습니다.
🔍 주요 기능 (Key Features)
✔ 1. Synthetic Security Log Generator
실제 보안 로그 형태(src_ip, dst_ip, port, protocol, action, bytes, resp_code)를 기반으로
5,000건 이상의 로그 데이터를 자동 생성합니다.
✔ 2. Spark 기반 분산 전처리 파이프라인
카테고리 변수 인코딩 (StringIndexer + OneHotEncoder)
시간 파생 변수 생성 (hour, day_of_week)
수치 스케일링(StandardScaler)
VectorAssembler 기반 feature 벡터 구성
Spark ML Pipeline으로 일관적 처리
✔ 3. 비지도 학습 기반 이상 탐지
KMeans(k=10) 클러스터링
각 로그 → 클러스터 중심점 거리 계산
상위 1% distance = anomaly
(운영 환경에서 임계값을 조정해도 유연하게 적용 가능)
✔ 4. 모델 저장 및 재사용
/content/preprocess_model
/content/kmeans_model
Spark MLlib 포맷으로 저장되어 재사용 가능.
🧪 공격 시나리오(Anomaly Scenario) (선택/추가 시 더 고급 프로젝트가 됨)
본 프로젝트에는 다음과 같은 공격 패턴을 시뮬레이션하여 포함할 수 있습니다:
공격 유형	설명
Port Scanning	특정 IP가 매우 많은 포트로 지속적으로 연결 시도
Data Exfiltration	비정상적으로 큰 bytes 전송 발생
Web Attack Attempt	404, 500 등 오류 응답 코드가 짧은 시간 동안 집중 발생
KMeans 기반 anomaly ranking이 실제 공격 시나리오를 상위 순위에서 탐지한 것을 통해
모델의 유효성을 평가합니다.
🏗 프로젝트 구조 (Project Structure)
📁 Spark-Security-Anomaly-Detection
│
├── src/
│   ├── preprocess.py
│   ├── train_kmeans.py
│   └── detect_anomaly.py
│
├── data/
│   └── security_logs.csv
│
├── models/
│   ├── preprocess_model/
│   └── kmeans_model/
│
├── notebooks/
│   └── anomaly_detection_colab.ipynb
│
└── README.md
📊 결과 예시 (Detection Results)
✔ Distance 기반 이상치 탐지 결과 (Top 1%)
timestamp                  src_ip    action   bytes   cluster   distance
2025-01-05T13:34:12Z       10.0.0.8  DENY     48739       7      92.184
2025-01-05T13:33:12Z       10.0.0.8  DENY     49211       7      91.002
2025-01-05T13:32:12Z       10.0.0.8  TCP      50120       7      89.553
...
✔ 공격 시나리오 탐지율 예시
Top 100 anomalies 중 81개가 공격 시뮬레이션 IP
→ 비지도 학습 기반이라도 상당한 탐지율을 보였음을 시사
🧠 기술 스택 (Tech Stack)
Language: Python
Framework: Apache Spark (3.5.0)
ML: Spark MLlib (KMeans)
Data Handling: PySpark SQL, Pandas
Environment: Google Colab / Jupyter Notebook
🎯 본 프로젝트의 의의 (Why This Project Matters)
✔ 보안 도메인 + 빅데이터 기술 융합
대규모 보안 로그 분석은 실제 대기업/공공기관에서 매우 중요한 과제입니다.
Spark 기반 이상 탐지 모델은 라벨링되지 않은 방대한 보안 로그에서도
효율적으로 비정상 행위를 탐지할 수 있는 강력한 접근 방식입니다.
✔ 고려대 정보보호대학원 포트폴리오 적합성
공격 시나리오 기반 로그 구성
데이터 엔지니어링 + 머신러닝 + 보안 도메인 이해
실제 서비스 가능한 수준의 파이프라인 구성
이 세 요소가 잘 결합되어 있어, 지원 과정에서 강한 인상을 줄 수 있음.
🚀 향후 개선 방향 (Future Work)
Isolation Forest, LOF 등 다른 anomaly 모델 비교
Spark Streaming 기반 실시간 보안 로그 처리
CIC-IDS2017 / UNSW-NB15 같은 공개 데이터셋 적용
그래프 기반 공격 탐지(Graph Analytics)로 확장
📄 라이선스 (License)
MIT License
🙋‍♂️ Author
Chae Youho (채윤호)
AI Software & Big Data Processing
Contact: (optional)
GitHub: (your link here)
