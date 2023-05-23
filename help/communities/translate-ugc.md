---
title: 翻譯用戶生成的內容
seo-title: Translating User Generated Content
description: 翻譯功能的工作原理
seo-description: How the translation feature works
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# 翻譯用戶生成的內容 {#translating-user-generated-content}

AEM Communities的翻譯特徵擴展了 [翻譯頁面內容](../../help/sites-administering/translation.md) 發佈到社區網站的用戶生成內容(UGC) [社會元件框架(SCF)元件](scf.md)。

UGC的翻譯使網站訪問者和成員能夠通過消除語言障礙來體驗全球社區。

例如，假設：

* 一位來自法國的成員用法語向一個跨國烹飪網站的社區論壇發佈了一份配方。
* 另一位來自日本的成員使用翻譯功能來觸發配方從法語翻譯成日語。
* 日文讀完食譜後，這位來自日本的會員便用日文發表了評論。
* 來自法國的成員使用翻譯功能將日語注釋翻譯成法語。
* 全球通信。

## 概觀 {#overview}

本文檔的這一節專門討論翻譯服務如何與UGC協作，同時假定瞭解如何連AEM接到 [翻譯服務提供商](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 通過配置 [翻譯整合框架](../../help/sites-administering/tc-tic.md)。

當翻譯服務提供商與站點相關聯時，站點的每個語言副本維護其自己通過SCF元件（如注釋）發佈的UGC線程。

當除了翻譯服務提供者之外配置翻譯整合框架時，站點的每個語言副本可以共用UGC的單個線程，從而提供跨語言副本的全局通信。 已配置的討論線程不是按語言分隔的 [全局共用儲存](#global-translation-of-ugc) 使整個線程可見，而不管查看該線程的語言副本來自何種語言。 此外，可以配置多個翻譯整合配置來指定用於全局參與者的邏輯分組的不同全局共用儲存，例如按區域。

## 預設翻譯服務 {#the-default-translation-service}

AEM Communities [試用許可](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) 為 [預設翻譯服務](../../help/sites-administering/tc-msconf.md) 已啟用多種語言。

當 [建立社區網站](sites-console.md)，預設翻譯服務在 `Allow Machine Translation` 從 [翻譯](sites-console.md#translation) 的子菜單。

>[!CAUTION]
>
>預設翻譯服務僅用於演示。
>
>對於生產系統，需要許可的翻譯服務。 如果未獲得許可，預設翻譯服務應 [關閉](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors)。

## UGC的全球翻譯 {#global-translation-of-ugc}

當網站具有多個 [語言副本](../../help/sites-administering/tc-prep.md)，預設翻譯服務不識別在一個站點上輸入的UGC可能與在另一個站點上輸入的UGC相關，因為UGC實際上是由同一元件（包含該元件的頁面的語言副本）生成的。

這與討論某個主題的群體相似，他們不知道在他們自己之外的群體中發表評論，而與參與一個對話的大群體中的每個人相比。

如果需要「一個組對話」，則可以跨具有多個語言副本的網站啟用全局翻譯，這樣，無論查看該線程的語言副本來自何種語言副本，整個線程都可見。

例如，如果在基站點上建立論壇，建立語言副本，並啟用了全局翻譯，則發佈到論壇的一個以一種語言副本製作的主題將出現在所有語言副本中。 對於任何答復，也是如此，不論答復的輸入語言是哪種。 結果是，無論查看主題的語言副本來自何種語言，主題及其全部答復線程都可見。

>[!CAUTION]
>
>在全局轉換之前存在的任何UGC都不再可見。
>
>當UGC還在 [普通商店](working-with-srp.md)，它位於特定於語言的UGC位置下，而配置全局轉換後添加的新內容正在從全局共用儲存位置檢索。
>
>沒有用於將特定於語言的內容移動或合併到全局共用儲存的遷移工具。

### 翻譯整合配置 {#translation-integration-configuration}

要建立新的翻譯整合，將翻譯服務連接器與作者實例上的網站整合：

* 以管理員身份登錄
* 從 [主菜單](http://localhost:4502/)
* 選擇 **[!UICONTROL 工具]**
* 選擇 **[!UICONTROL 操作]**
* 選擇 **[!UICONTROL 雲]**
* 選擇 **[!UICONTROL Cloud Services]**
* 向下滾動到 **[!UICONTROL 翻譯整合]**

   ![翻譯整合](assets/translation-integration.png)

* 選擇 **[!UICONTROL 顯示配置]**

   ![顯示配置](assets/translation-integration1.png)

* 選擇 `[+]` 表徵圖 **[!UICONTROL 可用配置]** 建立新配置

#### 「建立配置」對話框 {#create-configuration-dialog}

![建立配置](assets/translation-integration2.png)

* **[!UICONTROL 父設定]**

   （必需）通常保留為預設值。 預設值為 `/etc/cloudservices/translation`。

* **[!UICONTROL 標題]**

   （必需）輸入您選擇的顯示標題。 無預設值。

* **[!UICONTROL 名稱]**

   （可選）輸入配置的名稱。 預設值是基於標題的節點名稱。

* 選擇 **[!UICONTROL 建立]**

#### 翻譯配置對話框 {#translation-config-dialog}

![配置對話框](assets/translation-integration3.png)

有關詳細說明，請訪問 [建立翻譯整合配置](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL 站點]** 頁籤：可以保留為預設值。

* **[!UICONTROL 社區]** 頁籤：
   * **[!UICONTROL 翻譯提供程式]**
從下拉清單中選擇翻譯提供程式。 預設值為 
`microsoft`試用服務。

   * **[!UICONTROL 內容類別]**
選擇描述要翻譯的內容的類別。 預設值為 
`General.`

   * **[!UICONTROL 選擇區域設定……]**
（可選）通過選擇儲存UGC的區域設定，所有語言副本中的帖子將出現在一個全局對話中。 按慣例，選擇 [基語](sites-console.md#translation) 的雙曲餘切值。 選擇 `No Common Store` 將禁用全局翻譯。 預設情況下，全局轉換處於禁用狀態。

* **[!UICONTROL 資產]** 頁籤：可以保留為預設值。
* 選擇 **[!UICONTROL 確定]**

#### 啟用 {#activation}

新的翻譯整合雲服務需要激活到發佈環境。 與網站關聯時，如果尚未激活，則激活工作流將在發佈與其關聯的頁面時提示發佈此雲服務配置。

## 管理翻譯設定 {#managing-translation-settings}

>[!NOTE]
>
>**首選語言**
>
>為了檢測帖子是否使用與首選語言不同的語言，必須建立站點訪問者的首選語言。
>
>首選語言是當站點訪問者登錄並指定了語言首選項時，在用戶配置檔案中設定的語言首選項。
>
>當站點訪問者是匿名訪問者或在其配置檔案中未指定語言首選項時，首選語言是頁面模板的基本語言。

### 用戶首選項 {#user-preference}

#### 使用者設定檔 {#user-profile}

所有社區站點都提供登錄成員的用戶配置檔案，用戶配置檔案可以編輯以標識自己到社區並設定其首選項。

其中一種設定是是否始終以其首選語言顯示社區內容。 預設情況下，設定未設定，將預設為系統設定。 用戶可以將設定更改為「開啟」或「關閉」，從而覆蓋系統設定。

當頁面被自動翻譯成用戶的首選語言時，用於顯示原始文本和改進翻譯的UI仍然可用。

![用戶配置檔案](assets/translation-integration4.png)

### 社區網站設定 {#community-site-setting}

建立社區站點時，可以啟用和配置翻譯選項。 翻譯設定對匿名站點訪問者可以查看的內容有效，但被用戶的配置檔案設定覆蓋。
