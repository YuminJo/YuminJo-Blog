---
title: "싱글톤 패턴 / Singleton Pattern"
published: 2025-01-22
tags: ["Design Pattern", "Singleton", "Unity"]
category: "Software Engineering"
draft: false
lang: ko
---

# 싱글톤 패턴 / Singleton Pattern

> **한글:** 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴  
> **日本語:** 1つのクラスに対して、唯一のインスタンスしか持たないパターン

---

## Java 예시 / Java Example

```
public class Singleton {
    // 유일한 인스턴스를 저장하기 위한 정적 변수
    private static Singleton instance;

    // private 생성자를 사용하여 외부에서 인스턴스화하지 못하도록 방지
    private Singleton() {}

    // 유일한 인스턴스를 반환하는 정적 메서드
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

> **한글:** Unity Engine에서 게임 제작 시 많이 사용되는 패턴  
> **日本語:** Unity Engineでのゲーム制作でよく使われるパターン

---

## 장점 / 利点

- 인스턴스 생성 비용 감소  
- I/O 바운드 작업에 유용  
- DB 연결 모듈 등에 사용

---

## 단점 / 欠点

- TDD(Test Driven Development) 시 문제 발생  
- 단위 테스트의 독립성 유지가 어려움  
- 의존성이 높아 코드 유연성 감소  

> **한글:** 현재 제작중인 게임도 Manager에 싱글톤 패턴이 많이 사용됨. 편리하지만 장점과 단점을 반드시 인지하고 사용 필요  
> **日本語:** 現在制作中のゲームでもManagerにシングルトンパターンが多用されている。便利だが、利点と欠点を理解して使用することが重要
