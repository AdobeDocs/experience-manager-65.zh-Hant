---
title: 連線到 Microsoft Translator
description: 瞭解如何將AEM連線至現成的Microsoft Translator，以自動化您的翻譯工作流程。
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 4%

---

# 連線到 Microsoft Translator {#connecting-to-microsoft-translator}

建立[Microsoft Translator](https://www.microsoft.com/en-us/translator/business/)雲端服務的設定，以使用您的Microsoft Translation帳戶來翻譯AEM頁面內容或資產。

>[!NOTE]
>
>AEM提供試用的Microsoft翻譯帳戶，每月最多允許200萬個免費翻譯的字元。 若要取得足以用於生產系統的帳戶訂閱，請參閱[升級Microsoft Translator試用授權組態](#upgrading-the-microsoft-translator-trial-license-configuration)。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選用）對於使用者產生的內容，為已翻譯文字旁邊顯示的屬性，例如`Translations by Microsoft` |
| WORKSPACE ID | （選用）要使用的自訂Microsoft Translator引擎識別碼 |
| 訂閱金鑰 | 您的Microsoft Translator Microsoft訂閱金鑰 |

建立組態之後，您需要[啟動它](#activating-the-translator-service-configurations)。

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

   ![編輯翻譯設定](assets/edit-translation-config.png)

1. 按一下&#x200B;**連線**&#x200B;以驗證連線。
1. 按一下&#x200B;**「儲存並關閉」**。

## 升級Microsoft Translator試用授權設定 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft翻譯設定頁面提供指向Microsoft網站的便利連結，以取得足以用於生產系統的帳戶訂閱。

1. 在[導覽面板中，](/help/sites-authoring/basic-handling.md#first-steps)按一下&#x200B;**工具** > **Cloud Service** > **翻譯Cloud Service**。
1. 按一下您現有的Microsoft Translator設定。
1. 按一下&#x200B;**編輯**。
1. 在&#x200B;**編輯組態**&#x200B;視窗中，按一下&#x200B;**升級訂閱**。 隨即開啟一個包含服務詳細資訊的Microsoft網頁。

## 自訂Microsoft Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，讓您自訂Microsoft Translator引擎。

1. 在[導覽面板中，](/help/sites-authoring/basic-handling.md#first-steps)按一下&#x200B;**工具** > **Cloud Service** > **翻譯Cloud Service**。
1. 按一下您現有的Microsoft Translator設定。
1. 按一下&#x200B;**編輯**。
1. 在&#x200B;**編輯組態**&#x200B;視窗中，按一下&#x200B;**自訂Translator**。 使用開啟的Microsoft網頁來自訂您的服務。

## 啟用Translator服務設定 {#activating-the-translator-service-configurations}

您需要啟動雲端服務設定，以支援復寫至發佈執行個體的翻譯內容。 使用[發佈樹狀結構](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法，啟動儲存Microsoft Translator設定的存放庫節點。 這些節點位於下列父節點的下方：

* `/libs/settings/cloudconfigs/translation/msft-translation`
