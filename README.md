# Pull-Request Labeler

## Input
- `repo-token` : 레포지토리 접근을 위한 github token 입니다.
- `config-pathname`: 설정 파일이 위치한 경로입니다. 해당 경로에 위치한 yml파일을 읽어 규칙에 맞게 라벨러를 생성합니다.

## config file 작성 방법 
```yml
# 아래 base 또는 head 브랜치에 맞는 PR이 생성했을 때 붙는 라벨러의 이름입니다.
enhancement:
  # 생성된 PR의 base 브랜치 입니다. 
  base: ["feature/*"]
  # 생성된 PR의 head 브랜치 입니다.
  head: ["enhance/*", "enhancement/*"]
```

## github action file example (for use)
- you only need `github secret token`

```yml
name: PR Branch Labeler

on: pull_request

jobs:
  label_prs:
    runs-on: ubuntu-latest
    steps:
      - name: Label PRs
        uses: creatrip/pr-labeler@v1
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
          config-pathname: .github/pr-labeler-config.yml

```

## config file example
- config file must be placed at `.github/pr-labeler-config.yml`

```yml
## .github/pr-labeler-config.yml
develop:
  base: ["develop/*", "develop*", "develop"]
release:
  base: ["main"]
feature:
  head: ["feature/*", "feat/*"]
fix:
  head: ["bugfix/*", "fix/*"]
hotfix:
  head: "hotfix/*"
enhancement:
  base: ["feature/*"]
  head: ["enhance/*", "enhancement/*"]
```
