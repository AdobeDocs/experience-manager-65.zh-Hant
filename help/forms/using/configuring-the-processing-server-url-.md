---
title: 設定AEM DS設定
seo-title: 設定AEM DS設定
description: 您必須先指定處理伺服器URL，才能送出表單。
seo-description: 您必須先指定處理伺服器URL，才能送出表單。
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 設定AEM DS設定{#configuring-aem-ds-settings}

本文說明如何設定 **AEM DS設定服務**。 此設定可用於多個藍本，例如：

* 在通信管理中

   * 若要設定AEM Forms工作流程
   * 使用表單入口網站遠端儲存草稿／提交

* 在最適化表單中，當從發佈例項提交最適化表單時

以下是設定 **[!UICONTROL AEM DS設定的步驟]**:

1. 使用URL在發佈例項上開啟「設定管理員」:\
   *https://localhost:port/system/console/configMgr*.

   ![AEM Web Console設定](assets/web_configuration_console_new.png)

1. 在「 **[!UICONTROL Adobe Experience Manager Web Console Configuration]** 」視窗中，找到並按一下 **[!UICONTROL 「AEM DS設定」選項]** 。

   ![DS設定](assets/ds_settings_new.png)

1. 「 **[!UICONTROL AEM DS Settings Service]** 」視窗會顯示「AEM DS元件」的常見組態設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在各自的欄位中新增下列資訊：

   **[!UICONTROL 處理伺服器URL]**:「處理伺服器」是需要觸發表單或AEM工作流程的伺服器。 這可以與AEM作者例項的URL或其他伺服器URL(即https://localhost:port/)相同。

   **[!UICONTROL 處理伺服器用戶名]**:根據所使用的伺服器URL, [工作流程使用者的使用者名稱]

   **[!UICONTROL 處理伺服器密碼]**:工作流用戶密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用表單或AEM工作流程時，在您從發佈伺服器提交任何內容之前，必須先設定DS設定服務。 否則，提交表單應當失敗。


