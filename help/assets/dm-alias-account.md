---
title: 配置Dynamic Media公司別名帳戶
description: 瞭解如何在Dynamic Media配置公司別名帳戶。
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

# 關於配置Dynamic Media公司別名帳戶 {#about-dm-alias-acct}

Dynamic MediaURL和查看器嵌入代碼包含您的公司帳戶名。 此帳戶名是在設定Dynamic Media時建立的。 在某些情況下，您的企業可能已經歷收購或品牌重塑，或者您只想使用一個更令人難忘的名稱。 在這種情況下，在所有URL和查看器嵌入的出廠代碼中手動更新公司帳戶名稱並不容易。 此外，您可能會影響您現有的Dynamic Media儲存庫或影響即時內容。 要解決此問題，可以配置Dynamic Media公司別名帳戶。

Dynamic Media公司別名帳戶可確保用戶介面中所有出廠設定的Dynamic MediaURL和查看者嵌入代碼都反映對您的業務上下文所做的任何更新，如重新標識。 別名帳戶對您的SEO（搜索引擎優化）也有積極影響，因為Dynamic MediaURL和查看器嵌入代碼反映了新公司帳戶名。

配置Dynamic Media公司別名帳戶時，請注意以下事項：

* 任何現有的Dynamic MediaURL或查看器在您的 *活* 必須手動更新數字屬性以反映新別名。 但是，任何URL或查看者都會嵌入帶有您原Dynamic Media公司名稱的代碼，這些代碼仍然適用於現有或新資產。
* Dynamic Media公司別名帳戶功能僅限於Experience Manager Assets創作模式和交付。 公司別名與Experience Manager Sites不配合。 未為此更改更新WCM（Web內容管理）元件。 這些元件繼續使用原Dynamic Media公司名稱來提取Dynamic Media資產。
* 您只能在 **[!UICONTROL 編輯Dynamic Media配置]** 的子菜單。 但是，您可以通過支援案例建立盡可能多的公司別名帳戶，並在Dynamic MediaURL或查看器嵌入代碼中手動反映必要的別名。
* 開箱即用 [快取無效](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media的功能使在Dynamic Media配置頁中Cloud Services配置的公司帳戶和公司別名帳戶的URL無效。
* 在上配置公司別名帳戶時 **[!UICONTROL 編輯Dynamic Media配置]** 頁，要使快取無效成功，必須使 *兩者* 這樣 **[!UICONTROL 公司]** 帳戶和 **[!UICONTROL 公司別名]** 同時計算。

另請參閱 [在Cloud Services中建立Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 配置Dynamic Media公司別名帳戶 {#configure-dm-alias-account}

您首先提交支援案例，開始配置Dynamic Media公司別名帳戶。 此步驟是必需的。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在支援案例中提供以下資訊：

   * 要使用的Dynamic Media公司別名。 名稱必須包含 *僅* 字母（允許使用混合大小寫）、數字、連字元和下划線。
   * 你的地區。
   * 是否 [規則集](/help/assets/using-rulesets-to-transform-urls.md) 以前用於通過Dynamic Media公司的備用帳戶名實現Dynamic Media內容的服務。

1. 在支援建立Dynamic Media別名帳戶後，在Experience Manageras a Cloud Service作者實例中，選擇Experience Manageras a Cloud Service徽標以訪問全局導航控制台。
1. 在控制台左側，選擇「工具」表徵圖，然後轉到 **[!UICONTROL Cloud Services>Dynamic Media配置]**。
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，選擇 **[!UICONTROL 全球]** (不選擇資料夾表徵圖 **[!UICONTROL 全球]**)。 然後選擇 **[!UICONTROL 編輯]**。

   ![Dynamic Media公司別名文本欄位](/help/assets/assets-dm/dm-company-alias.png)

1. 在 **[!UICONTROL 編輯Dynamic Media配置]** 的 **[!UICONTROL 公司別名]** 文本欄位，鍵入您在支援案例中指定的Dynamic Media別名帳戶名。
1. 在頁面的右上角，選擇 **[!UICONTROL 保存]**。
Dynamic Media公司別名帳戶現已保存並啟用；現有資產和新資產的所有URL和查看器嵌入代碼現在都反映了新公司別名。
