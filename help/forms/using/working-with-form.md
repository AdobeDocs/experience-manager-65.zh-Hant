---
title: 使用表單
description: 檢視和更新與AEM Forms應用程式中的任務或起點相關聯的表單
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 使用表單 {#working-with-a-form}

如果表單已啟用在表單應用程式中同步，則會下載表單，且您可以直接使用表單。

這些表單會從您的應用程式下載，並可離線使用。 例如，您正在執行一家銀行公司，而客戶在您的網站上填寫應用程式。 應用程式是調適型表單，可接受客戶的資訊，並將其儲存以供稽核。 管理員會稽核表單，並在AEM編寫執行個體中建立驗證表單。 管理員可讓表單與AEM Forms應用程式同步。 如果AEM Forms應用程式中有提供驗證表單，您的欄位代理程式可使用行動裝置來驗證客戶的詳細資料。 行動裝置與伺服器同步，且驗證表單已載入應用程式中。 您的欄位代理程式可以造訪您的客戶、驗證詳細資料、將資料儲存為草稿或提交驗證表單。 每次應用程式上線時，表單都會與伺服器同步。

若要在AEM Forms應用程式中同步處理您的表單：

1. 在作者執行個體中，選取表單，然後按一下&#x200B;**檢視屬性**。
1. 在屬性頁面中，按一下&#x200B;**進階。**
1. 在[進階]下，啟用選項： **與AEM Forms應用程式同步**，然後選取&#x200B;**儲存**。

若要同步多個表單，請在作者執行個體中，選取表單管理員中的多個表單，然後選取&#x200B;**與AEM Forms應用程式同步**。 表單發佈時，AEM Forms應用程式可連線至發佈伺服器並擷取表單。

如果您的AFA (AEM Form Application) Android應用程式無法同步，請執行下列步驟以修正同步問題：

1. 移至&#x200B;**https://[伺服器]：[連線埠]/system/console/configMgr**。
1. 搜尋&#x200B;**[!UICONTROL AdobeGranite權杖驗證處理常式]**，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 從下拉式功能表中選取登入權杖Cookie ]**屬性之**[!UICONTROL  SameSite屬性的&#x200B;**[!UICONTROL 無]**&#x200B;選項。
1. 按一下「**[!UICONTROL 儲存]**」。

![將影像與AFA Android應用程式同步](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>支援的表單：
>
>* 調適型表單（無延遲載入）
>* 行動表單
>
>在與AEM Forms OSGi伺服器同步的AEM Forms應用程式中擷取的最適化表單不支援表單層級附件。 如果作者在編寫表單時啟用了欄位層級附件，則使用者可以在欄位中附加檔案。


**若要開啟並更新表單**

1. 若要開啟表單，請選取主畫面中的&#x200B;**[!UICONTROL 表單]**。
1. 您可以更新表單欄位、新增附件、另存為草稿並提交表單。
