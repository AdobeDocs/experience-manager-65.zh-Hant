---
title: 建立自訂表單映射
seo-title: 建立自訂表單映射
description: 當您在Adobe Campaign中建立自訂表格時，您可能想要在AEM中建立對應至該自訂表格的表格
seo-description: 當您在Adobe Campaign中建立自訂表格時，您可能想要在AEM中建立對應至該自訂表格的表格
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建立自訂表單映射{#creating-custom-form-mappings}

當您在Adobe Campaign中建立自訂表格時，您可能想要在AEM中建立對應至該自訂表格的表格。

本檔案說明如何建立自訂表單對應。 當您完成本檔案中的步驟時，您將會提供您的使用者一個活動頁面，讓使用者可在其中註冊即將舉行的活動。 然後您透過Adobe Campaign跟進這些使用者。

## 必備條件 {#prerequisites}

您需要安裝下列程式碼：

* Adobe Experience Manager
* Adobe Campaign Classic

如需詳 [細資訊，請參閱「整合AEM與Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) 」。

## 建立自訂表單映射 {#creating-custom-form-mappings-2}

若要建立自訂表單映射，您必須遵循下列高階步驟，這些步驟在下列各節中有詳細說明：

1. 建立自訂表格。
1. 延伸種 **子表** 。
1. 建立自訂對應。
1. 根據自訂對應建立傳送。
1. 在AEM中建立表單，然後使用已建立的傳送。
1. 提交表單以進行測試。

### 在Adobe Campaign中建立自訂表格 {#creating-the-custom-table-in-adobe-campaign}

首先，在Adobe Campaign中建立自訂表格。 在此範例中，我們使用下列定義來建立事件表：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

建立事件表後，運行「更新數 **據庫結構」嚮導** ，以建立表。

### 擴展種子表 {#extending-the-seed-table}

在Adobe Campaign中，點選／按一 **下「新增** 」，以建立新的 **種子位址(nms)表格延伸** 。

![chlimage_1-194](assets/chlimage_1-194.png)

現在，請使用事件表 **格中** 的欄位來擴 **展種子表** :

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之後，運行「更 **新資料庫」嚮導** ，以應用更改。

### 建立自訂目標對應 {#creating-custom-target-mapping}

在「管 **理／促銷活**&#x200B;動管理」中， **移至「目標對應** 」並新增新的「**目標對應」。**

>[!NOTE]
>
>請確定您對內部名稱使用有意義 **的名稱**。

![chlimage_1-195](assets/chlimage_1-195.png)

### 建立自訂傳送範本 {#creating-a-custom-delivery-template}

在此步驟中，您要新增使用已建立之 **Target對應的傳送範本**。

在「 **資源／範本**」中，導覽至「傳送範本」並複製現有的AEM傳送。 按一下「至 **」**，選取建立事件 **Target對應**。

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM中建立表格 {#building-the-form-in-aem}

在AEM中，請確定您已在「頁面屬性」中設定 **雲端服務**。

然後，在「 **Adobe Campaign** 」標籤中，選取在「建立自訂傳送範本」 [中建立的傳送](#creating-a-custom-delivery-template)。

![chlimage_1-197](assets/chlimage_1-197.png)

設定欄位時，請務必為表單欄位指定唯一的元素名稱。

配置欄位後，您需要手動變更對應。

在CRXDE-lite中，移至 **jcr:content** (of the page)節點，並將 **acMapping** 值變更為 **Target映射的內部名稱**。

![chlimage_1-198](assets/chlimage_1-198.png)

在表單的配置中，請務必勾選核取方塊以在非現有時建立

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表格 {#submitting-the-form}

您現在可以提交表單，並在Adobe Campaign端驗證是否儲存值。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑難排解 {#troubleshooting}

**&quot;元素&#39;@eventdate&#39;中值&#39;02/02/2015&#39;的類型無效(&#39;Event([adb:event])&#39;類型的檔案)&quot;**

提交表單時，此錯誤會記錄在AEM **的error.log** 中。

這是由於日期欄位的格式無效。 因應措施是 **提供yyyy-mm-dd** 作為值。

