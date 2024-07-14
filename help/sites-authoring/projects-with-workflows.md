---
title: 使用專案工作流程
description: 各種專案工作流程都可立即使用。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 3%

---


# 使用專案工作流程 {#working-with-project-workflows}

現成可用的專案工作流程包括下列專案：

* **專案核准工作流程** — 此工作流程可讓您指派內容給使用者、檢閱及核准。
* **要求啟動** — 要求啟動的工作流程。
* **要求登陸頁面** — 此工作流程會要求登陸頁面。
* **要求電子郵件** — 要求電子郵件的工作流程。
* **產品拍照和產品拍照(Commerce)** — 將資產與產品對應
* **DAM建立和翻譯復本及DAM建立語言復本** — 為資產和資料夾建立翻譯的二進位檔、中繼資料和標籤。

根據您選取的專案範本，您有特定可用的工作流程：

|   | **簡單專案** | **媒體專案** | **產品拍照專案** | **翻譯專案** |
|---|:-:|:-:|:-:|:-:|
| 請求副本 |  | x |  |  |
| 產品拍照 |  | x | x |  |
| 產品拍照(Commerce) |  |  | x |  |
| 專案核准 | x |  |  |  |
| 要求啟動 | x |  |  |  |
| 請求登陸頁面 | x |  |  |  |
| 要求電子郵件 | x |  |  |  |
| DAM建立語言副本&amp;amp；ast； |  |  |  | x |
| DAM建立及翻譯語言副本&amp;amp；ast； |  |  |  | x |

>[!NOTE]
>
>&amp;amp；ast；這些工作流程並非從專案中的&#x200B;**工作流程**&#x200B;圖磚開始。 請參閱[建立Assets的語言復本。](/help/sites-administering/tc-manage.md)

無論您選擇哪個工作流程，開始和完成工作流程的步驟都相同。 只有步驟會變更。

您直接在專案中啟動工作流程（DAM建立語言副本或DAM建立和翻譯語言副本除外）。 有關專案中所有未完成任務的資訊會列在&#x200B;**任務**&#x200B;圖磚中。 使用者圖示旁會顯示需要完成之工作的通知。

如需在AEM中使用工作流程的詳細資訊，請參閱下列檔案：

* [參與工作流程](/help/sites-authoring/workflows-participating.md)
* [將工作流程套用至頁面](/help/sites-authoring/workflows-applying.md)
* [設定工作流程](/help/sites-administering/workflows.md)

本節說明專案可用的工作流程。

## 請求複製工作流程 {#request-copy-workflow}

此工作流程可讓您向使用者要求手稿，然後核准它。 若要啟動請求複製工作流程：

1. 在媒體專案中，按一下&#x200B;**工作流程**&#x200B;圖磚右上方的向下>形箭號，並選取&#x200B;**開始工作流程**。
1. 在工作流程精靈中選取&#x200B;**要求復本**，然後按一下&#x200B;**下一步**。
1. 輸入手稿標題和您請求的簡短摘要。 如果適用，請輸入目標字數、工作優先順序和到期日。

   ![要求複製工作流程](assets/project-request-copy-workflow.png)

1. 按一下「**提交**」。

工作流程隨即開始。 任務出現在&#x200B;**任務**&#x200B;卡片上。

## 產品拍照工作流程 {#product-photo-shoot-workflow}

**產品拍照**&#x200B;工作流程（商務和非商務）已在檔案[創意專案](/help/sites-authoring/managing-product-information.md)中詳細說明

## 專案核准工作流程 {#project-approval-workflow}

在&#x200B;**專案核准**&#x200B;工作流程中，您指派內容給使用者、檢閱並核准內容。

1. 在簡單專案中，按一下&#x200B;**工作流程**&#x200B;圖磚右上方的向下>形箭號，然後選取&#x200B;**開始工作流程**。
1. 在工作流程精靈中選取&#x200B;**專案核准工作流程**，然後按一下&#x200B;**下一步**。
1. 輸入標題並選取指派對象。 如果適用，請輸入說明、內容路徑、工作優先順序和到期日。

   ![專案核准工作流程](assets/project-approval-workflow.png)

1. 按一下「**提交**」。

工作流程隨即開始。 任務出現在&#x200B;**任務**&#x200B;卡片上。

## 請求啟動工作流程 {#request-launch-workflow}

此工作流程可讓您請求啟動。

1. 在簡單專案中，按一下&#x200B;**工作流程**&#x200B;圖磚右上方的向下>形箭號，然後選取&#x200B;**開始工作流程**。
1. 在工作流程精靈中選取&#x200B;**要求啟動工作流程**，然後按一下&#x200B;**下一步**。
1. 輸入啟動的標題並提供啟動來源路徑。 您也可以新增說明和上線日期（如適用）。 根據您想要啟動項的行為，選取「繼承來源頁面即時資料」或「排除子頁面」 。

   ![要求啟動工作流程](assets/project-request-launch-workflow.png)

1. 按一下「**提交**」。

工作流程隨即開始。 工作流程出現在&#x200B;**工作流程**&#x200B;清單中。

## 請求登陸頁面工作流程 {#request-landing-page-workflow}

此工作流程可讓您請求登入頁面。

1. 在簡單專案中，按一下&#x200B;**工作流程**&#x200B;圖磚右上方的向下>形箭號，然後選取&#x200B;**開始工作流程**。
1. 在工作流程精靈中選取&#x200B;**要求登陸頁面**，然後按一下&#x200B;**下一步**。
1. 輸入登入頁面的標題和父路徑。 如果適用，請輸入即時日期或選擇登陸頁面的檔案。

   ![要求登陸頁面工作流程](assets/project-request-landing-page-workflow.png)

1. 按一下「**提交**」。

工作流程隨即開始。 任務出現在&#x200B;**任務**&#x200B;卡片上。

## 請求電子郵件工作流程 {#request-email-workflow}

此工作流程可讓您請求電子郵件。 **電子郵件**&#x200B;動態磚中出現相同的工作流程。

1. 在簡單專案中，按一下&#x200B;**工作流程**&#x200B;圖磚右上方的向下>形箭號，然後選取&#x200B;**開始工作流程**。
1. 在工作流程精靈中選取&#x200B;**要求電子郵件**，然後按一下&#x200B;**下一步**。
1. 輸入電子郵件標題，以及行銷活動和範本路徑。 此外，您還可以提供名稱、說明和上線日期。

   ![要求電子郵件工作流程](assets/project-request-email-workflow.png)

1. 按一下「**提交**」。

工作流程隨即開始。 任務出現在&#x200B;**任務**&#x200B;卡片上。

## 建立（及翻譯）Assets的語言副本工作流程 {#create-and-translate-language-copy-workflow-for-assets}

**建立語言副本**&#x200B;和&#x200B;**建立和翻譯語言副本**&#x200B;工作流程已在檔案[為Assets建立語言副本](/help/assets/translation-projects.md)中詳細說明。
