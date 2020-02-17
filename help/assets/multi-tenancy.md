---
title: 系列、程式碼片段和程式碼片段範本的多租用功能
description: 瞭解多租賃功能如何讓您根據客戶組織來隔離CRX存放庫中的內容，以防止未經授權的存取。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 系列、程式碼片段和程式碼片段範本的多租用功能 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租賃功能可讓您根據組織首碼和組織ID，在CRX中區隔內容，以保護內容不受其他組織使用者未經授權的存取。

Adobe Experience Manager(AEM)Assets會將每個組織的資料儲存在不同的路徑中。 每個組織特定路徑都由組織首碼和組織ID來識別，這些ID包含在CRX中儲存不同類型資產的傳統位置中。

例如，如果您建立名為的檔案夾， `Demo`AEM資產通常會將檔案夾儲存在 `../content/dam/Demo`。 啟用多租賃後，您現在可以將資料儲存在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果 [!DNL Adobe Marketing Cloud] AEM Assets（隨選）的使用者已指派給組織 `aodpremium` ，您可以使用多租賃功能來設定路徑以區 `../content/dam/<mac>/<aodpremium>Demo` 隔其內容。 在此範例中， `mac` 是組織首碼 `aodpremium` 和組織ID。

根據使用者的組織和ID，此合格路徑會顯示在AEM Assets介面和各種精靈中，包括「移動」和「程式碼片段建立」精靈，以強制隔離。

「多租賃」功能可讓您分隔下列資產和元件類型：

* 集合
* 公開系列
* 目錄（包括「新增／選擇頁面」精靈）
* 範本
* 程式碼片段範本
* 燈箱
