# bakery-manual-book

베이커리 4개 매장 신입 직원용 매뉴얼북 웹사이트입니다.

## 배포 및 데이터 저장 구조

`index.html`은 기존 [bonnoel-manager-logbook](../bonnoel-manager-logbook) 로그북과 **같은 Supabase 계정**을 사용합니다(같은 프로젝트에 매뉴얼북 전용 테이블만 새로 추가). 어떤 기기·브라우저로 접속해도 같은 매뉴얼/확인 기록을 보고 저장할 수 있습니다.

- **데이터베이스**: Supabase 프로젝트(`caetlljnyxsusswqhtci`)의 `manual_categories`, `manuals`, `manual_staff`, `manual_confirmations` 테이블
- **사진 저장**: Supabase Storage `manual-photos` 버킷 (public)
- `index.html`에 박혀 있는 Supabase URL과 `anon`/`publishable` 키는 공개되어도 안전한 값입니다(Row Level Security 정책으로 접근을 제어). **`service_role` 키는 절대 이 파일에 넣지 마세요.**

## 처음 한 번만 하면 되는 준비 작업

1. https://supabase.com 대시보드 접속 → 로그북과 같은 프로젝트 선택
2. 왼쪽 메뉴 **SQL Editor** → New query → 이 저장소의 [`supabase-setup.sql`](./supabase-setup.sql) 내용을 전체 복사해서 붙여넣고 **Run**
3. 왼쪽 메뉴 **Storage** → New bucket → 이름 `manual-photos` → **Public bucket 켜기** → Create
4. 다시 SQL Editor로 돌아가서 `supabase-setup.sql` 맨 아래쪽 "Storage 버킷 설정" 부분(anon upload/delete 정책)을 실행 (1번에서 전체를 한 번에 실행했다면 이미 끝난 상태)

## 관리자 비밀번호

`index.html` 안의 `ADMIN_PIN` 값(기본값 `2024`)을 원하는 비밀번호로 바꿔서 사용하세요. 메모장으로 파일을 열어 `var ADMIN_PIN = '2024';` 줄만 수정하면 됩니다.

## 파일 구성

- `index.html` — 매뉴얼북 전체 (HTML + CSS + JS 단일 파일)
- `supabase-setup.sql` — Supabase 테이블/보안 정책 설정 스크립트 (최초 1회 실행)

## 배포 방법 (로그북과 동일)

1. 이 폴더를 GitHub 저장소로 push
2. https://vercel.com 에서 이 저장소를 Import → 배포
3. 이후 `main` 브랜치에 push할 때마다 Vercel이 자동으로 재배포합니다
