---
title: 收藏集、代碼片段和代碼片段範本的多重租用
description: 瞭解多租使用者功能如何讓您根據客戶組織在CRX存放庫中區隔內容，以防止未經授權的存取。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 收藏集、代碼片段和代碼片段範本的多重租用 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租使用者功能可讓您根據組織首碼和組織ID在CRX中分隔內容，以防止其他組織的使用者未經授權存取內容。

[!DNL Adobe Experience Manager Assets]會以不同路徑儲存每個組織的資料。 每個組織特定的路徑由組織首碼和組織識別碼來識別
包括在傳統位置，不同型別的資產會儲存在CRX中。

例如，如果您建立名為`Demo`的資料夾，[!DNL Experience Manager]資產傳統上會將資料夾儲存在`../content/dam/Demo`。 啟用多租使用者後，您現在可以將資料儲存在`../content/dam/<organization prefix>/<organization id>Demo`

例如，如果針對指派給`aodpremium`組織的[!DNL Assets] （隨選）的[!DNL Adobe Marketing Cloud]位使用者，您可以使用多租使用者功能來設定`../content/dam/<mac>/<aodpremium>Demo`路徑以分隔其內容。 在此範例中，`mac`是組織首碼，`aodpremium`是組織識別碼。

根據使用者的組織和ID，此合格路徑會顯示在[!DNL Assets]介面和各種精靈中，包括強制隔離的「移動」和「程式碼片段」建立精靈。

多租使用者功能可讓您分隔下列資產和元件型別：

* 集合
* 公開集合
* 目錄（包括「新增/選取頁面」精靈）
* 範本
* 程式碼片段範本
* Lightbox
