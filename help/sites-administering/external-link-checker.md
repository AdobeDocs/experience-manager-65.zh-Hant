---
title: 連結檢查程式
description: 「連結檢查器」可協助驗證內部和外部連結，並允許連結重寫。
translation-type: tm+mt
source-git-commit: 8a551cce581056cb274b1d8567f579fc73a95d3c
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# 鏈路檢查器{#the-link-checker}

內容作者不必擔心驗證其內容頁面中包含的每個連結。

「連結檢查器」會自動協助內容作者取得其連結，包括：

* 當連結新增至內容時驗證連結
* 顯示內容中所有外部連結的清單
* 執行連結轉換

「連結檢查器」具有許多[配置選項](#configuring)，例如定義內部驗證、允許在驗證中忽略某些連結或連結路徑，以及重寫連結重寫規則。

「連結檢查器」驗證[內部連結](#internal)和[外部連結。](#external)

>[!NOTE]
>
>由於「連結檢查器」會檢查每個內容頁面的連結，因此「連結檢查器」可能會影響大型儲存庫的效能。 在這種情況下，您可能需要[配置連結檢查器運行](#configuring)或[的頻率。](#disabling)

## 內部鏈路檢查{#internal}

內部連結是AEM儲存庫中其他內容的連結。 可使用路徑選擇器RTE或使用自訂元件來新增內部連結。 例如：

* 您的頁面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文字元件中包含至`/content/wknd/us/en/adventures/extreme-ironing.html`的連結。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

當內容作者新增內部連結至頁面時，內部連結會立即進行驗證。 如果連結變成無效：

* 它會從發行者移除。 連結的文字仍會保留，但連結本身會移除。
* 在製作介面中，它會顯示為中斷的連結。

![編寫頁面時，內部連結中斷](assets/link-checker-invalid-link-internal.png)

## 外部鏈路檢查{#external}

外部連結是AEM存放庫以外內容的連結。 可使用RTE或使用自定義元件添加外部連結。 例如：

* 您的頁面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文字元件中包含至`https://bunwarmerthermalunderwear.com`的連結。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

外部連結的語法和可用性通過檢查來驗證。 此檢查在可配置的內部非同步完成。 如果「連結檢查器」發現外部連結無效：

* 它會從發行者移除。 連結的文字仍會保留，但連結本身會移除。
* 在製作介面中，它會顯示為中斷的連結。

![編寫頁面時，內部連結中斷](assets/link-checker-invalid-link-external.png)

此外，[外部連結檢查器](#external-link-checker)介面提供內容頁面上所有外部連結的概述。

### 使用外部鏈路檢查器{#external-link-checker}

要使用外部連結檢查器：

1. 使用&#x200B;**Navigation**，選擇&#x200B;**Tools**，然後選擇&#x200B;**Sites**。
1. 選擇「**外部連結檢查器**」，並顯示所有外部連結的清單。

![「外部連結檢查器」窗口](assets/external-link-checker.png)

將顯示以下資訊：

* **狀態** -連結的驗證狀態，可以是下列其中一項：
   * **有效** - 「連結檢查器」可以訪問外部連結
   * **待定** -已將外部連結新增至網站內容，但尚未由連結檢查器驗證
   * **無效** - 「連結檢查器」無法訪問外部連結
* **URL**  —— 外部連結
* **反向連結** -包含外部連結的內容頁面
   * 如果已配置，則僅填入[。](#configuring)
* **上次檢查** -連結檢查器上次驗證外部連結的時間
   * [檢查連結的頻率是可設定的。](#configuring)
* **上次狀態** -當「已勾選的連結上次勾選外部連結時，返回的最後一個HTML狀態代碼
* **上次可用** -自上次連結可供連結檢查器使用以來的時間
* **上次存取** -自具有外部連結的頁面上次在編寫介面中存取以來的時間

您可以使用連結清單頂端的兩個按鈕來控制視窗內容：

* **刷新** -刷新清單內容
* **Check** - To check an individual external link selected in the list

### 外部鏈路檢查器的工作方式{#how-it-works}

雖然易於使用，但「外部連結檢查器」依賴於許多服務並瞭解它們的工作方式，幫助您瞭解如何配置「連結檢查器」以滿足您的需求。[](#configuring)

1. 每當內容作者儲存頁面的任何連結時，就會觸發事件處理常式。
1. 事件處理常式會遍歷`/content`下的所有內容，並檢查是否有新的或更新的連結，並將它們新增至連結檢查器的快取。
1. 然後，**Day CQ Link Checker Service**&#x200B;會定期執行，以檢查快取中的項目是否有效語法。
1. 經過語法驗證的連結隨後會出現在[External Link Checker](#external-link-checker)窗口中。 但是，它們將處於&#x200B;**待定**&#x200B;狀態。
1. 然後，**天CQ連結檢查器任務**&#x200B;定期執行，以通過進行GET調用來驗證連結。
1. 然後，**天CQ連結檢查器任務**&#x200B;將使用GET調用的結果更新「外部連結檢查器」窗口中的條目。

## 配置鏈路檢查器{#configuring}

在AEM中，「連結檢查器」會自動立即可用。 但是，有許多OSGi配置可以修改以更改其行為：

* **Day CQ Link Checker Info Storage Service**  —— 此服務定義儲存庫中的Link Checker快取的大小。
* **Day CQ Link Checker Service**  —— 此服務會執行外部連結語法的非同步檢查。您可以定義檢查期間，以及檢查器在其他選項中跳過哪些類型的連結。
* **第CQ天連結檢查器任務** -此服務執行外部連結的GET驗證。它允許區間的不同定義，以檢查其他選項中的壞連結和好連結。
* **Day CQ Link Checker Transformer**  —— 允許根據用戶定義的規則集轉換連結。

有關如何更改OSGi設定的詳細資訊，請參閱文檔[OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md)。

## 禁用鏈路檢查器{#disabling}

您可以選擇完全停用「連結檢查器」。 若要這麼做：

1. 開啟OSGi主控台。
1. 編輯&#x200B;**Day CQ Link Checker Transformer**
1. 勾選您要停用的選項：
   * **停用檢查** -停用連結的驗證
   * **禁用重寫** -禁用連結轉換

>[!NOTE]
>
>如果您在開始建立內容後停用連結檢查，在[「外部連結檢查器」視窗](#external-link-checker)中仍可能看到項目，但這些項目將不會再更新。
