---
title: 在設計模式中設定預設元件
description: 在設計模式中設定Adobe Experience Manager元件。
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# 在設計模式中設定預設元件{#configuring-components-in-design-mode}

當現成安裝AEM執行個體時，元件瀏覽器中會立即提供一組元件選項。

除了這些以外，您也可以使用其他各種元件。 您可以使用設計模式 [啟用/停用這類元件](#enable-disable-components). 啟用並位於您的頁面後，您就可以使用設計模式來 [設定元件設計的各個層面](#configuring-the-design-of-a-component) 藉由編輯屬性引數。

>[!NOTE]
>
>編輯這些元件時務必謹慎。 設計設定通常是整個網站設計中不可或缺的一部分，因此這些設定只應由具有適當許可權和經驗的人進行變更，通常是管理員或開發人員。 另請參閱 [開發元件](/help/sites-developing/components.md) 以取得詳細資訊。

>[!NOTE]
>
>設計模式僅適用於靜態範本。 使用可編輯範本建立的範本應使用進行編輯 [範本編輯器](/help/sites-authoring/templates.md).

>[!NOTE]
>
>設計模式僅適用於儲存為( `/etc`)。
>
>從AEM 6.4開始，建議將設計儲存為下的設定資料 `/apps` 以支援連續部署案例。 設計儲存在 `/apps` 在執行階段不可編輯，且這類範本的非管理員使用者將無法使用設計模式。

這涉及新增或移除頁面段落系統中允許的元件。 段落系統( `parsys`)是包含所有其他段落元件的複合元件。 段落系統可讓作者將不同型別的元件新增至頁面，因為它包含所有其他段落元件。 每個段落型別都會表示為元件。

例如，產品頁面的內容可能包含包含以下內容的段落系統：

* 產品的影像（影像或文欄位落的形式）
* 產品說明（文欄位落）
* 含有技術資料的表格（作為表格段落）
* 使用者填寫的表單（表單開頭、表單元素和表單結尾段落）

>[!NOTE]
>
>另請參閱 [開發元件](/help/sites-developing/components.md) 和 [使用範本和元件的准則](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 有關詳細資訊 `parsys`.

>[!CAUTION]
>
>若要定義靜態範本的設計，建議使用本文所述的「設計模式」編輯設計
>
>例如，在CRX DE中修改設計並非最佳實務，且這類設計的應用可能會與預期行為有所差異。 檢視開發人員檔案 [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) 以取得詳細資訊。

## 啟用/停用元件 {#enable-disable-components}

要啟用或停用元件：

1. 選取 **設計** 模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 按一下元件。 選取時，元件會有藍色邊框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 按一下 **父級** 圖示。

   ![父級](do-not-localize/screen_shot_2018-03-22at103204.png)

   這將會選取包含目前元件的段落系統。

1. 此 **設定** 段落系統的圖示會顯示在父項的動作列中。

   ![設定](do-not-localize/screen_shot_2018-03-22at103256.png)

   選取此項以顯示對話方塊。

1. 使用對話方塊可定義編輯目前頁面時元件瀏覽器中可用的元件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   此對話方塊有兩個標籤：

   * 已允許的元件
   * 設定

   **允許的元件**

   在 **允許的元件** 標籤上，您可以定義parsys可用的元件。

   * 元件會依其元件群組分組，這些群組可展開和摺疊。
   * 勾選群組名稱即可選取整個群組，取消勾選可取消選取所有群組。
   * 減號表示至少選取了一個群組中的專案，但並未選取所有專案。
   * 搜尋可依名稱篩選元件。
   * 無論篩選條件為何，元件群組名稱右側所列的計數代表這些群組中選取的元件總數。

   您可以定義每頁元件的設定。 如果子頁面使用相同的範本和/或頁面元件（通常對齊），則相同的設定將套用至對應的段落系統。

   >[!NOTE]
   >
   >調適型表單元件可在調適型表單容器內運作，以使用Forms生態系統。 因此，這些元件必須僅在最適化表單編輯器中使用，在網站頁面編輯器中無法運作。

   **設定**

   在 **設定** 索引標籤您可以定義其他選項，例如為每個元件繪製錨點，以及定義每個容器的儲存格邊距。

1. 選取 **完成** 以儲存您的設定。

## 設定元件設計 {#configuring-the-design-of-a-component}

1. 選取 **設計** 模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 按一下具有藍色邊框的元件。 在此範例中，已選取主圖影像元件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用 **設定** 圖示以開啟對話方塊。

   ![「設定」圖示](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在「設計」對話方塊中，您可以根據可用的設計引數來設定元件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   此對話方塊有三個索引標籤：

   * 主要
   * 功能
   * 樣式

   **屬性**

   此 **屬性** 標籤可讓您設定元件的重要設計引數。 例如，對於影像元件，您可以定義影像允許的大小上限與下限。

   **功能**

   此 **功能** 索引標籤可讓您啟用或停用元件的其他功能。 例如，對於影像元件，您可以定義影像的方向、可用的裁切選項，以及是否可以上傳影像。

   **樣式**

   此 **樣式** tab可讓您定義要與元件搭配使用的CSS類別和樣式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用 **新增** 按鈕，將其他專案新增至多重專案對話方塊清單。

   ![新增其他專案](assets/chlimage_1-94.png)

   使用 **刪除** 圖示從多重專案對話方塊清單中移除專案。

   ![刪除](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用 **移動** 圖示可重新排列多專案對話方塊清單中的專案順序。

   ![移動](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 按一下 **完成** 圖示以儲存並關閉對話方塊。
