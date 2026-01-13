---
title: "Unity API 자동 문서화 / Unity API 自動ドキュメント化"
published: 2025-09-11
tags: ["Unity", "DocFX", "GitHub Actions", "Documentation"]
category: "Development"
draft: false
lang: ko
---

# DocFX와 GitHub Actions를 활용한 Unity API 자동화 / DocFXとGitHub Actionsを活用したUnity API自動化

이번 프로젝트에서는 **DocFX**와 **GitHub Actions**를 활용하여 Unity 코드에서 자동으로 API 문서를 생성하는 환경을 구축했습니다.  
今回のプロジェクトでは、**DocFX** と **GitHub Actions** を活用して Unity のコードから自動的に API ドキュメントを生成する仕組みを導入しました。  

[DocFX 공식 사이트 / 公式サイト](https://dotnet.github.io/docfx/)

---

## DocFX

- C# 주석 및 XML 문서에서 API 레퍼런스 생성  
- Markdown 형식의 기술 문서도 통합 가능  

C# コメントや XML ドキュメントから API リファレンスを生成  
Markdown 形式の技術ドキュメントも統合可能  

---

## GitHub Actions

- 레포지토리에 푸시될 때마다 자동 빌드  
- 항상 최신 문서를 공개 상태로 유지  

リポジトリにプッシュするたびに自動ビルド  
常に最新のドキュメントを公開状態に  

---

## 장점 / メリット

- 수동 업데이트 불필요  
- 구현과 명세의 차이 감소  
- 팀 내에서 명세 확인이 원활  

手作業での更新が不要  
仕様と実装の差分が減少  
チーム内での仕様確認がスムーズ  

---

짧은 도입이지만, 개발 효율이 크게 개선되었습니다.  
今後はさらに 운영 흐름을 확장할 예정입니다.
短い導入でしたが、開発効率が大きく改善されました。  
今後はさらに運用フローを拡張していく予定です。

![](https://velog.velcdn.com/images/doyaguri/post/79bfb09f-39d4-40d5-a87b-85fac9ca02f5/image.png)  
![](https://velog.velcdn.com/images/doyaguri/post/3f599458-716b-4d2e-b381-495395c1664b/image.png)
