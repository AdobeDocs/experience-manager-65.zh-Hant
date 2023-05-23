---
title: 使用窗體
seo-title: Working with a Form
description: 查看和更新與AEM Forms應用中的任務或起點關聯的表單
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: eb71119474f03a969a721c792b6f1ac330f9dbf3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 使用窗體 {#working-with-a-form}

如果表單在表單應用中啟用了同步功能，則會下載表單，您可以直接使用它。

表單將下載到您的應用上，並可離線使用。 例如，您正在運行一家銀行公司，而客戶在您的站點上填寫應用程式。 該應用程式是一種自適應表單，可接受客戶提供的資訊並儲存它以供審閱。 管理員審閱表單，並在作者實例中建立AEM驗證表單。 管理員啟用表單與AEM Forms應用同步。 如果驗證表單在AEM Forms應用中可用，則您的現場代理可以使用移動設備驗證客戶的詳細資訊。 移動設備與伺服器同步，驗證表單載入到應用中。 您的現場工程師可以訪問客戶、驗證詳細資訊、將資料另存為草稿或提交驗證表。 每次您的應用聯機時，表單都與伺服器同步。

要在AEM Forms應用中同步窗體：

1. 在作者實例中，選擇一個表單，然後按一下 **查看屬性**。
1. 在屬性頁中，按一下 **高級。**
1. 在「高級」下，啟用選項： **與AEM Forms應用同步**，然後點擊 **保存**。

要同步多個表單，請在作者實例中，在表單管理器中選擇多個表單，然後點擊 **與AEM Forms應用同步**。 在發佈表單時，AEM Forms應用可以連接到發佈伺服器並獲取表單。

如果您的AFA(表AEM單應用程式)Android應用無法同步，請執行以下步驟來解決同步問題：

1. 轉到 **https://[伺服器]:[埠]/system/console/configMgr**。
1. 搜索 **[!UICONTROL Adobe花崗岩令牌驗證處理程式]** 按一下 **[!UICONTROL 編輯]**。
1. 選擇 **[!UICONTROL 無]** 選項 **[!UICONTROL 登錄令牌Cookie的SameSite屬性]** 屬性。
1. 按一下「**[!UICONTROL 儲存]**」。

![與AFA Android應用同步映像](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>支援的表單：
>
>* 自適應表單（無延遲載入）
>* 移動表單
>
>在與AEM FormsOSGi伺服器同步的AEM Forms應用中讀取的自適應表單中，不支援表單級別附件。 如果作者在創作表單時啟用了欄位級附件，則用戶可以附加欄位中的檔案。


**開啟和更新表單**

1. 要開啟窗體，請點擊 **[!UICONTROL 窗體]** 在主螢幕上。
1. 您可以更新表單的欄位、添加附件、另存為草稿並提交。
