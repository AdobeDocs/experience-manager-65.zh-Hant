---
title: 將AEM Forms配置為在JEE流程上向AEM Forms提交表單資料
seo-title: 將AEM Forms配置為在JEE流程上向AEM Forms提交表單資料
description: AEM Forms可讓您將最適化表單與AEM Forms整合在JEE處理表單資料的流程上。
seo-description: AEM Forms可讓您將最適化表單與AEM Forms整合在JEE處理表單資料的流程上。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# 將AEM Forms配置為在JEE進程上向AEM Forms提交表單資料{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

最適化表單支援將資料提交至AEM Forms的JEE程式，以進一步處理。 它可讓您使用提交表單中的資料觸發AEM Forms的JEE程式。 執行以下步驟，讓您的AEM Forms實例在JEE流程中向AEM Forms提交適應性表單：

## 配置您的AEM Forms伺服器{#configure-your-aem-forms-server}

執行以下步驟，使AEM您的Forms伺服器能夠將資料提交到JEE伺服器上的AEM Forms:

1. 轉至AEMhttps://[*host*]&#x200B;的Web配置控制台：[*port*]/system/console/configMgr。

1. 找到並按一下&#x200B;**AdobeLiveCycle客戶端SDK配置**&#x200B;元件。
1. 按一下可編輯JEE伺服器上AEM Forms的配置伺服器URL、用戶名和密碼。
1. 查看設定並按一下&#x200B;**保存**。

![AdobeLiveCycle用戶端SDK組態](assets/clientsdkconfiguration.jpg)

## 使用進程欄位{#map-data-with-process-fields}映射資料

在您的AEM Forms完成配置後，將提交表單中的資料XML和附件映射到AEM Forms的JEE流程欄位。 要執行此操作：

1. 在Web配AEM置控制台中，按一下以編輯&#x200B;**指南LiveCycle流程定位器和發票程式**&#x200B;配置。
1. 指定下列參數：

   * **資料xml參數的名稱** （必填）:指定JEE程式上AEM Forms的XML屬性檔案，該檔案需要處理提交的資料。預設值為&#x200B;**dataxml**。

   * **檔案附件參數的名稱** （可選）:指定JEE上的AEM Forms進程需要處理的文檔對象清單。預設值為&#x200B;**fileAttachmentsList**。

1. 查看設定並按一下&#x200B;**保存**。

![指南LiveCycle流程貨位和發票人](assets/test3.jpg)

配置完成後，「提交到Forms Workflow提交」操作將列出包含指定資料xml參數的JEE伺服器進程上的AEM Forms。
