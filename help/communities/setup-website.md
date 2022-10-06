---
title: 設定網站結構
seo-title: Setup Website Structure
description: 設定目錄
seo-description: Set up directories
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---

# 設定網站結構 {#setup-website-structure}

若要設定您的網站，下列指示會說明要在下列位置建立的資料夾：

* `/apps/an-scf-sandbox`

   這是自訂應用程式和範本所在的位置。

* `/etc/designs/an-scf-sandbox`

   可下載的設計元素位於此處。

* `/content/an-scf-sandbox`

   這是可下載網頁的所在位置。

本教學課程中的程式碼將仰賴應用程式、設計和內容的主要資料夾名稱相同。 如果您為網站選擇其他名稱，請一律取代 `an-scf-sandbox` 以您選擇的名稱。

>[!NOTE]
>
>關於名稱：
>
>* CRXDE中顯示的名稱是構成可定址內容路徑的節點名稱。
>* 節點名稱可能包含空格，但在URI中使用時，該空格必須編碼為「%20」或「+」。
>* 節點名稱可能包含連字型大小和底線，但在Java檔案中以封裝名稱參考時，必須對連字型大小和底線進行編碼。 連字型大小和底線都會以底線逸出，後面接著其unicode值：
   >
   >   * 連字型大小變成「_002d」
   >   * 下划線變為「_005f」


## 設定應用程式目錄(/apps) {#setup-the-application-directory-apps}

存放庫中的/apps目錄包含的程式碼會實施從/content目錄提供的頁面的行為和轉譯。

/apps目錄受保護，不能公開訪問，/content和/etc/designs目錄亦然。

1. 建立 `/apps/an-scf-sandbox` 檔案夾。

   使用 **[!UICONTROL CRXDE Lite]**，在瀏覽器窗格中

   1. 選取 `/apps` 檔案夾。
   1. 按一下右鍵 **[!UICONTROL 建立]**...或下拉 **[!UICONTROL 建立……]** 功能表。
   1. 選擇 **[!UICONTROL 建立資料夾……]**.
   1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入 `an-scf-sandbox`.
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 建立 **[!UICONTROL 元件]** 子資料夾。

   1. 選取 `/apps/an-scf-sandbox` 檔案夾。
   1. 按一下 **[!UICONTROL 建立>建立資料夾]**.
   1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入 **[!UICONTROL 元件]**.
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 建立 **[!UICONTROL 範本]** 子資料夾。

   1. 選取 `/apps/an-scf-sandbox` 檔案夾。
   1. 按一下 **[!UICONTROL 建立>建立資料夾]**.
   1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入 **[!UICONTROL 範本]**.
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。
   1. 重新選取 `/apps/an-scf-sandbox`.
   1. 選擇 **[!UICONTROL 全部儲存]**.

   和任何編輯程式一樣，經常儲存。 如果您在輸入資料時遇到問題，可能是因為您的登入逾時，或您需要儲存先前的編輯內容。

1. CRXDE Lite的瀏覽器窗格中的結構現在應該如下所示：

   ![crxde-template](assets/crxde-template.png)

## 設定設計目錄(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs目錄包含要隨頁面內容一起下載的影像、指令碼和樣式表。

1. 若要在傳統UI中使用設計工具，請瀏覽至 [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   注意：如果您使用CRXDE Lite建立類型的節點 `cq:Page`，則「存取控制」和「復寫」不會設為頁面的預設設定。

1. 在瀏覽器窗格中，選取 **[!UICONTROL 設計]** ，然後按一下 **[!UICONTROL 新增]** > **[!UICONTROL 新頁面]**.

   輸入：

   * 標題： **[!UICONTROL SCF沙箱]**
   * 名稱： **[!UICONTROL an-scf — 沙箱]**
   * 選擇 **[!UICONTROL 設計頁面範本]**

   按一下&#x200B;**[!UICONTROL 建立]**。

   ![設計範本](assets/design-template.png)

1. 如果未顯示「SCF沙箱」資料夾，請刷新瀏覽器窗格。

1. 返回CRXDE Lite(http://localhost:4502/crx/de)，然後展開/etc/designs以查看名為「an-scf-sandbox」的節點。

   在CRXDE的右下窗格中，您可以查看「屬性」頁簽、「訪問控制」頁簽和「複製」頁簽，以查看使用「設計頁模板」定義的內容。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## 設定內容目錄(/content) {#setup-the-content-directory-content}

儲存庫中的/content目錄是網站內容所在的位置。 /content下的路徑包含瀏覽器要求的URL路徑。

*之後* the [頁面範本](initial-app.md#createthepagetemplate) 是作為初始應用程式的一部分建立的，可以根據模板建立初始頁面內容……. [**⇒**](initial-app.md)
