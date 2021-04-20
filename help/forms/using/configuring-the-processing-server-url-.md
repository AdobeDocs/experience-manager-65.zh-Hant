---
title: 配置AEMDS設定
seo-title: 配置AEMDS設定
description: 您必須先指定處理伺服器URL，才能送出表單。
seo-description: 您必須先指定處理伺服器URL，才能送出表單。
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 配置AEMDS設定{#configuring-aem-ds-settings}

本文介紹如何配置&#x200B;**AEM DS Settings Service**。 此設定可用於多個藍本，例如：

* 在通信管理中

   * 用於配置AEM Forms工作流
   * 使用表單入口網站遠端儲存草稿／提交

* 在最適化表單中，當從發佈例項提交最適化表單時

以下是配置&#x200B;**[!UICONTROL AEM DS Settings]**&#x200B;的步驟：

1. 使用URL在發佈例項上開啟「設定管理員」:\
   *https://localhost:port/system/console/configMgr*.

   ![Web控AEM制台配置](assets/web_configuration_console_new.png)

1. 在&#x200B;**[!UICONTROL Adobe Experience ManagerWeb控制台配置]**&#x200B;窗口中，找到並按一下&#x200B;**[!UICONTROL AEM DS設定]**&#x200B;選項。

   ![DS設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS Settings Service]**&#x200B;窗口顯示DS元件的常用配AEM置設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在各自的欄位中新增下列資訊：

   **[!UICONTROL 處理伺服器URL]**:處理伺服器是需要觸發Forms或AEM工作流程的伺服器。這可以與作者例項的URL或AEM其他伺服器URL(即https://localhost:port/)相同。

   **[!UICONTROL 處理伺服器用戶名]**:根據所使用的伺服器URL, [工作流程使用者的使用者名稱]

   **[!UICONTROL 處理伺服器密碼]**:工作流用戶密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用Forms或工AEM作流程時，在從發佈伺服器提交任何內容之前，必須先設定DS設定服務。 否則，提交表單應當失敗。


