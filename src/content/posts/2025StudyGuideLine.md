---
title: "최근 학습 내용 및 개발 가이드라인 / 最近学んだことと開発ガイドライン"
published: 2025-05-29
tags: ["Development", "PR", "QA", "Random"]
category: "Work Guidelines"
draft: false
lang: ja
---
## PR 관련 가이드라인 / PRに関するガイドライン

### PR은 가능한 한 작게 분할 / PRはできるだけ細かく短く分割すること
- 작은 단위의 변경으로 PR 작성 → 리뷰가 용이  
- 小さな変更単位でPRを作成し、レビューしやすくする。

### PR 제목과 내용 명확히 작성 / PRの内容とタイトルは明確にすること
- 제목과 설명에서 "무엇을, 왜" 했는지 즉시 파악 가능하도록 작성  
- タイトルと説明で「何を・なぜ」行ったのかがすぐに分かるように記述する。

### 리팩토링과 기능 추가는 분리 / リファクタリングと機能追加は別々にPRを作成すること
- 기능 추가 시 "어떤 기능", "어디에 적용" 등 명확히 구분  
- 特に機能追加の場合は「どんな機能か」「どこに適用したか」などを分かりやすく分離する。

---

## 업무 보고 작성 가이드 / 業務報告の書き方ガイドライン

### 보고 항목별로 제목 분리 / 報告項目ごとに見出しを分けること
- 어떤 작업인지 한눈에 파악 가능  
- 何に関する作業なのかが一目で分かるようにする。

### 작업 내용 간결하게 기록 / 対応内容を簡潔に記載すること
- 수행한 작업과 변경 사항 명확히 작성  
- なにをやったのか、どんな変更を加えたのかを明確に。

### 관련 URL 첨부 필수 / 関連URL（PR、チケット、資料など）を必ず添付すること
- 리뷰 및 확인 용이  
- レビューや確認がしやすくなる。

### 가능하면 작업 배경/목적 기록 / 可能であれば、作業の背景や目的も簡単に記載すること
- 왜 작업했는지 기록 → 전체 이해 용이  
- なぜその作業をしたのかが分かると、全体の把握がスムーズ。

---

## 머지(Merge) 규칙 / マージルール

### "Squash and Merge" 사용 금지 / 「Squash and Merge」は使用しないこと
- 커밋 기록이 1개로 합쳐져서 추적 어려움  
- 履歴が1コミットにまとまってしまい、誰が・いつ・何をしたか追いづらくなる。

- 여러 명 리뷰, 디버깅 어려움 → **Create a merge commit / Rebase and merge 권장**  
- また、複数人でのレビューやデバッグが困難になるため、**通常の「Create a merge commit」または「Rebase and merge」**を推奨。

### 최신 main/develop 반영 후 머지 / マージ前に必ず最新のmain / developを取り込んでリベースまたはマージすること
- 충돌 방지, CI 실패 예방  
- コンフリクト防止・CI落ちの回避。

---

## 브랜치 명명 기본 원칙 / 命名時の基本方針

### 브랜치명은 용도/목적에 맞게 구분 / ブランチ名は用途・目的に応じて分類し、わかりやすくすること
- 기능별로 구분, 앞으로는 **feature, fix, refactor 등 접두사 사용 권장**  
- 現在は機能ごとに分かれているが、今後は以下のように**feature, fix, refactorなどのプレフィックスを付けて明確に区分**すること。

---

## 난수 생성 방법 / 乱数作成方法

```csharp
using UnityEngine;

public class RandomExample : MonoBehaviour
{
    void Start()
    {
        // 0 이상 10 미만의 랜덤 정수
        int randInt = Random.Range(0, 10); 
        Debug.Log("Random Int: " + randInt);

        // 0.0 이상 1.0 미만의 랜덤 실수
        float randFloat = Random.value;
        Debug.Log("Random Float: " + randFloat);

        // 배열에서 랜덤 선택
        string[] items = {"apple", "banana", "cherry"};
        string randItem = items[Random.Range(0, items.Length)];
        Debug.Log("Random Item: " + randItem);
    }
}
```

- Unity에서 Random.Range, Random.value 등을 활용해 정수/실수/배열 등에서 난수 생성 가능  
- Unityでは Random.Range, Random.value を使って整数・実数・配列から乱数生成可能
