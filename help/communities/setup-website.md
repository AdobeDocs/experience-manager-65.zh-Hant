---
title: 設定網站結構
description: 瞭解如何設定您的網站結構，包括要建立的資料夾。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 設定網站結構 {#setup-website-structure}

若要設定您的網站，以下指示說明要在下列位置建立的資料夾：

* `/apps/an-scf-sandbox`

  這是自訂應用程式和範本所在的位置。

* `/etc/designs/an-scf-sandbox`

  這是可下載設計元素的所在位置。

* `/content/an-scf-sandbox`

  這是可下載網頁的所在位置。

本教學課程中的程式碼取決於應用程式、設計和內容的主要資料夾名稱是否相同。 如果您為網站選擇其他名稱，請一律將`an-scf-sandbox`取代為您選擇的名稱。

>[!NOTE]
>
>關於名稱：
>
>* 在CRXDE中看到的名稱是節點名稱，構成可定址內容的路徑。
>* 節點名稱可以包含空格，但在URI中使用時，空格必須編碼為&#39;%20&#39;或&#39;+&#39;。
>* 節點名稱可能包含連字型大小和底線，但若在Java™檔案中作為套件名稱參照，則必須加以編碼。 連字型大小和底線都會以底線逸出，後面跟著其Unicode值：
>
>   * 連字型大小會變成&#39;_002d&#39;
>   * 底線會變成&#39;_005f&#39;

## 設定應用程式目錄(/apps) {#setup-the-application-directory-apps}

存放庫中的/apps目錄包含程式碼，用於實作行為和呈現從/content目錄提供的頁面。

/apps目錄受到保護且無法與/content和/etc/designs目錄一樣公開存取。

1. 建立`/apps/an-scf-sandbox`資料夾。

   在總管窗格中使用&#x200B;**[!UICONTROL CRXDE Lite]**

   1. 選取`/apps`資料夾。
   1. 用滑鼠右鍵按一下&#x200B;**[!UICONTROL 建立]**...，或下拉式&#x200B;**[!UICONTROL 建立……]**&#x200B;功能表。
   1. 選取&#x200B;**[!UICONTROL 建立資料夾……]**。
   1. 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中，輸入`an-scf-sandbox`。
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 建立&#x200B;**[!UICONTROL 元件]**&#x200B;子資料夾。

   1. 選取`/apps/an-scf-sandbox`資料夾。
   1. 按一下&#x200B;**[!UICONTROL 建立>建立資料夾]**。
   1. 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中，輸入&#x200B;**[!UICONTROL 元件]**。
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 建立&#x200B;**[!UICONTROL 範本]**&#x200B;子資料夾。

   1. 選取`/apps/an-scf-sandbox`資料夾。
   1. 按一下&#x200B;**[!UICONTROL 建立>建立資料夾]**。
   1. 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中，輸入&#x200B;**[!UICONTROL 範本]**。
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。
   1. 重新選取`/apps/an-scf-sandbox`。
   1. 選取&#x200B;**[!UICONTROL 全部儲存]**。

   和任何編輯程式一樣，您應該經常儲存。 如果您在輸入資料時遇到問題，可能是因為您的登入已逾時，或您必須儲存先前的編輯。

1. CRXDE Lite總管窗格中的結構現在看起來應該像這樣：

   ![crxde-template](assets/crxde-template.png)

## 設定設計目錄(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs目錄包含要連同頁面內容一起下載的影像、指令碼和樣式表。

1. 若要在傳統UI中使用Designer工具，請瀏覽至[https://&lt;server>：&lt;port>/miscadmin](http://localhost:4502/miscadmin)。

   注意：如果您使用CRXDE Lite來建立型別`cq:Page`的節點，存取控制和復寫將不會設定為頁面的預設設定。

1. 在總管窗格中，選取&#x200B;**[!UICONTROL 設計]**&#x200B;資料夾，然後按一下&#x200B;**[!UICONTROL 新增]** > **[!UICONTROL 新增頁面]**。

   輸入：

   * 標題： **[!UICONTROL SCF沙箱]**
   * 名稱： **[!UICONTROL an-scf-sandbox]**
   * 選取&#x200B;**[!UICONTROL 設計頁面範本]**

   按一下&#x200B;**[!UICONTROL 建立]**。

   ![設計範本](assets/design-template.png)

1. 如果「SCF沙箱」資料夾未出現，請重新整理瀏覽器窗格。

1. 返回CRXDE Lite(http:// localhost：4502/crx/de)並展開/etc/designs以檢視名為「an-scf-sandbox」的節點。

   在CRXDE右下方的窗格中，您可以檢視「屬性」標籤、「存取控制」標籤和「復寫」標籤，以檢視使用「設計頁面範本」定義的內容。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## 設定內容目錄(/content) {#setup-the-content-directory-content}

存放庫中的/content目錄是網站內容所在的位置。 /content底下的路徑包含瀏覽器請求的URL路徑。

*在*&#x200B;建立[頁面範本](initial-app.md#createthepagetemplate)作為初始應用程式的一部分之後，可以根據範本建立初始頁面內容.... [**⇒**](initial-app.md)
