---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: a589836c77fd919838dce60a1eaf676683c165c0
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有管理員訪問權限的用戶 [!DNL Adobe Experience Manager] 安裝增強的連接器。 安裝前，請查看平台支援和其他 [連接器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

>[!TIP]
>
>您是否在 [!DNL Workfront for Experience Manager enhanced connector] as a Cloud ServiceAEM文檔？ 按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en)。

>[!IMPORTANT]
>
>Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅通過認證合作夥伴或 [!DNL Adobe Professional Services]。 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services]，它不受Adobe支援。
>
>Adobe可以發佈更新 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使這個連接器冗餘；如果發生這種情況，可能需要客戶從使用此連接器進行過渡。

要安裝連接器，請執行以下步驟：

1. 從下載連接器 [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)。

1. [配置防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。

1. 在調度程式上，允許HTTP標頭命名 `authorization`。 `username`, `apikey`。 允許 `GET`。 `POST`, `PUT` 請求 `/bin/workfront-tools`。

1. 確保中不存在以下路徑 [!DNL Experience Manager] 儲存庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用 [!UICONTROL 包管理器]。 要瞭解如何安裝軟體包，請參見 [包管理器文檔](/help/sites-administering/package-manager.md)。

1. 建立 `wf-workfront-users` 在 [!DNL Experience Manager] 用戶組並分配權限 `jcr:all` 至 `/content/dam`。

系統用戶 `workfront-tools` 自動建立，並自動管理所需權限。 所有用戶 [!DNL Workfront] 使用連接器的用戶將自動添加為此組的一部分。

## 配置之間的連接 [!DNL Experience Manager] 和 [!DNL Workfront] {#configure-connection}

要建立與Workfront的連接，請執行以下步驟：

1. 在 [!DNL Experience Manager]選中 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**。

1. 選擇 `workfront-tools` 在左面板中，然後選擇 **[!UICONTROL 建立]** 的上界。

1. 在 **[!UICONTROL Workfront]** 對話框，提供所需的詳細資訊 [!DNL Workfront] 部署，然後選擇 **[!UICONTROL 連接到Workfront]** 的雙曲餘切值。 成功連接後， [!DNL Workfront] 文檔自定義整合在 [!DNL Workfront] 環境。

   ![連接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 要驗證連接，請訪問 [!DNL Workfront] 並驗證API鍵是否相同且連接是 **[!UICONTROL 已啟用]**。 要執行此操作，請選擇 **[!UICONTROL 設定]** > **[!UICONTROL 文檔]** > **[!UICONTROL 自定義整合]** 在 [!DNL Workfront]。

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets使您能夠 [!DNL Workfront for Experience Manager enhanced connector] 從上一版本到最新版本。

更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載增強連接器的最新版本 [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)。

1. 使用 [!UICONTROL 包管理器]。 要瞭解如何安裝軟體包，請參見 [包管理器文檔](/help/sites-administering/package-manager.md)。


