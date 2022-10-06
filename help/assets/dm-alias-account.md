---
title: 設定Dynamic Media公司別名帳戶
description: 了解如何在Dynamic Media中設定公司別名帳戶。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# 關於設定Dynamic Media公司別名帳戶 {#about-dm-alias-acct}

Dynamic Media URL和檢視器內嵌程式碼包含您的公司帳戶名稱。 此帳戶名稱是在布建Dynamic Media時建立。 在某些情況下，您的企業可能已經經歷了收購或品牌重塑，或者您只想使用一個更令人難忘的名稱。 在這類情況下，若要手動更新所有URL和檢視器內嵌程式碼（隨即推出）中的公司帳戶名稱並不容易。 此外，您也可能會影響現有的Dynamic Media存放庫或影響即時內容。 若要解決此問題，您可以設定Dynamic Media公司別名帳戶。

Dynamic Media公司別名帳戶可確保使用者介面中的所有現成Dynamic Media URL和檢視器內嵌程式碼，都能反映對您業務內容所做的任何更新，例如品牌重塑。 別名帳戶對您的SEO（搜尋引擎最佳化）也有正面影響，因為Dynamic Media URL和檢視器內嵌程式碼會反映新的公司帳戶名稱。

設定Dynamic Media公司別名帳戶時，請注意下列事項：

* 您的任何現有Dynamic Media URL或檢視器內嵌程式碼 *live* 必須手動更新數字屬性，以反映新的別名。 不過，任何URL或檢視器內嵌程式碼搭配您原始的Dynamic Media公司名稱，仍可繼續用於現有或新資產。
* Dynamic Media公司別名帳戶功能僅限於Experience Manager Assets編寫模式和傳送。 公司別名不適用於Experience Manager Sites。 未針對此變更更新WCM（Web內容管理）元件。 這些元件會繼續與原始Dynamic Media公司名稱搭配使用，以擷取Dynamic Media資產。
* 您只能在 **[!UICONTROL 編輯Dynamic Media設定]** 頁面。 不過，您可以透過支援案例建立任意數量的公司別名帳戶，並在Dynamic Media URL或檢視器內嵌程式碼中手動反映必要的別名。
* 現成可用 [快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media的功能會讓Cloud Services中「Dynamic Media設定」頁面中已設定之公司帳戶和公司別名帳戶的URL失效。
* 當您在 **[!UICONTROL 編輯Dynamic Media設定]** 頁面，若要快取失效成功，您必須使 *both* the **[!UICONTROL 公司]** 帳戶和 **[!UICONTROL 公司別名]** 帳戶，同時。

另請參閱 [在Cloud Services中建立Dynamic Media設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 設定Dynamic Media公司別名帳戶 {#configure-dm-alias-account}

您必須先提交支援案例，以開始設定Dynamic Media公司別名帳戶。 此步驟為必要。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html).
1. 在您的支援案例中提供下列資訊：

   * 您要使用的Dynamic Media公司別名。 名稱必須包含 *僅限* 字母（允許混合大小寫）、數字、連字型大小和下划線。
   * 你的地區。
   * 是否有 [規則集](/help/assets/using-rulesets-to-transform-urls.md) 以前是用來透過替代的Dynamic Media公司帳戶名稱來提供Dynamic Media內容。

1. 在「支援」建立Dynamic Media別名帳戶後，在「Experience Manageras a Cloud Service作者」例項中，選取Experience Manageras a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取「工具」圖示，然後前往 **[!UICONTROL Cloud Services> Dynamic Media設定]**.
1. 在Dynamic Media設定瀏覽器頁面的左窗格中，選取 **[!UICONTROL 全球]** (不要選取 **[!UICONTROL 全球]**)。 然後選取 **[!UICONTROL 編輯]**.

   ![Dynamic Media公司別名文字欄位](/help/assets/assets-dm/dm-company-alias.png)

1. 在 **[!UICONTROL 編輯Dynamic Media設定]** 頁面，在 **[!UICONTROL 公司別名]** 文字欄位，輸入您先前在支援案例中指定的Dynamic Media別名帳戶名稱。
1. 在頁面的右上方，選取 **[!UICONTROL 儲存]**.
Dynamic Media公司別名帳戶現已儲存並啟用；現在，現有和新資產的所有URL和檢視器內嵌程式碼都會反映新公司別名。
