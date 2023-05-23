---
title: 管理對象
seo-title: Managing Audiences
description: Acuviements控制台使您能夠為您的Adobe Target帳戶建立、組織和管理受眾，或管理ContextHub或Client Context的段
seo-description: The Audiences console enables you to create, organize, and manage audiences for your Adobe Target account or manage segments for ContextHub or Client Context
uuid: 76408a8c-25db-4e9f-8a69-27e820a2a7cf
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9a7a31f9-aeb8-455f-a07e-7b1d1f0a88b6
docset: aem65
exl-id: 97e02986-049f-4747-a67a-6aa0677b281e
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 9%

---

# 管理對象{#managing-audiences}

Acuviements控制台使您能夠為您的Adobe Target帳戶建立、組織和管理受眾，或管理ContextHub或Client Context的段：

* 添加受眾 — Adobe Target受眾或ContextHub段。
* 管理受眾。

一個觀眾 *分部* 在ContextHub和Client Context中，訪問者是由特定條件定義的一類訪問者，然後由特定條件確定哪些人可以查看目標活動。 在目標活動時，您可以直接在「目標」進程中選擇受眾，也可以在「受眾」控制台中建立更多內容。

在觀眾控制台中，觀眾按品牌組織。

在「目標」模式下，受眾可 [創作目標內容](/help/sites-authoring/content-targeting-touch.md)，您也可以在其中建立觀眾(但必須在「觀眾」控制台中建立Adobe Target觀眾)。 在「目標」模式下建立的受眾將出現在「受眾」控制台中。

觀眾將顯示一個標籤，該標籤描述定義的受眾類型：

* CH - ContextHub段
* CC — 客戶端上下文段
* AT -Adobe Target觀眾

## 在Avociums Console中建立ContextHub段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在「受眾」控制台或在目標過程中建立ContextHub段。

要在Avociums控制台中建立ContextHub段：

1. 在導航控制台中，按一下或點擊 **個性化**。 按一下或點擊 **觀眾**。
1. 點擊或按一下 **建立ContextHub段**。

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. 在 **新建ContextHub段** 對話框，輸入標題並調整提示，然後按一下 **建立**。 您的新ContextHub段將出現在受眾清單中。

   >[!NOTE]
   >
   >您可以點選或按一下「已修改」來排序已修改的清單， **以依遞減順序排序** ，以查看任何新建立的對象。

有關使用ContextHub建立段的詳細資訊，請參閱 [使用ContextHub配置分段](/help/sites-administering/segmentation.md) 文檔。

## 使用受眾控制台建立Adobe Target受眾 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以直接使用「觀眾」控AEM制台建立Adobe Target觀眾。

受眾由確定目標活動中包括的對象的規則定義。 受眾定義可以包括多個規則，並且每個規則可以包括多個參數。

使用多個規則時，這些規則由布爾運算子AND組合，這意味著任何潛在受眾成員必須滿足要包含在活動中的所有定義條件。 例如，如果定義作業系統規則和瀏覽器規則，則活動中只包括使用定義的作業系統和定義瀏覽器的訪問者。

>[!NOTE]
>
>如果在中未看到**建立目標受眾** **建立** 菜單，您沒有建立訪問群體所需的權限。 您需要在 **/etc/分段** 才能創造觀眾。 群組內容作者預設具有寫入權限。

要建立Adobe Target受眾：

1. 在導航控制台中，按一下或點擊 **個性化**。 按一下或點擊 **觀眾**。

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. 在「Avocuments（觀眾）」控制台中，點擊或按一下 **建立** 然後**建立目標受眾**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 在 **Adobe Target配置** 對話框，選擇目標配置，然後點擊或按一下 **確定**。
1. 在「規則#1」區域，點擊或按一下屬性類型，然後在可用欄位中輸入任何屬性資訊。 完成後，選擇屬性右側的複選標籤以保存它。 請參閱 [屬性及其選項](#attributes-and-their-options) 的子菜單。
1. 按一 **下「新增規則** 」以新增其他規則。視需要輸入任意數量的規則。規則會與布林運算子AND結合，這表示對象必須符合每個規則的所有要求才能符合活動的資格。
1. 點選或按一下&#x200B;**下一步**。
1. 輸入受眾的名稱，點擊或按一下 **保存**。
1. 點選或按一下&#x200B;**儲存**。您的受眾列在「受眾」清單中。

### 屬性及其選項 {#attributes-and-their-options}

您可以為以下每個屬性建立目標規則：

| **屬性** | **說明** | **有關詳細資訊** |
|---|---|---|
| **行動** | 基於諸如移動設備、設備類型、設備供應商、螢幕尺寸（按像素）等參數的目標移動設備。 | 請參閱 [移動文檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) Adobe Target。 |
| **自訂** | 自定義參數是mbox參數。 如果將任何mbox參數傳遞到mboxes，或使用targetPageParams函式，則這些參數將出現在此供受眾使用。 | 請參閱 [自定義參數文檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) Adobe Target。 |
| **OS** | 您可以針對使用特定作業系統的訪問者。 | 目標使用Linux®、Macintosh或Windows的用戶。 |
| **網站頁面** | 目標訪問者，這些訪問者位於特定頁面或具有特定的mbox參數。 | 請參閱 [網站頁文檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) Adobe Target。 |
| **瀏覽器** | 您可以針對訪問您頁面時使用特定瀏覽器或特定瀏覽器選項的用戶。 | 請參閱 [瀏覽器選項文檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=en) Adobe Target。 |
| **訪客設定檔** | 滿足特定配置檔案參數的目標訪問者。 | 請參閱 [訪問者配置檔案文檔](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html) Adobe Target。 |
| **流量來源** | 根據搜索引擎或登錄頁將訪問者引至您的站點來確定目標訪問者。 | 請參閱 [通信源文檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) Adobe Target。 |

## 在受眾控制台中修改受眾 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能編輯在所編輯的同一實例中創AEM建的Adobe Target受眾。 無法編輯在不同AEM環境中建立的目標受眾。

可以從「受眾」控制台編輯任何ContextHub或「客戶端上下文」受眾。 您也可以編輯Adobe Target觀眾，但只能編輯在以下位置建立的觀AEM眾：

1. 在導航控制台中，按一下或點擊 **個性化**。 按一下或點擊 **觀眾**。
1. 點擊或按一下要編輯的ContextHub或Client Context段旁邊的表徵圖，點擊或按一下 **編輯**。
1. 在段編輯器中進行任何編輯。 請參閱 [客戶端上下文](/help/sites-administering/campaign-segmentation.md) 或 [上下文中心](/help/sites-developing/ch-configuring.md) 文檔。
