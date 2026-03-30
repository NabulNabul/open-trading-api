# open-trading-api 코드 분석 보고서

- 분석 대상: `open-trading-api`
- 기준 브랜치/커밋: `main` / `96408b2`
- 분석일: 2026-03-02

## 1) 한줄 요약

`open-trading-api`는 **한국투자 OpenAPI Python 샘플 코드 저장소**이며, 현재 구조는
1) LLM 친화 단일 기능 샘플(`examples_llm`),
2) 사용자 통합 예제(`examples_user`),
3) MCP 서버(`MCP/Kis Trading MCP`)의 3축으로 구성됩니다.

## 2) 정량 현황

- `examples_llm` Python 파일: **669개**
- `examples_user` Python 파일: **31개**
- MCP `tools` Python 파일: **10개**
- MCP `configs/*.json`: **8개**
- MCP API 엔트리(`github_url` 기준): **166개**

## 3) 폴더/역할 구조

### 루트
- `README.md`: 저장소 목적, 설치/실행 가이드
- `kis_devlp.yaml`: 사용자 인증/계좌 기본 템플릿
- `pyproject.toml`, `requirements.txt`: Python 의존성
- `docs/convention.md`: 네이밍/코딩/주석 컨벤션
- `legacy/`: 구 샘플 코드 보관

### `examples_llm`
- 목적: API 1기능 1폴더 구조로 LLM 탐색/호출 용이성 극대화
- 공통: `kis_auth.py`
- 패턴: `<api_name>.py` + `chk_<api_name>.py`

### `examples_user`
- 목적: 카테고리별 통합 함수 + 실행 예제 제공
- 공통: `kis_auth.py`
- 패턴: `<category>_functions.py`, `<category>_examples.py`, `*_ws.py`

### `MCP/Kis Trading MCP`
- FastMCP 기반 서버 (`server.py`)
- `tools/*.py`: 카테고리별 MCP 도구 래퍼
- `configs/*.json`: API 메타정보(파라미터, github_url, 설명)
- `module/plugin/*`: 환경설정, 마스터파일 업데이트, DB 관리

## 4) 핵심 코드 흐름

## 4.1 인증/공통 호출 (`examples_llm/kis_auth.py`, `examples_user/kis_auth.py`)
- 설정 파일: `~/KIS/config/kis_devlp.yaml`
- 토큰 파일: `~/KIS/config/KISYYYYMMDD`
- `auth()`:
  - 저장 토큰 유효 시 재사용
  - 만료 시 `/oauth2/tokenP` 재발급
- 실전/모의 전환: `svr="prod" | "vps"`, `product` 코드
- 공통 요청 헤더/호출/응답 래퍼 제공

## 4.2 REST 예제 함수 구조 (`examples_user/*_functions.py`)
- 함수 단위로 API URL/TR ID/파라미터 검증/호출/결과 가공 수행
- 다건 조회는 `tr_cont` 재귀 패턴으로 연속조회
- 결과는 주로 `pandas.DataFrame` 변환

## 4.3 WebSocket 예제 (`*_functions_ws.py`)
- `tr_id`, `tr_key`, `tr_type(등록/해제)` 기반 구독
- 반환: 메시지 + 컬럼 정의
- 실시간 필드명 매핑이 함수 내부에 명시됨

## 4.4 MCP 실행 흐름 (중요)
- `server.py`에서 도구 등록 후 `stdio/sse/streamable-http` 모드 실행
- `tools/base.py`의 `ApiExecutor`가 다음 순서로 동작:
  1. 임시 디렉토리 생성
  2. GitHub raw에서 `kis_auth.py` 다운로드
  3. 선택 API 코드 다운로드
  4. 코드 내부 파라미터 자동 주입/수정
  5. `.venv/bin/python` 서브프로세스로 실행
  6. 결과를 MCP 응답으로 변환

즉 MCP는 **로컬 고정 라이브러리 호출 방식**이 아니라,
**GitHub 소스를 런타임에 받아 실행하는 동적 실행 구조**입니다.

## 5) 장점

- API 범위가 매우 넓음(국내/해외/선물옵션/채권/ETF/ELW)
- 함수/폴더 네이밍 규칙이 비교적 일관됨
- LLM 용/사용자 용 샘플을 분리해 학습/실행 목적이 명확함
- MCP에서 `find_stock_code`, `find_api_detail` 같은 보조 기능 제공
- 마스터파일 관리 + DB 검색 체계가 있어 종목코드 자동화에 유리

## 6) 확인된 리스크/주의점

## 6.1 문서-실코드 불일치 가능성
- README에는 Python 3.9+ 안내가 있으나, `pyproject.toml`은 `>=3.13`
- README 경로 예시의 일부(`cd open-trading-api/kis_github`)는 현재 구조와 불일치

## 6.2 유지보수 관점
- `examples_user/domestic_stock/domestic_stock_functions.py`가 매우 대형(1파일 집중)
- `kis_auth.py`가 `examples_llm`/`examples_user`에 중복 유지

## 6.3 보안/운영 관점 (MCP)
- 런타임 GitHub 다운로드 후 코드 실행 구조는 공급망/재현성 리스크가 존재
- 운영 환경에서 고정 버전 핀/해시 검증/내부 미러링이 권장됨

## 7) 현재 KisAITrading 프로젝트와의 연계 관점

현재 프로젝트는 C# `KisClient` 중심 직접 연동 전략이므로,
`open-trading-api`는 **런타임 의존성**보다 **레퍼런스/검증 자산**으로 활용하는 것이 적합합니다.

추천 활용 방식:
- TR ID/엔드포인트/필수 파라미터의 참조 사전
- 신규 API 추가 시 Python 샘플로 선검증 후 C# 이식
- 오류코드/파라미터 검증 규칙 보강
- MCP의 `configs/*.json`를 API 메타데이터 원천으로 활용

## 8) 실무 적용 제안 (우선순위)

1. **API 카탈로그 자동 추출**
   - `MCP/Kis Trading MCP/configs/*.json`에서 `api_path`, `method`, `params`를 추출해 C# 대응표 생성

2. **C# 커버리지 갭 분석**
   - `KisClient` 현재 구현 API vs `open-trading-api` API 목록 비교
   - 상품군별(국내주식/해외주식/파생) 누락 목록 작성

3. **정책 가드 강화**
   - 이미 반영된 Primary-Only 주문 정책과 연동하여
   - API별 주문/조회 구분 메타데이터를 관리해 사전 차단 룰 강화

4. **문서 정합성 개선**
   - 내부 운영 문서에 Python 요구버전/실행 경로/설정경로를 실제 코드 기준으로 명시

## 9) 결론

`open-trading-api`는 단순 샘플을 넘어 **광범위한 API 인덱스 + 실행 레퍼런스**로 가치가 큽니다.
다만 현재 프로젝트 전략(직접 C# 연동) 기준에서는 이를 서비스 런타임에 직접 결합하기보다,
**명세 검증/기능 확장 가속용 기준 저장소**로 두는 것이 가장 안전하고 효율적입니다.