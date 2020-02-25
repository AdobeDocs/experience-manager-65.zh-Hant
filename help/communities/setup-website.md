---
title: 設定網站結構
seo-title: 設定網站結構
description: 設定目錄
seo-description: 設定目錄
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: 4f4f2897000a0afe26a0dbcc4514e20befdb4114

---


# 設定網站結構 {#setup-website-structure}

若要設定您的網站，下列指示說明要在下列位置建立的檔案夾：

* `/apps/an-scf-sandbox`
這是自訂應用程式和範本所在的位置

* `/etc/designs/an-scf-sandbox`
這是可下載設計元素所在的位置

* `/content/an-scf-sandbox`
這是可下載網頁的所在位置

本教學課程中的程式碼將依賴應用程式、設計和內容的主資料夾名稱相同。 如果您為網站選擇其他名稱，請一律以您 `an-scf-sandbox` 選擇的名稱取代。

>[!NOTE]
>
>關於名稱：
>
>* CRXDE中顯示的名稱是構成可定址內容路徑的節點名稱
>* 節點名稱可能包含空格，但在URI中使用時，空格必須編碼為&#39;%20&#39;或&#39;+&#39;
>* 節點名稱可能包含連字型大小和下划線，但是當它們被引用為Java檔案中的包名時，必須對其進行編碼。 連字型大小和下划線都會以下划線和其unicode值進行逸出：
>
>   * 連字型大小變為&#39;_002d&#39;
>   * 下划線變為&#39;_005f&#39;

## 設定應用程式目錄（/應用程式） {#setup-the-application-directory-apps}

儲存庫中的/apps目錄包含代碼，該代碼實現了從/content目錄提供的頁面的行為和呈現。

/apps目錄受到保護，無法像/content和/etc/designs目錄一樣公開存取。

1. Create `/apps/an-scf-sandbox` folder.

   使用 **[!UICONTROL CRXDE Lite]**，在檔案總管窗格中

   1. 選擇檔案 `/apps` 夾
   1. **[!UICONTROL 按一下右鍵]**&#x200B;建立&#x200B;**[!UICONTROL ...或下拉「建]**&#x200B;立」...菜單
   1. **[!UICONTROL 選擇]**&#x200B;建立資料夾…….
   1. 在「建立 **[!UICONTROL 資料夾]** 」對話框中，輸入 `an-scf-sandbox`
   1. 按一下「 **[!UICONTROL 確定」]**

1. 建立 **[!UICONTROL 元件]** 子資料夾。

   1. 選擇檔案 `/apps/an-scf-sandbox` 夾
   1. 按一下「 **[!UICONTROL 建立>建立資料夾」]**
   1. 在「建立 **[!UICONTROL 資料夾]** 」對話框中，輸 **[!UICONTROL 入]**
   1. 按一下「 **[!UICONTROL 確定」]**

1. 建立 **範本&#x200B;**子資料夾。

   1. 選擇檔案 `/apps/an-scf-sandbox` 夾
   1. 按一下「 **[!UICONTROL 建立>建立資料夾」]**
   1. 在「建立 **[!UICONTROL 資料夾]** 」對話框中，輸 **[!UICONTROL 入模板]**
   1. 按一下「 **[!UICONTROL 確定」]**
   1. 重新選取 `/apps/an-scf-sandbox`
   1. 選擇「 **[!UICONTROL 全部保存」]**
   和任何編輯程式一樣，經常節省成本。 如果您在輸入資料時遇到問題，可能是因為您的登入逾時，或是您需要儲存先前的編輯。

1. CRXDE Lite的瀏覽器窗格中的結構現在應該如下所示：

   ![chlimage_1-44](assets/chlimage_1-44.png)

## 設定設計目錄(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs目錄包含要與頁面內容一起下載的映像、指令碼和樣式表。

1. 若要在Classic UI中使用設計工具，請瀏 [覽至https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin)。

   注意：如果使用CRXDE Lite建立類型的節點 `cq:Page`，則Access Control和Replication不會設定為頁面的預設設定。

1. 在檔案總管窗格中，選取「 **[!UICONTROL Designs]** 」檔案夾，然後按 **[!UICONTROL 一下「新增>新頁面」]**。

   輸入：

   * 標題：SCF **沙盒**
   * 名稱： **an-scf-沙盒**
   * 選取 **設計頁面範本**
   Click **[!UICONTROL Create]**

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. 如果未顯示「SCF沙盒」資料夾，請刷新瀏覽器窗格。

1. 返回CRXDE Lite(http:// localhost:4502/crx/de)，然後展開/etc/designs以查看名為&quot;an-scf-sandbox&quot;的節點。

   在CRXDE的右下窗格中，您可以查看「屬性」頁籤、「訪問控制」頁籤和「複製」頁籤，以查看使用「設計頁模板」定義的內容。

   ![chlimage_1-46](assets/chlimage_1-46.png)

## 設定內容目錄（/內容） {#setup-the-content-directory-content}

儲存庫中的/content目錄是網站內容所在的位置。 /content下的路徑包含瀏覽器請求的URL路徑。

*在建立* 頁面範本 [](initial-app.md#createthepagetemplate) ，做為初始應用程式的一部分後，就可以根據範本建立初始頁面內容……. [**⇒**](initial-app.md)
