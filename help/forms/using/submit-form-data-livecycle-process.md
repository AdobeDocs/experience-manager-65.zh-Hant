---
title: 配置AEM Forms以向AEM Forms提交有關JEE流程的表單資料
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms允許您將自適應表單與AEM Forms整合在JEE流程中，以處理表單資料。
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

# 配置AEM Forms以向AEM Forms提交有關JEE流程的表單資料{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

自適應表格支援向AEM Forms提交關於JEE進程的資料，以便進一步處理。 它允許您使用提交的表單中提供的資料觸發JEE進程上的AEM Forms。 執行以下步驟，使您的AEM Forms實例能夠在JEE流程中向AEM Forms提交自適應表單：

## 配置您的AEM Forms伺服器 {#configure-your-aem-forms-server}

執行以下步驟，AEM使您的表單伺服器能夠向JEE伺服器上的AEM Forms提交資料：

1. 請訪問AEMhttps://上的Web配置控制台&#x200B;[*主機*]:[*埠*]/system/console/configMgr。

1. 找到並按一下 **AdobeLiveCycle客戶端SDK配置** 元件。
1. 按一下可編輯JEE伺服器上AEM Forms的配置伺服器URL、用戶名和密碼。
1. 查看設定並按一下 **保存**。

![AdobeLiveCycle客戶端SDK配置](assets/clientsdkconfiguration.jpg)

## 使用進程欄位映射資料 {#map-data-with-process-fields}

配置AEM Forms後，將資料XML和附件從提交的表單映射到AEM FormsJEE流程中的欄位。 要執行此操作：

1. 在Web配AEM置控制台中，按一下以編輯 **指南LiveCycle流程定位符和發票人** 配置。
1. 指定以下參數：

   * **資料xml參數的名稱** （強制）:指定需要處理提交資料的JEE進程上AEM Forms的XML屬性檔案。 預設值為 **dataxml**。

   * **檔案附件參數的名稱** （可選）:指定AEM FormsJEE進程需要處理的文檔對象清單。 預設值為 **檔案附件清單**。

1. 查看設定並按一下 **保存**。

![指南LiveCycle流程定位符和發票人](assets/test3.jpg)

配置完畢後，「提交至Forms Workflow」提交操作將列出包含指定資料xml參數的JEE伺服器進程上的AEM Forms。
