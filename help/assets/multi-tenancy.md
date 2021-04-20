---
title: 系列、程式碼片段和程式碼片段範本的多租用功能
description: 瞭解多租賃功能如何讓您根據客戶組織來隔離CRX存放庫中的內容，以防止未經授權的存取。
contentOwner: AG
role: Architect, Administrator, Leader
feature: Collections
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# 系列、程式碼片段和程式碼片段範本的多租賃{#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租賃功能可讓您根據組織首碼和組織ID，在CRX中區隔內容，以保護內容不受其他組織使用者未經授權的存取。

[!DNL Adobe Experience Manager Assets] 將每個組織的資料儲存在不同的路徑中。每個組織特定路徑都由組織首碼和組織ID來識別
它包含在CRX中儲存不同類型資產的傳統位置。

例如，如果您建立名為`Demo`的資料夾，則[!DNL Experience Manager]資產通常會將資料夾儲存在`../content/dam/Demo`。 啟用多租賃後，您現在可以在`../content/dam/<organization prefix>/<organization id>Demo`儲存資料

例如，如果[!DNL Assets]（隨選）的[!DNL Adobe Marketing Cloud]使用者已指派給`aodpremium`組織，您可以使用多租賃功能來設定`../content/dam/<mac>/<aodpremium>Demo`路徑以區隔其內容。 在此範例中，`mac`是組織首碼，`aodpremium`是組織ID。

根據使用者的組織和ID，此限定路徑會顯示在[!DNL Assets]介面和各種精靈中，包括「移動」和「程式碼片段建立」精靈，以執行隔離。

「多租賃」功能可讓您分隔下列資產和元件類型：

* 集合
* 公開系列
* 目錄（包括「新增／選擇頁面」精靈）
* 範本
* 程式碼片段範本
* 燈箱
