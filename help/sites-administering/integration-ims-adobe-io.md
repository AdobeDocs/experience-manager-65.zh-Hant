---
title: 使用Adobe I/O與Adobe Target整合
seo-title: 使用Adobe I/O與Adobe Target整合
description: 瞭解如何使用Adobe I/O將AEM與Adobe Target整合
seo-description: 瞭解如何使用Adobe I/O將AEM與Adobe Target整合
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---


# 使用Adobe I/O與Adobe Target整合{#integration-with-adobe-target-using-adobe-i-o}

AEM與Adobe Target透過Target Standard API整合需要設定Adobe IMS（身分管理系統）和Adobe I/O。

>[!NOTE]
>
>AEM 6.5中新增了Adobe Target Standard API支援。Target Standard API使用IMS驗證。
>
>在AEM中使用Adobe Target Classic API仍支援回溯相容性。 [Target Classic API使用用戶憑據驗證](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。
>
>API選擇是由用於AEM/Target整合的驗證方法所驅動。

## 必備條件 {#prerequisites}

開始此過程之前：

* [Adobe支](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html) 援必須為您的帳戶布建：

   * Adobe Console
   * Adobe I/O
   * Adobe Target和
   * Adobe IMS（身分管理系統）

* 貴組織的系統管理員應使用Admin Console將貴組織中必要的開發人員新增至相關的產品設定檔。

   * 這可讓特定開發人員擁有在Adobe I/O內啟用整合的權限。
   * 如需詳細資訊，請參閱[管理開發人員](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。


## 配置IMS配置——生成公鑰{#configuring-an-ims-configuration-generating-a-public-key}

設定的第一個階段是在AEM中建立IMS設定並產生公用金鑰。

1. 在AEM中，開啟&#x200B;**Tools**&#x200B;功能表。
1. 在&#x200B;**Security**&#x200B;區段中，選擇&#x200B;**Adobe IMS Configurations**。
1. 選擇&#x200B;**Create**&#x200B;以開啟&#x200B;**Adobe IMS技術帳戶設定**。
1. 使用&#x200B;**雲端設定**&#x200B;下方的下拉式清單，選取&#x200B;**Adobe Target**。
1. 激活&#x200B;**建立新證書**&#x200B;並輸入新別名。
1. 使用&#x200B;**建立憑證**&#x200B;進行確認。

   ![](assets/integrate-target-io-01.png)

1. 選擇&#x200B;**下載**（或&#x200B;**下載公開金鑰**）將檔案下載至本機磁碟機，以便在[設定Adobe I/O以與AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)整合時使用。

   >[!CAUTION]
   >
   >請保持此設定開啟，當[在AEM](#completing-the-ims-configuration-in-aem)中完成IMS設定時，將會再次需要此設定。

   ![](assets/integrate-target-io-02.png)

## 將Adobe I/O設定為與AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}整合的Adobe Target

您必須使用AEM將使用的Adobe Target建立Adobe I/O專案（整合），然後指派所需的權限。

### 建立項目{#creating-the-project}

開啟Adobe I/O主控台，以建立AEM將使用的Adobe Target I/O專案：

>[!NOTE]
>
>另請參閱[Adobe I/O教學課程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)。

1. 開啟專案的Adobe I/O主控台：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 您擁有的任何專案都會顯示。 選擇&#x200B;**建立新項目** —— 位置和使用情況取決於：

   * 如果您尚未有任何專案，**建立新專案**將位於底部中央。
      ![建立新專案——第一個專案](assets/integration-target-io-02.png)
   * 如果您已有現有的專案，則會列出這些專案，而&#x200B;**建立新專案**將會在右上方。
      ![建立新專案——多個專案](assets/integration-target-io-03.png)


1. 選擇&#x200B;**添加到項目**，後跟&#x200B;**API**:

   ![](assets/integration-target-io-10.png)

1. 選擇&#x200B;**Adobe Target**，然後選擇&#x200B;**Next**:

   >[!NOTE]
   >
   >如果您已訂閱Adobe Target，但未看到其列出，則應勾選[Prerequestes](#prerequisites)。

   ![](assets/integration-target-io-12.png)

1. **上傳您的公開金鑰**，完成時，請繼續「下 **一步**:

   ![](assets/integration-target-io-13.png)

1. 查看憑據，然後繼續&#x200B;**Next**:

   ![](assets/integration-target-io-15.png)

1. 選擇所需的產品配置檔案，然後繼續&#x200B;**保存配置的API** :

   >[!NOTE]
   >
   >顯示的產品設定檔取決於您是否有：
   >
   >* Adobe Target Standard —— 僅提供&#x200B;**預設工作區**
   >* Adobe Target Premium —— 會列出所有可用的工作區，如下所示


   ![](assets/integration-target-io-16.png)

1. 將確認建立。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 將權限分配給整合{#assigning-privileges-to-the-integration}

您現在必須將必要的權限指派給整合：

1. 開啟Adobe **管理控制台**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 導覽至&#x200B;**Products**（頂端工具列），然後選取&#x200B;**Adobe Target - &lt;*your-tenant-id*>**（從左側面板）。
1. 選擇「**產品描述檔**」，然後從顯示的清單中選擇您所需的工作區。 例如，預設工作區。
1. 選擇&#x200B;**整合**，然後選擇所需的整合設定。
1. 選擇&#x200B;**Editor**&#x200B;作為&#x200B;**產品角色**;而非&#x200B;**觀察者**。

## Adobe I/O整合專案的詳細資訊儲存在{#details-stored-for-the-adobe-io-integration-project}

從Adobe I/O Projects主控台，您可以看到所有整合專案的清單：

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

選擇&#x200B;**View**（位於特定項目條目的右側）以顯示有關配置的詳細資訊。 其中包括：

* 專案概觀
* 分析
* 認證
   * 服務帳戶(JWT)
      * 憑據詳細資訊
      * 生成JWT
* APIS
   * 例如，Adobe Target

其中有些您需要完成AEM中Target的Adobe I/O整合。

## 在AEM {#completing-the-ims-configuration-in-aem}中完成IMS設定

返回AEM時，您可以從Target的Adobe I/O整合新增必要值，以完成IMS設定：

1. 返回在AEM](#configuring-an-ims-configuration-generating-a-public-key)中開啟的[IMS設定。
1. 選擇&#x200B;**Next**。

1. 您可以在這裡使用Adobe I/O](#details-stored-for-the-adobe-io-integration-project)的[詳細資料：

   * **標題**:您的文字。
   * **授權伺服器**:從下方的Payloadsection `"aud"` 行複製/ **** 貼上此選項，例如 `"https://ims-na1.adobelogin.com"` 在下方範例中
   * **API金鑰**:從Adobe I/O [](#details-stored-for-the-adobe-io-integration-project) 整合的Overview區段中複製此項
   * **用戶端密碼**:在Target的Adobe I/O [](#details-stored-for-the-adobe-io-integration-project) 整合的「概述」區段中產生此項，並複製
   * **裝載**:從Adobe I/O [整合](#details-stored-for-the-adobe-io-integration-project) 的Generate JWTsection for Target複製此項

   ![](assets/integrate-target-io-10.png)

1. 使用&#x200B;**Create**&#x200B;確認。

1. 您的Adobe Target設定會顯示在AEM主控台中。

   ![](assets/integrate-target-io-11.png)

## 確認IMS配置{#confirming-the-ims-configuration}

要確認配置正如預期運行，請執行以下操作：

1. 開啟:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 選擇您的配置。
1. 從工具欄中選擇&#x200B;**Check Health** ，然後選擇&#x200B;**Check**。

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您將看到以下消息：

   ![](assets/integrate-target-io-13.png)

## 設定Adobe Target Cloud服務{#configuring-the-adobe-target-cloud-service}

現在，雲端服務可參考此設定，以使用Target Standard API:

1. 開啟&#x200B;**工具**&#x200B;菜單。 然後，在&#x200B;**雲服務**&#x200B;區段中，選擇&#x200B;**舊版雲服務**。
1. 向下捲動至&#x200B;**Adobe Target**，然後選取&#x200B;**立即設定**。

   將開啟&#x200B;**建立配置**&#x200B;對話框。

1. 輸入&#x200B;**Title**&#x200B;和&#x200B;**Name**（如果保留為空白，則會從標題生成）。

   您也可以選取所需範本（如果有多個範本可用）。

1. 使用&#x200B;**Create**&#x200B;確認。

   將開啟&#x200B;**編輯元件**&#x200B;對話框。

1. 在&#x200B;**Adobe Target Settings**&#x200B;標籤中輸入詳細資訊：

   * **驗證**:IMS
   * **租用戶ID**:adobe IMS租用戶ID

      >[!NOTE]
      >
      >對於IMS，此值必須取自Target本身。 您可以登入Target，並從URL擷取租用戶ID。
      >
      >例如，若URL為：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >然後您會使用`yourtenantid`。

   * **IMS設定**:選擇IMS設定的名稱
   * **API類型**:REST
   * **A4T Analytics雲端設定**:選取用於目標活動目標和度量的Analytics雲端設定。如果您在定位內容時使用Adobe Analytics做為報告來源，則需要此功能。 如果您看不到雲端設定，請參閱[設定A4T Analytics雲端設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)中的附註。
   * **使用精確的定位**:預設情況下，此複選框處於選中狀態。如果選取此選項，雲端服務設定會等待載入內容後再載入內容。 請參閱以下附註。
   * **從Adobe Target同步區段**:選取這個選項可下載在Target中定義的區段，以便在AEM中使用。當「API類型」屬性為REST時，您必須選取此選項，因為不支援內嵌區段，而且您一律需要使用Target中的區段。 （請注意，「區段」的AEM詞語等同於「目標對象」。）
   * **用戶端程式庫**:選擇您要AT.js用戶端程式庫或mbox.js（已過時）。
   * **使用標籤管理系統來傳送用戶端程式庫**:使用DTM（已過時）、Adobe Launch或任何其他標籤管理系統。
   * **自訂AT.js**:如果您勾選「標籤管理」方塊或使用預設AT.js，請留空。或者，上傳您的自訂AT.js。 只有在您選取了AT.js時才會顯示。

   >[!NOTE]
   >
   >[已停用雲端服務使用Target Classic ](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API的設定（使用Adobe Recommendations的「設定」標籤）。

   例如：

   ![](assets/integrate-target-io-14.png)

1. 按一下「連線至Target」，以初始化與Adobe Target的連線。****

   如果連接成功，則顯示消息&#x200B;**Connection successful**。

1. 在消息上選擇&#x200B;**OK**，然後在對話框上選擇&#x200B;**OK**&#x200B;以確認配置。
1. 您現在可以繼續[新增Target Framework](/help/sites-administering/target-configuring.md#adding-a-target-framework)，以設定將傳送至Target的ContextHub或ClientContext參數。 請注意，將AEM體驗片段匯出至Target時可能不需要這個功能。

