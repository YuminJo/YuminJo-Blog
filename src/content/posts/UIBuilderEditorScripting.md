---
title: "UI Builder를 활용한 Inspector 제작 / UI Builderを使用したInspector制作"
published: 2025-01-27
tags: ["Unity", "UI Toolkit", "Editor Scripting"]
category: "Unity Development"
draft: false
lang: ko
---

# UI Builder를 활용한 Inspector 제작 / UI Builderを使用したInspector制作

> Editor 스크립팅보다 UI Builder가 더 좋은 선택지가 될 수 있음  
> EditorスクリプトよりUI Builderの方が良い選択肢となる可能性あり

---

## 문제점 / 問題点

- 스타일시트 관리의 어려움  
- スタイルシート管理の難しさ

- 패턴화 되어있거나 재사용해야 하는 형식이 나오면 고민 필요 (디자인 시스템)  
- パターン化されていたり、再利用しなければならない形式が出てきたら、悩みの必要（デザインシステム）

---

## 해결법 / 解決法

- UI Toolkit 핵심은 웹개발 접근법  
- UI Toolkitの核心はウェブ開発アプローチ

- **uxml을 컴포넌트 단위로 쪼개서** 재사용  
- **uxmlをコンポーネント単位に分けて**再使用

![](https://velog.velcdn.com/images/doyaguri/post/6cc5c1e9-bd19-487e-b3dc-d4345bfcbf17/image.png)

---

## DefaultUss 예시 / DefaultUss例

```
.unity-foldout__checkmark {
    background-image: url("project://database/Assets/Scripts/Editor/Icons/Lock.png?fileID=2800000&guid=0589837adb4686a4183efa8cc07bde31&type=3#Lock");
}

Foldout > Toggle:checked .unity-foldout__checkmark {
    background-image: url("project://database/Assets/Scripts/Editor/Icons/LockOpen.png?fileID=2800000&guid=7d185f72de3ccbe4f8fb6f9d9d1ff77e&type=3#LockOpen");
}

Toggle > VisualElement {
    justify-content: flex-end;
}

.default-foldout {
    background-color: rgb(4, 184, 238);
    align-items: center;
    -unity-font-definition: resource('Font/Editor/GalmuriMono9');
    font-size: 14px;
    color: rgb(255, 255, 255);
    -unity-font-style: bold;
    text-shadow: 35px 35px 0 rgba(0, 0, 0, 0.47);
    display: flex;
    justify-content: space-between;
}

Label {
    color: rgb(230, 230, 230);
    margin-right: 40px;
}
```

---

## TurnManager_Inspector 예시 / TurnManager_Inspector例

```
using UnityEditor;
using UnityEngine;
using UnityEngine.UIElements;

[CustomEditor(typeof(TurnManager))]
public class TurnManager_Inspector : Editor
{
    public VisualTreeAsset m_InspectorXML;

    public override VisualElement CreateInspectorGUI()
    {
        // Create a new VisualElement to be the root of our inspector UI
        VisualElement myInspector = new VisualElement();

        // Load from default reference
        m_InspectorXML.CloneTree(myInspector);

        // Find the Foldout and Visual Elements
        var foldout = myInspector.Q<Foldout>("myFoldout");
        var visualElements = myInspector.Q<VisualElement>("myVisualElements");

        // Set initial state to false
        visualElements.style.display = DisplayStyle.None;

        // Register callback for Foldout state change
        foldout.RegisterValueChangedCallback(evt =>
        {
            visualElements.style.display = evt.newValue ? DisplayStyle.Flex : DisplayStyle.None;
        });
        
        // 버튼 가져오기 / ボタン取得
        Button myButton = myInspector.Q<Button>("StartButton");
        myButton.clicked += OnMyButtonClicked;

        // Return the finished inspector UI
        return myInspector;
    }

    public override bool UseDefaultMargins() => false;
    
    private void OnMyButtonClicked() {
        TurnManager myComponent = (TurnManager)target;
        myComponent.StartGame();
    }
}
```

---

> 핵심 포인트 / 重要ポイント
- UI Builder를 사용하면 Inspector UI 제작이 **편리하고 직관적**  
- UI Builderを使用するとInspector UI制作が**便利で直感的**
- UXML/USS를 재사용할 수 있으므로 **디자인 시스템 구축** 가능  
- UXML/USSを再利用できるので**デザインシステム構築**が可能