---
title: 與Adobe Campaign Standard整合
seo-title: Integrating with Adobe Campaign Standard
description: 與Adobe Campaign Standard整合。
seo-description: Integrating with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# 與Adobe Campaign Standard整合{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本檔案說明如何將AEM與訂閱式解決方案Adobe Campaign Standard整合。 如果您使用Adobe Campaign 6.1，請參閱 [與Adobe Campaign 6.1整合](/help/sites-administering/campaignonpremise.md) 以取得指示。

Adobe Campaign可讓您直接在Adobe Experience Manager中管理電子郵件傳遞內容和表單。

若要同時使用這兩個解決方案，您必須先將它們設定為彼此連線。 這需要Adobe Campaign和Adobe Experience Manager中的設定步驟。 本檔案詳細說明這些步驟。

在AEM中使用Adobe Campaign包含透過Adobe Campaign傳送電子郵件和表單的功能，相關說明請參閱 [使用Adobe Campaign](/help/sites-authoring/campaign.md).

此外，將AEM與 [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [電子郵件範本最佳實務](/help/sites-administering/best-practices-for-email-templates.md)
* [疑難排解Adobe Campaign整合](/help/sites-administering/troubleshooting-campaignintegration.md)

如果您要擴充與Adobe Campaign的整合，可能想查看下列頁面：

* [建立自訂擴充功能](/help/sites-developing/extending-campaign-extensions.md)
* [建立自訂表單對應](/help/sites-developing/extending-campaign-form-mapping.md)

## 設定Adobe Campaign {#configuring-adobe-campaign}

設定Adobe Campaign涉及下列事項：

1. 設定 **aemserver** 使用者。
1. 建立專用的外部帳戶。
1. 驗證AEMResourceTypeFilter選項。
1. 建立專用的傳遞範本。

>[!NOTE]
>
>若要執行這些操作，您必須具備 **管理** 在Adobe Campaign。

### 必備條件 {#prerequisites}

請事先確定您有下列元素：

* [AEM製作例項](/help/sites-deploying/deploy.md#getting-started)
* [AEM發佈例項](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign例項](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>操作詳見 [設定Adobe Campaign](#configuring-adobe-campaign) 和 [設定Adobe Experience Manager](#configuring-adobe-experience-manager) AEM和Adobe Campaign之間的整合功能必須有章節才能正常運作。

### 配置aemserver用戶 {#configuring-the-aemserver-user}

此 **aemserver** 必須在Adobe Campaign中設定使用者。 此 **aemserver** 是技術使用者，將用來將AEM伺服器連線至Adobe Campaign。

前往 **管理** >  **使用者與安全性** >  **使用者**，然後選取 **aemserver** 使用者。 按一下它以開啟使用者設定。

* 您必須為此用戶設定密碼。 無法透過UI完成此作業。 此配置必須由技術管理員在REST中完成。
* 您可以指派特定角色給此使用者，例如 **deliveryPrepare**，可讓使用者建立和編輯傳送。

### 設定Adobe Experience Manager外部帳戶 {#configuring-an-adobe-experience-manager-external-account}

您必須設定外部帳戶，讓您將Adobe Campaign連線至AEM執行個體。

>[!NOTE]
>
>在AEM中，請務必為campaign-remote使用者設定密碼。 您必須設定此密碼，才能將Adobe Campaign與AEM連線。 以管理員身分登入，並在使用者管理主控台中，搜尋campaign-remote使用者，然後按一下 **設定密碼**.

若要設定AEM外部帳戶：

1. 前往 **管理** > **應用程式設定** > **外部帳戶**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 選取預設值 **aemInstance** 外部帳戶，或按一下 **建立** 按鈕。
1. 選擇 **Adobe Experience Manager** i **類型** 欄位，然後輸入用於AEM製作執行個體的存取參數：伺服器地址、帳戶名和密碼。

   >[!NOTE]
   >
   >請確定您未新增結尾 **/** URL或連線結尾的斜線將無法運作。

1. 請確定 **已啟用** 核取方塊，然後按一下 **儲存** 以儲存您的修改。

### 驗證AEMResourceTypeFilter選項 {#verifying-the-aemresourcetypefilter-option}

此 **AEMResourceTypeFilter** 選項可用來篩選可在Adobe Campaign中使用的AEM資源類型。 這可讓Adobe Campaign擷取專門設計為僅用於Adobe Campaign的AEM內容。

此選項已預先設定；不過，如果您變更此選項，可能會導致整合無法正常運作。

驗證 **AEMResourceTypeFilter** 選項：

1. 前往 **管理** > **應用程式設定** > **選項**.
1. 在清單中，您可以確定 **AEMResourceTypeFilter** 選項，且路徑正確。

### 建立AEM專屬的電子郵件傳送範本 {#creating-an-aem-specific-email-delivery-template}

依預設，AEM功能不會在Adobe Campaign的電子郵件範本中啟用。 您可以設定新的電子郵件傳送範本，用於建立包含AEM內容的電子郵件。

若要建立AEM專用的電子郵件傳送範本：

1. 前往 **資源** > **範本** > **傳遞範本**.
1. **啟用選擇** 按一下動作列中的核取記號並選取現有 **標準電子郵件（郵件）** 預設範本，然後按一下 **複製** 表徵圖 **確認**.
1. 按一下 **x** 並開啟新建立的 **標準電子郵件（郵件）的副本** 範本，然後選取 **編輯屬性** 從範本控制面板的動作列。

   您可以修改範本的 **標籤**.

1. 在屬性中 **內容** 區段，更改 **內容來源** to **Adobe Experience Manager**. 然後選取先前建立的外部帳戶，然後按一下 **確認**.

   按一下以儲存您的修改 **確認** 按一下 **儲存。**

   從此範本建立的電子郵件傳送將啟用AEM內容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## 設定Adobe Experience Manager {#configuring-adobe-experience-manager}

若要設定AEM，您必須執行下列動作：

* 在執行個體之間配置復寫。
* 將AEM連線至Adobe Campaign。
* 配置外置程式。

### 在AEM例項之間設定復寫 {#configuring-replication-between-aem-instances}

從AEM製作例項建立的內容會先傳送至發佈例項。 然後，此發佈執行個體會將內容傳輸至Adobe Campaign。 因此，必須將復寫代理設定為從AEM製作執行個體複製到AEM發佈執行個體。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開的URL，您可以設定 **公用URL** 在OSGi的下列組態設定中(**工具** > **Web主控台** > **OSGi設定> AEM Campaign整合 — 設定**):
**公用URL:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

若要將某些製作執行個體設定複製到發佈執行個體，也必須執行此步驟。

要配置AEM實例之間的複製：

1. 在製作例項中，選取 **AEM標誌**> **工具** > **部署** > **復寫** > **作者代理**，然後按一下 **預設代理**.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   設定與Adobe Campaign的整合時，除非發佈和製作例項都位於同一部電腦上，否則請避免使用localhost(這是AEM的本機副本)。

1. 按一下 **編輯** 然後選取 **運輸** 標籤。
1. 通過替換 **localhost** 填入AEM發佈執行個體的IP位址或位址。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 將AEM連線至Adobe Campaign {#connecting-aem-to-adobe-campaign}

您必須先建立兩個解決方案之間的連結，才能同時使用AEM和Adobe Campaign。

1. 連線至您的AEM製作執行個體。
1. 選擇 **工具** > **操作** > **雲** > **Cloud Services**，然後 **立即配置** 在Adobe Campaign區段。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 輸入 **標題** 按一下 **建立**，或選擇您要連結至Adobe Campaign例項的現有設定。
1. 編輯設定，使其與Adobe Campaign執行個體的參數相符。

   * **使用者名稱**: **aemserver**，即Adobe Campaign AEM整合套件運算子，用來建立兩個解決方案之間的連結。
   * **密碼**:Adobe Campaign aemserver運算子密碼。 您可能必須直接在Adobe Campaign中重新指定此運算子的密碼。
   * **API端點**:Adobe Campaign例項URL。

1. 選擇 **連線至Adobe Campaign** 按一下 **確定**.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   在 [建立您的電子郵件並發佈](/help/sites-authoring/campaign.md)，您必須將設定重新發佈至您的發佈執行個體。

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果連線失敗，請務必檢查下列項目：
* 使用安全連線至Adobe Campaign例項(https)時，您可能會遇到憑證問題。 您必須將Adobe Campaign執行個體憑證新增至JDK的**cacerts **檔案。
* 此外，請參閱 [疑難排解AEM/Adobe Campaign整合](/help/sites-administering/troubleshooting-campaignintegration.md).
>


### 配置外置程式 {#configuring-the-externalizer}

您需要 [配置externalizer](/help/sites-developing/externalizer.md) 在AEM中。 Externalizer是OSGi服務，可讓您將資源路徑轉換為外部和絕對URL。 此服務提供設定這些外部URL和建置這些URL的集中位置。

請參閱 [配置外置程式](/help/sites-developing/externalizer.md) 一般說明。 若為Adobe Campaign整合，請務必在 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` 未指向 `localhost:4503` 但傳送至可透過Adobe Campaign主控台存取的伺服器。

如果指向 `localhost:4503` 或Adobe Campaign無法存取的其他伺服器，您的影像將不會顯示在Adobe Campaign主控台上。

![chlimage_1-131](assets/chlimage_1-131a.png)
