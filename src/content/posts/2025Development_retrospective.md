---
title: "개발 회고: 설계, 책임 분리, 네이밍, PR 소통 / 開発振り返り：設計、責任分離、命名、PRコミュニケーション"
published: 2025-08-19
tags: ["Development", "Design", "Code Review", "Naming"]
category: "Work Reflection"
draft: false
lang: ja
---

## 설계 / 設計
---

최근 개발하면서 느낀 점: 전체적으로 설계를 잘못하고 있었다는 사실을 깨달았습니다.
最近の開発で気づいたこと：全体的に設計が正しくなかった。

```csharp
public class GameData {
    public Dictionary<Tutorials, bool> TutorialStates { get; private set; } = new();
    public int CoinAmount { get; private set; }
    public int CashAmount { get; set; }
    public ItemData[] ShelfIngredients { get; } = new ItemData[9];
    public RecipesData[] CurrentPlayerFoods { get; } = new RecipesData[3];
    public Dictionary<string, RecipesData> KnownRecipes { get; } = new();
    public Dictionary<string, ItemData> KnownIngredients { get; } = new();
    public Dictionary<ItemData, int> IngredientStock { get; } = new();
}
```

- `GameData` 클래스는 데이터의 성격이 불명확하고 책임이 너무 많음  
- `GameData` クラスはデータの性質が不明瞭で、責任が多すぎる。

문제점 / 問題点:
- 마스터 데이터인지, 유저 데이터인지 구분 불가  
- 다른 스크립트에서 쉽게 접근/수정 가능 → 의존성 증가  
- Manager 안에 포함되어 있어 구조가 복잡  
- マスターデータかユーザーデータか不明  
- 他のスクリプトから簡単にアクセス可能 → 依存性が増加  
- Managerに含まれており、構造が複雑

---

## 책임의 분리 / 責任の分離
---

하나의 클래스가 너무 많은 일을 하면 SRP(Single Responsibility Principle) 위반  
一つのクラスがあまりにも多くの役割を持つと、SRP（単一責任の原則）違反になる。

### GameData 문제점 / GameDataの問題
- 튜토리얼 상태 / チュートリアル状態
- 재화 관리 / 通貨管理
- 아이템 재고 / アイテム在庫
- 레시피 정보 / レシピ情報
- 플레이어 상태 / プレイヤー状態

### 개선 방안 / 改善案
각 데이터 책임 분리:
- PlayerCurrency : 코인/캐시 / 通貨情報
- PlayerInventory : 아이템, 재고 / アイテム、在庫
- PlayerProgress : 튜토리얼/퀘스트 / チュートリアル、クエスト
- RecipeBook : 레시피 해금 / レシピ一覧と解放状態

독립 데이터 컨테이너로 두고 필요한 객체만 참조  
独立したデータコンテナとして保持し、必要なオブジェクトのみ参照する。

---

## 네이밍의 중요성 / 命名の重要性
---

네이밍 = 역할과 책임을 명확히 전달하는 계약  
命名 = クラスや変数、メソッドの役割と責任を明確に伝える契約

### 문제 / 問題
- `GameData` : 어떤 데이터인지 알 수 없음  
- 플레이어인지, 시스템 데이터인지, 캐싱인지 불명  
- `GameData`：何のデータか分からない  
- プレイヤーか、システムか、一時キャッシュか不明

### 개선 네이밍 / 改善ネーミング
- PlayerData : 플레이어 상태 / プレイヤー状態
- InventoryData : 인벤토리 / インベントリ
- RecipeData : 레시피 / レシピ
- CurrencyData : 재화 / 通貨

---

## PR에서의 소통과 설명 / PRでのコミュニケーション
---

코드 리뷰 = 설계 의도와 구현 이유 공유  
コードレビュー = 設計意図と実装理由の共有

### 문제 / 問題
- PR에 코드만 업로드, 설명 없음  
- 리뷰어가 의도를 이해하려고 추측해야 함  
- PRにコードだけアップロード、説明なし  
- レビュアーが意図を推測する必要がある

### 개선 방안 / 改善案
1. **PR 제목** : 변경 내용 명확 / 変更内容を明確に
2. **PR 설명** : 변경 이유, 설계 의도, 고려 대안, 영향 범위 기록  
   / 変更理由、設計意図、考慮した代替案、影響範囲を記録
3. **코드 단위 PR** : 관련 없는 변경 분리  
   / 関連のない変更はPRで分離

---

## 결론 / 結論
- 좋은 설계 + 책임 분리 + PR 설명 = 협업 기본  
- 데이터와 로직 혼합 금지, 명확한 네이밍, 싱글톤 신중 사용  
- 優れた設計 + 責任分離 + PR説明 = 協働の基本  
- データとロジックを混ぜない、明確な命名、シングルトンは慎重に使用
