---
title: 疑難排解程式報告
description: 針對JEE程式報告的AEM Forms問題進行疑難排解
page-status-flag: de-activated
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 165d4c69-d7ca-45f8-a9de-764cb8ecab7e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%
---
# 疑難排解程式報告 {#troubleshooting-process-reporting}

## 在Microsoft Windows 7的Internet Explorer 9上建立篩選器時遇到的問題 {#issues-faced-in-creating-filters-on-internet-explorer-on-microsoft-windows}

如果您為預先定義的報表建立篩選器，下列問題會間歇性地在&#x200B;**Microsoft Windows 7**&#x200B;環境的&#x200B;**Internet Explorer 9**&#x200B;上發生：

* 「值」欄位中的下拉式清單會顯示唯一識別碼，而非值。
* 「值」欄位中的「行事曆」控制項會顯示日文字元。
* 條件欄位不顯示。
* 「值」欄位中的「行事曆」控制項不會顯示。

### 解決方法 {#resolution}

當您仍登入「程式報告」時：

1. 清除瀏覽器快取。
1. 重新整理瀏覽器畫面。
