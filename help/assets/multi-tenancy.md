---
title: 集合、片段和程式碼片段範本的多租用戶
description: 了解多租用戶功能如何讓您根據客戶組織來分隔CRX存放庫中的內容，以防止未經授權的存取。
contentOwner: AG
role: Architect, Admin, Leader
feature: 集合
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 1%

---

# 集合、片段和程式碼片段範本的多租用戶 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租用戶功能可讓您根據組織首碼和組織ID來分隔CRX中的內容，以保護內容不會受到其他組織的使用者未經授權的存取。

[!DNL Adobe Experience Manager Assets] 將每個組織的資料儲存在不同的路徑中。每個組織特定路徑由組織首碼和組織ID識別
包含在CRX中儲存不同資產類型的傳統位置。

例如，如果您建立名為`Demo`的資料夾， [!DNL Experience Manager]資產傳統上會將資料夾儲存在`../content/dam/Demo`。 啟用多租用戶後，您現在可以在`../content/dam/<organization prefix>/<organization id>Demo`儲存資料

例如，如果[!DNL Assets]的[!DNL Adobe Marketing Cloud]用戶（按需）被分配給`aodpremium`組織，則可以使用多租賃功能配置`../content/dam/<mac>/<aodpremium>Demo`路徑以隔離其內容。 在此範例中，`mac`是組織首碼，而`aodpremium`是組織ID。

根據用戶的組織和ID，此限定路徑顯示在[!DNL Assets]介面和各種嚮導中，包括用於強制隔離的「移動」和「代碼段」建立嚮導。

多租用戶功能可讓您分隔下列資產和元件類型：

* 集合
* 公用集合
* 目錄（包括「添加/選擇頁面」嚮導）
* 範本
* 程式碼片段範本
* Lightbox
