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
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 翻譯多語言網站的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站。 為自動化翻譯工作流程，您將翻譯服務供應商與AEM整合，並建立專案，將內容翻譯成多種語言。 AEM支援人文和機器翻譯工作流程。

* 人類翻譯：內容會傳送給翻譯提供者，並由專業翻譯人員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會在AEM和翻譯提供者之間自動傳送。
* 機器翻譯：機器翻譯服務會立即翻譯您的內容。

翻譯內容需要執行下列步驟：

1. [將AEM與您的翻譯服務提供者連接](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) ，並 [建立翻譯整合架構設定](/help/sites-administering/tc-tic.md)。
1. [將語言主版頁面與翻譯服務](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 和框架配置關聯。
1. [識別要翻譯的內容類型](/help/sites-administering/tc-rules.md) 。
1. [編寫語言主版](/help/sites-administering/tc-prep.md) ，並建立語言副本的根頁面，以準備翻譯內容。
1. [建立翻譯專案](/help/sites-administering/tc-manage.md) ，以收集要翻譯的內容並準備翻譯程式。
1. 使用翻譯專案來 [管理內容翻譯程式](/help/sites-administering/tc-manage.md)。

如果您的翻譯服務供應商未提供與AEM整合的連接器，AEM支援以XML格式手動擷取和重新插入翻譯內容。

>[!NOTE]
>
>您的使用者必須是專案管理員群組的成員，才能使用「語言複製」功能。

## Best Practices {#best-practices}

「轉 [譯最佳實務](/help/sites-administering/tc-bp.md) 」頁面包含有關您實作的重要資訊。
