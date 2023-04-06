---
title: Adobe Experience Manager中的Web主控台
seo-title: Web Console
description: 了解如何使用AEM Web主控台。
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---

# Web 主控台{#web-console}

AEM中的Web主控台以 [Apache Felix Web Management Console](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix是社群的努力成果，目的是實作OSGi R4服務平台，其中包含OSGi架構和標準服務。

>[!NOTE]
>
>在Web主控台上，任何提及預設設定的說明都與Sling預設值相關。
>
>AEM有其專屬的預設值，因此預設值設定可能與主控台上記錄的不同。

Web主控台提供一系列標籤，用於維護OSGi套件組合，包括：

* [設定](#configuration):用於配置OSGi套件組合，因此是配置AEM系統參數的基礎機制
* [套件組合](#bundles):用於安裝套件
* [元件](#components):用於控制AEM所需元件的狀態

所做的任何更改都會立即應用於運行的系統。 不需要重新啟動。

此主控台可從 `../system/console`;例如：

`http://localhost:4502/system/console/components`

## 設定 {#configuration}

此 **設定** tab可用來設定OSGi套件組合，因此是設定AEM系統參數的基礎機制。

>[!NOTE]
>
>請參閱 [使用Web控制台進行OSGi配置](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊。

此 **設定** 標籤可透過下列任一方存取：

* 下拉式功能表：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/configMgr`

將顯示配置清單：

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

此畫面上的下拉式清單提供兩種設定：

* **配置**
可讓您更新現有的設定。 這些ID具有永久性身分(PID)，可以是：

   * 標準及整體AEM;如果刪除，則這些值會恢復為預設設定。
   * 從工廠配置建立的實例；這些執行個體由使用者建立，deletion會移除執行個體。

* **工廠配置**
可讓您建立所需功能物件的例項。

   系統會分配「永久性身分」，然後列在「設定」下拉式清單中。

從清單中選取任何項目時，都會顯示與該設定相關的參數：

![chlimage_1-21](assets/chlimage_1-21a.png)

接著，您就可以視需要更新參數，並：

* **儲存**

   儲存所做的變更。

   對於工廠配置，這將建立具有持久標識的新實例。 新執行個體便會列在「設定」下。

* **重設**

   將畫面上顯示的參數重設為上次儲存的參數。

* **刪除**

   刪除當前配置。 如果為標準，則參數會傳回至預設設定。 如果從工廠配置中建立，則刪除特定實例。

* **取消綁定**

   從捆綁包中取消綁定當前配置。

* **取消**

   取消任何當前更改。

## 套件組合 {#bundles}

此 **套件組合** tab是安裝AEM所需OSGi套件組合的機制。 索引標籤可透過下列任一方法存取：

* 下拉式功能表：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/bundles`

將會顯示套件組合清單：

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

使用此標籤，您可以：

* **安裝或更新**

   您可以 **瀏覽** 尋找包含套件的檔案，並指定是否應該 **開始** 立即 **開始層級**.

* **重新載入**

   重新整理顯示的清單。

* **刷新包**

   這會檢查所有套件的參考，並視需要重新整理。

   例如，更新後，由於先前的參考，舊版和新版本可能仍在執行中。 此選項會檢查並移動所有參照至新版本，讓舊版本停止。

* **啟動**

   根據指定的開始級別啟動包。

* **停止**

   停止捆綁。

* **解除安裝**

   從系統中卸載該包。

* **查看狀態**

   該清單指定了綁定的當前狀態；按一下特定套件名稱並顯示詳細資訊。

>[!NOTE]
>
>之後 **更新** 建議您執行 **刷新包**.

## 元件 {#components}

此 **元件** 索引標籤可讓您啟用和/或停用各種元件。 可透過下列任一方存取：

* 下拉式功能表：

   **主要 >**

* URL;例如：

   `http://localhost:4502/system/console/components`

將顯示元件清單。 您可使用各種圖示來啟用、停用或（如適用）開啟特定元件的設定詳細資訊。

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

按一下特定元件的名稱，將會顯示其狀態的詳細資訊。 您也可以在此啟用、停用或重新載入元件。

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>啟用或停用元件時，只有在AEM/CRX重新啟動前才會套用。
>
>啟動狀態在元件描述符內定義，該描述符在開發期間生成，並在建立包時儲存在包中。
