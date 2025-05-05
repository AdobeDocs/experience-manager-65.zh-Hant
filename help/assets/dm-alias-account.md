---
title: 設定Dynamic Media公司別名帳戶
description: 瞭解如何在Dynamic Media中設定公司別名帳戶。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# 關於設定Dynamic Media公司別名帳戶 {#about-dm-alias-acct}

Dynamic Media URL和檢視器內嵌程式碼包含您的公司帳戶名稱。 此帳戶名稱是在布建Dynamic Media時建立的。 在某些情況下，您的企業可能會經歷收購或重新品牌化，或者您只想使用更令人難忘的名稱。 在這種情況下，在開箱即用的所有URL和檢視器內嵌程式碼中，手動更新您的公司帳戶名稱並不容易。 此外，您也可能會影響現有的Dynamic Media存放庫或即時內容。 若要解決此問題，您可以設定Dynamic Media公司別名帳戶。

Dynamic Media公司別名帳戶可確保使用者介面中所有現成可用的Dynamic Media URL和檢視器內嵌程式碼都會反映對企業內容所做的任何更新，例如品牌重塑。 別名帳戶也會對您的SEO （搜尋引擎最佳化）產生正面影響，因為Dynamic Media URL和檢視器內嵌程式碼會反映新的公司帳戶名稱。

設定Dynamic Media公司別名帳戶時，請注意下列事項：

* 您&#x200B;*live*&#x200B;數位屬性上任何現有的Dynamic Media URL或檢視器內嵌程式碼都必須手動更新，以反映新的別名。 不過，使用您原始Dynamic Media公司名稱的任何URL或檢視器內嵌程式碼都能繼續用於現有或新資產。
* Dynamic Media公司別名帳戶功能僅限於Experience Manager Assets製作模式和傳送。 公司別名不適用於Experience Manager Sites。 WCM （Web內容管理）元件未針對此變更進行更新。 這些元件可繼續搭配原始Dynamic Media公司名稱運作，以擷取Dynamic Media資產。
* 您只能在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面上設定一個公司別名帳戶。 不過，您可以透過支援案例建立儘可能多的公司別名帳戶，並在Dynamic Media URL或檢視器內嵌程式碼中手動反映必要的別名。
* Dynamic Media的現成可用[快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)功能可讓Cloud Service中Dynamic Media設定頁面中已設定公司和公司別名帳戶的URL失效。
* 當您在&#x200B;**[!UICONTROL 編輯Dynamic Media組態]**&#x200B;頁面上設定公司別名帳戶時，為了成功讓快取失效，您必須同時使&#x200B;**&#x200B; &#x200B;**&#x200B;[!UICONTROL 公司]&#x200B;**&#x200B;帳戶和&#x200B;**&#x200B;[!UICONTROL 公司別名]**&#x200B;帳戶的URL失效。

另請參閱[在Cloud Service中建立Dynamic Media設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 設定Dynamic Media公司別名帳戶 {#configure-dm-alias-account}

請先提交支援案例，以開始設定Dynamic Media公司別名帳戶。 此為必要步驟。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支援案例中提供下列資訊：

   * 您要使用的Dynamic Media公司別名。 名稱只能包含&#x200B;*個*&#x200B;字母（允許混合大小寫）、數字、連字型大小和底線。
   * 您的地區。
   * 先前是否使用任何[規則集](/help/assets/using-rulesets-to-transform-urls.md)來透過替代Dynamic Media公司帳戶名稱提供Dynamic Media內容。

1. 支援人員建立Dynamic Media別名帳戶後，在Experience Manageras a Cloud Service作者例項中，選取Experience Manageras a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取[工具]圖示，然後移至&#x200B;**[!UICONTROL Cloud Service> Dynamic Media設定]**。
1. 在「Dynamic Media設定瀏覽器」頁面的左側窗格中，選取「**[!UICONTROL 全域]**」 （請勿選取「**[!UICONTROL 全域]**」左側的資料夾圖示）。 然後選取&#x200B;**[!UICONTROL 編輯]**。

   ![Dynamic Media公司別名文字欄位](/help/assets/assets-dm/dm-company-alias.png)

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的&#x200B;**[!UICONTROL 公司別名]**&#x200B;文字欄位中，輸入您先前在支援案例中指定的Dynamic Media別名帳戶名稱。
1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。
Dynamic Media公司別名帳戶現在已儲存並啟用；現有及新資產的所有URL和檢視器內嵌程式碼現在都會反映新的公司別名。
