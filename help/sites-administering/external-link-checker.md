---
title: 連結檢查程式
description: 連結檢查器可協助驗證內部和外部連結，並允許連結重寫。
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# 連結檢查程式 {#the-link-checker}

內容作者不必擔心要驗證自己包含在內容頁面中的每個連結。

連結檢查器會自動執行，以協助內容作者使用其連結，包括：

* 在新增至內容時驗證連結
* 顯示內容中所有外部連結的清單
* 執行連結轉換

連結檢查器有數個[組態選項](#configuring)，例如定義驗證內部、允許驗證中省略某些連結或連結模式，以及重寫連結重寫規則。

連結檢查器會驗證[內部連結](#internal)和[外部連結。](#external)

>[!NOTE]
>
>由於「連結檢查器」會檢查每個內容頁面的連結，因此「連結檢查器」可能會影響大型存放庫的效能。 在這種情況下，您可能需要[設定連結檢查器執行的頻率](#configuring)或[停用它。](#disabling)

## 內部連結檢查 {#internal}

內部連結是指向AEM存放庫中其他內容的連結。 可以使用RTE中的路徑選擇器或使用自訂元件來新增內部連結。 例如：

* 您的頁面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文字元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=zh-Hant)中包含`/content/wknd/us/en/adventures/extreme-ironing.html`的連結。

內容作者新增內部連結至頁面時，就會驗證內部連結。 如果連結失效：

* 它會從發佈者中移除。 連結的文字會保留，但連結本身會移除。
* 它會在編寫介面中顯示為中斷連結。

編寫頁面時![內部連結中斷](assets/link-checker-invalid-link-internal.png)

## 外部連結檢查 {#external}

外部連結是指AEM存放庫外部內容的連結。 外部連結可使用RTE或使用自訂元件來新增。 例如：

* 您的頁面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文字元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=zh-Hant)中包含`https://bunwarmerthermalunderwear.com`的連結。

系統會驗證外部連結的語法，並檢查其可用性。 此檢查會在可設定的內部非同步地完成。 如果連結檢查器發現外部連結無效：

* 它會從發佈者中移除。 連結的文字會保留，但連結本身會移除。
* 它會在編寫介面中顯示為中斷連結。

編寫頁面時![內部連結中斷](assets/link-checker-invalid-link-external.png)

此外，[外部連結檢查器](#external-link-checker)介面會提供內容頁面上所有外部連結的概觀。

### 使用外部連結檢查程式 {#external-link-checker}

使用外部連結檢查程式：

1. 使用&#x200B;**導覽**，選取&#x200B;**工具**，然後選取&#x200B;**網站**。
1. 選取「**外部連結檢查器**」並顯示所有外部連結的清單。

![外部連結檢查器視窗](assets/external-link-checker.png)

會顯示下列資訊：

* **狀態** — 連結的驗證狀態，可能是下列其中一項：
   * **有效** — 連結檢查器可存取外部連結
   * **擱置中** — 外部連結已新增至網站內容，但尚未由連結檢查器驗證
   * **無效** — 連結檢查器無法存取外部連結
* **URL** — 外部連結
* **反向連結** — 包含外部連結的內容頁面
   * 若已設定，則僅填入[。](#configuring)
* **上次檢查時間** — 連結檢查器上次驗證外部連結的時間
   * 可設定檢查連結的頻率[。](#configuring)
* **上次狀態** — 連結檢查上次檢查外部連結時傳回的最後HTML狀態碼
* **上次可用** — 連結檢查器上次使用連結後的時間
* **上次存取** — 自上次在編寫介面中存取含有外部連結的頁面以來的時間

您可以使用連結清單頂端的兩個按鈕來操控視窗的內容：

* **重新整理** — 重新整理清單的內容
* **檢查** — 檢查清單中選取的個別外部連結

### 外部連結檢查器的運作方式 {#how-it-works}

外部連結檢查程式雖然使用簡單，但依賴數項服務，並瞭解其運作方式，可協助您瞭解如何[設定連結檢查程式](#configuring)以符合您的需求。

1. 每當內容作者儲存任何頁面的連結時，就會觸發事件處理常式。
1. 事件處理常式會遍歷`/content`下的所有內容，檢查新的或更新連結，並將它們新增至連結檢查器的快取。
1. **Day CQ Link Checker Service**&#x200B;會定期執行，以檢查快取中的專案是否為有效語法。
1. 然後，語法驗證的連結會出現在[外部連結檢查器](#external-link-checker)視窗中。 但是它們會處於&#x200B;**擱置中**&#x200B;狀態。
1. 然後會定期執行&#x200B;**Day CQ連結檢查器工作**，以進行GET呼叫來驗證連結。
1. **天CQ連結檢查器工作**&#x200B;接著會以GET呼叫的結果更新外部連結檢查器視窗中的專案。

## 設定連結檢查器 {#configuring}

「連結檢查器」可在AEM中自動使用且立即可用。 不過，有數個OSGi設定可以修改以變更其行為：

* **天CQ連結檢查器資訊儲存服務** — 此服務會定義存放庫中連結檢查器快取的大小。
* **Day CQ Link Checker Service** — 此服務會執行外部連結語法的非同步檢查。 您可以定義檢查期間，以及檢查器會略過哪些型別的連結，還有其他選項。
* **天CQ連結檢查器工作** — 此服務會執行外部連結的GET驗證。 它允許間隔的單獨定義，以檢查其他選項中的壞連結和好連結。
* **天CQ連結檢查器轉換器** — 允許根據使用者定義的規則集轉換連結。

如需有關如何變更OSGi設定的詳細資訊，請參閱檔案[OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md)。

## 停用連結檢查器 {#disabling}

您可以選擇完全停用連結檢查器。 若要這麼做：

1. 開啟OSGi主控台。
1. 編輯&#x200B;**天CQ連結檢查器轉換器**
1. 勾選您要停用的選項：
   * **停用檢查** — 停用連結驗證
   * **停用重新寫入** — 停用連結轉換

>[!NOTE]
>
>如果您在開始建立內容後停用連結檢查，您仍可在[外部連結檢查器視窗](#external-link-checker)中看到專案，但專案將不再更新。
