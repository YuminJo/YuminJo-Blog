---
title: "Git 브랜치 단일 클론 / Git single-branch clone"
published: 2024-12-12
tags: ["Git", "Branch", "Clone"]
category: "Computer Science"
draft: false
lang: ko
---

# Git 브랜치 단일 클론 / Git single-branch clone

---

## 상황 설명 / Situation

> **한글:** front branch에서 front 작업을 하고, dev branch에서 backend 작업을 하는 경우  
> branch를 나눌 필요가 있음  

---

## 해결 방법 / Solution

- 별도의 clone branch를 생성하고, 해당 브랜치에서 작업
- 이렇게 하면 원하는 브랜치만 clone 가능

```
$ git clone -b {branch_name} --single-branch {저장소 URL}

예: git clone -b tempbranch --single-branch https://github.com/test/testtest
```

- 위 예시는 testtest 저장소의 tempbranch 브랜치만 clone함