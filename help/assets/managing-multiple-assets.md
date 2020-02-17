---
title: 管理多個資產和系列
description: 瞭解如何同時編輯多個資產和系列的中繼資料，以快速傳播常見的中繼資料變更。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 管理資產和系列 {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager(AEM)Assets可讓您同時編輯多個資產的中繼資料，以便快速將一般中繼資料變更大量傳播至資產。 您也可以大量編輯多個系列的中繼資料。

使用「屬性」頁面，對多個資產或系列執行中繼資料變更：

* 將中繼資料屬性變更為公用值
* 新增或修改標籤

若要自訂中繼資料屬性頁面，包括新增、修改、刪除中繼資料屬性，請使用架構編輯器。

>[!NOTE]
>
>大量編輯方法適用於資料夾或系列中的可用資產。 對於跨資料夾可用或符合一般准則的資產，可在搜尋後 [大量更新中繼資料](search-assets.md#metadataupdates)。

## 編輯多個資產的中繼資料屬性 {#editing-metadata-properties-of-multiple-assets}

1. 在「資產」使用者介面中，導覽至您要編輯的資產所在的位置。
1. 選取您要編輯其常用屬性的資產。
1. 在工具列中點選／按一下「 **[!UICONTROL 屬性]** 」圖示，以開啟所選資產的屬性頁面。

   >[!NOTE]
   >
   >當您選取多個資產時，會為資產選取最低的共同父級表單。 換言之，屬性頁面只會顯示所有個別資產屬性頁面上共用的中繼資料欄位。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消選取清單中的其餘資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在屬性頁面中，您可以取消選取資產，從資產清單中移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產的中繼資料不會更新。
   >* 在資產清單頂端，選取「標題」旁的核取方塊 **** ，以在選取資產和清除清單之間切換。


1. 若要為資產選取不同的中繼資料結構，請點選／按一下工具列中的 **[!UICONTROL 「設定]** 」圖示，然後選取所要的結構。
1. 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。 如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。 點選／按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 編輯多個系列的中繼資料屬性 {#editing-metadata-properties-of-multiple-collections}

1. 從「系列」控制台中，選取您要編輯的系列。
1. 在工具列中點選／按一 **[!UICONTROL 下「屬性]** 」，以開啟所選系列的屬性頁面。
1. 在各種標籤下修改所選系列的中繼資料屬性。

   >[!NOTE]
   >
   >您為所選系列新增的中繼資料會覆寫這些系列的先前中繼資料，但標籤除外。 您在「標籤」欄位中新 **[!UICONTROL 增的任何標籤]** ，都會附加至中繼資料中現有的標籤清單。

1. 若要檢視特定系列的中繼資料屬性，請取消選取系列清單中的其餘系列。 中繼資料編輯器欄位會填入特定系列的中繼資料。

   >[!NOTE]
   >
   >* 在系列屬性頁面中，您可以取消選取系列，從系列清單中移除系列。 系列清單預設會選取所有系列。 您移除之系列的中繼資料不會更新。
   >* 在清單頂端，選取「標題」( **[!UICONTROL Title]** )附近的核取方塊，在選取系列和清除清單之間切換。


1. 儲存變更。

## 設定大量中繼資料更新的限制 {#configlimit}

為避免DOS類似情況，AEM會限制Sling請求中支援的參數數。 一次更新許多資產的中繼資料時，您可能會達到限制，而且無法針對更多資產更新中繼資料。 AEM會在記錄檔中產生下列警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

若要變更限制，請存取Web Console( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**)並變更 **[!UICONTROL Apache Sling Parameters Request Apache Handling Osgi Configuration的]****** Maximum POST Parameters Praters Aremeters的值。
