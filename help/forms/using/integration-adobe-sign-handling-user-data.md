---
title: 與Adobe Sign整合 | 處理使用者資料
description: 瞭解AEM Forms與Adobe Sign的整合，以在適用性表單中提供電子簽章。 它支援各種工作流程的多個簽署選項。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 與Adobe Sign整合 | 處理使用者資料 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms]與[!DNL &#x200B; Adobe Sign]整合，以啟用最適化表單中的電子簽章工作流程，以處理法律、銷售、薪資、人力資源管理工作流程的表單或協定。 它允許單一和多使用者簽署、連續和同時簽署工作流程、以匿名或登入使用者身分簽署表單，以及多種驗證使用者的方式。

當簽署者或多位簽署者簽署並提交最適化表單時，會產生包含簽署者相關資訊的[!DNL Adobe Sign]合約。

如需有關[!DNL AEM Forms]與[!DNL Adobe Sign]整合的詳細資訊，請參閱[在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 使用者資料和資料存放區 {#data}

[!DNL Adobe Sign]啟用的最適化表單包含簽名者的相關資訊，並可能包含最適化表單收集的其他使用者資料。 [!DNL Adobe Sign]服務儲存使用者資料，並在合約內加上簽章。 合約已儲存在[!DNL AEM Forms]雲端服務中設定的[!DNL Adobe Sign]伺服器上。 此外，如果最適化表單設定為使用Forms Portal提交動作，則合約資料會與表單資料一起儲存在Forms Portal資料存放區。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

使用者資料會在合約中收集，但不會儲存在任何服務表格中。 [!DNL Adobe Sign]可讓系統管理員自行選擇管理他們在服務中控制的資料。 [!DNL Adobe Sign]服務的隱私權管理員可以根據要求者的電子郵件地址列出或移除協定。

[!DNL Adobe Sign]提供允許由參與者搜尋協定，並在必要時刪除協定的Web應用程式。 如需詳細資訊，請參閱[Adobe Sign — 功能：刪除使用者資訊](https://helpx.adobe.com/tw/sign/help/adobesign_gdpr_user_deletion.html)。

針對設定為使用Forms Portal提交動作的最適化表單而設定的協定資料也會儲存在Forms Portal資料存放區。 若要從Forms入口網站資料存放區存取和刪除資料，請參閱[Forms入口網站 | 正在處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md)。
