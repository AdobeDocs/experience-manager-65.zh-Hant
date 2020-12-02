---
title: 外部連結檢查器
seo-title: 外部連結檢查器
description: 瞭解AEM中的「外部連結檢查器」。
seo-description: 瞭解AEM中的「外部連結檢查器」。
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# 外部鏈路檢查器{#the-external-link-checker}

AEM中提供外部連結檢查程式。 連結檢查程式：

* 掃描所有內容頁面
* 生成所有有效和無效連結的清單
* 在個別內容頁面上將無效連結標示為原地中斷

## 如何驗證外部連結{#how-to-validate-external-links}

要使用外部連結檢查器：

1. 使用&#x200B;**Navigation**，選擇&#x200B;**Tools**，然後選擇&#x200B;**Sites**。
1. 選擇「**外部鏈路檢查器**」，將生成所有外部鏈路的清單。
1. 在清單中選擇特定連結，然後按一下&#x200B;**Check**&#x200B;來驗證該連結：

   ![](assets/telc-01.png)

   顯示資訊：

   * **連** 結狀態
   * **URL**
   * **反向連結**
   * 連結為&#x200B;**上次檢查時間**（已驗證）
   * **最後狀態**&#x200B;返回

   * 連結為&#x200B;**上次可用時間**&#x200B;的時間
   * 連結為&#x200B;**上次訪問時間**

1. 在個別內容頁面上，無效的連結會顯示為中斷：

   ![](assets/chlimage_1-143.png)