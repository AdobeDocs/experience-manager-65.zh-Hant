---
title: 集合、片段和程式碼片段範本的多租用戶
description: 了解多租用戶功能如何讓您根據客戶組織來分隔CRX存放庫中的內容，以防止未經授權的存取。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 集合、片段和程式碼片段範本的多租用戶 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租用戶功能可讓您根據組織首碼和組織ID來分隔CRX中的內容，以保護內容不會受到其他組織的使用者未經授權的存取。

[!DNL Adobe Experience Manager Assets] 將每個組織的資料儲存在不同的路徑中。 每個組織特定路徑都由組織首碼和組織ID識別，這些ID包含在傳統位置中，不同類型的資產會儲存在CRX中。

例如，若您建立的資料夾名稱為 `Demo`, [!DNL Experience Manager] 資產通常會在 `../content/dam/Demo`. 啟用多租用戶後，您現在可以將資料儲存在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，若 [!DNL Adobe Marketing Cloud] 使用者 [!DNL Assets] （隨選） `aodpremium` 組織，您可以使用多租用戶功能來設定 `../content/dam/<mac>/<aodpremium>Demo` 分隔其內容的路徑。 在此範例中， `mac` 是組織首碼和 `aodpremium` 是組織ID。

根據使用者的組織和ID，此合格路徑會顯示在 [!DNL Assets] 介面和各種嚮導，包括用於強制隔離的「移動」和「代碼段」建立嚮導。

多租用戶功能可讓您分隔下列資產和元件類型：

* 集合
* 公用集合
* 目錄（包括「添加/選擇頁面」嚮導）
* 範本
* 程式碼片段範本
* Lightbox
