---
title: 資產測試的命名約定
seo-title: Naming conventions for assets
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束。 但是，Adobe Experience Manager對資產節點的名稱作了進一步的約定。
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# 資產測試的命名約定{#naming-conventions-for-assets-testing}

儲存庫中的節點受 [Java內容儲存庫](/help/sites-developing/the-basics.md#java-content-repository)。 但是，Adobe Experience Manager對資產節點的名稱作了進一步的約定。

## 傳統 UI {#classic-ui}

經典UI施加了更嚴格的限制：

* 在以下任一情況下驗證資產名稱：

   * 提供資產標題以轉換為節點名稱
   * 提供了顯式節點名稱

* 有效字元（只有這些字元在從經典UI中建立資產時實際有效）:

   * 「a」到「z」
   * 「A」到「Z」
   * 「0」到「9」
   * _（下划線）
   * `-` （破折號/減號）
