---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---

# 安裝 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | 本文 |

具有管理員存取權的使用者 [!DNL Adobe Experience Manager] 安裝增強型連接器。 安裝之前，請先檢閱平台支援和其他 [連接器的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>* Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。
>
>* Adobe支援增強的連接器1.7.4版及更新版本。 不支援舊版和自訂版本。 若要檢查增強連接器版本，請導覽至 `digital.hoodoo` 群組(位於 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant).
>
>* 請參閱 [Workfront for Experience Manager Assets enhanced connector的合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


要安裝連接器，請執行以下步驟：

1. 從下載連接器 [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [配置防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. 在Dispatcher上，允許名為的HTTP標題 `authorization`, `username`，和 `apikey`. 允許 `GET`, `POST`，和 `PUT` 請求 `/bin/workfront-tools`.
1. 請確定中不存在下列路徑 [!DNL Experience Manager] 存放庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用安裝套件 [!UICONTROL 封裝管理員]. 若要了解如何安裝套件，請參閱 [套件管理器檔案](/help/sites-administering/package-manager.md).
1. 建立 `wf-workfront-users` in [!DNL Experience Manager] 使用者群組並指派權限 `jcr:all` to `/content/dam`.

系統用戶 `workfront-tools` 會自動建立，並自動管理所需的權限。 所有用戶來自 [!DNL Workfront] 使用連接器的使用者會自動新增為此群組的一部分。

## 配置之間的連接 [!DNL Experience Manager] 和 [!DNL Workfront] {#configure-connection}

若要建立與Workfront的連線，請執行下列步驟：

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**.

1. 選擇 `workfront-tools` 在左側面板中，選取 **[!UICONTROL 建立]** 選項。

1. 在 **[!UICONTROL Workfront Connection]** 對話方塊，提供您 [!DNL Workfront] 部署，並選擇 **[!UICONTROL 連線至Workfront]** 選項。 成功連線後， [!DNL Workfront] 檔案自訂整合會自動建立於 [!DNL Workfront] 環境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 若要驗證連線，請在 [!DNL Workfront] 並確認API金鑰相同，且連線相同 **[!UICONTROL 已啟用]**. 若要這麼做，請選取 **[!UICONTROL 設定]** > **[!UICONTROL 檔案]** > **[!UICONTROL 自訂整合]** in [!DNL Workfront].

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets可讓您更新 [!DNL Workfront for Experience Manager enhanced connector] 從舊版轉換為最新版本。

若要更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載最新版的Enhanced Connector [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. 使用安裝套件 [!UICONTROL 封裝管理員]. 若要了解如何安裝套件，請參閱 [套件管理器檔案](/help/sites-administering/package-manager.md).
