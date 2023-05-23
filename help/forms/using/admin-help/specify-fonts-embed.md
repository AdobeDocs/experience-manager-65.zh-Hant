---
title: 指定要嵌入的字型
seo-title: Specify fonts to embed
description: 瞭解如何指定要嵌入的字型。
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 指定要嵌入的字型{#specify-fonts-to-embed}

您可以指定始終嵌入或永遠不嵌入由輸出使用的表單的字型。 嵌入字型會增加表單的檔案大小。 嵌入用戶在其系統上不可能擁有的異常字型，並且不嵌入他們將要安裝的常見字型。

>[!NOTE]
>
>如果為「輸出」指定了自定義XCI檔案，則XCI檔案中的嵌入字型選項將覆蓋這些設定。 (請參閱 [為輸出指定檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)

1. 在管理控制台中，按一下「服務」>「輸出」。
1. 在「字型嵌入設定」下，在「始終嵌入字型」框中，鍵入要用表單嵌入的字型名稱，用逗號分隔。 指定的字型僅在生成的表單中使用時才嵌入。 如果已在傳遞給服務的XCI檔案中開啟嵌入字型選項，則忽略此設定。 在這種情況下，PDF中使用的所有字型都始終被嵌入。
1. 在「從不嵌入字型」框中，鍵入不用表單嵌入的字型的名稱，用逗號分隔。 您指定的字型不嵌入到PDF中，即使它們在生成的PDF中使用。 如果在傳遞給服務的XCI檔案中禁用了嵌入字型選項，則忽略此設定。 在這種情況下，PDF中使用的字型均未嵌入。
1. 按一下「儲存」。
