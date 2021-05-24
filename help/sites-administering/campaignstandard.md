---
title: 與Adobe Campaign Standard整合
seo-title: 與Adobe Campaign Standard整合
description: 與Adobe Campaign Standard整合。
seo-description: 與Adobe Campaign Standard整合。
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# 與Adobe Campaign Standard整合{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本檔案說明如何將AEM與訂閱式解決方案Adobe Campaign Standard整合。 如果您使用Adobe Campaign 6.1，請參閱[與Adobe Campaign 6.1整合以取得這些指示。](/help/sites-administering/campaignonpremise.md)

Adobe Campaign可讓您直接在Adobe Experience Manager中管理電子郵件傳遞內容和表單。

若要同時使用這兩個解決方案，您必須先將它們設定為彼此連線。 這需要Adobe Campaign和Adobe Experience Manager中的設定步驟。 本檔案詳細說明這些步驟。

在AEM中使用Adobe Campaign包括透過Adobe Campaign傳送電子郵件和表單的功能，相關說明請參閱[使用Adobe Campaign](/help/sites-authoring/campaign.md)。

此外，將AEM與[Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html)整合時，可能會感興趣下列主題：

* [電子郵件範本最佳實務](/help/sites-administering/best-practices-for-email-templates.md)
* [疑難排解Adobe Campaign整合](/help/sites-administering/troubleshooting-campaignintegration.md)

如果您要擴充與Adobe Campaign的整合，可能想查看下列頁面：

* [建立自訂擴充功能](/help/sites-developing/extending-campaign-extensions.md)
* [建立自訂表單對應](/help/sites-developing/extending-campaign-form-mapping.md)

## 配置Adobe Campaign {#configuring-adobe-campaign}

設定Adobe Campaign涉及下列事項：

1. 配置&#x200B;**aemserver**&#x200B;用戶。
1. 建立專用的外部帳戶。
1. 驗證AEMResourceTypeFilter選項。
1. 建立專用的傳遞範本。

>[!NOTE]
>
>若要執行這些操作，您必須在Adobe Campaign中擁有&#x200B;**administration**&#x200B;角色。

### 必備條件 {#prerequisites}

請事先確定您有下列元素：

* [AEM製作例項](/help/sites-deploying/deploy.md#getting-started)
* [AEM發佈例項](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign例項](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>若要讓AEM和Adobe Campaign之間的整合功能正常運作，必須執行[設定Adobe Campaign](#configuring-adobe-campaign)和[設定Adobe Experience Manager](#configuring-adobe-experience-manager)區段中詳述的操作。

### 配置aemserver用戶{#configuring-the-aemserver-user}

**aemserver**&#x200B;使用者必須在Adobe Campaign中設定。 **aemserver**&#x200B;是技術使用者，將用來將AEM伺服器連線至Adobe Campaign。

前往&#x200B;**Administration** > **Users &amp; Security** > **Users**，然後選取&#x200B;**aemserver**&#x200B;使用者。 按一下它以開啟使用者設定。

* 您必須為此用戶設定密碼。 無法透過UI完成此作業。 此配置必須由技術管理員在REST中完成。
* 您可以指派特定角色給此使用者，例如&#x200B;**deliveryPrepare**，讓使用者可建立和編輯傳送。

### 設定Adobe Experience Manager外部帳戶{#configuring-an-adobe-experience-manager-external-account}

您必須設定外部帳戶，讓您將Adobe Campaign連線至AEM執行個體。

>[!NOTE]
>
>在AEM中，請務必為campaign-remote使用者設定密碼。 您必須設定此密碼，才能將Adobe Campaign與AEM連線。 以管理員身分登入，並在使用者管理主控台中，搜尋campaign-remote使用者，然後按一下&#x200B;**設定密碼**。

若要設定AEM外部帳戶：

1. 前往「**管理** > **應用程式設定** > **外部帳戶**」。

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 選取預設的&#x200B;**aemInstance**&#x200B;外部帳戶，或按一下&#x200B;**Create**&#x200B;按鈕建立新帳戶。
1. 在&#x200B;**Type**&#x200B;欄位中選擇&#x200B;**Adobe Experience Manager**，並輸入用於AEM編寫實例的訪問參數：伺服器地址、帳戶名和密碼。

   >[!NOTE]
   >
   >請確定您未在URL結尾新增結尾&#x200B;**/**&#x200B;斜線，否則連線將無法運作。

1. 確認已選取&#x200B;**已啟用**&#x200B;核取方塊，然後按一下&#x200B;**儲存**&#x200B;以儲存您的修改。

### 驗證AEMResourceTypeFilter選項{#verifying-the-aemresourcetypefilter-option}

**AEMResourceTypeFilter**&#x200B;選項用於篩選可在Adobe Campaign中使用的AEM資源類型。 這可讓Adobe Campaign擷取專門設計為僅用於Adobe Campaign的AEM內容。

此選項已預先設定；不過，如果您變更此選項，可能會導致整合無法正常運作。

要驗證&#x200B;**AEMResourceTypeFilter**&#x200B;選項，請配置：

1. 前往「**管理** > **應用程式設定** > **選項**」。
1. 在清單中，您可以確保列出&#x200B;**AEMResourceTypeFilter**&#x200B;選項，並且路徑正確。

### 建立AEM專屬的電子郵件傳送範本{#creating-an-aem-specific-email-delivery-template}

依預設，AEM功能不會在Adobe Campaign的電子郵件範本中啟用。 您可以設定新的電子郵件傳送範本，用於建立包含AEM內容的電子郵件。

若要建立AEM專用的電子郵件傳送範本：

1. 前往「**資源** > **範本** > **傳送範本**」。
1. **按一** 下動作列中的核取標籤並選取現有的標準電子郵件（郵件） **預設範本，然後按一下「複製」圖示並按一下「確** 認」來複製 **** 範本，以啟用 **選取**。
1. 按一下&#x200B;**x**&#x200B;並開啟新建立的&#x200B;**標準電子郵件（郵件）**&#x200B;範本，然後從範本控制面板的動作列選取&#x200B;**編輯屬性**，以停用選取模式。

   您可以修改範本的&#x200B;**Label**。

1. 在屬性&#x200B;**Content**&#x200B;區段中，將&#x200B;**Content source**&#x200B;變更為&#x200B;**Adobe Experience Manager**。 然後選取先前建立的外部帳戶，然後按一下&#x200B;**Confirm**。

   按一下&#x200B;**Confirm**&#x200B;並按一下&#x200B;**Save.**&#x200B;以保存您的修改

   從此範本建立的電子郵件傳送將啟用AEM內容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## 配置Adobe Experience Manager {#configuring-adobe-experience-manager}

若要設定AEM，您必須執行下列動作：

* 在執行個體之間配置復寫。
* 將AEM連線至Adobe Campaign。
* 配置外置程式。

### 配置AEM實例{#configuring-replication-between-aem-instances}之間的複製

從AEM製作例項建立的內容會先傳送至發佈例項。 然後，此發佈執行個體會將內容傳輸至Adobe Campaign。 因此，必須將復寫代理設定為從AEM製作執行個體複製到AEM發佈執行個體。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開的URL，您可以在OSGi(**Tools** > **Web Console** > **OSGi設定> AEM Campaign整合 — 設定**)的下列組態設定中，設定&#x200B;**公用URL**:
**公用URL:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

若要將某些製作執行個體設定複製到發佈執行個體，也必須執行此步驟。

要配置AEM實例之間的複製：

1. 從創作實例中，選擇&#x200B;**AEM logo**> **Tools** > **Deployment** > **Replication** > **Agent on author**，然後按一下&#x200B;**Default Agent**。

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   設定與Adobe Campaign的整合時，除非發佈和製作例項都位於同一部電腦上，否則請避免使用localhost(這是AEM的本機副本)。

1. 按一下「**編輯**」，然後選擇「**傳輸**」頁簽。
1. 使用IP地址或AEM發佈實例的地址替換&#x200B;**localhost**&#x200B;以配置URI。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 將AEM連接到Adobe Campaign {#connecting-aem-to-adobe-campaign}

您必須先建立兩個解決方案之間的連結，才能同時使用AEM和Adobe Campaign。

1. 連線至您的AEM製作執行個體。
1. 選擇&#x200B;**工具** > **操作** > **雲** > **Cloud Services**，然後在Adobe Campaign區中選擇&#x200B;**立即配置**。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 輸入&#x200B;**Title**&#x200B;並按一下&#x200B;**Create**，或選擇您要連結至Adobe Campaign例項的現有設定，以建立新設定。
1. 編輯設定，使其與Adobe Campaign執行個體的參數相符。

   * **使用者名稱**: **aemserver**，此為Adobe Campaign AEM整合套件運算子，用於建立兩個解決方案之間的連結。
   * **密碼**:Adobe Campaign aemserver運算子密碼。您可能必須直接在Adobe Campaign中重新指定此運算子的密碼。
   * **API端點**:Adobe Campaign例項URL。

1. 選擇&#x200B;**連接到Adobe Campaign**，然後按一下&#x200B;**確定**。

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   在您[建立電子郵件並發佈後，您需要將設定重新發佈至您的發佈執行個體。](/help/sites-authoring/campaign.md)

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果連線失敗，請務必檢查下列項目：
* 使用安全連線至Adobe Campaign例項(https)時，您可能會遇到憑證問題。 您必須將Adobe Campaign執行個體憑證新增至JDK的**cacerts **檔案。
* 此外，請參閱[疑難排解AEM/Adobe Campaign整合](/help/sites-administering/troubleshooting-campaignintegration.md)。



### 配置外置程式{#configuring-the-externalizer}

您需要在製作例項的AEM中[設定外部化程式](/help/sites-developing/externalizer.md)。 Externalizer是OSGi服務，可讓您將資源路徑轉換為外部和絕對URL。 此服務提供設定這些外部URL和建置這些URL的集中位置。

有關一般說明，請參閱[配置外部化程式](/help/sites-developing/externalizer.md)。 針對Adobe Campaign整合，請務必在`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`設定發佈伺服器，其不指向`localhost:4503`，而是指向可透過Adobe Campaign主控台存取的伺服器。

如果指向`localhost:4503`或Adobe Campaign無法觸及的其他伺服器，您的影像將不會顯示在Adobe Campaign主控台上。

![chlimage_1-131](assets/chlimage_1-131a.png)
