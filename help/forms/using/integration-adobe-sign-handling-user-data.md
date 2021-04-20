---
title: 與Adobe Sign整合 |處理使用者資料
seo-title: 與Adobe Sign整合 |處理使用者資料
description: 與Adobe Sign整合 |處理使用者資料
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 與Adobe Sign整合 |處理用戶資料{#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 與整[!DNL  Adobe Sign] 合，讓電子簽名工作流程能夠在調適性表單中處理法律、銷售、薪資、人力資源管理工作流程的表單或合約。它允許單一和多使用者簽署、循序和同步簽署工作流程、以匿名或登入使用者身分簽署表單，以及多種方式來驗證使用者。

當簽署者或多位簽署者簽署並送出最適化表格時，會產生[!DNL Adobe Sign]合約，其中包含簽署者的相關資訊。

有關[!DNL AEM Forms]與[!DNL Adobe Sign]整合的詳細資訊，請參閱[以最適化形式使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 用戶資料和資料儲存{#data}

[!DNL Adobe Sign] 啟用的自適應表單包括關於簽署者的資訊，並且可以包括由自適應表單收集的其他用戶資料。[!DNL Adobe Sign]服務會將使用者資料與合約中的簽名一起儲存。 合約儲存在[!DNL AEM Forms]雲端服務中設定的[!DNL Adobe Sign]伺服器上。 此外，如果最適化表單設定為使用Forms入口網站提交動作，則合約資料會與表單資料一起儲存在表單入口網站資料儲存中。

## 存取和刪除使用者資料{#access-and-delete-user-data}

用戶資料在協定中收集，但不保存在任何服務表中。 [!DNL Adobe Sign] 可讓管理員在管理服務中控制的資料時做出自己的選擇。[!DNL Adobe Sign]服務的隱私權管理員可以根據要求者的電子郵件地址列出或移除合約。

[!DNL Adobe Sign] 提供Web應用程式，可讓參與者搜尋合約，並視需要刪除合約。如需詳細資訊，請參閱[Adobe Sign-功能：刪除用戶資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

配置為使用Forms門戶提交操作的最適化表單的協定資料也保存在表單門戶資料儲存中。 若要從表單入口資料存放區存取和刪除資料，請參閱[Forms入口 |處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md)。
