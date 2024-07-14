---
title: 翻譯使用者產生的內容
description: 瞭解UGC內容的翻譯如何透過移除語言障礙，讓網站訪客和成員體驗全球社群。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# 翻譯使用者產生的內容 {#translating-user-generated-content}

Adobe Experience Manager (AEM) Communities的翻譯功能將[翻譯頁面內容](../../help/sites-administering/translation.md)的概念延伸至使用[社交元件架構(SCF)元件](scf.md)張貼至社群網站的使用者產生內容(UGC)。

UGC的翻譯可讓網站訪客和成員移除語言障礙，體驗全球社群。

例如，假設：

* 一位法國成員在多國烹飪網站的社群論壇中張貼法文食譜。
* 來自日本的另一位成員使用此翻譯功能，將配方從法文翻譯成日文。
* 在閱讀日文的配方後，日本成員隨後發表日文評論。
* 來自法國的成員使用翻譯功能將日文註解翻譯成法文。
* 全球通訊。

## 概觀 {#overview}

本節具體說明翻譯服務如何與UGC搭配運作。 這也假設您瞭解如何將AEM連線至[翻譯服務提供者](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)，並透過設定[翻譯整合架構](../../help/sites-administering/tc-tic.md)將該服務整合至網站。

當翻譯服務提供者與網站相關聯時，網站的每個語言副本都會維護其透過SCF元件（例如註解）張貼的UGC對話串。

除了翻譯服務提供者之外，如果設定翻譯整合，網站的每個語言副本可能會共用單一UGC對話串，提供不同語言副本之間的全域通訊。 已設定的[全域共用存放區](#global-translation-of-ugc)可讓整個對話串可見，而不論檢視的是哪一個語言副本，而不用以語言分隔的討論對話串。 此外，可以設定多個翻譯整合設定，為全域參與者的邏輯分組（例如按區域）指定不同的全域共用存放區。

## 預設翻譯服務 {#the-default-translation-service}

AEM Communities包含[預設翻譯服務](../../help/sites-administering/tc-msconf.md)的[試用授權](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license)，已啟用多種語言。

當[建立社群網站](sites-console.md)時，從[TRANSLATION](sites-console.md#translation)子面板核取`Allow Machine Translation`時會啟用預設翻譯服務。

>[!CAUTION]
>
>預設翻譯服務僅供示範。
>
>生產系統需要授權的翻譯服務。 如果未授權，預設的翻譯服務應該是[關閉](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors)。

## UGC的全球翻譯 {#global-translation-of-ugc}

當網站有多個[語言副本](../../help/sites-administering/tc-prep.md)時，預設翻譯服務無法辨識一個網站上輸入的UGC可能與另一個網站上輸入的UGC有關。 相同元件（包含元件的頁面語言副本）產生UGC時，即會發生此情況。

這類似於討論主題的一群人。 他們不知道在自己以外的群組中發表的評論，而大型群組中的每個人則參加同一個交談。

如果需要「一個群組對話」，則可以在具有多語言副本的網站上啟用全域翻譯，以便檢視整個對話串，無論檢視的是哪一種語言副本。

例如，如果在基本網站上建立論壇、建立語言副本，並啟用全域翻譯，則以單一語言副本發佈在論壇上的主題會出現在所有語言副本中。 無論輸入回覆的語言副本為何，所有回覆均適用相同情況。 如此一來，無論檢視主題所用的語言副本為何，都會顯示主題及其整個回覆對話串。

>[!CAUTION]
>
>全域翻譯之前存在的任何UGC都不再可見。
>
>雖然UGC仍在[公用存放區](working-with-srp.md)中，但它位於特定語言的UGC位置下，而設定全域翻譯後新增的內容正在從全域共用存放區位置擷取。
>
>沒有移轉工具可將特定語言的內容移動或合併至全域共用存放區。

### 翻譯整合設定 {#translation-integration-configuration}

若要建立整合翻譯服務，將翻譯服務聯結器與作者執行個體上的網站整合：

* 以管理員身分登入
* 從[主功能表](http://localhost:4502/)
* 選取&#x200B;**[!UICONTROL 工具]**
* 選取&#x200B;**[!UICONTROL 作業]**
* 選取&#x200B;**[!UICONTROL 雲端]**
* 選取&#x200B;**[!UICONTROL Cloud Service]**
* 向下捲動至&#x200B;**[!UICONTROL 翻譯整合]**

  ![翻譯整合](assets/translation-integration.png)

* 選取&#x200B;**[!UICONTROL 顯示設定]**

  ![顯示設定](assets/translation-integration1.png)

* 選取&#x200B;**[!UICONTROL 可用組態]**&#x200B;旁的`[+]`圖示，以便您建立組態。

#### 建立設定對話方塊 {#create-configuration-dialog}

![建立組態](assets/translation-integration2.png)

* **[!UICONTROL 父設定]**

  （必要）通常會保留為預設值。 預設值為`/etc/cloudservices/translation`。

* **[!UICONTROL 標題]**

  （必要）輸入您選擇的顯示標題。 無預設值。

* **[!UICONTROL 名稱]**

  （選擇性）輸入組態的名稱。 預設值是根據標題的節點名稱。

* 選取&#x200B;**[!UICONTROL 建立]**

#### 翻譯設定對話方塊 {#translation-config-dialog}

![組態對話方塊](assets/translation-integration3.png)

如需詳細指示，請參閱[建立翻譯整合組態](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)。

* **[!UICONTROL 網站]**&#x200B;索引標籤：可以保留為預設值。

* **[!UICONTROL 社群]**&#x200B;標籤：
   * **[!UICONTROL 翻譯提供者]**
從下拉式清單中選取翻譯提供者。 預設值為`microsoft`，此為試用服務。

   * **[!UICONTROL 內容類別]**
選取說明正在翻譯之內容的類別。 預設為`General.`

   * **[!UICONTROL 選擇地區……]**
（選擇性）透過選取儲存UGC的語言環境，所有語言副本中的貼文都會顯示在一個全域對話中。 依照慣例，為網站選擇[基本語言](sites-console.md#translation)的地區設定。 選擇`No Common Store`會停用全域翻譯。 預設會停用全域翻譯。

* **[!UICONTROL Assets]**&#x200B;索引標籤：可保留為預設值。
* 選取&#x200B;**[!UICONTROL 確定]**

#### 啟用 {#activation}

必須將新的翻譯整合雲端服務啟動至Publish環境。 與網站建立關聯時，如果尚未啟動，則啟動工作流程會在與它關聯的頁面發佈時提示發佈此雲端服務設定。

## 管理翻譯設定 {#managing-translation-settings}

>[!NOTE]
>
>**偏好的語言**
>
>偵測貼文所使用的語言是否與慣用語言不同時，必須建立網站訪客的慣用語言。
>
>當網站訪客登入並已指定語言偏好設定時，慣用語言為使用者設定檔中設定的語言偏好設定。
>
>當網站訪客為匿名或未在其設定檔中指定語言偏好設定時，偏好的語言是頁面範本的基本語言。

### 使用者偏好設定 {#user-preference}

#### 使用者設定檔 {#user-profile}

所有社群網站都會提供使用者設定檔，登入成員可以編輯此設定檔，向社群識別自己並設定其偏好設定。

其中一項設定是是否一律以偏好語言顯示社群內容。 預設不會設定此設定，而是預設為系統設定。 使用者可以將設定變更為開啟或關閉，以覆寫系統設定。

當頁面自動翻譯成使用者偏好的語言時，仍提供用於顯示原始文字和改善翻譯的UI。

![使用者設定檔](assets/translation-integration4.png)

### 社群網站設定 {#community-site-setting}

建立社群網站時，可啟用和設定翻譯選項。 此翻譯設定對匿名網站訪客可檢視的內容有效，但會被使用者的設定檔設定覆寫。
