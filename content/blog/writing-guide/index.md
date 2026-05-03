+++
title = "글쓰기 가이드 / Markdown 데모"
date = 2026-05-03
draft = true
description = "Tabi 테마에서 자주 쓰는 마크다운·front matter·shortcode 레퍼런스. 라이브에는 노출되지 않음(draft = true)."

[taxonomies]
tags = ["meta", "reference"]

[extra]
toc = true
+++

이 글은 `draft = true` 라서 빌드 시 제외됩니다. 본인이 새 글 쓸 때 복사해서 시작점으로 쓸 수 있도록 자주 쓰는 패턴을 모아둔 레퍼런스입니다.

## Front matter 표준 형태

```toml
+++
title = "글 제목"
date = 2026-05-03
description = "검색·소셜 카드용 요약 1~2 문장"

[taxonomies]
tags = ["zola", "한국어"]

[extra]
toc = true            # 목차 표시 여부
katex = false         # 수식 사용 시 true
+++
```

- `date`는 따옴표 없이 ISO 형식 (`YYYY-MM-DD`)
- 폴더 구조: `content/blog/슬러그/index.md` — 같은 폴더에 이미지 두면 상대경로로 참조 가능

## 헤딩

`##` 부터 사용 (제목은 자동으로 `<h1>` 처리됨).

## 코드 블록

언어 지정 시 syntax highlighting 적용:

```rust
fn main() {
    println!("Hello, 한국어");
}
```

```python
# 한국어 주석도 자연스럽게 보임
def 안녕(이름: str) -> str:
    return f"안녕하세요, {이름}님"
```

코드 블록 우측 상단의 **복사 버튼** 자동 활성화 (`copy_button = true`).

## 인라인 코드와 강조

본문 중에 `inline code` 박을 수 있고, **굵게**, *기울임*, ~~취소선~~ 모두 됩니다.

## 인용

> 인용문은 이렇게 — 한국어 줄바꿈도 자연스러움.
> 두 줄 이상도 가능.

## 리스트

- 첫 번째
- 두 번째
  - 중첩
  - 또 중첩

순서 있는 리스트:

1. 일
2. 이
3. 삼

## 표

| 항목 | 값 | 비고 |
|------|----|----|
| Zola | 0.22.1 | SSG |
| Tabi | latest | 테마 |
| Pretendard | jsDelivr | 한국어 폰트 |

## 링크 / 이미지

- 외부 링크: [Zola 공식 문서](https://www.getzola.org/documentation/getting-started/overview/)
- 같은 사이트 다른 글: [`@/blog/hello-world/index.md`](@/blog/hello-world/index.md) ← 이렇게 `@/` 로 시작하면 빌드 시 깨진 링크 검증됨
- 이미지: 글과 같은 폴더에 두고 상대경로
  ```markdown
  ![대체 텍스트](./screenshot.png)
  ```

## 각주

본문에 각주를 다는 방법[^1]. 각주는 글 하단에 자동 정렬됨.

[^1]: 이렇게 각주 본문을 작성. Tabi의 `bottom_footnotes = true` 설정으로 화면 아래 모음.

## 수식 (KaTeX)

front matter에 `katex = true` 추가 후:

```
$$
e^{i\pi} + 1 = 0
$$
```

## 콜아웃 / 정보 박스

Tabi가 제공하는 shortcode 활용:

```markdown
{%/* note() */%}
참고할 만한 정보
{%/* end */%}
```

## 작성 → 배포 흐름

1. 새 글 폴더 만들고 `index.md` 작성
2. 로컬 미리보기: `zola serve` (자동 리로드)
3. 빌드 검증: `zola build`
4. 배포 (현재는 수동):
   ```bash
   wrangler pages deploy public --project-name wonjin --branch main
   ```
   → 자동 배포 워크플로우 활성화하면 `git push` 만으로 OK

## 글을 라이브로 올릴 때 체크

- [ ] `draft = true` 가 없는지
- [ ] `date` 가 정확한지
- [ ] `description` 이 1~2 문장으로 들어가 있는지 (소셜 카드/검색용)
- [ ] `tags` 가 일관되게 (소문자, 한국어 OK, 너무 세분화하지 않기)
- [ ] 코드 블록 언어 지정 (`rust`, `python`, `bash` 등)
- [ ] 외부 링크는 새 탭에서 안 열려도 OK (Tabi 기본값)
