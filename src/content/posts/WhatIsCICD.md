---
title: "CI/CD란? / CI/CDは?"
published: 2024-09-27
tags: ["Computer Science", "CI/CD", "DevOps"]
category: "Computer Science"
draft: false
lang: ko
---

# CI/CD란? / CI/CDは?

<details>
<summary>アプリケーション開発段階から配布までのすべての段階を自動化を通じて、より効率的かつ迅速にユーザーに配布できること</summary>

> **한글:** 애플리케이션 개발 단계부터 배포까지 모든 과정을 자동화하여, 보다 효율적이고 빠르게 사용자에게 배포할 수 있는 방법  
> **日本語:** アプリケーション開発段階から配布までのすべての段階を自動化を通じて、より効率的かつ迅速にユーザーに配布できること
</details>

---

## Continuous Integration란? / 継続的インテグレーションとは?

:::tip[설명 / 説明]
**한글:** 코드를 빌드(Build), 테스트(Test), 병합(Merge) 하는 과정  
**日本語:** コードをビルド(Build)、テスト(Test)、マージ(Merge)するプロセス
:::

**흐름 / フロー**
Build -> Test -> Merge

yaml
코드 복사

- Build: Webpack 사용  
- Test: Mocha 같은 대표적인 테스트 도구  
- Merge: Git을 사용하여 충돌 최소화

---

## Continuous Delivery란? / 継続的デリバリーとは?

:::tip[설명 / 説明]
**한글:** 자동으로 레포지토리에 릴리스하는 과정  
**日本語:** 自動でリポジトリにリリースするプロセス
:::

**흐름 / フロー**
자동 빌드 후 Repository에 릴리스

yaml
코드 복사

---

## Continuous Deployment란? / 継続的デプロイメントとは?

:::tip[설명 / 説明]
**한글:** 릴리스를 실제 프로덕션 환경, 즉 사용자 서비스에 배포하는 과정  
**日本語:** リリースを実際のプロダクション環境、つまりユーザーサービスにデプロイするプロセス
:::

**흐름 / フロー**
자동 빌드 & 테스트 -> Production에 배포

diff
코드 복사

- 배포 범위: 사용자, QA 엔지니어, 관리자 페이지, 데이터 웨어하우스, 백엔드 개발자 등  
- Tools: GitHub Actions, Jenkins, CircleCI, Heroku 등