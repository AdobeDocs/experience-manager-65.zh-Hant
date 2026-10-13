---
title: 變更字元集
description: 您可以指定用來編碼輸出資料流的字元集。 瞭解如何變更字元集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
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
source-wordcount: '144'
ht-degree: 1%
---
# 變更字元集 {#change-the-character-set}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以指定用來編碼輸出資料流的字元集。

1. 在管理主控台中，按一下&#x200B;**[!UICONTROL 服務>輸出]**。
1. 在「國際化」下的「字元集」清單中，選取字元集。 此設定相依於透過API指定的`TransformationFormat`和`PrintFormat`。 若要指定所列字元集以外的字元集，請選取「自訂」，並在顯示的方塊中指定編碼值。

   如果`TransformationFormat`是PDF，而PDF/A或`PrintFormat`是PCL、PostScript、Zebra標籤、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，則僅支援特定字元集。

   字元集必須是有效的正式名稱。 預設值為ISO-8859-1。

1. 按一下&#x200B;**[!UICONTROL 儲存]**。
