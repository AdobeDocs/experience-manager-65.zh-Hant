---
title: 管理訂閱
seo-title: 管理訂閱
description: 您可以透過AEM網頁上使用的表單元件，要求使用者訂閱電子郵件服務提供者的郵件清單。 要準備具有註冊表格的AEM頁面以訂購電子郵件服務郵寄清單，必須將相應的服務配置應用於潛在訂閱者將訪問的AEM頁面。
seo-description: 您可以透過AEM網頁上使用的表單元件，要求使用者訂閱電子郵件服務提供者的郵件清單。 要準備具有註冊表格的AEM頁面以訂購電子郵件服務郵寄清單，必須將相應的服務配置應用於潛在訂閱者將訪問的AEM頁面。
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# 管理訂閱{#managing-subscriptions}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售機會和清單）。
>建議您運用[Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md)。

在AEM網頁上使用的&#x200B;**Form**&#x200B;元件的協助下，可以要求使用者訂閱&#x200B;**電子郵件服務提供者的**&#x200B;郵件清單。 要準備具有註冊表格的AEM頁面以訂購電子郵件服務郵寄清單，必須將相應的服務配置應用於潛在訂閱者將訪問的AEM頁面。

## 將電子郵件服務配置應用到頁{#applying-email-service-configuration-to-a-page}

設定AEM頁面：

1. 導覽至&#x200B;**Websites**&#x200B;標籤。
1. 選取需要為服務設定的頁面。 按一下右鍵該頁，然後選擇&#x200B;**屬性**。

1. 依序選擇&#x200B;**Cloud Services**&#x200B;和&#x200B;**添加服務**。 從可用配置清單中選擇配置。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 按一下&#x200B;**「確定」**。

## 在AEM頁面上建立註冊表單以訂閱/取消訂閱清單{#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

要建立註冊表單並將其配置為訂閱電子郵件服務提供商的郵件清單，請執行以下操作：

1. 開啟使用者將造訪的AEM頁面。
1. 將電子郵件服務提供者的設定套用至頁面。

1. 將元件從sidekick拖曳，將&#x200B;**Form**&#x200B;元件新增至頁面。 如果元件不可用，請切換到設計模式並啟用&#x200B;**Form**&#x200B;組。
1. 按一下&#x200B;**Start of Form**&#x200B;列中的&#x200B;**Edit**，並導覽至&#x200B;**Advanced**&#x200B;標籤。
1. 在&#x200B;**Form**&#x200B;下拉菜單中，選擇&#x200B;**電子郵件服務：建立訂閱者**&#x200B;並添加到清單。
1. 在對話框底部，開啟&#x200B;**Action Configuration**&#x200B;下拉清單，該下拉清單允許您選擇一個或多個訂閱清單。
1. 在&#x200B;**Select list**&#x200B;中，選擇希望用戶訂閱的清單。 您可以使用加號按鈕（**新增項目**）來新增多個清單。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >您的對話框可能因電子郵件服務提供商而異。

1. 在&#x200B;**Form**&#x200B;標籤中，選擇您希望用戶在提交表單後轉到的感謝頁（如果保留為空，則在提交時表單將重新顯示）。 按一下&#x200B;**「確定」**。表單中會顯示&#x200B;**電子郵件ID**&#x200B;元件，可讓您建立表單，讓使用者提交電子郵件地址以訂閱或取消訂閱郵寄清單。
1. 從sidekick中的&#x200B;**Form**&#x200B;區段新增&#x200B;**Submit**&#x200B;按鈕元件。

   表單已就緒。 將上述步驟中設定的頁面與&#x200B;**感謝**&#x200B;頁面發佈至發佈執行個體。 任何造訪頁面的潛在訂閱者都可填寫表單並訂閱設定中提供的清單。

   >[!NOTE]
   >
   >若要讓表單訂閱功能正確運作，必須在發佈執行個體](#exporting-keys-from-author-and-importing-on-publish)上匯出和匯入來自作者的[加密金鑰。

## 從作者匯出金鑰並在發佈時匯入{#exporting-keys-from-author-and-importing-on-publish}

若要透過發佈執行個體上的註冊表單來訂閱和取消訂閱工作的電子郵件服務，您必須執行下列步驟：

1. 在製作例項上，導覽至套件管理器。
1. 建立新套件。 將篩選器設定為`/etc/key`。
1. 建置並下載套件。
1. 導覽至發佈執行個體上的套件管理器，然後上傳此套件。
1. 導覽至Publish osgi主控台，然後重新啟動名為&#x200B;**AdobeGranite Crypto Support**&#x200B;的套件組合。

## 從清單{#unsubscribing-users-from-lists}取消訂閱用戶

若要取消訂閱清單中的用戶：

1. 開啟具有註冊表單的AEM頁面的頁面屬性，以取消訂閱銷售機會。
1. 將服務配置應用到頁。
1. 在頁面上建立註冊表單。
1. 配置元件時，選擇&#x200B;**E-mail Service**&#x200B;操作：**從清單中取消訂閱用戶。**
1. 從下拉式功能表中，選取取消訂閱時將從中移除使用者的適當清單。

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. 從作者匯出索引鍵至發佈。

## 為電子郵件服務{#configuring-auto-responder-emails-for-email-service}配置自動回應者電子郵件

為訂閱者配置自動響應者電子郵件：

1. 開啟具有註冊表單的AEM頁面的頁面屬性，以設定銷售機會的自動回應者。
1. 將ExactTarget設定套用至頁面。

1. 將元件從sidekick拖曳，將&#x200B;**Form**&#x200B;元件新增至頁面。 如果元件不可用，請切換到設計模式並啟用&#x200B;**Form**&#x200B;組。
1. 按一下&#x200B;**Start of Form**&#x200B;列中的&#x200B;**Edit**，並導覽至&#x200B;**Advanced**&#x200B;標籤。
1. 在&#x200B;**Form**&#x200B;下拉菜單中，選擇&#x200B;**電子郵件服務：傳送自動回應者電子郵件。**
1. **選取電子郵件** （這是以自動回應者電子郵件傳送的郵件）。

1. **選取「分類** 」（此分類用於傳送電子郵件）。
1. 選取&#x200B;**感謝**&#x200B;頁面（使用者提交表單後即被導向至的頁面）。

   在&#x200B;**Form**&#x200B;標籤中，選取您希望使用者在提交表單後前往的感謝頁面。 （如果保留為空白，則提交時會重新顯示表單。） 按一下&#x200B;**「確定」**。

1. 從作者匯出索引鍵至發佈。
1. 從sidekick中的&#x200B;**Form**&#x200B;區段新增&#x200B;**Submit**&#x200B;按鈕元件。

   註冊表已準備好。 將上述步驟中設定的頁面與&#x200B;**感謝**&#x200B;頁面發佈至發佈執行個體。 任何可能造訪頁面的訂閱者皆可填寫表單，在提交表單時，訪客會在表單中填入的電子郵件ID上收到自動回應者的電子郵件。

   >[!NOTE]
   >
   >為了讓註冊表單訂閱正確運作，必須在發佈執行個體](#exporting-keys-from-author-and-importing-on-publish)上匯出和匯入來自作者的[加密密鑰。

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
