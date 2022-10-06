---
title: 建立自訂表單對應
seo-title: Creating Custom Form Mappings
description: 在Adobe Campaign中建立自訂表格時，您可能想在AEM中建立對應至該自訂表格的表單
seo-description: When you create a custom table in Adobe Campaign, you may want to build a form in AEM that maps to that custom table
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 建立自訂表單對應{#creating-custom-form-mappings}

在Adobe Campaign中建立自訂表格時，您可能想在AEM中建立對應至該自訂表格的表單。

本檔案說明如何建立自訂表單對應。 完成本檔案中的步驟後，您會為使用者提供一個事件頁面，讓他們註冊即將發生的事件。 接著，請透過Adobe Campaign追蹤這些使用者。

## 必備條件 {#prerequisites}

您需要安裝下列程式：

* Adobe Experience Manager
* Adobe Campaign Classic

請參閱 [整合AEM與Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) 以取得更多資訊。

## 建立自訂表單對應 {#creating-custom-form-mappings-2}

若要建立自訂表單對應，您必須遵循下列高階步驟，以下各節將詳細說明這些步驟：

1. 建立自訂表格。
1. 擴充 **種子** 表格。
1. 建立自訂對應。
1. 根據自訂對應建立傳送。
1. 在AEM中建置表單，使用已建立的傳送。
1. 提交表單以測試。

### 在Adobe Campaign中建立自訂表格 {#creating-the-custom-table-in-adobe-campaign}

首先，在Adobe Campaign中建立自訂表格。 在此範例中，我們使用下列定義來建立事件表格：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

建立事件表格後，執行 **更新資料庫結構嚮導** 來建立表格。

### 擴展種子表 {#extending-the-seed-table}

在Adobe Campaign中，點選/按一下 **新增** 若要建立新的擴充功能 **種子地址(nms)** 表格。

![chlimage_1-194](assets/chlimage_1-194.png)

現在，請使用 **事件** 表以擴展 **種子** 表格：

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之後，執行 **更新資料庫嚮導** 來套用變更。

### 建立自訂目標對應 {#creating-custom-target-mapping}

在 **管理/行銷活動管理** t，轉到 **目標對應** 並添加新T **目標映射。**

>[!NOTE]
>
>請務必為 **內部名稱**.

![chlimage_1-195](assets/chlimage_1-195.png)

### 建立自訂傳送範本 {#creating-a-custom-delivery-template}

在此步驟中，您新增的傳送範本會使用建立的 **目標對應**.

在 **資源/範本**，導覽至「傳送範本」並複製現有的AEM傳送。 當您按一下 **結束日期**，選取「建立事件」 **目標對應**.

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM中建立表單 {#building-the-form-in-aem}

在AEM中，請確定您已在 **頁面屬性**.

然後，在 **Adobe Campaign** 索引標籤，選取在 [建立自訂傳送範本](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

設定欄位時，請務必為表單欄位指定唯一的元素名稱。

設定欄位後，您需要手動變更對應。

在CRXDE-lite中，前往 **jcr:content** （頁面的）節點，並變更 **acMapping** 值轉換為 **目標對應**.

![chlimage_1-198](assets/chlimage_1-198.png)

在表單的設定中，請務必勾選核取方塊，以在非現有時建立

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表單 {#submitting-the-form}

您現在可以提交表單，並在Adobe Campaign端驗證值是否已儲存。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑難排解 {#troubleshooting}

**&quot;元素&#39;@eventdate&#39;中值&#39;02/02/2015&#39;的類型無效(&#39;Event&#39;類型的檔案([adb:event])&#39;)&quot;**

提交表單時，此錯誤會記錄在 **error.log** 在AEM中。

這是因為日期欄位的格式無效。 因應措施是 **yyyy-mm-dd** 作為值。
