---
title: 指定要嵌入的字型
seo-title: Specifying fonts to embed
description: 瞭解如何指定要嵌入的字型。
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 指定要嵌入的字型 {#specifying-fonts-to-embed}

您可以指定始終嵌入或永遠不嵌入Forms服務生成的表單的字型。 嵌入字型會增加表單的檔案大小。 嵌入用戶在其系統上很少使用的異常字型。 不要嵌入通常安裝的常用字型。

>[!NOTE]
>
>如果為Forms指定了自定義XCI檔案，則XCI檔案中的嵌入字型選項將覆蓋這些設定。 (請參閱 [配置Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)

1. 在管理控制台中，按一下 **[!UICONTROL 服務>Forms]**。
1. 下 **[!UICONTROL 字型嵌入設定]**，也請參見Wiki頁。 **[!UICONTROL 始終嵌入字型]** 框中，鍵入要嵌入的字型的名稱，用逗號分隔。 指定的字型僅在生成的表單中使用時才嵌入。 如果已在傳遞給服務的XCI檔案中啟用了嵌入字型選項，則忽略此設定，因為在這種情況下，PDF中使用的所有字型都始終是嵌入的。
1. 在 **[!UICONTROL 從不嵌入字型]** 框中，鍵入不用表單嵌入的字型的名稱，用逗號分隔。 您指定的字型不嵌入到PDF中，即使它們在生成的PDF中使用。 如果傳遞到服務的XCI檔案中的嵌入字型選項已關閉，則忽略此設定，因為在這種情況下，PDF中使用的字型都未嵌入。
1. 按一下「**[!UICONTROL 儲存]**」。
