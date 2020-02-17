---
title: 管理觀眾
seo-title: 管理觀眾
description: 「對象」主控台可讓您建立、組織和管理Adobe target帳戶的對象，或管理ContextHub或Client context的區段
seo-description: 「對象」主控台可讓您建立、組織和管理Adobe target帳戶的對象，或管理ContextHub或Client context的區段
uuid: 76408a8c-25db-4e9f-8a69-27e820a2a7cf
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9a7a31f9-aeb8-455f-a07e-7b1d1f0a88b6
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 管理觀眾{#managing-audiences}

「對象」主控台可讓您建立、組織和管理Adobe target帳戶的對象，或管理ContextHub或用戶端內容的區段：

* 新增對象- Adobe target對象或ContextHub區段。
* 管理受眾。

「對象」(在ContextHub和「 *用戶端內容* 」中稱為「區段」)是由特定條件定義的訪客類別，然後由特定條件決定誰可以看到目標活動。 當您定位活動時，可以直接在「定位」程式中選取對象，或在「對象」主控台中建立新對象。

在「觀眾」主控台中，觀眾是依品牌組織。

「目標」模式中提供觀眾 [來製作目標內容](/help/sites-authoring/content-targeting-touch.md)，您也可以在此建立觀眾（但您需要在「觀眾」主控台中建立Adobe Target觀眾）。 您在「定位」模式中建立的對象會顯示在「對象」控制台中。

觀眾會以標籤來顯示，以說明定義的觀眾類型：

* CH - ContextHub區段
* CC —— 用戶端內容區段
* AT - Adobe target受眾

## 在「觀眾控制台」中建立ContextHub區段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在「對象」控制台或定位程式中建立ContextHub區段。

若要在「對象」控制台中建立ContextHub區段：

1. 在導覽主控台中，按一下或點選「個 **人化」**。 按一下或點選「 **觀眾**」。
1. 點選或按一 **下「建立ContextHub區段**」。

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. 在「新 **建ContextHub區段** 」對話方塊中，輸入標題並調整提示，然後按一下「 **建立」**。 您的新ContextHub區段會出現在觀眾清單中。

   >[!NOTE]
   >
   >您可以點選或按一下「已修改」來排序已修改的清單， **以依遞減順序排序** ，以查看任何新建立的對象。

如需使用ContextHub建立區段的詳細資訊，請參閱「使用ContextHub [設定區段](/help/sites-administering/segmentation.md) 」檔案。

## 使用Audience console建立Adobe Target觀眾 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以使用「對象」主控台，直接在AEM中建立Adobe target對象。

觀眾是由可決定目標活動所包含者的規則所定義。 對象定義可包含多個規則，而每個規則可包含多個參數。

當您使用多個規則時，這些規則會由布林運算元AND組合，這表示任何潛在讀者成員都必須符合要包含在活動中的所有已定義條件。 例如，如果您定義作業系統規則和瀏覽器規則，活動中只會包含使用已定義作業系統和已定義瀏覽器的訪客。

>[!NOTE]
>
>如果您在「建立」功能表中未看到「建立目標對象」 **** **，則您沒有建立對象的必要權限。 您需要在 **/etc/segmentation下的寫入權限** ，才能建立觀眾。 群組內容作者預設具有寫入權限。

若要建立Adobe target觀眾：

1. 在導覽主控台中，按一下或點選「個 **人化」**。 按一下或點選「 **觀眾**」。

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. 在「對象」主控台中，點選或按一 **下「建立** 」，然後**「建立目標對象」**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 在「 **Adobe Target設定** 」對話方塊中，選取目標設定，然後點選或按一下「 **確定」**。
1. 在「規則#1」區域，點選或按一下屬性類型，然後在可用欄位中輸入任何屬性資訊。 完成後，選擇屬性右側的複選標籤以保存它。 有關 [所有屬性的資訊](#attributes-and-their-options) ，請參閱屬性及其選項。
1. 按一 **下「新增規則** 」以新增其他規則。 視需要輸入任意數量的規則。 規則會與布林運算子AND結合，這表示對象必須符合每個規則的所有要求才能符合活動的資格。
1. 點選或按「下 **一步**」。
1. 輸入對象的名稱，然後點選或按一下「儲 **存**」。
1. 點選或按一下「 **儲存**」。 您的觀眾會列在觀眾清單中。

### 屬性及其選項 {#attributes-and-their-options}

您可以為下列每個屬性建立定位規則：

| **屬性** | **說明** | **如需詳細資訊** |
|---|---|---|
| **行動** | 根據行動裝置、裝置類型、裝置廠商、螢幕尺寸（依像素）等參數來定位行動裝置。 | 請參 [閱Adobe Target的](https://marketing.adobe.com/resources/help/en_US/target/target/c_mobile.html) Mobile檔案。 |
| **自訂** | 自訂參數是mbox參數。 如果您將任何mbox參數傳遞至mbox，或使用targetPageParams函式，這些參數會出現在此處，以供觀眾使用。 | 請參 [閱Adobe Target的自訂參數](https://marketing.adobe.com/resources/help/en_US/target/target/c_custom_parameters.html) 檔案。 |
| **OS** | 您可以定位使用特定作業系統的訪客。 | 鎖定使用Linux、Macintosh或Windows的使用者。 |
| **網站頁面** | 定位位於特定頁面或具有特定mbox參數的訪客。 | 請參 [閱Adobe Target的網站](https://marketing.adobe.com/resources/help/en_US/target/target/c_site_pages.html) 「頁面」檔案。 |
| **瀏覽器** | 您可以定位使用特定瀏覽器或特定瀏覽器選項的使用者瀏覽您的頁面。 | 請參 [閱Adobe Target的](https://marketing.adobe.com/resources/help/en_US/target/target/c_browser_options.html)瀏覽器選項檔案。 |
| **訪客設定檔** | 定位符合特定描述檔參數的訪客。 | 請參 [閱Adobe Target的訪客資料](https://marketing.adobe.com/resources/help/en_US/target/target/c_visitor_profile.html) 檔案。 |
| **流量來源** | 根據將訪客引用至您網站的搜尋引擎或著陸頁面來定位訪客。 | 請參 [閱Adobe target的流量來源](https://marketing.adobe.com/resources/help/en_US/target/target/c_traffic_sources.html) 檔案。 |

## 在「對象控制台」中修改對象 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能編輯在您所編輯之相同AEM例項中建立的Adobe target觀眾。 無法編輯在不同AEM環境中建立的目標對象。

您可以從「對象」控制台編輯任何ContextHub或「用戶端內容」對象。 您可以編輯Adobe target觀眾，但只能編輯在AEM中建立的觀眾：

1. 在導覽主控台中，按一下或點選「個 **人化」**。 按一下或點選「 **觀眾**」。
1. 點選或按一下您要編輯的ContextHub或Client Context區段旁的圖示，然後點選或按一下「編 **輯」**。
1. 在區段編輯器中進行任何編輯。 請參 [閱Client Context](/help/sites-administering/campaign-segmentation.md) 或 [ContextHub檔案](/help/sites-administering/contexthub-config.md) 。
