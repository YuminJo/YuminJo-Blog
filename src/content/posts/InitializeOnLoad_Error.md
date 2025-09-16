---
title: "InitializeOnLoad에 의한 무한 컴파일링/ InitializeOnLoadによる無限リコンパイル"
published: 2025-09-16
tags: ["Development", "Bug"]
category: "Development"
draft: false
lang: ja
---
## InitializeOnLoad에 의한 무한 컴파일링 / InitializeOnLoadによる無限リコンパイル

### 무한 리컴파일링이 발생 / 無限リコンパイルが発生
`InitializeOnLoad`는 에디터를 실행하거나 어셈블리를 로딩할 때 자동으로 코드를 실행합니다.  
このとき特定のパッケージのインストールやアップデートのタイミングによって、無限コンパイルループが発生することがあります。  
이때 특정 패키지의 설치 및 업데이트 타이밍으로 인해 무한 컴파일 루프가 발생할 수 있습니다.  

실제로는 `PlayerSettings`의 **Define Symbols** 업데이트 타이밍으로 인해 무한 리컴파일이 발생했습니다。  
実際には `PlayerSettings` の **Define Symbols** 更新タイミングにより、無限リコンパイルが発生しました。  

---

### 해결 방법 / 解決方法
- `InitializeOnLoadMethod`를 사용하여 특정 메소드에서만 컴파일이 실행되도록 변경  
- `InitializeOnLoadMethod` を使用して特定のメソッドでのみコンパイルが走るように変更  

- 타이밍이 중복되는 부분은 `InitializeOnLoad`를 삭제하여 대처  
- タイミングが重複している部分は `InitializeOnLoad` を削除して対応  

---

### 참고 에러 / 参考エラー
[Infinite compilation loop after importing postprocessing (Unity Forum)](https://discussions.unity.com/t/infinite-compilation-loop-after-importing-postprocessing/711817)
