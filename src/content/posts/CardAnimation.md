---
title: "Card Animation 담당 / カードアニメーション担当"
published: 2025-01-27
tags: ["Unity", "DOTween", "Card Animation"]
category: "Unity Development"
draft: false
lang: ko
---

# 카드 애니메이션 담당 / カードアニメーション担当

![](https://velog.velcdn.com/images/doyaguri/post/4a2f3d53-9b70-48f7-bbfd-b99cd2eeeed3/image.gif)

최근 여러 프로젝트에 참여 중인데, "몸이 4개였으면 좋겠다~" 라고 생각함  
最近、いくつかのプロジェクトに参加していて、「体が4つあったらなぁ～」と思うことがあります

그럼 모든 일을 자신에게 맡길 수 있음  
そうすれば、全部自分で任せられるのに！

---

2025년 1월 24일부터 담당하고 있는 게임에 관한 설명  
2025年1月24日から担当しているゲームについて説明します

- 처음 카드: HearthStone 카드 배분 시스템 참고 (고라니님)  
- 最初のカード：HearthStoneのカード配布システムを参考にしました（ゴラニ氏）

- 이후 카드: Slay the Spire 카드 선택 시 다른 카드들이 밀려나는 점 참고  
- その後のカード：Slay the Spireでカード選択時に他のカードが少し押し出される仕組みを参考にしました

- 수정할 부분은 있지만, 대체로 만족스러운 애니메이션 완성  
- まだ修正する部分はありますが、全体的には満足のいくアニメーションが完成

- 현재 프로젝트에서는 못 써본 기능들을 배우며 적용 예정  
- 現在担当しているプロジェクトでは、自分がまだ使ったことのない機能を学びながら適用予定

- 한정된 기간 내에 효율적인 방안 고민 필요  
- 限られた期間内で効率的な方法を考える必要あり

---

## Sample Code / サンプルコード

```
for (int i = 0; i < objCount; i++) {
    var targetPos = Vector3.Lerp(leftTr.position, rightTr.position, objLerps[i]);
    var targetRot = Utils.QI;
    if (objCount >= 4) {
        float curve = Mathf.Sqrt(Mathf.Pow(height, 2) - Mathf.Pow(objLerps[i] - 0.5f, 2));
        curve = height >= 0 ? curve : -curve;
        targetPos.y += curve;
        targetRot = Quaternion.Slerp(leftTr.rotation, rightTr.rotation, objLerps[i]);
    }

    results.Add(new PRS(targetPos, targetRot, scale));
}
```

```
void EnlargeCard(bool isEnlarge, CardView card) {
    DOTween.Kill(card.transform);
    if (isEnlarge) {
        Vector3 enlargePos = new Vector3(card.originPRS.pos.x, -4.8f, -10f);
        card.MoveTransform(new PRS(enlargePos, Utils.QI, Vector3.one * 2.5f), true, 0.5f);
        AdjustOtherCards(card, true);
    } else {
        card.MoveTransform(card.originPRS, true, 0.3f);
        AdjustOtherCards(card, false);
    }

    card.GetComponent<Order>().SetMostFrontOrder(isEnlarge);
}
```

```
void AdjustOtherCards(CardView centerCard, bool isEnlarge) {
    float offset = 3.0f; // Adjust this value to control how much other cards move
    for (int i = 0; i < myCards.Count; i++) {
        if (myCards[i] == centerCard) continue;

        Vector3 newPos = myCards[i].originPRS.pos;
        if (isEnlarge) {
            if (myCards[i].originPRS.pos.x < centerCard.originPRS.pos.x) {
                newPos.x -= offset;
            } else {
                newPos.x += offset;
            }
        }

        myCards[i].MoveTransform(new PRS(newPos, myCards[i].originPRS.rot, myCards[i].originPRS.scale), true, 0.5f);
    }
}