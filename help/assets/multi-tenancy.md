---
title: 集合、代碼段和代碼段模板的多租賃
description: 瞭解多租賃功能如何讓您能夠根據客戶組織將CRX儲存庫中的內容隔離，以防止未經授權的訪問。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 集合、代碼段和代碼段模板的多租賃 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租賃功能允許您根據組織前置詞和組織ID在CRX中隔離內容，以保護內容不受其他組織用戶未經授權的訪問。

[!DNL Adobe Experience Manager Assets] 將每個組織的資料儲存在不同的路徑中。 每個特定於組織的路徑都由組織前置詞和組織ID標識，這些ID包括在傳統位置中，在該位置，不同類型的資產儲存在CRX中。

例如，如果建立名為 `Demo`。 [!DNL Experience Manager] 資產通常將資料夾儲存在 `../content/dam/Demo`。 啟用多租賃後，您現在可以在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果 [!DNL Adobe Marketing Cloud] 用戶 [!DNL Assets] （按要求） `aodpremium` 組織，您可以使用多租賃功能來配置 `../content/dam/<mac>/<aodpremium>Demo` 分離其內容的路徑。 在本例中， `mac` 是組織前置詞 `aodpremium` 是組織ID。

根據用戶的組織和ID，此限定路徑顯示在 [!DNL Assets] 介面和各種嚮導，包括用於強制隔離的「移動」和「代碼段建立」嚮導。

「多租賃」功能允許您隔離以下類型的資產和元件：

* 集合
* 公共集合
* 目錄（包括「添加/選擇頁面」嚮導）
* 範本
* 代碼段模板
* 燈箱
