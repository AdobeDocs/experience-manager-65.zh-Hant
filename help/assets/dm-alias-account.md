---
title: Configure a Dynamic Media company alias account
description: Learn how to configure a company alias account in Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 20d6c716b4ba799a7d4ae2858459f7c38cf3da02
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

<!--
hide: true
hidefromtoc: yes
-->

# About configuring a Dynamic Media company alias account {#about-dm-alias-acct}

Dynamic Media URLs and viewer embed code contain your company account name. This account name was created at the time of provisioning Dynamic Media. There may be scenarios where your business has undergone an acquisition, or a rebranding, or you simply want to use a more memorable name. In such scenarios, it is not easy to manually update your company account name in all URLs and viewer embed code that comes out of the box. Furthermore, there is the possibility that you may impact your existing Dynamic Media repository or impact live content. To resolve this issue, you can configure a Dynamic Media company alias account.

A Dynamic Media company alias account ensures that all out-of-the-box Dynamic Media URLs and viewer embed code in the user interface reflect any updates made to your business context, such as rebranding. An alias account also has a positive impact on your SEO (Search Engine Optimization) because the Dynamic Media URLs and viewer embed code reflect the new company account name.

When you configure a Dynamic Media company alias account, be aware of the following:

* Any existing Dynamic Media URLs or viewer embed code on your *live* digital properties must be updated manually to reflect the new alias name. However, any URLs or viewers embed code with your original Dynamic Media company name continue to work for existing or new assets.
* The Dynamic Media company alias account capability is limited to Experience Manager Assets Authoring mode and delivery. The company alias name does not work with Experience Manager Sites. WCM (Web Content Management) components are not updated for this change. Those components continue to work with the original Dynamic Media company name for fetching Dynamic Media assets.
* You can set up only one company alias account on the **[!UICONTROL Edit Dynamic Media Configuration]** page. However, you can create as many company alias accounts by way of a support case, and manually reflect the necessary alias name in the Dynamic Media URLs or viewer embed code.
* The out-of-the-box [Cache Invalidation](/help/assets/invalidate-cdn-cache-dynamic-media.md) capability of Dynamic Media invalidates the URLs with both Company and Company Alias accounts configured in the Dynamic Media Configuration page in Cloud Services.
* When you configure a company alias account on the **[!UICONTROL Edit Dynamic Media Configuration]** page, for cache invalidation to be successful, you must invalidate URLs for *both* the **[!UICONTROL Company]** account and the **[!UICONTROL Company Alias]** account, simultaneously.

See also [Create a Dynamic Media Configuration in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configure a Dynamic Media company alias Account {#configure-dm-alias-account}

You begin configuring a Dynamic Media company alias account by first submitting a Support case. 此為必要步驟。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支援案例中提供下列資訊：

   * 您要使用的Dynamic Media公司別名。 名稱只能包含&#x200B;*個*&#x200B;字母（允許混合大小寫）、數字、連字型大小和底線。
   * 您的地區。
   * 先前是否使用任何[規則集](/help/assets/using-rulesets-to-transform-urls.md)來透過替代Dynamic Media公司帳戶名稱提供Dynamic Media內容。

1. 支援人員建立Dynamic Media別名帳戶後，在Experience Manager as a Cloud Service Author例項中，選取Experience Manager as a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取[工具]圖示，然後前往&#x200B;**[!UICONTROL 雲端服務> Dynamic Media設定]**。
1. 在[Dynamic Media設定瀏覽器]頁面的左側窗格中，選取&#x200B;**[!UICONTROL 全域]** （不要選取&#x200B;**[!UICONTROL 全域]**&#x200B;左側的資料夾圖示）。 然後選取&#x200B;**[!UICONTROL 編輯]**。

   ![Dynamic Media公司別名文字欄位](/help/assets/assets-dm/dm-company-alias.png)

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的&#x200B;**[!UICONTROL 公司別名]**&#x200B;文字欄位中，輸入您先前在支援案例中指定的Dynamic Media別名帳戶名稱。
1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。
Dynamic Media公司別名帳戶現在已儲存並啟用；現有及新資產的所有URL和檢視器內嵌程式碼現在都會反映新的公司別名。
