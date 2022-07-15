---
title: 教程 — 建立您的第一個互動式通信
seo-title: Create your first Interactive Communication
description: 學習建立第一個互動式通信。
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

# 教程：建立您的第一個互動式通信 {#tutorial-create-your-first-interactive-communication}

學習建立第一個互動式通信。

![01-Create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

互動式通信集中管理安全、個性化和互動式通信的建立、匯編和交付，如業務通信、文檔、報表、營銷郵件、帳單和歡迎套件。 互動式通信可以使用兩種渠道進行傳送：打印和Web。 打印通道用於建立PDF和紙張通信，而Web通道用於提供線上體驗。

本教程提供了一個端到端框架，用於建立互動式通信。 本教程分為使用案例和多個指南。 每個指南都幫助您建立用作構建塊的功能，以建立互動式通信。

下圖說明了建立互動式通信所需的構建塊。

![工作流程](assets/workflow.gif)

在本教程的結束時，您將能夠：

* 建立構建塊（表單資料模型、文檔片段和模板）
* 建立互動式通信
* Test並發佈互動式通信

## 用例 {#use-case}

這一過程始於學習使用案例：

電信運營商通過電子郵件向客戶發送每月賬單。 該法案是互動通訊。 電子郵件包括：

* 受密碼保護的PDF，在本教程中稱為打印通道。 它包括客戶詳細資訊、帳單詳細資訊、費用匯總、支付帳單的方便模式和使用詳細資訊。
* 指向Web版本的帳單的連結，在本教程中稱為Web渠道。 除了PDF版中涉及的細節外，帳單的Web版本還以圖形方式表示使用細節和基於Adobe Target的個性化優惠。 Web版本還包含線上付款表單。 在不離開IC的情況下進行線上支付，這對我們有幫助。
* 指向增值服務的連結，如線上儲存、音樂訂閱和按需視頻訂閱。

## 必備條件 {#prerequisites}

* 設定作AEM者實例。
* 安裝 [AEM Forms附加](/help/forms/using/installing-configuring-aem-forms-osgi.md) 關於作者實例
* 設定MYSQL資料庫
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 本教程中的示例基於MySQL資料庫並使用Oracle [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html)。

## 步驟1:規劃互動式通信 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

規劃互動式通信的第一步是最終確定互動式通信的內容。 定稿後，您必須分析內容以確定建立互動式通信所需的各種資產類型。

**目標：**

要使用以下資料輸入模式為互動式通信建立解剖結構：

* 靜態文本
* 窗體資料模型
* Agent UI
* 條件資料
* 影像

[ ](/help/forms/using/planning-interactive-communications.md)

## 步驟2:建立表單資料模型 {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表單資料模型允許您將互動式通信連接到不同的資料源。 例如，AEM用戶配置檔案、REST風格的Web服務、基於SOAP的Web服務、OData服務和關係資料庫。 表單資料模型是在連接資料源中可用的業務實體和服務的統一資料表示模式。 您可以將表單資料模型與互動式通信一起使用，從連接的資料源檢索資料。 有關表單資料模型的詳細資訊，請參見 [AEM Forms資料整合](/help/forms/using/data-integration.md)。

**目標：**

* 將資料庫實例（MySQL資料庫）配置為資料源
* 使用MySQL資料庫作為資料源建立表單資料模型
* 添加資料模型對象以形成資料模型
* 為表單資料模型配置讀和寫服務
* 建立資料模型對象之間的關聯
* 查看自動生成的示例資料
* 編輯示例資料
* Test表單資料模型和具有test資料的配置服務

[ ](/help/forms/using/create-form-data-model0.md)

## 第3步：建立文檔片段 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

文檔片段是用於構成互動式通信的通信的可重用元件。 文檔片段的類型有：文本、清單和條件。

**目標：**

* 建立文檔片段
* 建立變數
* 建立和應用規則

[ ](/help/forms/using/create-document-fragments.md)

## 第4步：建立模板 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

要建立互動式通信，必須在伺服器上提供用於打AEM印和Web通道的模板。

打印通道的模板是在AdobeForms設計器中建立並上載到服AEM務器。 然後，這些模板在建立交互通信時可用。

Web通道的模板是在中建立AEM的。 模板作者和管理員可以建立、編輯和啟用Web模板。 建立並啟用後，這些模板可在建立交互通信時使用。

**目標：**

* 使用AdobeForms設計器為打印通道建立XDP模板
* 將XDP模板上載到AEM Forms伺服器
* 為Web渠道建立和啟用模板

[ ](/help/forms/using/create-templates-print-web.md)

## 第5步：建立互動式通信 {#step-create-an-interactive-communication}

![09樣式自適應形式小](assets/09-style-your-adaptive-form-small.png)

一旦為Web版本建立了所有構建塊（如表單資料模型、文檔片段和模板），就可以開始建立互動式通信。

互動式通信可以通過兩種渠道進行：打印和Web。 還可以建立以打印通道為主的互動式通信。 作為Web頻道的主選項打印可確保Web頻道的內容、繼承和資料綁定是從打印頻道派生的。

**目標：**

* 為打印通道建立互動式通信
* 為Web通道建立互動式通信
* 建立以打印為主的打印和Web交互通信
* 在Web版本的Interactive Communication中建立動態表
* 在Web版的互動式通信中建立圖表
* 在Web版本的互動式通信中建立超連結

[ ](/help/forms/using/create-interactive-communication0.md)

## 步驟6:發佈互動式通信 {#step-publish-your-interactive-communication}

![12 — 發佈 — 自適應 — 窗體 — _small](assets/12-publish-your-adaptive-form-_small.png)

使用打印和Web渠道建立和test互動式通信後，可以發佈這些資產。 本教程中介紹的使用案例重點介紹將這些資產與電子郵件客戶端整合。 電子郵件客戶端充當將互動式通信發送到多個電子郵件地址的橋梁。

**目標：**

* 將互動式通信與電子郵件客戶端整合，以便能夠向客戶發送通信
* 將PDF文檔作為附件（在打印通道中建立的互動式通信）
* 包括指向互動式通信的Web版本的連結
