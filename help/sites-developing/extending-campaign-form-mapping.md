---
title: 建立自定義表單映射
seo-title: Creating Custom Form Mappings
description: 在Adobe Campaign建立自定義表時，可能希望在中生成一個映射AEM到該自定義表的表單
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
ht-degree: 2%

---

# 建立自定義表單映射{#creating-custom-form-mappings}

在Adobe Campaign建立自定義表時，可能希望在映射到該自AEM定義表的窗體中生成。

本文檔介紹如何建立自定義表單映射。 完成本文檔中的步驟後，您將為用戶提供一個活動頁面，在該頁面中他們可以註冊一個即將發生的事件。 然後，您通過Adobe Campaign跟蹤這些用戶。

## 必備條件 {#prerequisites}

您需要安裝以下元件：

* Adobe Experience Manager
* Adobe Campaign Classic

請參閱 [與AEMAdobe Campaign Classic](/help/sites-administering/campaignonpremise.md) 的子菜單。

## 建立自定義表單映射 {#creating-custom-form-mappings-2}

要建立自定義表單映射，您需要遵循以下高級步驟，這些步驟將在以下各節中詳細介紹：

1. 建立自定義表。
1. 擴展 **種子** 的子菜單。
1. 建立自定義映射。
1. 基於自定義映射建立交貨。
1. 在中生成表單AEM，該表單將使用建立的傳遞。
1. 提交表單以test它。

### 在Adobe Campaign建立自定義表 {#creating-the-custom-table-in-adobe-campaign}

首先在Adobe Campaign建立自定義表。 在本示例中，我們使用以下定義建立事件表：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

建立事件表後，運行 **更新資料庫結構嚮導** 的子菜單。

### 擴展種子表 {#extending-the-seed-table}

在Adobe Campaign，點擊/按一下 **添加** 建立新擴展 **種子地址(nms)** 的子菜單。

![chlimage_1-194](assets/chlimage_1-194.png)

現在，使用 **事件** 要擴展的表 **種子** 表：

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

然後，跑 **更新資料庫嚮導** 按鈕。

### 建立自定義目標映射 {#creating-custom-target-mapping}

在 **管理/市場活動管理** t，轉到 **目標映射** 並添加新T **目標映射。**

>[!NOTE]
>
>確保使用有意義的名稱 **內部名稱**。

![chlimage_1-195](assets/chlimage_1-195.png)

### 建立自定義交貨模板 {#creating-a-custom-delivery-template}

在此步驟中，您將添加使用建立的 **目標映射**。

在 **資源/模板**，導航到「交貨模板」並複製現有AEM交貨。 按一下 **至**，選擇建立事件 **目標映射**。

![chlimage_1-196](assets/chlimage_1-196.png)

### 在中構建表AEM單 {#building-the-form-in-aem}

在AEM中，確保已在 **頁面屬性**。

然後，在 **Adobe Campaign** 頁籤，選擇在 [建立自定義交貨模板](#creating-a-custom-delivery-template)。

![chlimage_1-197](assets/chlimage_1-197.png)

配置欄位時，請確保為form-field指定唯一的element-name。

配置欄位後，需要手動更改映射。

在CRXDE-lite中，轉到 **jcr：內容** （共頁）節點，並更改 **acMapping** 的內部名稱的值 **目標映射**。

![chlimage_1-198](assets/chlimage_1-198.png)

在表單的配置中，確保選中複選框以在不存在時建立

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表單 {#submitting-the-form}

現在，您可以提交表單，並在Adobe Campaign一側驗證是否保存了這些值。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑難排解 {#troubleshooting}

**&quot;元素&quot;@eventdate&quot;中值&quot;02/02/2015&quot;的類型無效(類型為&quot;Event&quot;的文檔([adb：事件])&#39;)**

提交表單時，此錯誤將記錄在 **錯誤.log** 的上AEM界。

這是由於日期欄位的格式無效。 解決方法是提供 **yyyy-mm-dd** 值。
