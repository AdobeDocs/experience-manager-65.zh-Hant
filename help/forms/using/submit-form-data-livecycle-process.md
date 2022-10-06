---
title: 設定AEM Forms以在JEE程式中將表單資料提交至AEM Forms
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms可讓您將適用性表單與AEM Forms的JEE程式整合，以處理表單資料。
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 設定AEM Forms以在JEE程式中將表單資料提交至AEM Forms{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

適用性表單支援在JEE上將資料提交至AEM Forms程式，以便進一步處理。 它可讓您使用提交表單中可用的資料，在JEE上觸發AEM Forms程式。 執行下列步驟，讓您的AEM Forms執行個體能在JEE程式中將最適化表單提交至AEM Forms:

## 設定您的AEM Forms伺服器 {#configure-your-aem-forms-server}

執行下列步驟，讓AEM表單伺服器可將資料提交至JEE伺服器上的AEM Forms:

1. 前往AEM Web設定主控台： https://[*主機*]:[*埠*]/system/console/configMgr。

1. 找到並按一下 **AdobeLiveCycle用戶端SDK設定** 元件。
1. 按一下以編輯JEE伺服器上AEM Forms的設定伺服器URL、使用者名稱及密碼。
1. 檢閱設定，然後按一下 **儲存**.

![AdobeLiveCycle用戶端SDK設定](assets/clientsdkconfiguration.jpg)

## 使用流程欄位映射資料 {#map-data-with-process-fields}

設定AEM Forms後，將資料XML和附件從提交的表單對應至JEE流程上AEM Forms的欄位。 要執行此操作：

1. 在AEM Web配置控制台中，按一下以編輯 **指南LiveCycle流程貨位和發票人** 設定。
1. 指定下列參數：

   * **資料xml參數的名稱** （強制）:指定JEE上AEM Forms程式需要處理已提交資料的XML屬性檔案。 預設值為 **dataxml**.

   * **檔案附件參數的名稱** （可選）:指定JEE上的AEM Forms程式需要處理的檔案物件清單。 預設值為 **fileAttachmentsList**.

1. 檢閱設定，然後按一下 **儲存**.

![指南LiveCycle流程貨位和發票人](assets/test3.jpg)

設定後， 「提交至Forms Workflow」提交動作會列出JEE伺服器上包含指定資料xml參數的AEM Forms程式。
