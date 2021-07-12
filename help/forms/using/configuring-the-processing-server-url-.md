---
title: 配置AEM DS設定
seo-title: 配置AEM DS設定
description: 提交表單之前，您必須指定處理伺服器URL。
seo-description: 提交表單之前，您必須指定處理伺服器URL。
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
source-wordcount: '258'
ht-degree: 0%

---

# 配置AEM DS設定{#configuring-aem-ds-settings}

本文說明如何配置&#x200B;**AEM DS設定服務**。 此設定可用於多個案例，例如：

* 在通信管理中

   * 用於設定AEM Forms工作流程
   * 使用表單入口網站遠端儲存草稿/提交

* 在適用性表單中，適用於從發佈例項提交適用性表單的案例

以下是配置&#x200B;**[!UICONTROL AEM DS設定]**&#x200B;的步驟：

1. 使用URL在發佈執行個體上開啟Configuration Manager:\
   *https://localhost:port/system/console/configMgr*.

   ![AEM Web主控台設定](assets/web_configuration_console_new.png)

1. 在&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;窗口中，找到並按一下&#x200B;**[!UICONTROL AEM DS設定]**&#x200B;選項。

   ![DS設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS設定服務]**&#x200B;窗口顯示AEM DS元件的常見配置設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在個別欄位中新增下列資訊：

   **[!UICONTROL 處理伺服器URL]**:處理伺服器是需要觸發Forms或AEM工作流程的伺服器。這可以與AEM製作例項的URL或其他伺服器URL(即https://localhost:port/)相同。

   **[!UICONTROL 正在處理伺服器用戶名]**:工作流程使用者的 [使用者名稱（根據使用的伺服器URL）]

   **[!UICONTROL 處理伺服器密碼]**:工作流用戶密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用Forms或AEM工作流程時，必須先設定DS設定服務，才能從發佈伺服器提交。 否則，提交表格應當失敗。



