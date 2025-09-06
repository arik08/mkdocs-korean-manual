# API 문서

## 개요

이 섹션에서는 프로젝트의 API 문서를 제공합니다.

## 주요 함수

### `get_data()`

데이터를 가져오는 함수입니다.

**매개변수:**
- `source` (str): 데이터 소스의 경로
- `format` (str, optional): 데이터 형식 (기본값: 'json')

**반환값:**
- `dict`: 가져온 데이터

**예시:**
```python
data = get_data('data.json', format='json')
print(data)
```

### `process_data(data)`

데이터를 처리하는 함수입니다.

**매개변수:**
- `data` (dict): 처리할 데이터

**반환값:**
- `dict`: 처리된 데이터

**예시:**
```python
processed = process_data(raw_data)
```

### `save_data(data, filename)`

데이터를 파일로 저장하는 함수입니다.

**매개변수:**
- `data` (dict): 저장할 데이터
- `filename` (str): 저장할 파일명

**반환값:**
- `bool`: 저장 성공 여부

**예시:**
```python
success = save_data(data, 'output.json')
if success:
    print("저장 완료!")
```

## 오류 코드

| 코드 | 설명 | 해결 방법 |
|------|------|-----------|
| 100 | 데이터 없음 | 올바른 데이터 소스 확인 |
| 200 | 형식 오류 | 지원되는 형식 사용 |
| 300 | 저장 실패 | 파일 권한 확인 |

!!! danger "중요"
    API를 사용하기 전에 반드시 인증이 필요합니다.

## 응답 예시

### 성공적인 응답

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "name": "Example",
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

### 오류 응답

```json
{
  "status": "error",
  "message": "데이터를 찾을 수 없습니다",
  "error_code": 100
}
```