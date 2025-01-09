---
title: 連線到 Microsoft Translator
description: 瞭解如何將AEM連線至現成的Microsoft Translator，以自動化您的翻譯工作流程。
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3bb516289dbff4fb3b94685b9e25360e7717776e
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 7%

---

# 連線到 Microsoft Translator {#connecting-to-microsoft-translator}

AEM為[Microsoft Translator](https://www.microsoft.com/en-us/translator/business/)提供內建聯結器，用於翻譯頁面內容或資產。 從Microsoft取得使用Microsoft Translator的授權後，請依照本頁面上的指示設定聯結器。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選用）對於使用者產生的內容，為已翻譯文字旁邊顯示的屬性，例如`Translations by Microsoft` |
| WORKSPACE ID | （選用）要使用的自訂Microsoft Translator引擎識別碼 |
| 訂閱金鑰 | 您的Microsoft Translator Microsoft訂閱金鑰 |

下列程式會建立Microsoft Translator設定。

1. 在[導覽面板中，](/help/sites-authoring/basic-handling.md#first-steps)按一下&#x200B;**工具** > **Cloud Service** > **翻譯Cloud Service**。
1. 導覽至您要建立設定的位置。 這通常位於您的網站根目錄中，或可為全域預設設定。
1. 按一下&#x200B;**建立**&#x200B;按鈕。
1. 定義您的設定。
   1. 在下拉式清單中選取&#x200B;**Microsoft翻譯工具**。
   1. 輸入設定的標題。 標題可識別Cloud Service控制檯和頁面屬性下拉式清單中的設定。
   1. 選擇性地輸入儲存組態之儲存庫節點的名稱。

   ![建立翻譯設定](assets/create-translation-config.png)

1. 按一下&#x200B;**建立**。
1. 在&#x200B;**編輯組態**&#x200B;視窗中，提供上一個表格所述之翻譯服務的值。

   ![編輯翻譯設定](assets/msft-config-ui.png)

1. 按一下&#x200B;**連線**&#x200B;以驗證連線。
1. 按一下「**儲存並關閉**」。

## 發佈Translator服務設定 {#publishing-the-translator-service-configurations}

最後一個步驟，請使用[發佈樹狀結構](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)動作，發佈您的Microsoft Translator設定，以支援已發佈的翻譯內容。
