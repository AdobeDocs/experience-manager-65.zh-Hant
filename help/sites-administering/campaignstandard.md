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
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e

---


# 與Adobe Campaign Standard整合{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本檔案說明如何將AEM與訂閱型解決方案Adobe Campaign Standard整合。 如果您使用Adobe Campaign 6.1，請參閱 [與Adobe Campaign 6.1整合](/help/sites-administering/campaignonpremise.md) ，以取得這些指示。

Adobe Campaign可讓您直接在Adobe Experience manager中管理電子郵件傳送內容和表單。

要同時使用這兩種解決方案，您必須先將它們配置為彼此連接。 這包括Adobe Campaign和Adobe Experience manager中的設定步驟。 本檔案將詳細說明這些步驟。

在AEM中使用Adobe Campaign包括透過Adobe Campaign傳送電子郵件和表單的功能，如「使用Adobe Campaign」 [一文所述](/help/sites-authoring/campaign.md)。

此外，在整合AEM與 [Adobe Campaign時，可能會關注下列主題](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [電子郵件範本的最佳做法](/help/sites-administering/best-practices-for-email-templates.md)
* [疑難排解您的Adobe Campaign整合](/help/sites-administering/troubleshooting-campaignintegration.md)

如果您要延伸與Adobe Campaign的整合，您可能想要查看下列頁面：

* [建立自訂擴充功能](/help/sites-developing/extending-campaign-extensions.md)
* [建立自訂表單映射](/help/sites-developing/extending-campaign-form-mapping.md)

## 設定Adobe Campaign {#configuring-adobe-campaign}

設定Adobe Campaign涉及下列事項：

1. 配置 **aemserver** 用戶。
1. 建立專屬的外部帳戶。
1. 驗證AEMResourceTypeFilter選項。
1. 建立專用的傳送範本。

>[!NOTE]
>
>若要執行這些作業，您必須在Adobe Campaign中 **擔任** 管理角色。

### 必備條件 {#prerequisites}

請務必事先具備下列元素：

* [AEM製作實例](/help/sites-deploying/deploy.md#getting-started)
* [AEM發佈例項](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign例項](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>AEM與Adobe Campaign之間 [的整合功能必須具備設定](#configuring-adobe-campaign) Adobe Campaign [和設定Adobe Experience Manager](#configuring-adobe-experience-manager) 章節中詳述的操作，才能正常運作。

### 配置aemserver用戶 {#configuring-the-aemserver-user}

Aemserver **使用者** ，必須在Adobe Campaign中設定。 The **aemserver** is a technical user, will be used to connect the AEM server to Adobe Campaign.

前往「管 **理** >使用者與安 **全性** >使用 **者**」，並選 **** 取Aemserver User。 按一下以開啟使用者設定。

* 您必須為此用戶設定密碼。 這無法透過UI完成。 此配置必須由技術管理員在REST中完成。
* 您可以指派特定角色給此使用者，例如 **deliveryPrepare**，讓使用者可建立和編輯傳送。

### 設定Adobe Experience manager外部帳戶 {#configuring-an-adobe-experience-manager-external-account}

您必須設定外部帳戶，以便將Adobe Campaign連線至您的AEM例項。

>[!NOTE]
>
>在AEM中，請確定您已設定促銷活動遠端使用者的密碼。 您必須設定此密碼，才能將Adobe Campaign與AEM連線。 以管理員身分登入，並在使用者管理主控台中搜尋促銷活動遠端使用者，然後按一下「設 **定密碼」**。

若要設定AEM外部帳戶：

1. 前往「管 **理** >應用程 **式設定** >外 **部帳戶」**。

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 選取預設 **aemInstance** 外部帳戶，或按一下「建立」按 **鈕建立新帳戶** 。
1. 在「類 **型**」欄位中選 **取「Adobe Experience Manager** 」，並輸入用於AEM製作例項的存取參數：伺服器位址、帳戶名稱和密碼。

   >[!NOTE]
   >
   >請確定您未在URL結尾加 **入結** 尾／斜線，否則連線將無法運作。

1. 請確定已選取「 **啟用** 」核取方塊，然後按一下「 **儲存** 」以儲存您的修改。

### 驗證AEMResourceTypeFilter選項 {#verifying-the-aemresourcetypefilter-option}

AEMResourceTypeFilter **** 選項可用來篩選可用於Adobe Campaign的AEM資源類型。 這可讓Adobe Campaign擷取專門設計為僅用於Adobe Campaign的AEM內容。

此選項已預先設定；不過，如果您變更此選項，可能會導致無法運作的整合。

要驗證 **AEMResourceTypeFilter** 選項是否已配置：

1. 前往「管 **理** >應用程 **式設定** >選 **項**」。
1. 在清單中，您可以確保列 **出AEMResourceTypeFilter** 選項，並確保路徑正確。

### 建立AEM專用的電子郵件傳送範本 {#creating-an-aem-specific-email-delivery-template}

依預設，Adobe Campaign的電子郵件範本中未啟用AEM功能。 您可以設定新的電子郵件傳送範本，以便用來建立包含AEM內容的電子郵件。

若要建立AEM專用的電子郵件傳送範本：

1. 前往「 **資源** >范 **本** > **傳送範本**」。
1. **按一下** 「動作列」中的核取標籤，並選取現有的 **Standard電子郵件（郵件）** ，然後按一下「複製」圖示並按一下「確認」，以啟用選取範圍 ********。
1. 按一下 **x** ，並開啟新建立的標準電子郵件（郵件） **「復本」範本，然後從範本控制面板的動作列選取「編輯屬性****** 」，以停用選取模式。

   您可以修改範本的標 **簽**。

1. 在「內容 **」區段** ，將「內容」 **來源變更為****Adobe Experience Manager**。 然後選取先前建立的外部帳戶，然後按一下「 **確認**」。

   按一下「確認」並按一 **下「儲存** 」，以儲 **存您的修改。**

   根據此範本建立的電子郵件傳送將啟用AEM內容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## 設定Adobe Experience Manager {#configuring-adobe-experience-manager}

若要設定AEM，您必須執行下列動作：

* 配置實例之間的複製。
* 將AEM連線至Adobe Campaign。
* 設定外部化器。

### 在AEM例項間設定複製 {#configuring-replication-between-aem-instances}

從AEM製作例項建立的內容會先傳送至發佈例項。 然後，此發佈例項會將內容傳輸至Adobe Campaign。 因此，必須將複製代理設定為從AEM製作例項複製至AEM發佈例項。

>[!NOTE]
>
>如果您不想使用複製URL，而是使用公開對應的URL，您可以在OSGi( **Tools** >**Web Console** > **OSGi Configuration > AEM Campaign Integration - Configuration Contegration)中的下列組態設定中設定** Public URL ****:
**** 公開URL:com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

此步驟也是將特定編寫執行個體組態複製至發佈執行個體的必要步驟。

若要在AEM例項之間設定複製：

1. 從實例中，選擇 **AEM**> **Tools **icon > **Deployment** Replication **Agents********** on authoring，然後按一下Adobe Agent的預設標誌Default Agent。

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   在設定與Adobe Campaign的整合時，請避免使用localhost（這是AEM的本機副本），除非發佈和作者實例都位於同一部電腦上。

1. 按一 **下「編輯** 」，然後選 **取「傳輸** 」標籤。
1. 以IP位址或AEM發佈 **例項的位址** ，取代localhost，以設定URI。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 將AEM連線至Adobe Campaign {#connecting-aem-to-adobe-campaign}

您必須先建立兩個解決方案之間的連結，才能搭配使用AEM和Adobe Campaign。

1. 連線至您的AEM製作實例。
1. 選擇 **>** > **Operations** > **Cloud** > cloud服務，然後 ******** 選擇Adobe促銷活動中的Configure Cloud Services Now。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 輸入「標題 **」並按一下「** 建立 ****」，或選擇您要連結至Adobe Campaign例項的現有設定，以建立新的設定。
1. 編輯設定，使其符合您Adobe Campaign例項的參數。

   * **使用者名稱**:Aemserver ****,Adobe Campaign AEM整合套件運算子，用來建立兩個解決方案之間的連結。
   * **密碼**:Adobe Campaign aemserver運算子密碼。 您可能必須直接在Adobe Campaign中重新指定此運算子的密碼。
   * **API端點**:Adobe Campaign例項URL。

1. 選取 **連線至Adobe Campaign** ，然後按一 **下確定**。

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   建立電 [子郵件並發佈後](/help/sites-authoring/campaign.md)，您需要將設定重新發佈至發佈例項。

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果連線失敗，請務必勾選下列項目：
* 使用Adobe Campaign例項(https)的安全連線時，可能會遇到憑證問題。 您必須將Adobe Campaign例項憑證新增至JDK的**cacerts **檔案。
* 此外，請參閱「 [疑難排解您的AEM/Adobe Campaign整合」](/help/sites-administering/troubleshooting-campaignintegration.md)。



### 設定外部化器 {#configuring-the-externalizer}

您必須在 [您的作者例項上](/help/sites-developing/externalizer.md) ，在AEM中設定externalizer。 Externalizer是OSGi服務，可讓您將資源路徑轉換為外部和絕對URL。 此服務提供一個集中位置，以設定這些外部URL並建立這些URL。

如需 [一般指示，請參閱](/help/sites-developing/externalizer.md) Configure the externalizer。 若是Adobe Campaign整合，請務必在Adobe Campaign主控台可 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` 存取的伺服器 `localhost:4503` 上設定發佈伺服器，但不要指向。

如果指向Adobe Campaign `localhost:4503` 無法觸及的其他伺服器，您的影像將不會顯示在Adobe Campaign主控台上。

![chlimage_1-131](assets/chlimage_1-131a.png)

