---
title: 使用專案工作流程
seo-title: Working with Project Workflows
description: 各種項目工作流都可開箱即用。
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---


# 使用專案工作流程 {#working-with-project-workflows}

現成的項目工作流包括以下內容：

* **項目審批工作流**  — 此工作流允許您將內容分配給用戶、審閱和批准。
* **請求啟動**  — 請求啟動的工作流。
* **請求登錄頁**  — 此工作流請求登錄頁。
* **請求電子郵件**  — 請求電子郵件的工作流。
* **產品照片和產品照片（商業）**  — 用產品映射資產
* **DAM建立和翻譯副本和DAM建立語言副本**  — 為資產和資料夾建立已轉換的二進位檔案、元資料和標籤。

根據您選擇的項目模板，您可以使用某些工作流：

|  | **簡單專案** | **媒體專案** | **產品照片拍攝項目** | **翻譯專案** |
|---|:-:|:-:|:-:|:-:|
| 請求副本 |  | x |  |  |
| 產品照片拍攝 |  | x | x |  |
| 產品照片拍攝（商業） |  |  | x |  |
| 項目審批 | x |  |  |  |
| 請求啟動 | x |  |  |  |
| 請求登錄頁 | x |  |  |  |
| 請求電子郵件 | x |  |  |  |
| &amp;DAM建立語言複製； |  |  |  | x |
| &amp;DAM建立和翻譯語言副本； |  |  |  | x |

>[!NOTE]
>
>&amp;ast;這些工作流不是從 **工作流** 在項目中平鋪。 請參閱 [為資產建立語言副本。](/help/sites-administering/tc-manage.md)

無論您選擇哪個工作流，啟動和完成工作流的步驟都相同。 只有步驟會改變。

您可以直接在項目中啟動工作流（DAM建立語言副本或DAM建立和翻譯語言副本除外）。 有關項目中任何未完成任務的資訊列於 **任務** 平鋪。 需要完成的任務的通知顯示在用戶表徵圖旁邊。

有關使用中的工作流的詳細信AEM息，請參閱以下文檔：

* [參與工作流](/help/sites-authoring/workflows-participating.md)
* [將工作流應用於頁面](/help/sites-authoring/workflows-applying.md)
* [配置工作流](/help/sites-administering/workflows.md)

本節介紹可用於項目的工作流。

## 請求複製工作流 {#request-copy-workflow}

此工作流允許您從用戶請求手稿，然後批准它。 要啟動請求複製工作流，請執行以下操作：

1. 在媒體項目中，點擊或按一下右上角的向下雪形 **工作流** 平鋪和選擇 **啟動工作流**。
1. 在工作流嚮導中，選擇 **請求副本** 按一下 **下一個**。
1. 輸入手稿標題和您請求的內容的摘要。 如果適用，請輸入目標字數、任務優先順序和到期日期。

   ![請求複製工作流](assets/project-request-copy-workflow.png)

1. 按一下 **提交**。

工作流將啟動。 任務將出現在 **任務** 卡。

## 產品照片拍攝工作流 {#product-photo-shoot-workflow}

的 **產品照片拍攝** 文檔詳細介紹了工作流（商業和非商業） [創意項目](/help/sites-authoring/managing-product-information.md)

## 項目審批工作流 {#project-approval-workflow}

在 **項目審批** 工作流，您可以將內容分配給用戶、審閱，然後批准內容。

1. 在簡單的項目中，點擊或按一下右上角的向下雪形 **工作流** 平鋪和選擇 **啟動工作流**。
1. 在工作流嚮導中，選擇 **項目審批工作流** 按一下 **下一個**。
1. 輸入標題，然後選擇要將其分配給誰。 如果適用，請輸入說明、內容路徑、任務優先順序和到期日期。

   ![項目審批工作流](assets/project-approval-workflow.png)

1. 按一下 **提交**。

工作流將啟動。 任務將出現在 **任務** 卡。

## 請求啟動工作流 {#request-launch-workflow}

此工作流允許您請求啟動。

1. 在簡單的項目中，點擊或按一下右上角的向下雪形 **工作流** 平鋪和選擇 **啟動工作流**。
1. 在工作流嚮導中，選擇 **請求啟動工作流** 按一下 **下一個**。
1. 輸入啟動的標題並提供啟動源路徑。 如果適用，還可以添加說明和即時日期。 根據您希望啟動的行為方式選擇「繼承源頁即時資料」或「排除子頁」。

   ![請求啟動工作流](assets/project-request-launch-workflow.png)

1. 按一下 **提交**。

工作流將啟動。 工作流將出現在 **工作流** 清單框。

## 請求登錄頁工作流 {#request-landing-page-workflow}

此工作流允許您請求登錄頁。

1. 在簡單的項目中，點擊或按一下右上角的向下雪形 **工作流** 平鋪和選擇 **啟動工作流**。
1. 在工作流嚮導中，選擇 **請求登錄頁** 按一下 **下一個**。
1. 輸入登錄頁和父路徑的標題。 如果適用，請輸入即時日期或為登錄頁選擇檔案。

   ![請求登錄頁工作流](assets/project-request-landing-page-workflow.png)

1. 按一下 **提交**。

工作流將啟動。 任務將出現在 **任務** 卡。

## 請求電子郵件工作流 {#request-email-workflow}

此工作流允許您請求電子郵件。 顯示在 **電子郵件** 平鋪。

1. 在簡單的項目中，點擊或按一下右上角的向下雪形 **工作流** 平鋪和選擇 **啟動工作流**。
1. 在工作流嚮導中，選擇 **請求電子郵件** 按一下 **下一個**。
1. 輸入電子郵件標題以及市場活動和模板路徑。 此外，您還可以提供名稱、說明和即時日期。

   ![請求電子郵件工作流](assets/project-request-email-workflow.png)

1. 按一下 **提交**。

工作流將啟動。 任務將出現在 **任務** 卡。

## 為資產建立（和翻譯）語言複製工作流 {#create-and-translate-language-copy-workflow-for-assets}

的 **建立語言副本** 和 **建立和翻譯語言副本** 文檔詳細介紹了工作流 [為資產建立語言副本。](/help/assets/translation-projects.md)
