---
title: Web控制台AEM
description: 瞭解如何在中使用Web控制台AEM。
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# Web 主控台{#web-console}

(Adobe Experience Manager)中AEM的Web控制台基於 [Apache Felix Web管理控制台](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html)。 Apache Felix是一個社區努力來實施OSGi R4服務平台，該平台包括OSGi框架和標準服務。

>[!NOTE]
>
>在Web控制台上，任何提及預設設定的說明都與Sling預設值相關。
>
>具AEM有自己的預設值，因此預設設定可能與控制台上記錄的預設設定不同。

Web控制台提供了一系列頁籤，用於維護OSGi捆綁包，包括：

* [配置](#configuration):用於配置OSGi包，因此是配置系統參數AEM的基礎機制
* [捆綁](#bundles):用於安裝捆綁包
* [元件](#components):用於控制所需元件的狀AEM態

所做的任何更改都會立即應用於正在運行的系統。 不需要重新啟動。

可以從訪問控制台 `../system/console`;例如：

`http://localhost:4502/system/console/components`

## 設定 {#configuration}

的 **配置** 頁籤用於配置OSGi捆綁包，因此是配置系統參數的基礎AEM機制。

>[!NOTE]
>
>請參閱 [OSGi與Web控制台的配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 的上界。

的 **配置** 頁籤可通過以下任一方式訪問：

* 下拉菜單：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/configMgr`

將顯示配置清單：

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

此螢幕上的下拉清單中提供了兩種類型的配置：

* **設定**

   允許您更新現有配置。 它們具有持久標識(PID)，可以是：

   * 標準及整AEM體；如果刪除這些值，則這些值將返回預設設定。
   * 從工廠配置建立的實例；這些實例由用戶建立，刪除會刪除實例。

* **工廠配置**

   允許您建立所需功能對象的實例。

   這將分配一個持久標識，然後列在「配置」下拉清單中。

從清單中選擇任何條目將顯示與該配置相關的參數：

![chlimage_1-61](assets/chlimage_1-61.png)

然後，您可以根據需要更新參數，並：

* **儲存**

   保存所做的更改。

   對於工廠配置，這將建立具有持久標識的新實例。 新實例將列在「配置」下。

* **重設**

   將螢幕上顯示的參數重置為上次保存的參數。

* **刪除**

   刪除當前配置。 如果為標準，則參數將返回到預設設定。 如果從「工廠配置」建立，則刪除特定實例。

* **解除綁定**

   從捆綁包中解除綁定當前配置。

* **取消**

   取消任何當前更改。

## 捆綁 {#bundles}

的 **捆綁** tab是安裝所需OSGi束的機AEM制。 可通過以下任一方法訪問該頁籤：

* 下拉菜單：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/bundles`

將顯示捆綁包清單：

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

使用此頁籤，您可以：

* **安裝或更新**

   你可以 **瀏覽** 查找包含捆綁包的檔案，並指定是否應 **開始** 立即和 **起始級別**。

* **重新載入**

   刷新顯示的清單。

* **刷新包**

   這將檢查所有包的引用並根據需要刷新。

   例如，在更新後，由於先前的引用，舊版本和新版本可能仍在運行。 此選項將檢查並移動對新版本的所有引用，從而停止舊版本。

* **啟動**

   根據指定的起始級別啟動包。

* **停止**

   停止捆綁。

* **解除安裝**

   從系統中卸載該包。

* **查看狀態**

   該清單指定捆綁包的當前狀態；按一下特定束的名稱，並顯示詳細資訊。

>[!NOTE]
>
>之後 **更新** 建議執行 **刷新包**。

## 元件 {#components}

的 **元件** 頁籤中，您可以啟用和/或禁用各種元件。 可通過以下任一方訪問：

* 下拉菜單：

   **主要 >**

* URL;例如：

   `http://localhost:4502/system/console/components`

將顯示元件清單。 可以使用各種表徵圖來啟用、禁用或（在適當情況下）開啟特定元件的配置詳細資訊。

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

按一下特定元件的名稱將顯示有關其狀態的詳細資訊。 在此，您還可以啟用、禁用或重新載入元件。

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>啟用或禁用元件將只應用到AEM/CRX重新啟動。
>
>開始狀態在元件描述符中定義，該描述符在開發期間生成，並在包建立時儲存在包中。
