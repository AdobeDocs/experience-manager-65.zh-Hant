---
title: 管理智慧標籤和搜尋
description: 更新或移除不正確的智慧型標籤，以改善標籤的相關性
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 管理智慧標籤和搜尋 {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

您可以組織智慧型標籤，移除可能指派給品牌影像的任何不正確標籤，以便只顯示最相關的標籤。

協調智慧型標籤也有助於調整以標籤為基礎的影像搜尋，確保影像出現在搜尋結果中，以找出最相關的標籤。 基本上，它有助於消除不相關影像在搜尋結果中顯示的機率。

您也可以指派較高的排名給標籤，以提高其與影像的相關性。 促銷影像的標籤會增加當根據特定標籤執行搜尋時，在搜尋結果中出現影像的機率。

1. 在OmniSearch方塊中，根據標籤搜尋資產。
1. 檢查搜尋結果，以識別與搜尋無關的影像。
1. 選取影像，然後從工具列點選「 **[!UICONTROL 管理標籤]** 」。
1. 從「管 **[!UICONTROL 理標籤]** 」頁面檢查標籤。 如果您不想根據特定標籤來搜尋影像，請選取標籤，然後從工具列點選「 **[!UICONTROL 刪除]** 」。 或者，按一下／點選 `X` 出現在標籤旁的符號。
1. 若要指派較高的排名給標籤，請選取標籤並點選工具列 **[!UICONTROL 中的]** 「升級」。 您促銷的標籤會移至「標籤 **[!UICONTROL 」區]** 域。
1. 按一下／點 **[!UICONTROL 選「儲存]**」，然後按一下／點選「 **[!UICONTROL 確定]** 」以關閉「成功」對話方塊。
1. 導覽至影像的屬性頁面。 請注意，您促銷的標籤已指派高關聯性，因此在搜尋結果中會顯示高度。

## 使用智慧型標籤瞭解AEM搜尋結果 {#understandsearch}

依預設，AEM搜尋會將搜尋詞與子句結 `AND` 合。 使用智慧型標籤不會變更此預設行為。 使用智慧型標籤會新增一 `OR` 個額外的子句，以尋找套用智慧型標籤中的任何搜尋詞。 For example, consider searching for `woman running`. 預設情況下， `woman` 中繼資 `running` 料中只包含或只包含關鍵字的資產不會出現在搜尋結果中。 但是，標籤有或使用智 `woman` 慧標 `running` 記的資產會出現在此類搜尋查詢中。 所以搜索結果是，

* 資產 `woman` 和 `running` 中繼資料中的關鍵字。

* 資產智慧標籤為其中一個關鍵字。

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 的匹配 `woman running` 項。
1. 在智慧型標 `woman running` 簽中的相符項目。
1. 在智慧標 `woman` 記中 `running` 的相符項目。
