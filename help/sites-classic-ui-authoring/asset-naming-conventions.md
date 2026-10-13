---
title: 資產測試的命名慣例
description: 存放庫中的節點會遵守Java內容存放庫的命名慣例。 不過，Adobe Experience Manager對資產節點名稱實施進一步的慣例。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%
---
# 資產測試的命名慣例{#naming-conventions-for-assets-testing}

存放庫中的節點會遵循[Java內容存放庫](/help/sites-developing/the-basics.md#java-content-repository)的命名慣例。 不過，Adobe Experience Manager對資產節點名稱實施進一步的慣例。

## 傳統 UI {#classic-ui}

傳統UI會實施更嚴格的限制：

* 當出現下列任一情況時，以明確節點名稱驗證資產名稱：

  * 提供了資產標題，以便轉換為節點名稱
  * 提供了明確的節點名稱

* 有效字元（從傳統UI中建立資產時，實際只有這些字元有效）：

  * &#39;a&#39;至&#39;z&#39;
  * &#39;A&#39;至&#39;Z&#39;
  * &#39;0&#39;至&#39;9&#39;
  * _ （底線）
  * `-` （破折號/減號）
