# 캐글 노트북 설정 가이드 (Kaggle Notebook Setup Guide)

## 필요한 파일들 (Required Files)

캐글 노트북을 실행하기 위해 다음 파일들을 캐글 데이터셋으로 업로드해야 합니다.

### 1. 모델 파일 (Model Files)

**다운로드:** Dryad에서 `t15_pretrained_rnn_baseline.zip` 다운로드
- 링크: https://datadryad.org/stash/dataset/doi:10.5061/dryad.dncjsxm85

**필요한 파일 구조:**
```
t15_pretrained_rnn_baseline/
├── checkpoint/
│   ├── args.yaml          # 모델 설정 파일 (필수)
│   └── best_checkpoint     # 모델 가중치 파일 (필수)
└── training_log            # (선택사항)
```

### 2. 데이터 파일 (Data Files)

**다운로드:** Dryad에서 `t15_copyTask_neuralData.zip` 다운로드

**필요한 파일:**
- `hdf5_data_final/` 디렉토리 전체 (세션별 HDF5 파일들 포함)
- `t15_copyTaskData_description.csv` (메타데이터 파일)

**파일 구조 예시:**
```
hdf5_data_final/
├── t15.2023.08.11/
│   └── data_train.hdf5
├── t15.2023.08.13/
│   ├── data_train.hdf5
│   ├── data_val.hdf5
│   └── data_test.hdf5
└── ... (다른 세션들)

t15_copyTaskData_description.csv
```

## 캐글에 업로드하는 방법

### 방법 1: 데이터셋으로 업로드 (권장)

1. **Dryad에서 파일 다운로드**
   - `t15_pretrained_rnn_baseline.zip` 다운로드 및 압축 해제
   - `t15_copyTask_neuralData.zip` 다운로드 및 압축 해제

2. **캐글 데이터셋 생성**
   - Kaggle 웹사이트에서 "Datasets" → "New Dataset" 클릭
   - 압축 해제한 파일들을 업로드
   - 데이터셋 이름 지정 (예: `brain-to-text-model-and-data`)

3. **노트북에 데이터셋 추가**
   - 노트북 편집 페이지에서 "Add Data" 버튼 클릭
   - 생성한 데이터셋 선택

### 방법 2: 노트북에 직접 업로드

1. 노트북 편집 페이지에서 "File" → "Upload" 클릭
2. 필요한 파일들을 직접 업로드

## 노트북 실행 전 확인사항

노트북의 **Cell 3 (Find and Setup Data/Model Paths)**를 실행하면:
- 자동으로 파일 경로를 찾아줍니다
- 파일이 없으면 명확한 에러 메시지를 표시합니다
- 사용 가능한 입력 디렉토리 목록을 보여줍니다

파일이 자동으로 찾아지지 않으면, **Cell 5 (Configuration)**에서 수동으로 경로를 설정할 수 있습니다:

```python
CONFIG['model_path'] = '/kaggle/input/your-dataset-name/t15_pretrained_rnn_baseline'
CONFIG['data_dir'] = '/kaggle/input/your-dataset-name/hdf5_data_final'
CONFIG['csv_path'] = '/kaggle/input/your-dataset-name/t15_copyTaskData_description.csv'
```

## 파일 크기 참고

- `t15_pretrained_rnn_baseline.zip`: 약 수백 MB
- `t15_copyTask_neuralData.zip`: 수 GB (전체 데이터셋)
- 캐글 노트북의 디스크 공간 제한을 고려하여 필요한 세션만 선택적으로 업로드할 수 있습니다

## 문제 해결

### 파일을 찾을 수 없다는 에러가 발생하는 경우:

1. **Cell 3 실행 결과 확인**
   - 어떤 파일이 없는지 확인
   - 사용 가능한 입력 디렉토리 목록 확인

2. **경로 수동 설정**
   - Cell 5에서 `CONFIG` 딕셔너리의 경로를 실제 데이터셋 경로로 수정

3. **데이터셋 구조 확인**
   - 캐글 데이터셋의 파일 구조가 위의 "필요한 파일 구조"와 일치하는지 확인

## 추가 정보

- Dryad 데이터셋: https://datadryad.org/stash/dataset/doi:10.5061/dryad.dncjsxm85
- 프로젝트 README: [README.md](README.md)
- 모델 훈련 가이드: [model_training/README.md](model_training/README.md)

