---
title: 與Adobe Sign |處理用戶資料
seo-title: Integration with Adobe Sign | Handling user data
description: 與Adobe Sign |處理用戶資料
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 與Adobe Sign |處理用戶資料 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 整合[!DNL  Adobe Sign] 使電子簽名工作流能夠以自適應形式處理法律、銷售、工資單、人力資源管理工作流的表單或協定。 它允許單個和多用戶簽名、順序和同時簽名工作流、以匿名用戶或登錄用戶身份對表單進行簽名，以及通過多種方法驗證用戶。

當簽名者或多個簽名者簽名並提交自適應表單時， [!DNL Adobe Sign] 生成包括關於簽名者的資訊的協定。

有關 [!DNL AEM Forms] 整合 [!DNL Adobe Sign]，請參閱 [以自適應形式使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 用戶資料和資料儲存 {#data}

[!DNL Adobe Sign] 啟用的自適應表單包括關於簽名者的資訊，並且可以包括由自適應表單收集的其他用戶資料。 的 [!DNL Adobe Sign] 服務將用戶資料與協定中的簽名一起保存。 協定保存於 [!DNL Adobe Sign] 配置的伺服器 [!DNL AEM Forms] 雲服務。 此外，如果將自適應表單配置為使用Forms門戶提交操作，則協定資料將與表單資料一起保存在表單門戶資料儲存中。

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

用戶資料在協定內收集，但未保存在任何服務表中。 [!DNL Adobe Sign] 使管理員能夠在管理服務中控制的資料時做出自己的選擇。 上的隱私管理員 [!DNL Adobe Sign] 服務可以根據請求者的電子郵件地址列出或刪除協定。

[!DNL Adobe Sign] 提供了一個Web應用程式，允許參與者搜索協定，並在需要時刪除協定。 有關詳細資訊，請參見 [Adobe Sign — 功能：刪除用戶資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

配置為使用Forms門戶提交操作的自適應表單的協定資料也保存在表單門戶資料儲存中。 要訪問和刪除表單門戶資料儲存中的資料，請參見 [Forms門戶 |處理用戶資料](/help/forms/using/forms-portal-handling-user-data.md)。
