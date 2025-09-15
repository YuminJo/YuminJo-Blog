---
title: "Unity DI / UnityのDI"
published: 2025-02-04
tags: ["Unity", "Dependency Injection", "Service Locator"]
category: "Unity Development"
draft: false
lang: ko
---

# Unity DI / UnityのDI

최근 유니티에서 DI(Dependency Injection)에 많은 생각을 하고 있습니다.  
最近、ユニティでDI（Dependency Injection）について多く考えています。

Spring에서는 Spring Framework가 알아서 의존성을 주입해주지만  
Springでは、Spring Frameworkが自動的に依存関係を注入してくれますが、

Unity는 Inspector에서 직접 주입하거나 코드에서 처리해야 합니다.  
UnityではInspectorから直接注入するか、コードで処理する必要があります。

---

## 기존 프로젝트 / 以前のプロジェクト

- 싱글톤 + MVP 패턴 이용  
- シングルトン + MVPパターンを利用

---

## 새로운 프로젝트 / 新しいプロジェクト

- MVP 패턴 + 서비스 로케이터 패턴 이용  
- MVPパターン + サービスロケーターパターンを利用

---

## Service Locator 예제 / Service Locatorの例

```
using System;
using System.Collections.Generic;

public static class ServiceLocator
{
    public static IDictionary<Type, object> Services { get => _services; }
    private static Dictionary<Type, object> _services = new();
    
    // 서비스 등록 / サービス登録
    public static void Register<T>(T service)
    {
        if (!_services.ContainsKey(typeof(T)))
        {
            _services[typeof(T)] = service;
        }
        else
        {
            throw new InvalidOperationException($"Service of type {typeof(T)} is already registered.");
        }
    }

    // 서비스 가져오기 / サービス取得
    public static T Get<T>()
    {
        if (_services.TryGetValue(typeof(T), out var service))
        {
            return (T)service;
        }
        else
        {
            throw new KeyNotFoundException($"Service of type {typeof(T)} is not registered.");
        }
    }
    
    // 서비스 제거 / サービス削除
    public static void UnRegister<T>()
    {
        if (_services.ContainsKey(typeof(T)))
        {
            _services.Remove(typeof(T));
        }
        else
        {
            throw new KeyNotFoundException($"Service of type {typeof(T)} is not registered.");
        }
    }
}
```

---

## 서비스 로케이터 패턴 주의점 / サービスロケーターパターンの注意点

- 남발 시 전역 종속성이 강해지고, 테스트가 어려워짐  
- 過度に使用するとグローバル依存が強くなり、テストが困難になる

- 블랙박스화 발생 가능  
- ブラックボックス化が発生する可能性

---

## 해결 방법 / 解決方法

- 인터페이스 분리: 서비스가 제공하는 인터페이스를 정의하고 이를 사용  
- インターフェイス分離：サービスが提供するインターフェイスを定義し、それを利用

- 로깅을 통한 블랙박스화 방지  
- ロギングによるブラックボックス化防止

- 외부 DI Framework 고려 가능: Zenject(Extenject), VContainer 등  
- 外部DIフレームワークを検討可能：Zenject(Extenject)、VContainerなど

---

## 선택 이유 / 採用理由

- Zenject: 업데이트 미지원 / 更新未対応
- VContainer: 적용까지 시간 필요 / 適用に時間がかかる

따라서 개인 프로젝트에서는 사용하지 않음  
よって、個人プロジェクトでは使用しないことに決定

---

## 구현 방향 / 実装方針

- 동적 서비스 등록 및 해제 기능 추가 (Register(), Unregister())  
- 動的サービス登録と解除機能の追加（Register(), Unregister()）

- 인터페이스 기반 관리로 유연성 확보 (IAudioService 등)  
- インターフェイスベース管理で柔軟性確保（IAudioServiceなど）

- 씬 별 서비스 관리 (Lazy Loading & Cleanup)  
- シーンごとのサービス管理（Lazy Loading & Cleanup）

- Lazy Initialization 적용: 필요할 때만 인스턴스 생성  
- Lazy Initializationの適用：必要なときだけインスタンス生成

---

최근 .NET Core와 EF Core를 공부하며 개발에 재미를 느끼고 있네요
最近、.NET CoreとEF Coreを勉強しながら、開発がとても楽しいと感じています
