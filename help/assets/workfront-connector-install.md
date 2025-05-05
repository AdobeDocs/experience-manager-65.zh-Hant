---
title: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
description: 安裝 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# 安裝[!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

在[!DNL Adobe Experience Manager]中擁有管理員存取許可權的使用者會安裝增強型聯結器。 安裝之前，請先檢閱平台支援和聯結器[&#128279;](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)的其他必要條件。

>[!IMPORTANT]
>
>* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署和設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
>
>* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請瀏覽至[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)左側窗格中可用的`digital.hoodoo`群組。
>
>* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

若要安裝聯結器，請遵循下列步驟：

1. 從[[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下載聯結器。
1. [設定防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。
1. 在Dispatcher上，允許名為`authorization`、`username`和`apikey`的HTTP標頭。 允許`GET`、`POST`和`PUT`要求傳送給`/bin/workfront-tools`。
1. 確定[!DNL Experience Manager]存放庫中不存在下列路徑：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用[!UICONTROL 封裝管理員]安裝封裝。 若要瞭解如何安裝封裝，請參閱[封裝管理員檔案](/help/sites-administering/package-manager.md)。
1. 在[!DNL Experience Manager]使用者群組中建立`wf-workfront-users`並將許可權`jcr:all`指派給`/content/dam`。
1. 新增自訂屬性至&#x200B;**`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**&#x200B;的現成索引定義。 執行以下步驟：
   * 將名為&#x200B;**`wfReferenceNumber`**&#x200B;的&#x200B;**`nt:unstructured`**&#x200B;屬性新增至：

     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`。
   * 將重新索引旗標翻轉到`true`來重新索引`index /oak:index/ntFolderDamLucene`。

系統使用者`workfront-tools`會自動建立，且必要的許可權會自動管理。 來自[!DNL Workfront]且使用聯結器的所有使用者都會自動新增為此群組的一部分。

## 設定[!DNL Experience Manager]與[!DNL Workfront]之間的連線 {#configure-connection}

若要建立與Workfront的連線，請遵循下列步驟：

1. 在[!DNL Experience Manager]中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具組態]**。

1. 在左側面板中選取`workfront-tools`，然後在頁面的右上角區域選取&#x200B;**[!UICONTROL 建立]**&#x200B;選項。

1. 在&#x200B;**[!UICONTROL Workfront連線]**&#x200B;對話方塊中，提供您[!DNL Workfront]部署的必要詳細資料，並選取&#x200B;**[!UICONTROL 連線至Workfront]**&#x200B;選項。 成功連線後，[!DNL Workfront]檔案自訂整合會在[!DNL Workfront]環境中自動建立。

   ![連線[!DNL Experience Manager]和[!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 若要驗證連線，請在[!DNL Workfront]中存取該連線，並驗證API金鑰是否相同，以及連線是否為&#x200B;**[!UICONTROL 已啟用]**。 若要這麼做，請在[!DNL Workfront]中選取&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 檔案]** > **[!UICONTROL 自訂整合]**。

## 更新[!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets可讓您將[!DNL Workfront for Experience Manager enhanced connector]從舊版更新至最新版本。

若要將[!DNL Workfront for Experience Manager enhanced connector]更新至最新版本：

1. 從[[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下載最新版本的增強型聯結器。
1. 使用[!UICONTROL 封裝管理員]安裝封裝。 若要瞭解如何安裝封裝，請參閱[封裝管理員檔案](/help/sites-administering/package-manager.md)。
