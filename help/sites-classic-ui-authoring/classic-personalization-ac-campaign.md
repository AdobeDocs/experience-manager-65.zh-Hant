---
title: 協作使用Adobe Campaign 6.1和Adobe Campaign Standard
seo-title: 協作使用Adobe Campaign 6.1和Adobe Campaign Standard
description: 您可以在AEM中建立電子郵件內容，並在Adobe Campaign電子郵件中處理。
seo-description: 您可以在AEM中建立電子郵件內容，並在Adobe Campaign電子郵件中處理。
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---

# 使用Adobe Campaign 6.1和Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

您可以在AEM中建立電子郵件內容，並在Adobe Campaign電子郵件中處理。 要執行此操作，您必須：

1. 從Adobe Campaign專用範本在AEM中建立新電子報。
1. 在編輯內容以存取所有功能之前，請選取[Adobe Campaign服務](#selectingtheadobecampaigncloudservice)。
1. 編輯內容。
1. 驗證內容。

然後，內容便可在Adobe Campaign中與傳送同步。 本檔案將詳細說明。

>[!NOTE]
>
>您必須先將AEM設定為與[Adobe Campaign](/help/sites-administering/campaignonpremise.md)或[Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)整合，才能使用此功能。

## 透過Adobe Campaign傳送電子郵件內容{#sending-email-content-via-adobe-campaign}

設定AEM和Adobe Campaign後，您可以直接在AEM中建立電子郵件傳送內容，然後在Adobe Campaign中處理。

您在AEM中建立Adobe Campaign內容時，必須先連結至Adobe Campaign服務，才能編輯內容以存取所有功能。

可能有兩種情況：

* 內容可與來自Adobe Campaign的傳送同步。 這可讓您在傳遞中使用AEM內容。
* (僅限Adobe Campaign內部部署)內容可直接傳送至Adobe Campaign，而自動產生新的電子郵件傳送。 此模式有其限制。

本檔案將詳細說明。

### 建立新電子郵件內容{#creating-new-email-content}

>[!NOTE]
>
>新增電子郵件範本時，請務必在&#x200B;**/content/campaigns**&#x200B;下新增範本，以便使用。


1. 在AEM中，選取&#x200B;**Websites**&#x200B;資料夾，然後瀏覽您的瀏覽器，以尋找管理電子郵件促銷活動的位置。 在以下範例中，相關節點為&#x200B;**網站** > **促銷活動** > **Geometrixx Outdoors** > **電子郵件促銷活動**。

   >[!NOTE]
   >
   >[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md#weretail)。請從「封裝共用」下載Geometrixx內容範例。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. 選擇「**新建** > **新建頁面**」以建立新的電子郵件內容。
1. 選取Adobe Campaign專用的其中一個可用範本，然後填入頁面的一般屬性。 預設提供三個範本：

   * **Adobe Campaign電子郵件(AC 6.1)**:可讓您先將內容新增至預先定義的範本，再將其傳送至Adobe Campaign 6.1進行傳送。
   * **Adobe Campaign電子郵件(ACS)**:可讓您先將內容新增至預先定義的範本，再將其傳送至Adobe Campaign Standard進行傳送。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 按一下&#x200B;**建立**&#x200B;以建立電子郵件或電子報。

### 選取Adobe Campaign雲端服務與範本{#selecting-the-adobe-campaign-cloud-service-and-template}

若要與Adobe Campaign整合，您必須將Adobe Campaign雲端服務新增至頁面。 這麼做可讓您存取個人化和其他Adobe Campaign資訊。

此外，您可能還需要選取Adobe Campaign範本並變更主旨，以及為不會以HTML檢視電子郵件的使用者新增純文字內容。

1. 在sidekick中選擇&#x200B;**Page**&#x200B;頁簽，然後選擇&#x200B;**Page properties.**
1. 在快顯視窗的&#x200B;**雲端服務**&#x200B;標籤中，選取&#x200B;**新增服務**&#x200B;以新增Adobe Campaign服務，然後按一下&#x200B;**確定**。

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 從下拉式清單中選取符合您Adobe Campaign例項的設定，然後按一下&#x200B;**確定**。

   >[!NOTE]
   >
   >新增雲端服務後，請務必點選/按一下「**確定**」或「**套用**」。 這可讓&#x200B;**Adobe Campaign**&#x200B;標籤正常運作。

1. 如果要套用預設&#x200B;**mail**&#x200B;範本以外的特定電子郵件傳送範本(來自Adobe Campaign)，請再次選取&#x200B;**頁面屬性**。 在&#x200B;**Adobe Campaign**&#x200B;標籤中，在相關Adobe Campaign例項中輸入電子郵件傳送範本的內部名稱。

   在Adobe Campaign Standard中，範本為&#x200B;**透過AEM內容傳送**。 在Adobe Campaign 6.1中，範本為&#x200B;**具有AEM內容的電子郵件傳送**。

   選取範本時，AEM會自動啟用&#x200B;**Adobe Campaign電子報**&#x200B;元件。

### 編輯電子郵件內容{#editing-email-content}

您可以在傳統使用者介面或觸控最佳化使用者介面中編輯電子郵件內容。

1. 通過從工具箱中選擇&#x200B;**Page properties** > **Email**，輸入電子郵件的主題和文本版本。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 從sidekick中可用的元素新增您想要的元素，以編輯電子郵件內容。 要執行此操作，請拖放它們。 然後連按兩下您要編輯的元素。

   例如，您可以新增包含個人化欄位的文字。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   如需Adobe Campaign電子報/電子郵件促銷活動可用元件的說明，請參閱[Adobe Campaign元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 插入個人化{#inserting-personalization}

編輯內容時，您可以插入：

* Adobe Campaign內容欄位。 這些欄位可插入在您的文字中，並會根據收件者的資料進行調整（例如名字、姓氏或目標維度的任何資料）。
* Adobe Campaign個人化區塊。 這些是與收件者資料無關的預先定義內容區塊，例如品牌標誌或鏡像頁面連結。

如需Campaign元件的完整說明，請參閱[Adobe Campaign元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

>[!NOTE]
>
>* 僅考慮Adobe Campaign **Profiles**&#x200B;目標維度的欄位。
>* 從&#x200B;**Sites**&#x200B;檢視屬性時，您無權存取Adobe Campaign內容欄位。 您可以在編輯時直接從電子郵件存取這些內容。

>



1. 插入新的&#x200B;**電子報** > **文字與個人化（促銷活動）**&#x200B;元件。
1. 連按兩下元件以開啟元件。 **Edit**&#x200B;視窗具有可讓您插入個人化元素的功能。

   >[!NOTE]
   >
   >可用的內容欄位對應至Adobe Campaign中的&#x200B;**Profiles**&#x200B;目標維度。
   >
   >請參閱[將AEM頁面連結至Adobe Campaign電子郵件](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail)。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 在sidekick中選取&#x200B;**用戶端內容** ，以使用角色設定檔中的資料來測試個人化欄位。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 隨即出現一個窗口，可讓您選擇所需的角色。 個人化欄位會自動取代為所選設定檔的資料。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 預覽新聞稿{#previewing-a-newsletter}

您可以預覽電子報的外觀，並預覽個人化。

1. 開啟您要預覽的電子報，然後按一下「預覽」（放大鏡）以縮小側鍵。
1. 按一下其中一個電子郵件用戶端圖示，即可查看您的電子報在每個電子郵件用戶端中的外觀。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 展開sidekick以重新開始編輯。

### 在AEM {#approving-content-in-aem}中核准內容

內容完成後，您就可以開始核准程式。 前往工具箱的&#x200B;**Workflow**&#x200B;標籤，然後選取&#x200B;**Approve for Adobe Campaign**&#x200B;工作流程。

此現成可用的工作流程包含兩個步驟：修訂然後批准，或修訂然後拒絕。 然而，該工作流可以擴展並適應更複雜的過程。

![chlimage_1-182](assets/chlimage_1-182.png)

若要核准Adobe Campaign的內容，請在sidekick中選取&#x200B;**Workflow**&#x200B;並選取&#x200B;**Approve for Adobe Campaign**，然後按一下&#x200B;**Start Workflow**，以套用工作流程。 執行步驟並核准內容。 您也可以在最後一個工作流程步驟中選取&#x200B;**拒絕**，而非&#x200B;**核准**，以拒絕內容。

![chlimage_1-183](assets/chlimage_1-183.png)

內容核准後，在Adobe Campaign中會顯示為已核准。 然後即可傳送電子郵件。

在Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

在Adobe Campaign 6.1中：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>在Adobe Campaign中，未核准的內容可與傳送同步，但無法執行傳送。 只能透過Campaign傳送傳送已核准的內容。

## 將AEM連結至Adobe Campaign Standard和Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>如需詳細資訊，請參閱標準編寫檔案中[使用Adobe Campaign 6.1和Adobe Campaign Standard](/help/sites-authoring/campaign.md)底下的[將AEM與Adobe Campaign Standard和Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic)連結。
