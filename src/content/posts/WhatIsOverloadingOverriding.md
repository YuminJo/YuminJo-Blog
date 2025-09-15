---
title: "Overloading과 Overriding이란? / オーバーローディングとオーバーライディングとは?"
published: 2024-11-14
tags: ["Java", "OOP", "Method"]
category: "Computer Science"
draft: false
lang: ko
---

# Overloading과 Overriding이란? / オーバーローディングとオーバーライディングとは?

---

## Overloading란? / オーバーローディングとは?

<details>
<summary>같은 이름의 메서드를 여러 개 정의 가능</summary>

> **한글:** 같은 이름인데 여러 함수를 정의할 수 있으며, 유연성이 높아지고 클린 코드 유지가 가능  
> **日本語:** 同じ名前ですが、複数の関数を定義でき、柔軟性が高まりクリーンコードになります  
> **한글:** 같은 클래스 내에서 사용된다  
> **日本語:** 同じクラス内で使用されます
</details>

```
void add(int a, int b) {}
void add(int a, int b, int c){}

c.add(a,b);
c.add(a,b,c);
```

---

## Overriding란? / オーバーライディングとは?

<details>
<summary>상위 클래스 메서드를 하위 클래스가 재정의</summary>

> **한글:** 상위 클래스가 가진 메서드를 하위 클래스가 **재정의**하는 것  
> **日本語:** 上位クラスが持っているメソッドを下位クラスが**再定義**すること  
> **한글:** 정적으로 선언한 메서드는 오버라이딩 불가  
> **日本語:** 静的に宣言されたメソッドはオーバーライディングできません
</details>

```
class Robot{
    void make(){
        System.out.println("MAKING..");
    }
}

class MACHINE extends Robot{
    @Override
    void make(){
        System.out.println("Robot MAKING Computer..");
    }
}
```

---

:::
**한글:** Overloading은 같은 클래스 내 여러 메서드 정의, Overriding은 상속 구조에서 메서드 재정의  
**日本語:** オーバーローディングは同じクラス内での複数メソッド定義、オーバーライディングは継承構造でのメソッド再定義
:::