---
title: 管理憑證撤銷清單
description: 瞭解如何管理憑證撤銷清單。 您可以使用「信任存放區管理」來匯入、編輯和刪除憑證撤銷清單(CRL)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# 管理憑證撤銷清單{#managing-certificate-revocationlists}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

使用「信任存放區管理」，您可以匯入、編輯和刪除憑證撤銷清單(CRL)。 支援Base64和DER編碼的憑證撤銷清單。

## 匯入CRL {#import-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」，然後按一下「匯入」。
1. 在「別名」方塊中，輸入CRL的識別碼。
1. 按一下「瀏覽」來尋找CRL，然後按一下「確定」。

## 匯出CRL {#export-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 按一下CRL的別名以便匯出，然後按一下「匯出」。
1. 請依照指示匯出CRL。 CRL會以Base64編碼匯出。
1. 按一下「確定」。

## 刪除CRL {#delete-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 選取要刪除的CRL核取方塊，按一下「刪除」，然後按一下「確定」。
