---
title: 在AEM中建立Adobe Campaign Forms
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM可讓您建立和使用網站上與Adobe Campaign互動的表單
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---

# 在AEM中建立Adobe Campaign Forms {#creating-adobe-campaign-forms-in-aem}

AEM可讓您建立和使用與網站上的Adobe Campaign互動的表單。 特定欄位可插入您的表單中，並對應至Adobe Campaign資料庫。

您可以管理新的連絡人訂閱、取消訂閱和使用者設定檔資料，同時將他們的資料整合至您的Adobe Campaign資料庫。

若要在AEM中使用Adobe Campaign表單，您必須依照本檔案所述的步驟操作：

1. 讓範本可供使用。
1. 建立表單。
1. 編輯表單內容。

預設提供Adobe Campaign專用的三種表單：

* 儲存設定檔
* 訂閱服務
* 取消訂閱服務

這些表單會定義URL參數，此參數接受Adobe Campaign設定檔的加密主要金鑰。 表單會根據此URL參數更新相關聯Adobe Campaign設定檔的資料。

雖然您可以單獨建立這些表單，但在一般的使用案例中，您會產生個人化連結至電子報內容內的表單頁面，讓收件者可以開啟連結，並調整其設定檔資料（無論是取消訂閱、訂閱或更新其設定檔）。

表單會根據使用者自動更新。 請參閱 [編輯表單內容](#editing-form-content) 以取得更多資訊。

## 讓範本可供使用 {#making-a-template-available}

您必須先在AEM應用程式中提供不同的範本，才能建立Adobe Campaign專屬的表單。

若要這麼做，請參閱 [範本檔案](/help/sites-developing/templates.md#template-availability).

## 建立表單 {#creating-a-form}

首先，檢查製作與發佈執行個體之間的連線，讓Adobe Campaign正常運作。 請參閱 [與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md) 或 [與Adobe Campaign Classic整合](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>請確定 **acMapping** 頁面的 **jcr:content** 節點設為 **mapRecipient** 或 **設定檔** 分別使用Adobe Campaign Classic或Adobe Campaign Standard時

1. 在AEM中，導覽至您要建立新頁面的位置。
1. 建立頁面並選取 **Adobe Campaign Classic設定檔**&#x200B;或&#x200B;**Adobe Campaign Standard設定檔** 按一下 **下一個**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果所需的範本無法使用，請參閱 [範本可用性](/help/sites-developing/templates.md#template-availability).

1. 在 **名稱** 欄位，新增頁面名稱。 它必須是有效的JCR名稱。
1. 在 **標題** 欄位，輸入標題並按一下 **建立**.
1. 開啟頁面並選取 **開啟屬性** 在「Cloud Services」中新增Adobe Campaign設定，並選取核取記號以儲存您的變更。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. 在頁面上， **表單開始** 元件，請選取其形式類型 —  **訂閱、取消訂閱、**&#x200B;或&#x200B;**儲存設定檔**. 每個表單只能有一種類型。 您現在可以 [編輯表單的內容](#editing-form-content).

## 編輯表單內容 {#editing-form-content}

專屬於Adobe Campaign的Forms具有特定元件。 這些元件可讓您將表單的每個欄位連結至Adobe Campaign資料庫中的欄位。

>[!NOTE]
>
>如果所需的範本無法使用，請參閱 [讓範本可供使用](/help/sites-authoring/adobe-campaign.md).

本節僅詳細說明連線至Adobe Campaign的特定連結。 如需更一般概述如何在Adobe Experience Manager中使用表單的詳細資訊，請參閱 [編輯模式元件](/help/sites-authoring/default-components-foundation.md).

1. 選擇 **開啟屬性** 在「Cloud Services」中新增Adobe Campaign設定，並選取核取記號以儲存您的變更。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 在頁面上， **表單開始** 元件，按一下「配置」表徵圖。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下 **進階** 頁簽，並選取其形式類型 —  **訂閱、取消訂閱、** 或 **儲存設定檔** 按一下 **好。** 每個表單只能有一種類型。

   * **Adobe Campaign:儲存設定檔**:可讓您在Adobe Campaign中建立或更新收件者（預設值）。
   * **Adobe Campaign:訂閱服務**:可讓您在Adobe Campaign中管理收件者的訂閱。
   * **Adobe Campaign:取消訂閱服務**:可讓您取消Adobe Campaign中收件者的訂閱。

1. 您必須有 **加密的主密鑰** 元件。 此元件定義將使用哪個URL參數來接受Adobe Campaign設定檔的加密主要金鑰。 在「元件」中，選取「Adobe Campaign」，只顯示這些元件。
1. 拖曳元件 **加密的主密鑰** 至表單（任何位置），然後按一下或點選 **設定** 表徵圖。 在 **Adobe Campaign** ，請為URL參數指定任何名稱。 按一下或點選核取記號以儲存您的變更。

   產生的連結必須使用此URL參數，並為其指派Adobe Campaign設定檔的加密主要金鑰。 加密的主金鑰必須正確進行URL（百分比）編碼。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 視需要將元件新增至表單，例如文字欄位、日期欄位、核取方塊欄位、選項欄位等。 請參閱 [Adobe Campaign表單元件](/help/sites-authoring/adobe-campaign-components.md) 以取得每個元件的詳細資訊。
1. 按一下「設定」圖示以開啟元件。 例如，在 **文字欄位（促銷活動）** 元件，更改標題和文本。

   按一下 **Adobe Campaign** 將表單欄位對應至Adobe Campaign中繼資料變數。 提交表單時，會在Adobe Campaign中更新對應欄位。 變數選擇器中只有具有相符類型的欄位可用（例如，文字欄位的字串變數）。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >您可以依照以下指示，新增/移除收件者表格中顯示的欄位： [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. 按一下 **發佈頁面**. 頁面已在您的網站上啟動。 您可以前往AEM出版物例項進行檢視。 您也可以 [測試表單](#testing-a-form).

   >[!CAUTION]
   >
   >您必須向雲端服務上的匿名使用者提供讀取權限，才能在發佈時使用表單。 不過，請注意向匿名使用者提供讀取權限的潛在安全性問題，並確實透過設定Dispatcher等方式來緩解此問題。

## 測試表單 {#testing-a-form}

建立表單並編輯表單內容後，您可能想要手動測試表單是否如預期般運作。

>[!NOTE]
>
>您必須有 **加密的主密鑰** 元件。 在「元件」中，選取「Adobe Campaign」，只顯示這些元件。
>
>雖然在此程式中，您需手動輸入epk編號，但實際上，使用者會在電子報中取得本頁面的連結（無論是取消訂閱、訂閱或更新您的設定檔）。 epk會根據使用者自動更新。
>
>若要建立該連結，請使用變數 **主要資源標識符**(Adobe Campaign Standard)或 **加密的識別碼** (Adobe Campaign Classic)(例如 **文字與個人化（行銷活動）** 元件)，此元件會連結至Adobe Campaign中的epk。

若要這麼做，您需要手動取得Adobe Campaign設定檔的EPK，然後將其附加至URL:

1. 若要取得Adobe Campaign設定檔的加密主金鑰(EPK):

   * 在Adobe Campaign Standard中 — 導覽至 **設定檔與對象** > **設定檔**，列出現有設定檔。 請確定表格顯示 **主要資源標識符** 欄中的欄位(按一下/點選即可設定 **配置清單**)。 複製所需設定檔的主要資源識別碼。
   * 在Adobe Campaign Classic中，前往 **設定檔與目標** >  **收件者**，列出現有設定檔。 請確定表格顯示 **加密的識別碼** 欄中的欄位(可透過以滑鼠右鍵按一下項目並選取「 」來設定 **配置清單……**)。 複製所需設定檔的加密識別碼。

1. 在AEM中，開啟發佈例項上的表單頁面，並將步驟1的EPK附加為URL參數：在編寫表單時使用先前在EPK元件中定義的相同名稱(例如： `?epk=...`)
1. 此表單現在可用來修改與連結Adobe Campaign設定檔相關聯的資料和訂閱。 修改部分欄位並提交表單後，您可以在Adobe Campaign內確認適當的資料已更新。

驗證表單後，會更新Adobe Campaign資料庫中的資料。
