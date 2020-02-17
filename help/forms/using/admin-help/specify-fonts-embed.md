---
title: 指定要內嵌的字型
seo-title: 指定要內嵌的字型
description: 瞭解如何指定要內嵌的字型。
seo-description: 瞭解如何指定要內嵌的字型。
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定要內嵌的字型{#specify-fonts-to-embed}

您可以指定哪些字型永遠嵌入或永遠不嵌入「輸出」使用的表單。 內嵌字型會增加表單的檔案大小。 內嵌使用者在其系統上不可能擁有的不尋常字型，且不會嵌入他們將會安裝的常見字型。

>[!NOTE]
>
>如果您已為「輸出」指定自訂XCI檔案，XCI檔案中的內嵌字型選項會覆寫這些設定。 (請參 [閱指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)

1. 在管理控制台中，按一下「服務>輸出」。
1. 在「字型內嵌設定」的「永遠內嵌字型」方塊中，輸入要與表單內嵌的字型名稱，並以逗號分隔。 您指定的字型只會內嵌在產生的表單中（如果在表單中使用）。 如果已在傳遞至服務的XCI檔案中開啟內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的所有字型都一律會內嵌。
1. 在「永不嵌入字型」方塊中，輸入不要與表單內嵌的字型名稱（以逗號分隔）。 您指定的字型不會嵌入在PDF中，即使這些字型用在產生的PDF中亦然。 如果已在傳送至服務的XCI檔案中關閉內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的字型都不會嵌入。
1. 按一下「儲存」。

