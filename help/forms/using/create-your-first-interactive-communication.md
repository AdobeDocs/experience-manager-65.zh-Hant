---
title: 教學課程 — 建立您的第一個互動式通訊
seo-title: Create your first Interactive Communication
description: 了解如何建立您的第一個互動式通訊。
seo-description: Learn to create your first Interactive Communication.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# 教學課程：建立您的第一個互動式通訊 {#tutorial-create-your-first-interactive-communication}

了解如何建立您的第一個互動式通訊。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

「互動式通訊」可集中處理和管理安全、個人化與互動式通信的建立、集合與傳送，例如商業信函、檔案、對帳單、行銷郵件、帳單和歡迎套件。 互動式通訊可透過兩個通道提供：打印和Web。 「列印」管道可用來建立PDF和紙張通訊，而「網頁」管道則可用來提供線上體驗。

本教學課程提供端對端架構，以建立互動式通訊。 本教學課程可整合為一個使用案例和多個指南。 每本指南都可協助您建立功能，這些功能可作為建立互動式通訊的基礎。

下圖說明建立互動式通訊所需的建置區塊。

![工作流程](assets/workflow.gif)

在本教學課程結束時，您將能夠：

* 建立建置區塊（表單資料模型、檔案片段和範本）
* 建立互動式通訊
* 測試並發佈互動式通訊

## 使用案例 {#use-case}

歷程從學習使用案例開始：

電信營運商會透過電子郵件傳送每月帳單給客戶。 賬單是互動式通訊。 電子郵件包括：

* 受密碼保護的PDF，在本教學課程中稱為「列印通道」。 它包括客戶詳細資訊、帳單詳細資訊、費用摘要、支付賬單的方便模式和使用詳細資訊。
* 指向Web版本的帳單的連結，在本教學課程中稱為Web渠道。 除了PDF版本中涵蓋的詳細資訊外，帳單的Web版本還提供使用詳細資訊的圖形表示，以及基於Adobe Target的個性化優惠。 該Web版本還包含線上支付表。 在不離開IC的情況下進行線上支付是有幫助的。
* 增值服務的連結，例如線上儲存、音樂訂閱和隨選視訊訂閱。

## 必備條件 {#prerequisites}

* 設定AEM製作例項。
* 安裝 [AEM Forms附加元件](/help/forms/using/installing-configuring-aem-forms-osgi.md) 在作者例項上
* 設定MYSQL資料庫
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 本教程中的示例基於MySQL資料庫，並使用Oracle [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html).

## 步驟1:規劃互動式通訊 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

規劃互動式通訊的第一步是完成互動式通訊的內容。 內容完成後，您必須分析內容，以識別建立互動式通訊所需的各種資產類型。

**目標：**

使用以下資料輸入模式建立互動式通信的解剖結構：

* 靜態文字
* 表單資料模型
* Agent UI
* 條件式資料
* 影像

[ ](/help/forms/using/planning-interactive-communications.md)

## 步驟2:建立表單資料模型 {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表單資料模型可讓您將互動式通訊連接至不同的資料來源。 例如，AEM用戶配置檔案、RESTful Web服務、基於SOAP的Web服務、OData服務和關係資料庫。 表單資料模型是業務實體和服務在連接資料源中提供的統一資料表示模式。 您可以使用具有互動式通訊的表單資料模型，從連線的資料來源擷取資料。 如需表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](/help/forms/using/data-integration.md).

**目標：**

* 將資料庫實例（MySQL資料庫）配置為資料源
* 使用MySQL資料庫作為資料源建立表單資料模型
* 添加資料模型對象以形成資料模型
* 為表單資料模型配置讀寫服務
* 建立資料模型對象之間的關聯
* 檢視自動產生的範例資料
* 編輯範例資料
* 測試表單資料模型和已配置的服務（含測試資料）

[ ](/help/forms/using/create-form-data-model0.md)

## 步驟3:建立檔案片段 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

文檔片段是用於構成互動式通信的通信的可重複使用的元件。 檔案片段的類型為：文字、清單和條件。

**目標：**

* 建立檔案片段
* 建立變數
* 建立和套用規則

[ ](/help/forms/using/create-document-fragments.md)

## 步驟4:建立範本 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

若要建立互動式通訊，您必須在AEM伺服器上提供用於列印和網頁頻道的範本。

列印管道的範本是在AdobeForms Designer中建立，並上傳至AEM伺服器。 然後，這些模板便可在建立互動式通信時使用。

網頁管道的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

**目標：**

* 使用AdobeForms Designer為列印管道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用Web通道的模板

[ ](/help/forms/using/create-templates-print-web.md)

## 步驟5:建立互動式通訊 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

在您為Web版本建立所有構建模組（如表單資料模型、文檔片段和模板）後，就可以開始建立互動式通信。

互動式通訊可透過兩個通道提供：打印和Web。 您也可以建立以「打印」通道作為主資訊的互動式通信。 Web頻道的打印為主選項可確保從打印頻道導出Web頻道的內容、繼承和資料綁定。

**目標：**

* 為打印通道建立互動式通信
* 為Web通道建立互動式通信
* 以Print as Master建立打印和Web交互通信
* 在Web版互動式通信中建立動態表
* 在Web版互動式通信中建立圖表
* 在互動式通訊的網頁版本中建立超連結

[ ](/help/forms/using/create-interactive-communication0.md)

## 步驟6:發佈您的互動式通訊 {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

使用列印和網頁通道建立和測試互動式通訊後，您就可以發佈這些資產。 本教學課程中說明的使用案例著重於將這些資產與電子郵件用戶端整合。 電子郵件用戶端可作為傳送互動式通訊至多個電子郵件地址的橋梁。

**目標：**

* 將互動式通訊與電子郵件用戶端整合，以便能夠傳送通訊給客戶
* 將PDF文檔作為附件（在打印通道中建立的互動式通信）
* 包括到Interactive Communication Web版本的連結
