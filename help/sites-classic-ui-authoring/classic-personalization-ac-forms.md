---
title: 在AEM中建立Adobe Campaign表格
seo-title: 在AEM中建立Adobe Campaign表格
description: AEM可讓您建立並使用網站上與Adobe Campaign互動的表單。 特定欄位可插入表單中，並對應至Adobe Campaign資料庫。
seo-description: AEM可讓您建立並使用網站上與Adobe Campaign互動的表單。 特定欄位可插入表單中，並對應至Adobe Campaign資料庫。
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在AEM中建立Adobe Campaign表格{#creating-adobe-campaign-forms-in-aem}

AEM可讓您建立並使用網站上與Adobe Campaign互動的表單。 特定欄位可插入表單中，並對應至Adobe Campaign資料庫。

您可以管理新的連絡人訂閱、取消訂閱和使用者個人檔案資料，同時將其資料整合到您的Adobe Campaign資料庫。

若要在AEM中使用Adobe Campaign表單，您必須依照本檔案所述的步驟進行：

1. 讓範本可供使用。
1. 建立表格。
1. 編輯表單內容。

預設提供三種Adobe Campaign專用的表單：

* 儲存描述檔
* 訂閱服務
* 取消訂閱服務

這些表單會定義接受Adobe Campaign設定檔加密主要金鑰的URL參數。 表單會根據此URL參數更新相關聯Adobe Campaign設定檔的資料。

雖然您是獨立建立這些表單，但在典型的使用案例中，您會在電子報內容中產生表單頁面的個人化連結，讓收件者可以開啟連結並調整其個人資料（不論是取消訂閱、訂閱或更新其個人資料）。

表單會根據使用者自動更新。 如需詳 [細資訊，請參閱編輯表單內容](#editing-form-content) 。

## 讓範本可供使用 {#making-a-template-available}

您必須先在AEM應用程式中提供不同的範本，才能建立Adobe Campaign專屬的表單。

若要這麼做，請參閱范 [本檔案](/help/sites-developing/page-templates-static.md#templateavailability)。

首先，檢查作者和發佈例項之間的連線，Adobe Campaign就能運作。 請參 [閱「與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md) 」 [或「與Adobe Campaign 6.1整合」](/help/sites-administering/campaignonpremise.md)。

>[!NOTE]
>
>使用Adobe Campaign 6.1.x或Adobe Campaign Standard時，請確 **定頁面的** jcr:content **node上的acMapping** 屬性已分別設定為 **mapRecipient** 或 **** profileStandard。


### 建立表單 {#creating-a-form}

1. 從網站管理員開始。
1. 在樹狀結構中捲動以移至您要在所選網站中建立表單的位置。
1. **選擇**「新建&#x200B;**」>**「新建頁面……」。.
1. 選取 **Adobe Campaign Profile(AC 6.1)** 或 **** Adobe Campaign Profile(ACS)範本，然後輸入頁面屬性。

   >[!NOTE]
   >
   >如果模板不可用，請參閱「使模 [板可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) 」部分。

1. 按一 **下「建立** 」以建立表格。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   然後，您 [就可以編輯和設定表單的內容](#editing-form-content)。

## 編輯表單內容 {#editing-form-content}

Adobe Campaign專用的表單具有特定的元件。 這些元件可讓您將表單的每個欄位連結至Adobe Campaign資料庫中的欄位。

>[!NOTE]
>
>如果所要的範本不可用，請參閱 [使範本可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)。

本節僅詳細說明Adobe Campaign的特定連結。 如需有關如何在Adobe Experience Manager中使用表單的更一般性概觀的詳細資訊，請參閱「編輯模式 [元件」](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)。

1. 導覽至您要編輯的表單。
1. **在工具箱中，選擇「**&#x200B;頁面&#x200B;**>頁**&#x200B;面屬性……」然後前往快 **顯視窗的** 「雲端服務」標籤。
1. 按一下「新增服務 ****」，然後在服務的下拉式清單中選取與您的Adobe Campaign例項對應的設定，以新增Adobe Campaign服務。 此配置是在設定實例之間的連接時執行的。 如需詳細資訊，請 [參閱「連線AEM至Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)」。

   >[!NOTE]
   >
   >如有必要，按一下掛鎖圖示即可解除鎖定設定，以新增Adobe Campaign服務。

1. 使用表單開頭的「編輯」 **按鈕** ，存取表單的一般參數。 「表 **單** 」標籤可讓您選取感謝頁面，使用者在驗證表單後將會重新導向至該頁面。

   高 **級表單** 允許您選擇表單類型。 「貼 **文選項** 」欄位可讓您在三種Adobe Campaign表單類型中做出選擇：

   * **Adobe Campaign:儲存設定檔**:可讓您在Adobe Campaign中建立或更新收件者（預設值）。
   * **Adobe Campaign:訂閱服務**:可讓您管理Adobe Campaign中收件者的訂閱。
   * **Adobe Campaign:取消訂閱服務**:可讓您取消Adobe Campaign中收件者的訂閱。
   「動 **作設定** 」欄位可讓您指定如果Adobe Campaign資料庫尚未存在，是否要在其中建立收件者描述檔。 若要這麼做，請勾選「如果 **不存在，則建立使用者** 」選項。

1. 將選取的元件從工具箱中拖曳並拖曳至表格中，以新增這些元件。 如需可用Adobe Campaign特定元件的詳細資訊，請參閱 [Adobe表單元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 連按兩下新增的欄位，即可設定欄位。 「 **Adobe Campaign** 」標籤可讓您將欄位連結至Adobe Campaign收件者表格中的欄位。 您也可以指定欄位是否為協調金鑰的一部分，讓已存在於Adobe Campaign資料庫中的收件者可加以辨識。

   >[!CAUTION]
   >
   >每個 **表單欄位** ，元素名稱必須不同。 視需要變更。
   >
   >每個表單都必須包含 **Encrypted Primary Key** （加密的主要金鑰）元件，才能正確管理Adobe Campaign資料庫中的收件者。

1. 在工具箱中選取「頁 **面** >啟 **動頁面** 」來啟動頁面。 頁面會在您的網站上啟動。 您可以前往AEM出版物例項來檢視它。 在驗證表單後，Adobe Campaign資料庫中的資料會更新。

## 測試表單 {#testing-a-form}

在建立表單並編輯表單內容後，您可能想要手動測試表單是否如預期般運作。

>[!NOTE]
>
>每個表單上都必 **須有加密的主密鑰** (Encrypted Primary Key)元件。 在「元件」中，選取「Adobe Campaign」，只顯示這些元件。
>
>雖然在此程式中您手動輸入epk編號，但實際上，使用者會在電子報中取得此頁面的連結（無論要取消訂閱、訂閱或更新您的個人檔案）。 Epk會根據使用者自動更新。
>
>若要建立該連結，請使用變數 **Main資源識別碼**(Adobe Campaign Standard)或 **Encrypted識別碼(Adobe Campaign 6.1)(例如，在****** Text &amp; Personalization(Campaign)元件中)，這些識別碼會連結至Adobe Campaign中的頁面。

若要這麼做，您必須手動取得Adobe Campaign描述檔的EPK，然後將它附加至URL:

1. 若要取得Adobe Campaign設定檔的加密主金鑰(EPK):

   * 在Adobe Campaign Standard —— 導覽至「設定檔 **與觀眾** >設定 **檔**」，其中列出現有的設定檔。 請確定表格在欄中顯 **示「主資源識別碼** 」欄位(按一下／點選「設定清單 ****」即可設定此欄位)。 複製所要描述檔的主要資源識別碼。
   * 在Adobe Campaign 6.11中，前往「設定檔 **與目標** >收 **件者**」，其中列出現有的設定檔。 請確定表在列中顯示「 **Encrypted identifier** 」(加密的標識符 **)欄位(可通過按一下右鍵某個條目並選擇「** Configure list...)來配置此欄位。 複製所需描述檔的加密識別碼。

1. 在AEM中，開啟發佈例項上的表單頁面，並將步驟1的EPK附加為URL參數：在編寫表單時，請使用先前在EPK元件中定義的相同名稱(例如： `?epk=...`)
1. 現在，該表單可用來修改與連結的Adobe Campaign設定檔相關聯的資料和訂閱。 在您修改部分欄位並送出表單後，您可以在Adobe Campaign中驗證是否已更新適當的資料。

在驗證表單後，Adobe Campaign資料庫中的資料會更新。
