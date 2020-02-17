---
title: 指定要嵌入的字型
seo-title: 指定要嵌入的字型
description: 瞭解如何指定要內嵌的字型。
seo-description: 瞭解如何指定要內嵌的字型。
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定要嵌入的字型 {#specifying-fonts-to-embed}

您可以指定哪些字型永遠嵌入或永遠不嵌入Forms服務生成的表單。 內嵌字型會增加表單的檔案大小。 內嵌使用者很少在其系統上使用的不尋常字型。 請勿嵌入通常已安裝的常用字型。

>[!NOTE]
>
>如果您已為Forms指定自訂XCI檔案，XCI檔案中的內嵌字型選項會覆寫這些設定。 (請參 [閱設定表單位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)

1. 在管理控制台中，按一 **[!UICONTROL 下「服務>表單]**」。
1. 在「 **[!UICONTROL 字型內嵌設定]**」下方的「永遠內嵌字型 **** 」方塊中，輸入要與表單內嵌的字型名稱，以逗號分隔。 您指定的字型只會內嵌在產生的表單中（如果在表單中使用）。 如果傳遞至服務的XCI檔案中已開啟內嵌字型選項，則會忽略此設定，因為在這種情況下，PDF中使用的所有字型都會一律內嵌。
1. 在「不 **[!UICONTROL 要嵌入字型]** 」方塊中，輸入不要與表單內嵌的字型名稱，以逗號分隔。 您指定的字型不會嵌入在PDF中，即使這些字型用在產生的PDF中亦然。 如果傳遞至服務的XCI檔案中的內嵌字型選項已關閉，則會忽略此設定，因為在此情況下，PDF中使用的字型均未內嵌。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

