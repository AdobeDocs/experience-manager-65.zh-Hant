---
title: 指定要嵌入的字型
description: 瞭解如何指定要嵌入最適化表單的字型。 您可以指定將哪些字型嵌入或絕不嵌入到Forms服務產生的表單中。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 指定要嵌入的字型{#specify-fonts-to-embed}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以指定哪些字型永遠會嵌入或絕不會嵌入至「輸出」使用的表單。 嵌入字型會增加表單的檔案大小。 嵌入使用者不太可能在其系統上擁有的異常字型，並且不要嵌入他們將會安裝的常見字型。

>[!NOTE]
>
>如果您已經為輸出指定了自訂XCI檔案，則XCI檔案中的內嵌字型選項會覆寫這些設定。 （請參閱[指定輸出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)的檔案位置。）

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「字型嵌入設定」下的「永遠嵌入字型」方塊中，輸入要嵌入表單的字型名稱，並以逗號分隔。 您指定的字型只有在用於表單時，才會內嵌在產生的表單中。 如果在傳遞給服務的XCI檔案中開啟了內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的所有字型一律會內嵌。
1. 在「永不嵌入字型」方塊中，輸入不要嵌入表單的字型名稱，並以逗號分隔。 您指定的字型不會內嵌在PDF中，即使這些字型用於產生的PDF中亦然。 如果已在傳遞給服務的XCI檔案中關閉內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的字型都不會嵌入。
1. 按一下「儲存」。
