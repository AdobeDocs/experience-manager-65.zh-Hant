---
title: 使用Adobe Campaign 6.1和Adobe Campaign Standard
description: 您可以在AEM中建立電子郵件內容，並在Adobe Campaign電子郵件中處理。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 2%

---

# 使用Adobe Campaign 6.1和Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

您可以在AEM中建立電子郵件內容，並在Adobe Campaign電子郵件中處理。 若要這麼做，您必須：

1. 從Adobe Campaign專用的範本在AEM中建立Newsletter。
1. 選取 [Adobe Campaign服務](#selectingtheadobecampaigncloudservice) 編輯內容以存取所有功能之前。
1. 編輯內容。
1. 驗證內容。

然後，內容就可以與Adobe Campaign中的傳送同步。 本檔案將說明詳細說明。

>[!NOTE]
>
>在您可以使用此功能之前，您必須設定AEM以與以下任一功能整合 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## 透過Adobe Campaign傳送電子郵件內容 {#sending-email-content-via-adobe-campaign}

設定AEM和Adobe Campaign後，您可以直接在AEM中建立電子郵件傳遞內容，然後在Adobe Campaign中處理。

在AEM中建立Adobe Campaign內容時，您必須先連結至Adobe Campaign服務，才能編輯內容以存取所有功能。

有兩種可能的情況：

* 內容可以與Adobe Campaign的傳送同步。 這可讓您在傳送中使用AEM內容。
* (僅限Adobe Campaign內部部署)內容可直接傳送至Adobe Campaign，這會自動產生新的電子郵件傳送。 此模式具有限制。

本檔案將說明詳細說明。

### 建立新電子郵件內容 {#creating-new-email-content}

>[!NOTE]
>
>新增電子郵件範本時，請務必將其新增至 **/content/campaigns** 以便使用。
>

1. 在AEM中，選取 **網站** 資料夾，然後瀏覽檔案總管以找出管理電子郵件行銷活動的位置。 在以下範例中，相關的節點為 **網站** > **行銷活動** > **Geometrixx Outdoors** > **電子郵件行銷活動**.

   >[!NOTE]
   >
   >[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md#weretail). 從封裝共用下載範例Geometrixx內容。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. 選取 **新增** > **新頁面** 以建立新的電子郵件內容。
1. 選取其中一個專用於Adobe Campaign的可用範本，然後填寫頁面的一般屬性。 預設提供三個範本：

   * **Adobe Campaign電子郵件(AC 6.1)**：可讓您將內容新增至預先定義的範本，再傳送至Adobe Campaign 6.1進行傳送。
   * **Adobe Campaign電子郵件(ACS)**：可讓您將內容新增至預先定義的範本，再傳送至Adobe Campaign Standard進行傳送。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 按一下 **建立** 以建立您的電子郵件或電子報。

### 選取Adobe Campaign雲端服務和範本 {#selecting-the-adobe-campaign-cloud-service-and-template}

若要與Adobe Campaign整合，您需要將Adobe Campaign雲端服務新增至頁面。 如此一來，您便可存取個人化及其他Adobe Campaign資訊。

此外，您可能還需要選取Adobe Campaign範本，並變更主旨，為不會以HTML檢視電子郵件的使用者新增純文字內容。

1. 選取 **頁面** 索引標籤，然後選取「 」 **頁面屬性。**
1. 在 **雲端服務** 在快顯視窗中選取 **新增服務** 新增Adobe Campaign服務，然後按一下 **確定**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 從下拉式清單中選取與您的Adobe Campaign執行個體相符的設定，然後按一下 **確定**.

   >[!NOTE]
   >
   >請務必按一下 **確定** 或 **套用** 新增雲端服務之後。 如此可啟用 **Adobe Campaign** 標籤以正常運作。

1. 如果您想要套用預設以外的特定電子郵件傳遞範本(來自Adobe Campaign) **郵件** 範本，選取 **頁面屬性** 再來一次。 在 **Adobe Campaign** 索引標籤中，在相關的Adobe Campaign例項中輸入電子郵件傳遞範本的內部名稱。

   在Adobe Campaign Standard中，範本為 **使用AEM內容傳遞**. 在Adobe Campaign 6.1中，範本為 **包含AEM內容的電子郵件傳遞**.

   當您選取範本時，AEM會自動啟用 **Adobe Campaign電子報** 元件。

### 編輯電子郵件內容 {#editing-email-content}

您可以在傳統使用者介面或觸控最佳化使用者介面中編輯電子郵件內容。

1. 輸入電子郵件的主旨和文字版本，方法是選取 **頁面屬性** > **電子郵件** 從工具箱。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 從Sidekick中新增您想要的元素，以編輯電子郵件內容。 若要這麼做，請拖放它們。 然後按兩下您要編輯的元素。

   例如，您可以新增包含個人化欄位的文字。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   另請參閱 [Adobe Campaign元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) 以取得Adobe Campaign電子報/電子郵件行銷活動可用元件的說明。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 插入個人化 {#inserting-personalization}

編輯內容時，您可以插入：

* Adobe Campaign內容欄位。 這些欄位可插入文字中，並依據收件者的資料（例如名字、姓氏或目標維度的任何資料）進行調整。
* Adobe Campaign個人化區塊。 這些是與收件者資料無關的預先定義內容區塊，例如品牌標誌或映象頁面的連結。

另請參閱 [Adobe Campaign元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) 以取得Campaign元件的完整說明。

>[!NOTE]
>
>* 僅限Adobe Campaign的欄位 **設定檔** 會考慮目標維度。
>* 從檢視屬性時 **網站**，您無權存取Adobe Campaign內容欄位。 您可以在編輯時直接從電子郵件存取這些專案。
>

1. 插入新專案 **電子報** > **文字與個人化（行銷活動）** 元件。
1. 按兩下元件以開啟該元件。 此 **編輯** 視窗具備可讓您插入個人化元素的功能。

   >[!NOTE]
   >
   >可用的內容欄位對應至 **設定檔** Adobe Campaign中的目標維度。
   >
   >另請參閱 [將AEM頁面連結至Adobe Campaign電子郵件](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 選取 **使用者端內容** 在sidekick中，使用角色設定檔中的資料來測試個人化欄位。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 畫面會顯示一個視窗，供您選取喜歡的角色。 個人化欄位會自動被所選設定檔中的資料取代。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 預覽電子報 {#previewing-a-newsletter}

您可以預覽Newsletter的外觀並預覽個人化。

1. 開啟您要預覽的Newsletter，然後按一下「預覽」（放大鏡）以縮小Sidekick。
1. 按一下其中一個電子郵件使用者端圖示，即可檢視您的電子報在每個電子郵件使用者端中的面貌。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 展開sidekick以再次開始編輯。

### 在AEM中核准內容 {#approving-content-in-aem}

內容完成後，您可以開始核准程式。 前往 **工作流程** 標籤並選取 **核准Adobe Campaign** 工作流程。

這個現成的工作流程有兩個步驟：依序修訂及核准，或依序修訂及拒絕。 然而，此工作流程可以延伸並適應更複雜的流程。

![chlimage_1-182](assets/chlimage_1-182.png)

若要核准Adobe Campaign的內容，請選取以下專案以套用工作流程 **工作流程** 在sidekick中選擇 **核准Adobe Campaign** 並按一下 **開始工作流程**. 進行各個步驟並核准內容。 您也可以選取「 」，拒絕內容 **拒絕** 而非 **核准** 在最後一個工作流程步驟中。

![chlimage_1-183](assets/chlimage_1-183.png)

內容在核准後，會在Adobe Campaign中顯示為已核准。 然後可以傳送電子郵件。

在Adobe Campaign Standard中：

![chlimage_1-184](assets/chlimage_1-184.png)

在Adobe Campaign 6.1中：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>未核准的內容可以與Adobe Campaign中的傳遞同步，但傳遞無法執行。 只有已核准的內容才能透過Campaign傳遞傳送。

## 將AEM與Adobe Campaign Standard和Adobe Campaign 6.1連結 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>另請參閱 [將AEM與Adobe Campaign Standard和Adobe Campaign 6.1連結](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) 在 [使用Adobe Campaign 6.1和Adobe Campaign Standard](/help/sites-authoring/campaign.md) 詳細資訊，請參閱標準撰寫檔案。
