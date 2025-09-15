---
title: "MVP 패턴이란? / MVPパターンとは?"
published: 2024-10-19
tags: ["Unity", "Design Pattern", "MVP"]
category: "Software Architecture"
draft: false
lang: ko
---

# MVP 패턴이란? / MVPパターンとは?

![](https://velog.velcdn.com/images/doyaguri/post/fee9ce1e-3481-4d08-b2fa-a57b49b0241e/image.png)

최근 자주 즐겨쓰는 MVP 패턴인데 괜찮다고 생각해서 글을 적어본다.

<details>
<summary>MVPとは Model, View, Presenterで構成されるアーキテクチャパターン</summary>

> **한글:** MVP 패턴은 Model, View, Presenter로 구성되며,  
> View는 UI 구성 요소를 담당하고, Presenter는 View와 Model을 연결하며,  
> Model은 변수 및 연산을 처리합니다.  
> **日本語:** MVPパターンは Model, View, Presenter で構成され、  
> ViewはUIコンポーネントの役割、PresenterはViewとModelを仲介、  
> Modelは変数や演算処理を担当します。
</details>

---

## View란? / Viewとは?

```
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class FarmSubItemView : UI_Base
{
public override bool Init() {
if (base.Init() == false) return false;
return true;
}


void Update() {
    if (_presenter.GetSeedExist()) {
        if (!_presenter.GetIsFarmEnd()) {
            _presenter.Timer();
        }
        else {
            if(GetImage((int)Images.CheckMarkImg).gameObject.activeInHierarchy) return;
            if(_presenter.GetFarmAnimationState()) return;
            GetImage((int)Images.CheckMarkImg).gameObject.SetActive(true);
            GetText((int)Texts.TimeText).gameObject.SetActive(false);
        }
    }
}

void OnApplicationPause(bool pauseStatus) {
    if (_presenter == null) return;
    if (!_presenter.GetSeedExist()) return;
    if (!pauseStatus) _presenter.OnAppPause();
}
}

```

> **한글:** View는 단순히 UI 처리를 담당한다.  
> **日本語:** Viewは単にUI処理を担当します。

---

## Presenter란? / Presenterとは?

```
public int GetRandomAmount() {
int randomAmount = Random.Range(2, 5);
return randomAmount;
}

public bool GetFarmAnimationState() {
return _model.farmAnimation;
}

public void SetFarmAnimationState(bool state) {
_model.SetFarmAnimation(state);
}

public void SetWaterState(bool state) {
_model.SetIsWatered(state);
}

public void UseFarmBoost() {
if (_model.currentSec >= 5) {
Managers.Game.UseDeliveryBoost();
_view.EndWaterDrop();
_model.SetEndTime(1);
}
}

```

> **한글:** Presenter는 Model과 View를 연결시키는 역할을 한다.  
> **日本語:** PresenterはModelとViewをつなぐ役割を担います。

---

## Model란? / Modelとは?

```
public int dirtValue { get; private set; }
public bool farmAnimation { get; private set; }
public bool isWatered { get; private set; }

public void SetCurrentSeed(ItemData seed) {
currentSeed = seed;
}

public void InitFarm() {
isWatered = false;
currentSeed = null;
endTime = (int)(DateTime.UtcNow - new DateTime(1970, 1, 1)).TotalSeconds + 99999;
}
```
> **한글:** Model은 변수 및 연산 처리를 담당하며, 공용 로직도 포함 가능하다.  
> **日本語:** Modelは変数と演算処理を担当し、共通ロジックも含められます。

---

:::tip[개발 경험 / 開発経験]
**한글:** 화면, 기능, 변수/연산을 각각 나누니 클린 코드 유지가 용이하며 Mobile 개발에서 유용하다.  
**日本語:** 画面、機能、変数・演算を分けることでクリーンコードが維持でき、モバイル開発で便利です。
:::

> **한글:** 이전에는 하나의 스크립트에 모두 담았지만, 이렇게 나누니 훨씬 관리가 쉬워졌다.  
> **日本語:** 以前は1つのスクリプトにまとめていたが、分けることで管理が容易になった。
