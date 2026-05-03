# wonjin.xyz

[Zola](https://www.getzola.org) + [Tabi](https://github.com/welpo/tabi) 로 만든 개인 블로그.
주 호스팅은 **Cloudflare Pages**, GitHub Pages 폴백 워크플로우는 비활성 상태로 보관.

## 로컬 개발

```bash
zola serve              # http://127.0.0.1:1111
zola build              # public/ 에 정적 파일 생성
```

테마 업데이트:

```bash
git submodule update --remote --merge themes/tabi
```

## 배포

### Cloudflare Pages (기본)

- 빌드 명령: `zola build`
- 출력 디렉터리: `public`
- 환경 변수: `ZOLA_VERSION = 0.22.1`
- 사용자 도메인: `wonjin.xyz` (Cloudflare 대시보드 → Pages → Custom domains)

### GitHub Pages (폴백)

`.github/workflows/gh-pages.yml` 에 정의됨. 평소 비활성. 활성화 절차는 파일 상단 주석 참조.

### 자동 배포 (선택 사항)

`.github/workflows/cloudflare-pages.yml` 가 staged 상태로 들어있음. CF API 토큰 발급 + GitHub secret 등록 후 `on: push:` 주석 해제하면 main 푸시 시 자동 배포됨. 상세 절차는 워크플로우 파일 상단 주석 참조.

## 글 작성 참고

`content/blog/writing-guide/` 에 마크다운/front matter/shortcode 레퍼런스가 `draft = true` 로 들어있음. 새 글 시작 시 복사해서 사용 가능.

## 외부 서비스 설정 체크리스트

`zola.toml` 의 placeholder 들을 채워야 활성화되는 항목:

- [ ] **GoatCounter** (`[extra.analytics].id`) — https://www.goatcounter.com 가입 후 코드 입력
- [ ] **Giscus 댓글** (`[extra.giscus].repo_id`, `category_id`) — 절차:
  1. 저장소 Settings → General → Features → **Discussions 활성화**
  2. https://github.com/apps/giscus 설치 (이 저장소에 권한 부여)
  3. https://giscus.app 에서 repo·category 선택 후 ID들 복사
  4. `enabled_for_all_posts = true` 로 변경
- [ ] **DNS**: 도메인 등록처에서 `wonjin.xyz` 를 Cloudflare Pages 로 연결

## 메모

- 한국어 본문에는 [Pretendard](https://github.com/orioncactus/pretendard) 폰트 적용 (jsDelivr CDN, `static/custom.css`)
- CSP 활성화 상태 (`enable_csp = true`); 외부 서비스 추가 시 `allowed_domains` 도 업데이트할 것
- 검색 기능은 한국어 토크나이징 한계로 비활성 (`build_search_index = false`)
