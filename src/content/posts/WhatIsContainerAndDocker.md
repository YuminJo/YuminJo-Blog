---
title: "Container와 Docker란? / コンテナとDockerとは?"
published: 2024-09-26
tags: ["Computer Science", "Container", "Docker"]
category: "Computer Science"
draft: false
lang: ko
---

# Container와 Docker란? / コンテナとDockerとは?

---

## Container란? / コンテナとは?

<details>
<summary>Containerは、簡単に言うと、部屋にパソコン、キーボード、机があれば一つ一つ運ぶのではなく、すべて選択して引っ越すことです。</summary>

> **한글:** Container는 어플리케이션이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행되도록 코드와 모든 종속성을 패키징하는 소프트웨어의 표준 단위  
> **日本語:** Containerは、アプリケーションがあるコンピューティング環境から他のコンピューティング環境へ迅速かつ安定的に実行されるよう、コードとすべての従属性をパッケージングするソフトウェアの標準単位
</details>

:::note[주의 / 注意]
**한글:** Container는 OS를 공유합니다. OS 문제 발생 시 다른 애플리케이션에도 영향을 미칠 수 있습니다.  
**日本語:** ContainerはOSを共有します。OSに問題が生じると、他のアプリにも影響を及ぼします。
:::

---

## Docker란? / Dockerとは?

<details>
<summary>DockerはContainer配布に必要なほぼすべての機能を提供するプラットフォーム</summary>

> **한글:** Docker는 Container 배포에 필요한 거의 모든 기능을 제공하는 플랫폼으로, 이식성, 효율성, 유용성을 갖춤  
> **日本語:** DockerはContainer配布に必要なほぼすべての機能を提供するプラットフォームで、移植性、有用性、効率性を持っています
</details>

**Docker 흐름 / Dockerフロー**  
Docker File -> Docker Image -> 다양한 Container