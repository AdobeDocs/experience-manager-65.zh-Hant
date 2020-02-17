---
title: 與Adobe Sign整合|處理使用者資料
seo-title: 與Adobe Sign整合|處理使用者資料
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 與Adobe Sign整合|處理使用者資料 {#integration-with-adobe-sign-handling-user-data}

AEM Forms與Adobe Sign整合，讓電子簽名工作流程能夠在調適性表單中處理表單或合約，以處理法律、銷售、薪資、人力資源管理工作流程。 它允許單一和多使用者簽署、循序和同步簽署工作流程、以匿名或登入使用者身分簽署表單，以及多種方式來驗證使用者。

當簽署者或多位簽署者簽署並送出最適化表格時，就會產生包含簽署者相關資訊的Adobe Sign合約。

如需AEM Forms與Adobe sign整合的詳細資訊，請參閱「在 [最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)」。

## 使用者資料與資料儲存 {#data}

啟用Adobe Sign的最適化表單包含簽署者的相關資訊，並可能包含最適化表單所收集的其他使用者資料。 Adobe Sign服務會將使用者資料與合約中的簽名一起儲存。 合約會儲存在AEM Forms雲端服務中設定的Adobe Sign伺服器上。 此外，如果最適化表單設定為使用表單入口網站提交動作，則合約資料會與表單資料一起儲存在表單入口網站資料儲存中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

用戶資料在協定中收集，但不保存在任何服務表中。 Adobe Sign可讓管理員自行選擇如何管理服務中控制的資料。 Adobe Sign服務的隱私權管理員可以根據要求者的電子郵件地址來列出或移除合約。

Adobe Sign提供網頁應用程式，可讓參與者搜尋合約，並視需要刪除合約。 如需詳細資訊，請參 [閱Adobe Sign —— 功能：刪除使用者資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

為使用表單入口網站提交動作而設定的最適化表單的合約資料也會儲存在表單入口網站資料儲存中。 若要從表單入口網站資料存放區存取和刪除資料，請參閱 [Forms入口網站|處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md)。
