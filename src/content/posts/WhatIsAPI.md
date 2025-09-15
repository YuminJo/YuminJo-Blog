---
title: "API란? / APIは？"
published: 2024-09-26
tags: ["Computer Science"]
category: "Computer Science"
draft: false
lang: ko
---

# API란? / APIは？

## Application Programming Interface

<details>
<summary>複数のコンピュータプログラムが互いに通信する方法</summary>

> **한글:** 둘 이상의 컴퓨터 프로그램이 서로 통신하는 방법이고, 컴퓨터 사이에 있는 중계 계층  
> **일본어:** 複数のコンピュータプログラムが互いに通信する方法であり、コンピュータ間にある中継階層
</details>

---

## API 장점 / APIの長所

:::tip[팁 / ヒント]
**한글:** API는 필요한 기능만 노출 가능하며, 매번 재개발할 필요 없이 쉽게 활용할 수 있습니다.  
**일본어:** APIは必要な基本機能だけを公開でき、毎回自己開発せず簡単に利用できます。
:::

:::note[주의 / 注意]
**한글:** 개발 워크플로우가 단순해지고, 앱 확장이 쉬워집니다.  
**일본어:** 開発ワークフローが簡素化され、アプリケーションの拡張が容易になります。
:::

---

## API 유형 / APIタイプ

| API 종류 / 種類 | 공개 범위 / 公開範囲 | 사용 목적 / 使用目的 |
|-----------------|-------------------|------------------|
| Private API / プライベートAPI | 내부 / 内部 | 회사 내부 사용 / 社内利用 |
| Public API / パブリックAPI   | 모두 / 誰でも | 외부 사용자용 / 外部利用 |
| Partner API / パートナーAPI  | 특정 / 特定 | 파트너와 데이터 공유 / パートナー共有 |

---

### 코드 예시 / コード例

```csharp {} "Hello World 예제"
using UnityEngine;

public class HelloWorld : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Hello World");  // 2번째 라인 강조
    }
}