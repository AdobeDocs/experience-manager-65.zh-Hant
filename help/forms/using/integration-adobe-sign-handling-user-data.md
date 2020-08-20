---
title: 與Adobe Sign整合 |處理使用者資料
seo-title: 與Adobe Sign整合 |處理使用者資料
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 與Adobe Sign整合 |處理使用者資料 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 與整合[!DNL  Adobe Sign] ，讓電子簽名工作流程能夠在調適性表單中處理法律、銷售、薪資、人力資源管理工作流程的表單或合約。 它允許單一和多使用者簽署、循序和同步簽署工作流程、以匿名或登入使用者身分簽署表單，以及多種方式來驗證使用者。

當簽署者或多位簽署者簽署並送出最適化表格時，就會產生 [!DNL Adobe Sign] 包含簽署者相關資訊的合約。

如需與整合的 [!DNL AEM Forms] 詳細資 [!DNL Adobe Sign]訊，請 [參閱在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 使用者資料與資料儲存 {#data}

[!DNL Adobe Sign] 啟用的自適應表單包括關於簽署者的資訊，並且可以包括由自適應表單收集的其他用戶資料。 服務 [!DNL Adobe Sign] 會以合約中的簽名儲存使用者資料。 合約儲存在雲端服務 [!DNL Adobe Sign] 中設定的 [!DNL AEM Forms] 伺服器上。 此外，如果最適化表單設定為使用表單入口網站提交動作，則合約資料會與表單資料一起儲存在表單入口網站資料儲存中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

用戶資料在協定中收集，但不保存在任何服務表中。 [!DNL Adobe Sign] 可讓管理員在管理服務中控制的資料時做出自己的選擇。 服務的隱私權管 [!DNL Adobe Sign] 理員可以根據要求者的電子郵件地址，列出或移除合約。

[!DNL Adobe Sign] 提供Web應用程式，可讓參與者搜尋合約，並視需要刪除合約。 如需詳細資訊，請參 [閱Adobe Sign —— 功能：刪除使用者資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

為使用表單入口網站提交動作而設定的最適化表單的合約資料也會儲存在表單入口網站資料儲存中。 若要從表單入口網站資料存放區存取和刪除資料，請參閱 [Forms入口網站 |處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md)。
