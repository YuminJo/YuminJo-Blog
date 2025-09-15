---
title: "Unity Editor.CreateEditor 메모리 관리 / Unity Editor.CreateEditor メモリ管理"
published: 2025-08-27
tags: ["Unity", "Editor", "Memory"]
category: "Programming"
draft: false
lang: ko
---

Unity에서 `Editor.CreateEditor(m_TargetObject)`를 사용하면 새로운 Editor 인스턴스가 생성됩니다.  
Unityで`Editor.CreateEditor(m_TargetObject)`を使うと、新しいEditorインスタンスが生成されます。

커스텀 에디터를 만들 때 사용하였지만, 주의할 점이 있습니다.  
カスタムエディタを作るときに使いましたが、注意点があります。

> 이 Editor 인스턴스는 가비지 컬렉션에 자동으로 제거되지 않습니다.  
> このEditorインスタンスはガベージコレクションで自動的に破棄されません。

즉, 명시적으로 해제하지 않으면 메모리에 계속 남게 됩니다.  
つまり、明示的に破棄しないとメモリに残り続けます。

---

## 문제점 / 問題点

`CreateEditor`로 계속 에디터를 생성하면 메모리에 계속 남아서 부하가 걸림  
`CreateEditor`で繰り返しエディタを生成すると、メモリに残り続けて負荷がかかる

---

## 해결법 / 解決法

Unity에서 안전하게 처리하려면 다음과 같이 합니다.  
Unityで安全に処理するには、次のようにします。

```csharp
Editor editor = Editor.CreateEditor(m_TargetObject);

// ... editor 사용 / editorを使用 ...

// 더 이상 필요 없으면 / もう必要ない場合
DestroyImmediate(editor); // 메모리 해제 / メモリ解放
```

---

## 추가 팁 / 追加のヒント

개발 중 Disable 처리 시 Editor와 코드에서 중복 Destroy 발생 가능  
開発中にDisableする場合、EditorとコードでDestroyが重複する可能性があります

대신 `AssetPreview.GetAssetPreview`로 Preview Texture만 가져오는 방법 추천  
代わりに`AssetPreview.GetAssetPreview`でプレビューのテクスチャだけ取得する方法を推奨

```csharp
Texture2D m_PreviewTexture = AssetPreview.GetAssetPreview(m_TargetObject);
GUI.DrawTexture(previewRect, m_PreviewTexture, ScaleMode.ScaleToFit);
```

---

## 요약 / まとめ

- Editor 객체는 MonoBehaviour나 ScriptableObject처럼 자동 해제되지 않음  
- EditorオブジェクトはMonoBehaviourやScriptableObjectのように自動破棄されない

- `DestroyImmediate(editor)`로 반드시 해제해야 메모리 누수 방지 가능  
- `DestroyImmediate(editor)`で必ず破棄することでメモリリークを防げる

- 반복적으로 CreateEditor 호출 시 메모리 누수 발생 가능 → GetAssetPreview 사용 권장  
- 繰り返しCreateEditorを呼び出すとメモリリークが発生する可能性 → GetAssetPreviewの使用を推奨
