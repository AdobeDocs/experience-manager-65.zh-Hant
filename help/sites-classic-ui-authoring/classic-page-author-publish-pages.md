---
title: 發佈頁面
seo-title: Publishing Pages
description: 一旦您在製作環境中建立並檢閱內容後，其目標就是將其發佈在您的公開網站上。
seo-description: Once you have created and reviewed your content on the author environment, the goal is to make it available on your public website.
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# 發佈頁面{#publishing-pages}

在製作環境中建立並檢閱內容後，目標就是讓它可在您的公開網站（您的發佈環境）上使用。

這稱為發佈頁面。 如果您想從發佈環境中移除頁面，即為取消發佈。 發佈和取消發佈頁面時，製作環境仍可供進一步變更，直到您刪除為止。

您也可以立即發佈/取消發佈頁面，或在日後預先定義的日期/時間發佈。

>[!NOTE]
>
>與發佈相關的某些術語可能會混淆：
>
>* **發佈/取消發佈**
   >  這些是可讓您的內容在您的發佈環境（或不可）上公開的動作的主要辭彙。
>
>* **啟用/停用**
   >  這些詞語等同於發佈/取消發佈。
>
>* **複製/複製**
   >  這些技術術語說明資料（例如頁面內容、檔案、程式碼、使用者註解）在某個環境間移動的情形，例如發佈或反向複製使用者註解時。
>


>[!NOTE]
>
>如果您沒有發佈特定頁面所需的權限：
>
>* 系統會觸發工作流程，通知您發佈請求的適當人員。
>* 系統會顯示訊息（在短時間內），通知您此情況。
>


## 發佈頁面 {#publishing-a-page}

啟用頁面的方法有兩種：

* [從網站主控台](#activating-a-page-from-the-websites-console)
* [來自頁面本身的sidekick](#activating-a-page-from-sidekick)

>[!NOTE]
>
>您也可以使用 [激活樹](#howtoactivateacompletesectiontreeofyourwebsite) 在工具控制台上。

### 從網站主控台啟用頁面 {#activating-a-page-from-the-websites-console}

您可以在網站主控台中啟用頁面。 開啟頁面並修改其內容後，您會返回「網站」主控台：

1. 在網站主控台中，選取您要啟用的頁面。
1. 選擇 **啟動**，可從頂端功能表或所選頁面項目的下拉式功能表執行。

   若要啟用頁面及其所有子頁面的內容，請使用 [**工具** 主控台](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >如有必要，AEM會要求您啟用或重新啟用連結至頁面的任何資產。 您可以選取或清除核取方塊以啟用這些資產。

1. 如有必要，AEM會要求您啟用或重新啟用連結至頁面的任何資產。 您可以選取或清除核取方塊以啟用這些資產。

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM會啟動選取的內容。 發佈的頁面或頁面會顯示在 [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) （標示為綠色），提供關於啟動內容的使用者以及啟動日期和時間的資訊。

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### 從Sidekick啟用頁面 {#activating-a-page-from-sidekick}

您也可以在開啟頁面進行編輯時啟動該頁面。

開啟頁面並修改其內容後，您可以：

1. 選取 **頁面** 標籤。
1. 按一下 **啟動頁面**.
視窗右上方會顯示訊息，確認頁面已啟用。

## 取消發佈頁面 {#unpublishing-a-page}

若要從發佈環境中移除頁面，請停用內容。

停用頁面：

1. 在網站主控台中，選取您要停用的頁面。
1. 選擇 **停用**，可從頂端功能表或所選頁面項目的下拉式功能表執行。 系統會要求您確認刪除。

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. 重新整理 [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) 內容會以紅色標示，表示不再發佈。

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## 稍後啟用/停用 {#activate-deactivate-later}

### 稍後啟動 {#activate-later}

若要排程稍後的啟動時間：

1. 在網站主控台中，前往 **啟動** ，然後選擇 **稍後啟用**.
1. 在開啟的對話方塊中，您提供啟動的日期和時間，然後按一下 **確定**. 這會建立在指定時間啟動的頁面版本。

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

稍後啟動會啟動工作流程，以在指定時間啟動此版本的頁面。 反之，稍後停用會啟動工作流程，在特定時間停用此版本的頁面。

如果要取消此激活/停用，請轉至 [工作流程主控台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 終止相應的工作流。

### 稍後停用 {#deactivate-later}

要安排稍後停用時間：

1. 在網站主控台中，前往 **停用** ，然後選擇 **稍後停用**.

1. 在開啟的對話方塊中，提供停用的日期和時間，然後按一下 **確定**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**延遲停用** r會啟動工作流程，在特定時間停用此版本的頁面。

如果要取消此停用，請轉至 [工作流程主控台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 終止相應的工作流。

## 排程的啟動/停用（開/關時間） {#scheduled-activation-deactivation-on-off-time}

您可以使用 **準時** 和 **關閉時間** 可在 [頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### 決定頁面發佈狀態 {#determining-page-publication-status-classic-ui}

從 [網站主控台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). 顏色表示發佈狀態。

## 啟用網站的完整區段（樹狀結構） {#activating-a-complete-section-tree-of-your-website}

從 **網站** 標籤中，您可以啟用個別頁面。 當您輸入或更新相當多的內容頁面時（所有頁面都位於相同的根頁面下），在一個動作中啟動整個樹狀結構會較為容易。 您也可以執行「乾式執行」來模擬啟動，並反白顯示要啟動的頁面。

1. 開啟 **工具** 主控台，從 **歡迎** 頁面，然後按兩下 **復寫** 若要開啟主控台( `https://localhost:4502/etc/replication.html`)。

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. 在 **復寫** 主控台，按一下 **激活樹**.

   以下視窗( `https://localhost:4502/etc/replication/treeactivation.html`)。

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. 輸入 **起始路徑**. 這會指定您要啟用（發佈）之區段的根路徑。 此頁和下面的所有頁均被視為激活（或在選中「乾運行」時用於模擬）。
1. 視需要啟動選取標準：

   * **僅已修改**:僅啟用已修改的頁面。
   * **僅激活**:僅啟用已（已）啟用的頁面。 可做為重新啟用的形式。
   * **忽略已停用**:忽略已停用的任何頁面。

1. 選取要執行的動作：

   1. 選擇 **乾流** 如果您想檢查哪些頁面 *wold* 的URL。 這只是模擬，不會啟動任何頁面。

   1. 選擇 **啟動** 如果您想要啟用頁面。
