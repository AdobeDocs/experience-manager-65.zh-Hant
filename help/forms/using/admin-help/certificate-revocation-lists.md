---
title: 管理憑證轉換清單
seo-title: Managing certificate revocationlists
description: 了解如何管理憑證撤銷清單。
seo-description: Learn how to manage certificate revocation lists.
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# 管理憑證轉換清單{#managing-certificate-revocationlists}

使用信任儲存管理，可以導入、編輯和刪除證書吊銷清單(CRL)。 支援Base64和DER編碼的證書吊銷清單。

## 導入CRL {#import-a-crl}

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「證書吊銷清單」，然後按一下「導入」。
1. 在「別名」框中，鍵入CRL的標識符。
1. 按一下「瀏覽」以查找CRL，然後按一下「確定」。

## 導出CRL {#export-a-crl}

1. 在管理控制台中，按一下「設定>信任存放區管理>憑證撤銷清單」。
1. 按一下要導出的CRL的別名，然後按一下導出。
1. 按照指示導出CRL。 CRL以Base64編碼導出。
1. 按一下「確定」。

## 刪除CRL {#delete-a-crl}

1. 在管理控制台中，按一下「設定>信任存放區管理>憑證撤銷清單」。
1. 選擇要刪除的CRL的複選框，按一下「刪除」，然後按一下「確定」。
