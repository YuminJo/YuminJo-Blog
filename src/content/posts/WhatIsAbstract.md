---
title: "Abstract vs Virtual이란? / AbstractとVirtualとは?"
published: 2024-11-17
tags: ["Java", "C#", "OOP", "Method"]
category: "Computer Science"
draft: false
lang: ko
---

# Abstract vs Virtual이란? / AbstractとVirtualとは?

---

## Java Abstract란? / JavaのAbstractとは?

<details>
<summary>Java에서 abstract 클래스와 메서드</summary>

> **한글:** abstract 클래스는 인스턴스화할 수 없으며, abstract 메서드는 반드시 파생 클래스에서 구현해야 한다  
> **日本語:** abstractクラスはインスタンス化できず、abstractメソッドは派生クラスで必ず実装する必要があります
</details>

```
public abstract class BaseClass {
    public abstract void display();
}

public class DerivedClass extends BaseClass {
    @Override
    public void display() {
        System.out.println("DerivedClass Display");
    }
}
```

---

## C# Virtual란? / C#のVirtualとは?

<details>
<summary>C#에서 virtual 키워드</summary>

> **한글:** virtual은 메서드, 속성, 이벤트 등을 오버라이드할 수 있도록 하며 기본 구현을 제공  
> 파생 클래스에서 선택적으로 오버라이드 가능  
> **日本語:** virtualはメソッド、プロパティ、イベントなどをオーバーライド可能にし、基本実装を提供します  
> 派生クラスで任意にオーバーライド可能
</details>

```
public class BaseClass {
    public virtual void Display() {
        Console.WriteLine("BaseClass Display");
    }
}

public class DerivedClass : BaseClass {
    public override void Display() {
        Console.WriteLine("DerivedClass Display");
    }
}
```

---

## 공통점과 차이점 / 共通点と違い

<details>
<summary>핵심 의미</summary>

> **한글:** Virtual과 Abstract 모두 “기능”을 제공하는 개념  
> 공통점은 모으고, 차이점은 버리는 기능  
> **日本語:** VirtualとAbstractはどちらも“機能”を提供する概念  
> 共通点は集めて、違いは捨てる機能
</details>

:::
**한글:** Java abstract는 구현 강제, C# virtual은 선택적 오버라이드  
**日本語:** Javaのabstractは実装強制、C#のvirtualは任意オーバーライド
:::