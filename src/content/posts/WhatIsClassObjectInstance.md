---
title: "Class, Object, Instance란? / クラス・オブジェクト・インスタンスとは?"
published: 2024-09-28
tags: ["Computer Science", "OOP", "Java"]
category: "Computer Science"
draft: false
lang: ko
---

# Class, Object, Instance란? / クラス・オブジェクト・インスタンスとは?

---

## Class란? / クラスとは?

<details>
<summary>オブジェクトを作り出すための枠組みであり、作り出すオブジェクトの属性とメソッドの集合を盛り込んだもの</summary>

> **한글:** Class는 객체를 생성하기 위한 틀이며, 객체가 가질 속성과 메서드의 집합을 포함합니다.  
> **日本語:** オブジェクトを作り出すための枠組みであり、作り出すオブジェクトの属性とメソッドの集合を盛り込んだもの
</details>

---

## Object란? / オブジェクトとは?

<details>
<summary>クラスから作られる実体、クラスで宣言された変数をオブジェクトといいます。</summary>

> **한글:** Object는 Class에서 만들어진 실체이며, Class에서 선언한 변수들을 가지는 객체입니다.  
> **日本語:** クラスから作られる実体、クラスで宣言された変数をオブジェクトといいます。
</details>

---

## Instance란? / インスタンスとは?

<details>
<summary>オブジェクトがメモリに割り当てられた状態であり、ランタイムに駆動されるオブジェクトのことです。</summary>

> **한글:** Instance는 Object가 메모리에 할당되어 실제로 사용 가능한 상태이며, 런타임에 실행되는 객체를 의미합니다. Object와 같은 의미로 쓰이기도 합니다.  
> **日本語:** オブジェクトがメモリに割り当てられた状態であり、ランタイムに駆動されるオブジェクトのことです。オブジェクトと同じ意味でも使われます。
</details>

:::tip[비유 / 例え]
- **한글:**  
  - 빵을 만들 때 쓰는 틀(속성들의 집합) → Class  
  - 틀로부터 나오는 서로 다른 특징을 가진 빵 → Object  
  - 빵을 굽는 동작 → Method  
- **日本語:**  
  - パンを作るときの型(属性の集合) → Class  
  - 型から生まれるそれぞれのパン → Object  
  - パンを焼く動作 → Method
:::

---

## 코드 예제 / コード例

```java
public class Bread {
    // 멤버변수 (속성)
    String breadName;
    int flour;
    int sugar;
    
    // 생성자
    public Bread(String breadName, int flour, int sugar){
        this.breadName = breadName;
        this.flour = flour;
        this.sugar = sugar;
    }
    
    // Method
    public void bake(){
        System.out.println(breadName + " 굽는 중...");
    }
    
    public static void main(String[] args){
        Bread b;           // Object 선언
        b = new Bread("식빵", 500, 50); // Instance 생성
        b.bake();          // Method 실행
    }
}
