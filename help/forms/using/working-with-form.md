---
title: 使用表單
seo-title: 使用表單
description: 在AEM Forms應用程式中檢視並更新與工作或起點相關聯的表單
seo-description: 在AEM Forms應用程式中檢視並更新與工作或起點相關聯的表單
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 使用表單 {#working-with-a-form}

如果表單已啟用在表單應用程式中同步的功能，表單會下載，您可以直接使用。

表單會下載到您的應用程式中，並可離線使用。 例如，您經營的是一家銀行，而客戶填寫了您網站上的應用程式。 應用程式是可接受客戶資訊並儲存以供審核的調適性表單。 管理員會檢閱表單，並在AEM作者例項中建立驗證表單。 管理員可啟用表單與AEM Forms應用程式的同步。 如果驗證表單可在AEM Forms應用程式中使用，您的現場代理可以使用行動裝置來驗證客戶的詳細資訊。 行動裝置與伺服器同步，驗證表單會載入應用程式中。 您的現場工程師可以造訪客戶、驗證詳細資訊、將資料儲存為草稿，或提交驗證表單。 每次您的應用程式連線時，表單都會與伺服器同步。

若要在AEM Forms應用程式中同步您的表格：

1. 在作者實例中，選擇一個表單，然後按一下「查 **看屬性」**。
1. 在屬性頁面中，按一下進 **階。**
1. 在「進階」下方，啟用選項：與 **AEM Forms應用程式同步**，然後點選「 **儲存」**。

若要同步多個表單，請在作者例項中，在表單管理員中選取多個表單，然後點選「與AEM Forms應 **用程式同步」**。 發佈表單時，AEM Forms應用程式可以連線至發佈伺服器並擷取表單。

>[!NOTE]
>
>支援的表單：
>
>* 最適化表單（無延遲載入）
>* 行動表單
>
>
在與AEM Forms OSGi伺服器同步的AEM Forms應用程式中擷取的最適化表單中，不支援表單層級附件。 如果作者在編寫表單時啟用了欄位級附件，用戶可以在欄位中附加檔案。

**要開啟和更新表單**

1. 若要開啟表格，請點選主畫面中的表格。
1. 您可以更新表單的欄位、新增附件、另存為草稿，然後送出。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
