---
title: 管理對象
seo-title: Managing Audiences
description: 「對象」主控台可讓您建立、組織和管理Adobe Target帳戶的對象，或管理ContextHub或Client Context的區段
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

「對象」主控台可讓您建立、組織和管理Adobe Target帳戶的對象，或管理ContextHub或Client Context的區段：

* 新增對象 — Adobe Target對象或ContextHub區段。
* 管理對象。

對象，稱為 *區段* 在ContextHub和Client Context中，是由特定條件定義的一類訪客，可決定哪些人會看到目標活動。 鎖定目標活動時，您可以直接在鎖定目標程式中選取對象，或在「對象」主控台中建立更多對象。

在「對象」主控台中，對象會依品牌組織。

在鎖定目標模式中可用的對象 [製作目標內容](/help/sites-authoring/content-targeting-touch.md)，您也可以在這裡建立對象(但您必須在對象主控台中建立Adobe Target對象)。 您在「鎖定目標」模式中建立的對象會出現在「對象」主控台中。

對象會以標籤顯示，說明所定義的對象型別：

* CH - ContextHub區段
* CC — 使用者端內容區段
* AT - Adobe Target對象

## 在受眾主控台中建立ContextHub區段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在「對象」主控台中或在鎖定過程中建立ContextHub區段。

若要在「對象」主控台中建立ContextHub區段：

1. 在導覽主控台中，按一下或點選 **個人化**. 按一下或點選 **受眾**.
1. 點選或按一下 **建立ContextHub區段**.

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. 在 **新增ContextHub區段** 輸入標題並調整提升，然後按一下 **建立**. 您的新ContextHub區段會顯示在對象清單中。

   >[!NOTE]
   >
   >您可以點選或按一下「已修改」來排序已修改的清單， **以依遞減順序排序** ，以查看任何新建立的對象。

如需使用ContextHub建立區段的詳細資訊，請參閱 [使用ContextHub設定分段](/help/sites-administering/segmentation.md) 說明檔案。

## 使用Audience Console建立Adobe Target對象 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以使用受眾主控台，直接在AEM中建立Adobe Target受眾。

對象是由可決定要包含在目標活動中的規則所定義。 對象定義可包含多個規則，而每個規則均可包含多個引數。

當您使用多個規則時，這些規則會由布林運運算元AND組合，這表示任何可能的對象成員都必須符合要包含在活動中的所有已定義條件。 例如，如果您定義作業系統規則和瀏覽器規則，則活動中只會包含同時使用已定義作業系統和已定義瀏覽器的訪客。

>[!NOTE]
>
>如果您在中看不到**建立目標對象** **建立** 選單中，您沒有建立對象的必要許可權。 您需要下方的寫入許可權 **/etc/segmentation** 才能建立對象。 群組內容作者預設具有寫入權限。

若要建立Adobe Target對象：

1. 在導覽主控台中，按一下或點選 **個人化**. 按一下或點選 **受眾**.

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. 在「對象」主控台中，點選或按一下 **建立** 然後**立目標對象**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 在 **Adobe Target設定** 對話方塊中，選取目標組態，然後點選或按一下 **確定**.
1. 在「規則#1」區域中，點選或按一下屬性型別，然後在可用的欄位中輸入任何屬性資訊。 完成後，選取屬性右側的核取記號以儲存它。 另請參閱 [屬性及其選項](#attributes-and-their-options) 以取得所有屬性的相關資訊。
1. 按一 **下「新增規則** 」以新增其他規則。視需要輸入任意數量的規則。規則會與布林運算子AND結合，這表示對象必須符合每個規則的所有要求才能符合活動的資格。
1. 點選或按一下&#x200B;**下一步**。
1. 輸入對象名稱，然後點選或按一下 **儲存**.
1. 點選或按一下&#x200B;**儲存**。您的對象會列在「對象」清單中。

### 屬性及其選項 {#attributes-and-their-options}

您可以為下列每個屬性建立鎖定目標規則：

| **屬性** | **說明** | **如需詳細資訊** |
|---|---|---|
| **行動** | 根據行動裝置、裝置型別、裝置廠商、熒幕大小（依畫素）等引數來鎖定行動裝置。 | 另請參閱 [行動檔案](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) 在Adobe Target。 |
| **自訂** | 自訂引數為mbox引數。 如果您將任何mbox引數傳遞至mbox，或使用targetPageParams函式，這些引數就會顯示在這裡，以供對象使用。 | 另請參閱 [自訂引數檔案](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) 在Adobe Target。 |
| **OS** | 您可以鎖定使用特定作業系統的訪客。 | 定位使用Linux®、Macintosh或Windows的使用者。 |
| **網站頁面** | 位在特定頁面或具有特定mbox引數的目標訪客。 | 另請參閱 [網站頁面檔案](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) 在Adobe Target。 |
| **瀏覽器** | 您可以鎖定造訪您的頁面時使用特定瀏覽器或特定瀏覽器選項的使用者。 | 另請參閱 [瀏覽器選項檔案](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=en) 在Adobe Target。 |
| **訪客設定檔** | 符合特定設定檔引數的目標訪客。 | 另請參閱 [訪客資料檔案](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html) 在Adobe Target。 |
| **流量來源** | 根據參照至您網站的搜尋引擎或著陸頁面鎖定訪客。 | 另請參閱 [流量來原始檔](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) 在Adobe Target。 |

## 在對象主控台中修改對象 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能編輯在您編輯的相同AEM例項中建立的Adobe Target對象。 無法編輯在不同的AEM環境中建立的Target對象。

您可以從「對象」主控台編輯任何ContextHub或Client Context對象。 您也可以編輯Adobe Target對象，但僅限在AEM中建立的對象：

1. 在導覽主控台中，按一下或點選 **個人化**. 按一下或點選 **受眾**.
1. 點選或按一下您要編輯的ContextHub或Client Context區段旁的圖示，然後點選或按一下 **編輯**.
1. 在區段編輯器中進行任何編輯。 另請參閱 [使用者端內容](/help/sites-administering/campaign-segmentation.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 說明檔案。
