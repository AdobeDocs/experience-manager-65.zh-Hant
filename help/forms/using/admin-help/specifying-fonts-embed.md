---
title: 指定要嵌入的字型
description: 瞭解如何指定要嵌入最適化表單的字型。 您可以指定將哪些字型嵌入或絕不嵌入到Forms服務產生的表單中。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%
---
# 指定要嵌入的字型 {#specifying-fonts-to-embed}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以指定哪些字型一律會內嵌或絕不會內嵌於Forms服務產生的表單。 嵌入字型會增加表單的檔案大小。 內嵌使用者很少在其系統上使用的不尋常字型。 請勿嵌入通常已安裝的常用字型。

>[!NOTE]
>
>如果您已為Forms指定自訂XCI檔案，則XCI檔案中的內嵌字型選項會覆寫這些設定。 （請參閱[設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。）

1. 在管理控制檯中，按一下&#x200B;**[!UICONTROL 服務> Forms]**。
1. 在&#x200B;**[!UICONTROL 字型內嵌設定]**&#x200B;下，在&#x200B;**[!UICONTROL 永遠內嵌字型]**&#x200B;方塊中，鍵入要內嵌表單的字型名稱（以逗號分隔）。 您指定的字型只有在用於表單時，才會內嵌在產生的表單中。 如果已在傳遞至服務的XCI檔案中開啟內嵌字型選項，則會忽略此設定，因為在此情況下，PDF中使用的所有字型都會內嵌。
1. 在&#x200B;**[!UICONTROL 永不嵌入字型]**&#x200B;方塊中，輸入不要嵌入表單的字型名稱，並以逗號分隔。 您指定的字型不會內嵌於PDF中，即使這些字型用於產生的PDF中亦然。 如果在傳遞給服務的XCI檔案中關閉了內嵌字型選項，則會忽略此設定，因為在這種情況下，PDF中使用的字型都不會內嵌。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。
