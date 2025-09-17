---
title: "csp.rsp"
published: 2025-09-18
tags: ["C#", "Compiler", "Response File"]
category: "Programming"
draft: false
lang: ko
---
## csc.rsp (C# Compiler Response File)
Unity에서 C# 컴파일러에게 추가 옵션을 전달하기 위한 설정 파일이다.
UnityでC#コンパイラーに追加オプションを渡すための設定ファイル。

### 기본 사용법 / 基本的な使い方
Assets/csc.rsp 파일을 만들고 컴파일러 옵션을 한 줄씩 작성한다.
Assets/csc.rspファイルを作成し、コンパイラオプションを一行ずつ記述する。
-define:MY_DEFINE
-unsafe
-nowarn:0168,0219
-additionalfile:".refrules"
-analyzer:"SomeAnalyzer.dll"

### 주요 옵션들 / 主要オプション
-define:SYMBOL : 전처리기 심볼 정의 / プリプロセッサシンボル定義
-unsafe : unsafe 코드 허용 / unsafeコード許可
-nowarn:번호 : 특정 경고 무시 / 特定の警告を無視
-additionalfile:"파일" : Analyzer용 추가 파일 / Analyzer用追加ファイル
-analyzer:"dll파일" : Roslyn Analyzer 추가 / Roslyn Analyzer追加
-r:"라이브러리.dll" : 외부 라이브러리 참조 / 外部ライブラリ参照


### 언제 사용하나? / いつ使う？
Roslyn Analyzer 설정할 때 (가장 흔한 용도)
Roslyn Analyzerを設定する時（最も一般的な用途）
Unity에서 지원하지 않는 고급 컴파일 옵션이 필요할 때
Unityでサポートしていない高度なコンパイルオプションが必要な時
조건부 컴파일용 define 심볼 추가할 때
条件付きコンパイル用defineシンボルを追加する時


### 주의사항 / 注意事項
Unity가 프로젝트를 재생성해도 csc.rsp는 그대로 남아있음(안전함)
Unityがプロジェクトを再生成してもcsc.rspはそのまま残る
잘못된 옵션을 넣으면 컴파일 에러 발생
間違ったオプションを入れるとコンパイルエラーが発生
파일이 있으면 모든 스크립트 컴파일에 영향을 줌
ファイルがあると全てのスクリプトコンパイルに影響する
- 結局は1つのクラスなので、変数の重複やアクセス制限はそのまま適用される

- 무분별하게 남용하면 오히려 "이 메서드 어디 있지?" 하고 헷갈릴 수 있음  
- 無分別に乱用すると、「このメソッドどこにあるの？」と混乱する可能性がある
