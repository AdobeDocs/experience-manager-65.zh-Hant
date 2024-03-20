---
title: 翻譯多語言網站的內容
description: 瞭解如何翻譯多語言網站的內容。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 74%

---

# 翻譯多語言網站的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站。 若要自動化翻譯工作流程，您可以將翻譯服務提供商與 AEM 相整合，並建立用於將內容翻譯成多種語言的專案。AEM 支援人工和機器翻譯工作流程。

* 人工翻譯：內容會傳送給您的翻譯提供者，並由專業翻譯人員進行翻譯。 完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。
* 機器翻譯：機器翻譯服務會立即翻譯您的內容。

翻譯內容涉及以下步驟：

1. [將 AEM 與您的翻譯服務提供商連接](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)並[建立翻譯整合框架設定](/help/sites-administering/tc-tic.md)。
1. [將您語言主版的頁面](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 與翻譯服務和框架設定相關聯。
1. [識別要翻譯的內容類型](/help/sites-administering/tc-rules.md)。
1. 編寫語言主版並建立語言副本的根頁面，[以備妥內容進行翻譯](/help/sites-administering/tc-prep.md)。
1. [建立翻譯專案](/help/sites-administering/tc-manage.md)以收集要翻譯的內容並準備翻譯流程。
1. 使用翻譯專案[管理內容翻譯流程](/help/sites-administering/tc-manage.md)。

如果您的翻譯服務提供商不提供連接器以與 AEM 整合，AEM 支援手動擷取和重新插入 XML 格式的翻譯內容。

>[!NOTE]
>
>您的使用者必須是專案 — 管理員群組的成員，才能使用語言複製功能。

## 最佳做法 {#best-practices}

[翻譯最佳做法](/help/sites-administering/tc-bp.md)頁面包含與您的實作相關的重要資訊。
