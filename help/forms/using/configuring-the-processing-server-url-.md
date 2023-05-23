---
title: 配置AEMDS設定
seo-title: Configuring AEM DS settings
description: 在提交表單之前，需要指定處理伺服器URL。
seo-description: You need to specify the processing server URL before you submit a form.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 配置AEMDS設定{#configuring-aem-ds-settings}

本文介紹如何配置 **AEM DS設定服務**。 此設定可用於多個方案，例如：

* 在函件管理中

   * 配置AEM Forms工作流
   * 使用表單門戶遠程保存草稿/提交

* 在自適應表單中，針對從發佈實例提交自適應表單的情況

以下是配置 **[!UICONTROL AEM DS設定]**:

1. 使用URL在發佈實例上開啟Configuration Manager:\
   *https://localhost:port/system/console/configMgr*。

   ![Web控AEM制台配置](assets/web_configuration_console_new.png)

1. 在 **[!UICONTROL Adobe Experience ManagerWeb控制台配置]** ，找到並按一下 **[!UICONTROL AEM DS設定]** 的雙曲餘切值。

   ![DS設定](assets/ds_settings_new.png)

1. 的 **[!UICONTROL AEM DS設定服務]** 窗口顯示DS元件的常AEM用配置設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在相應欄位中添加以下資訊：

   **[!UICONTROL 正在處理伺服器URL]**:處理伺服器是需要觸發Forms或AEM工作流的伺服器。 這可以與作者實例的URL或AEM其他伺服器URL(即https://localhost:port/)相同。

   **[!UICONTROL 正在處理伺服器用戶名]**:工作流用戶的用戶名 [基於正在使用的伺服器URL]

   **[!UICONTROL 正在處理伺服器密碼]**:工作流用戶的密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 在使用Forms或AEM工作流時，在從發佈伺服器提交任何資料之前，必須配置DS設定服務。 否則，報表不予受理。

