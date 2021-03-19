---
title: 翻譯多語言網站的內容
seo-title: 翻譯多語言網站的內容
description: 瞭解如何翻譯多語言網站的內容。
seo-description: 瞭解如何翻譯多語言網站的內容。
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: 語言副本
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# 翻譯多語言網站的內容{#translating-content-for-multilingual-sites}

自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站。 為自動化翻譯工作流程，您將翻譯服務提供商與AEM建立項目，以便將內容翻譯成多種語言。 AEM支援人文和機器翻譯工作流程。

* 人類翻譯：內容會傳送給翻譯提供者，並由專業翻譯人員翻譯。 完成時，會傳回翻譯的內容並匯入至AEM。 當翻譯提供者與之整合時AEM，內容會自動在翻譯提供AEM者與之間傳送。
* 機器翻譯：機器翻譯服務會立即翻譯您的內容。

翻譯內容需要執行下列步驟：

1. [與您的AEM翻譯服務提供商](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) 聯繫並 [建立翻譯整合框架配置](/help/sites-administering/tc-tic.md)。
1. [將您語言的首頁與翻](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 譯服務和框架配置相關聯。
1. [識別要翻譯的](/help/sites-administering/tc-rules.md) 內容類型。
1. [編寫語言主版](/help/sites-administering/tc-prep.md) 並建立語言副本的根頁面，以準備翻譯內容。
1. [建立轉](/help/sites-administering/tc-manage.md) 譯專案以收集要翻譯的內容並準備轉譯程式。
1. 使用翻譯項目到[管理內容翻譯流程](/help/sites-administering/tc-manage.md)。

如果您的翻譯服務提供商未提供與整合的連接器AEM,AEM則支援以XML格式手動提取和重新插入翻譯內容。

>[!NOTE]
>
>您的使用者必須是專案管理員群組的成員，才能使用「語言複製」功能。

## 最佳作法 {#best-practices}

[翻譯最佳實踐](/help/sites-administering/tc-bp.md)頁包含有關您實施的重要資訊。
