---
title: AEM中的網頁主控台
description: 瞭解如何使用Adobe Experience Manager (AEM)中的網頁主控台。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# Web 主控台{#web-console}

Adobe Experience Manager (AEM)中的Web主控台是根據 [Apache Felix Web管理主控台](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix是社群努力實施OSGi R4服務平台，其中包括OSGi架構和標準服務。

>[!NOTE]
>
>在Web主控台上，提及預設設定的任何說明都與Sling預設值有關。
>
>AEM有其本身的預設值，因此預設集可能會與主控台上的記錄不同。

Web主控台提供一系列用於維護OSGi套裝的標籤，包括：

* [設定](#configuration)：用於設定OSGi套件組合，因此是設定AEM系統引數的基礎機制
* [組合](#bundles)：用於安裝套件組合
* [元件](#components)：用於控制AEM所需元件的狀態

所做的任何變更都會立即套用至執行中的系統。 不需要重新啟動。

主控台可從下列位置存取： `../system/console`；例如：

`http://localhost:4502/system/console/components`

## 設定 {#configuration}

此 **設定** tab可用來設定OSGi組合，因此是設定AEM系統引數的基礎機制。

>[!NOTE]
>
>另請參閱 [使用Web主控台進行OSGi設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 以取得更多詳細資料。

此 **設定** 索引標籤可透過以下任一方式存取：

* 下拉式功能表：

  **OSGi >**

* URL；例如：

  `http://localhost:4502/system/console/configMgr`

隨即顯示設定清單：

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

此畫面上的下拉式清單提供兩種型別的設定：

* **設定**

  可讓您更新現有的組態。 這些具有持續性身分(PID)，可以是：

   * 標準及為AEM不可或缺的一部分；若刪除這些值，則會傳回預設設定。
   * 從「工廠組態」建立的執行處理；這些執行處理是由使用者建立的，刪除會移除執行處理。

* **工廠組態**

  建立所需功能物件的例項。

  這會配置給「持續性身分」，並列在「組態」下拉式清單中。

從清單中選取任何專案時，會顯示與該組態相關的引數：

![chlimage_1-61](assets/chlimage_1-61.png)

之後，您可以視需要更新引數，並且：

* **儲存**

  儲存所做的變更。

  對於「工廠組態」，這會建立具有持續識別的執行個體。 新執行個體會列在「設定」底下。

* **重設**

  將熒幕上顯示的引數重設為上次儲存的引數。

* **刪除**

  刪除目前的設定。 若為standard，引數會傳回預設設定。 如果是從「工廠組態」建立，則會刪除特定的執行處理。

* **解除繫結**

  從套件組合解除繫結目前組態。

* **取消**

  取消任何目前的變更。

## 組合 {#bundles}

此 **組合** tab是安裝AEM所需的OSGi套件組合的機制。 可透過下列任一方法來存取標籤：

* 下拉式功能表：

  **OSGi >**

* URL；例如：

  `http://localhost:4502/system/console/bundles`

隨即顯示套件組合清單：

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

您可以使用此標籤：

* **安裝或更新**

  您可以 **瀏覽** 以尋找包含您的套件組合的檔案，並指定它是否應 **開始** 立即且 **開始層級**.

* **重新載入**

  重新整理顯示的清單。

* **重新整理封裝**

  這會檢查所有套件的參考，並在必要時重新整理。

  例如，在更新後，由於先前的參照，舊版本和新版本可能仍在執行。 此選項會檢查並移動新版本的所有參照，讓舊版本停止。

* **啟動**

  根據指定的起始層級啟動束。

* **停止**

  停止束。

* **解除安裝**

  從系統解除安裝套件。

* **檢視狀態**

  清單會指定束的狀態；按一下包含進一步資訊的特定束名稱。

>[!NOTE]
>
>晚於 **更新**，Adobe建議您執行 **重新整理封裝**.

## 元件 {#components}

此 **元件** 索引標籤可讓您啟用和/或停用各種元件。 您可透過以下任一方式存取該區域：

* 下拉式功能表：

  **主要 >**

* URL；例如：

  `http://localhost:4502/system/console/components`

隨即顯示元件清單。 有各種圖示可讓您啟用、停用或（在適當時）開啟特定元件的組態詳細資訊。

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

按一下特定元件的名稱會顯示其狀態的進一步資訊。 您也可以在此處啟用、停用或重新載入元件。

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>啟用或停用元件只適用於AEM/CRX重新啟動之前。
>
>開始狀態是在元件描述項中定義，在開發期間產生並在套件建立時儲存在套件中。
