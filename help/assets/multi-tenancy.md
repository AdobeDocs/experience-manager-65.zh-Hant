---
title: 收藏集、代碼片段和代碼片段範本的多重租用
description: 瞭解多租使用者功能如何讓您根據客戶組織在CRX存放庫中區隔內容，以防止未經授權的存取。
contentOwner: AG
role: Developer, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c73531c3-4c05-471e-beff-cefb35857910
    internal-label: Collections
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%
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
