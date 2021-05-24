---
title: 轉譯多語言網站的內容
seo-title: 轉譯多語言網站的內容
description: 了解如何翻譯多語言網站的內容。
seo-description: 了解如何翻譯多語言網站的內容。
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: 語言副本
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 轉譯多語言網站的內容{#translating-content-for-multilingual-sites}

自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站。 為了自動化翻譯工作流，您將翻譯服務提供商與AEM整合，並建立項目以將內容翻譯成多種語言。 AEM支援人工和機器翻譯工作流程。

* 人類翻譯：內容將發送給您的翻譯提供商，並由專業翻譯人員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會自動在AEM和翻譯提供者之間傳送。
* 機器翻譯：機器翻譯服務會立即翻譯您的內容。

轉譯內容涉及下列步驟：

1. [將AEM與您的翻譯服務提供](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) 商連 [接，並建立翻譯整合架構設定](/help/sites-administering/tc-tic.md)。
1. [將您語言首頁與翻](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 譯服務和框架配置相關聯。
1. [識別要翻譯的](/help/sites-administering/tc-rules.md) 內容類型。
1. [編寫語言主版](/help/sites-administering/tc-prep.md) 並建立語言副本的根頁面，以準備翻譯內容。
1. [建立翻](/help/sites-administering/tc-manage.md) 譯專案以收集要翻譯的內容並準備翻譯程式。
1. 使用翻譯專案至[管理內容翻譯程式](/help/sites-administering/tc-manage.md)。

如果您的翻譯服務提供者未提供與AEM整合的連接器，AEM支援以XML格式手動擷取和重新插入翻譯內容。

>[!NOTE]
>
>您的使用者必須是專案管理員群組的成員，才能使用語言副本功能。

## 最佳作法 {#best-practices}

[翻譯最佳實務](/help/sites-administering/tc-bp.md)頁面包含有關您實作的重要資訊。
