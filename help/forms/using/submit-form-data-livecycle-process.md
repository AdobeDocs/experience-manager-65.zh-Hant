---
title: 設定AEM Forms以將表單資料提交至JEE程式上的AEM Forms
seo-title: 設定AEM Forms以將表單資料提交至JEE程式上的AEM Forms
description: AEM Forms可讓您將最適化表單與JEE流程上的AEM Forms整合，以處理表單資料。
seo-description: AEM Forms可讓您將最適化表單與JEE流程上的AEM Forms整合，以處理表單資料。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 設定AEM Forms以將表單資料提交至JEE程式上的AEM Forms{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

最適化表單支援將資料提交至JEE上的AEM表單程式，以進一步處理。 它可讓您使用已提交表單中的可用資料，觸發AEM Forms on JEE流程。 請執行下列步驟，讓您的AEM Forms例項能夠將最適化表單提交至JEE流程的AEM Forms:

## 設定您的AEM Forms伺服器 {#configure-your-aem-forms-server}

請執行下列步驟，讓您的AEM Forms伺服器將資料送出至JEE伺服器上的AEM Forms:

1. 請前往https://[*host*]:[*port*]/system/console/configMgr的AEM web組態主控台。

1. 找到並按一下 **Adobe liveCycle Client SDK Configuration** （Adobe LiveCycle用戶端SDK組態）元件。
1. 按一下以編輯JEE伺服器上AEM Forms的設定伺服器URL、使用者名稱和密碼。
1. 檢閱設定，然後按一下「 **儲存**」。

![Adobe LiveCycle Client SDK組態](assets/clientsdkconfiguration.jpg)

## 使用流程欄位映射資料 {#map-data-with-process-fields}

在您的AEM Forms設定完成後，將資料XML和附件從提交的表單對應至AEM Forms on JEE流程中的欄位。 要執行此操作：

1. 在AEM web組態主控台中，按一下以編輯 **Guide LiveCycle Process Locator和Invoker組態** 。
1. 指定下列參數：

   * **資料xml參數的名稱** （必填）:指定AEM Forms on JEE程式的XML屬性檔案，以處理提交的資料。 預設值為 **dataxml**。

   * **檔案附件參數的名稱** （可選）:指定AEM Forms on JEE程式需要處理的檔案物件清單。 預設值為 **fileAttachmentsList**。

1. 檢閱設定，然後按一下「 **儲存**」。

![指南LiveCycle流程貨位和發票商](assets/test3.jpg)

設定好後，「提交至表單工作流程」提交動作會列出JEE伺服器上的AEM Forms程式，其中包含指定的資料xml參數。
