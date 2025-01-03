---
title: 設定國際化選項
description: 瞭解如何指定用於呈現表單的區域設定，以及如何指定用於編碼輸出資料流的字元集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# 設定國際化選項{#setting-internationalization-options}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

## 指定用於呈現表單的地區設定 {#specify-the-locale-used-to-render-forms}

您可以指定呈現PDF表單時使用的地區設定。 PDF表單上的欄位會使用指定的地區設定來顯示資料。 例如，如果語言環境設定為德文，則表單會使用德文小數分隔符號來分隔數值。 地區設定也可用來傳送驗證訊息給使用者端裝置（例如網頁瀏覽器），作為HTML轉換的一部分。

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「國際化」下的「語言」清單中，選取用來呈現表單的區域設定。 預設值為英文（美國）。
1. 按一下「儲存」。

## 指定用來編碼輸出資料流的字元集 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 在「國際化」下的「字元集」清單中，選取字元集。 此設定取決於所使用的API，即renderHTMLForm或renderPDFForm。 若要指定所列字元集以外的字元集，請選取「自訂」，並在顯示的方塊中指定編碼值。

   對於HTML轉換，AEM表單支援由`java.nio.charset`封裝定義的字元編碼值。 如果sFormPreference為PDForm，則僅支援特定字元集。 字元集必須是有效的正式名稱。 預設值為ISO-8859-1。

1. 按一下「儲存」。
