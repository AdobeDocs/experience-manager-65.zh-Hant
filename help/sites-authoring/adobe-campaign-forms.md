---
title: 建立Adobe CampaignForms在Adobe Experience Manager
description: Adobe Experience Manager允許您建立和使用網站上與Adobe Campaign交互的表單
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# 建立Adobe CampaignForms AEM {#creating-adobe-campaign-forms-in-aem}

允AEM許您建立和使用網站上與Adobe Campaign交互的表單。 可將特定欄位插入表單並映射到Adobe Campaign資料庫。

您可以管理新的聯繫人訂閱、取消訂閱和用戶配置檔案資料，同時將其資料整合到您的Adobe Campaign資料庫中。

要在中使用Adobe Campaign表AEM單，您需要遵循本文檔中介紹的以下步驟：

1. 使模板可用。
1. 建立窗體。
1. 編輯表單內容。

預設情況下，有三種類型的表單(特定於Adobe Campaign)可用：

* 保存配置檔案
* 訂閱服務
* 取消訂閱服務

這些表單定義一個URL參數，該參數接受Adobe Campaign配置檔案的加密主鍵。 基於此URL參數，表單更新關聯的Adobe Campaign配置檔案的資料。

雖然您獨立建立了這些表單，但在典型的使用案例中，您會生成到新聞稿內容內表單頁面的個性化連結，以便收件人可以開啟該連結並調整其配置檔案資料（無論是取消訂閱、訂閱還是更新其配置檔案）。

表單會根據用戶自動更新。 請參閱 [編輯表單內容](#editing-form-content) 的子菜單。

## 使模板可用 {#making-a-template-available}

在能夠建立特定於Adobe Campaign的表單之前，必須在應用程式中提供不同的模AEM板。

要執行此操作，請參閱 [模板文檔](/help/sites-developing/templates.md#template-availability)。

## 建立窗體 {#creating-a-form}

首先，檢查作者和發佈實例之間的聯繫，Adobe Campaign正在工作。 請參閱 [與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md) 或 [與Adobe Campaign Classic整合](/help/sites-administering/campaignonpremise.md)。

>[!NOTE]
>
>確保 **acMapping** 頁的 **jcr：內容** 節點設定為 **mapRecipient** 或 **輪廓** 使用Adobe Campaign Classic或Adobe Campaign Standard時

1. 在中AEM的「站點」中，導航到要建立新頁面的位置。
1. 建立頁面並選擇 **Adobe Campaign Classic檔案**&#x200B;或&#x200B;**Adobe Campaign Standard檔案** 按一下 **下一個**。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果所需模板不可用，請參見 [模板可用性](/help/sites-developing/templates.md#template-availability)。

1. 在 **名稱** 欄位，添加頁面名稱。 它必須是有效的JCR名稱。
1. 在 **標題** 欄位，輸入標題並按一下 **建立**。
1. 開啟頁面並選擇 **開啟屬性** 在Cloud Services中，添加Adobe Campaign配置並選擇複選標籤以保存更改。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. 在頁面上，在 **窗體開始** 的子菜單。 **訂閱、取消訂閱、**&#x200B;或&#x200B;**保存配置檔案**。 每個表單只能有一種類型。 你現在可以 [編輯表單的內容](#editing-form-content)。

## 編輯表單內容 {#editing-form-content}

Forms專門研究Adobe Campaign，有一些具體的組成部分。 這些元件具有一個選項，允許您將表單的每個欄位連結到Adobe Campaign資料庫中的一個欄位。

>[!NOTE]
>
>如果所需模板不可用，請參見 [使模板可用](/help/sites-authoring/adobe-campaign.md)。

本節僅詳細說明指向Adobe Campaign的特定連結。 有關如何在Adobe Experience Manager使用表單的更一般性概述的詳細資訊，請參見 [編輯模式元件](/help/sites-authoring/default-components-foundation.md)。

1. 選擇 **開啟屬性** 在Cloud Services中，添加Adobe Campaign配置並選擇複選標籤以保存更改。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 在頁面上，在 **窗體開始** 元件，按一下「配置」表徵圖。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下 **高級** 的子菜單。 **訂閱、取消訂閱、** 或 **保存配置檔案** 按一下 **好。** 每個表單只能有一種類型。

   * **Adobe Campaign:保存配置檔案**:允許您在Adobe Campaign建立或更新收件人（預設值）。
   * **Adobe Campaign:訂閱服務**:允許您管理收件人在Adobe Campaign的訂閱。
   * **Adobe Campaign:取消訂閱服務**:允許您取消Adobe Campaign的收件人訂閱。

1. 您必須 **加密的主密鑰** 元件。 此元件定義將使用哪些URL參數來接受Adobe Campaign配置檔案的加密主鍵。 在「元件」中，選擇「Adobe Campaign」，以便只顯示那些元件。
1. 拖動元件 **加密的主密鑰** 按一下或點擊 **配置** 表徵圖 在 **Adobe Campaign** 頁籤，指定URL參數的任何名稱。 按一下或點擊複選標籤以保存更改。

   生成的到此表單的連結需要使用此URL參數並為其分配Adobe Campaign配置檔案的加密主鍵。 加密的主密鑰必須正確進行URL（百分比）編碼。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 根據需要將元件添加到表單中，如文本欄位、日期欄位、複選框欄位、選項欄位等。 請參閱 [Adobe Campaign窗體元件](/help/sites-authoring/adobe-campaign-components.md) 的子菜單。
1. 按一下「配置」表徵圖以開啟元件。 例如，在 **文本欄位（市場活動）** 的子菜單。

   按一下 **Adobe Campaign** 將表單域映射到Adobe Campaign元資料變數。 當您提交表單時，映射欄位將在Adobe Campaign更新。 變數選取器中只有具有匹配類型的欄位可用（例如，文本欄位的字串變數）。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >您可以按照以下說明添加/刪除在收件人表中顯示的欄位： [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. 按一下 **發佈頁面**。 該頁面在您的站點上被激活。 您可以轉到發佈實例來AEM查看它。 您也可以 [test窗體](#testing-a-form)。

   >[!CAUTION]
   >
   >您需要向雲服務上的匿名用戶提供讀取權限才能在發佈時使用表單。 但是，要瞭解向匿名用戶提供讀取權限可能存在的安全問題，並確保通過配置調度程式來緩解此問題。

## 測試表單 {#testing-a-form}

建立表單並編輯表單內容後，您可能需要手動test表單正按預期工作。

>[!NOTE]
>
>您必須 **加密的主密鑰** 元件。 在「元件」中，選擇「Adobe Campaign」，以便只顯示那些元件。
>
>雖然在此過程中您手動輸入epk編號，但在實踐中，用戶將在新聞簡報中獲得指向此頁面的連結（是取消訂閱、訂閱還是更新您的個人資料）。 基於用戶，epk自動更新。
>
>要建立該連結，請使用變數 **主資源標識符**(Adobe Campaign Standard或 **加密的標識符** (Adobe Campaign Classic)(例如， **文本和個性化（市場活動）** 元件)，它連結到Adobe Campaign的epk。

為此，您需要手動獲取Adobe Campaign配置檔案的EPK，然後將其附加到URL:

1. 要獲取Adobe Campaign配置檔案的加密主密鑰(EPK)，請執行以下操作：

   * 在Adobe Campaign Standard — 導航到 **配置檔案和受眾** > **配置檔案**，其中列出現有配置檔案。 確保表顯示 **主資源標識符** 欄位(可通過按一下/點擊來配置 **配置清單**)。 複製所需配置檔案的主資源標識符。
   * 在Adobe Campaign Classic，轉到 **配置檔案和目標** >  **收件人**，其中列出現有配置檔案。 確保表顯示 **加密的標識符** 欄位(可通過按一下右鍵條目並選擇 **配置清單……**)。 複製所需配置檔案的加密標識符。

1. 在AEM中，開啟發佈實例上的表單頁，並將步驟1中的EPK作為URL參數追加：創作表單時，使用先前在EPK元件中定義的相同名稱(例如： `?epk=...`)
1. 現在，該表單可用於修改與連結的Adobe Campaign配置檔案關聯的資料和訂閱。 修改某些欄位並提交表單後，您可以在Adobe Campaign內驗證是否更新了相應的資料。

一旦對表格進行驗證，Adobe Campaign資料庫中的資料就會更新。
