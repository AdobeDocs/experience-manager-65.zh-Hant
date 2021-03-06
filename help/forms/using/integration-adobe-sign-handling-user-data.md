---
title: 與Adobe Sign整合 |處理用戶資料
seo-title: 與Adobe Sign整合 |處理用戶資料
description: 與Adobe Sign整合 |處理用戶資料
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 與Adobe Sign整合 |處理用戶資料 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 整[!DNL  Adobe Sign] 合，以在最適化表單中啟用電子簽名工作流程，以處理法律、銷售、工資單、人力資源管理工作流程的表單或協定。它允許單一和多用戶簽名、循序和同時的簽名工作流、以匿名或登錄用戶身份簽名表單，以及多種驗證用戶的方法。

當簽署者或多個簽署者簽署並提交最適化表單時，會產生[!DNL Adobe Sign]協定，其中包含與簽署者相關的資訊。

如需[!DNL AEM Forms]與[!DNL Adobe Sign]整合的詳細資訊，請參閱[在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 使用者資料和資料儲存 {#data}

[!DNL Adobe Sign] 啟用的最適化表單包括關於簽署者的資訊，並可包括由最適化表單收集的其他使用者資料。[!DNL Adobe Sign]服務保存了協定內具有簽名的用戶資料。 協定儲存在[!DNL AEM Forms]雲端服務中設定的[!DNL Adobe Sign]伺服器上。 此外，如果最適化表單設定為使用Forms Portal提交動作，則合約資料會與表單資料一起儲存在表單入口網站資料存放區中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

用戶資料在協定中收集，但不保存在任何服務表中。 [!DNL Adobe Sign] 可讓管理員自行選擇管理自己在服務中控制的資料。[!DNL Adobe Sign]服務的隱私權管理員可以根據請求者的電子郵件地址列出或刪除協定。

[!DNL Adobe Sign] 提供了一個web應用程式，允許按參與者搜索協定，如果需要，還可以刪除協定。如需詳細資訊，請參閱[Adobe Sign — 功能：刪除用戶資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

設定為使用Forms Portal提交動作的適用性表單的合約資料也會儲存在表單入口網站資料存放區中。 若要從表單入口網站資料存放區存取和刪除資料，請參閱[Forms入口網站 |處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md)。
