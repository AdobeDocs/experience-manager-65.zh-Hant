---
title: 部落格功能
seo-title: Blog Feature
description: 日誌格式的社區資訊
seo-description: Community information in a journaling format
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 6%

---

# 部落格功能 {#blog-feature}

## 簡介 {#introduction}

AEM Communities的部落格功能已從創作活動轉變為在發佈環境中進行的真正社區活動。

部落格功能支援以日誌格式提供社區資訊。 部落格條目由授權成員（註冊、登錄用戶）在發佈環境中建立。

部落格功能提供：

* 部落格和評論的發佈端建立
* 富格文本編輯
* 內嵌影像（支援拖放）
* 嵌入式社交網路內容([嵌入支援](/help/communities/blog-developer-basics.md#allowing-rich-media))
* 繪製模式
* 計畫發佈
* 代表撰寫(a [特權成員](/help/communities/users.md#privileged-members-group) 可以代表不同的社區成員建立內容)
* [上下文和批量審核](/help/communities/moderate-ugc.md) 部落格和評論

文檔的本節介紹：

* 將部落格功能添加到網AEM站
* 部落格元件的配置設定

>[!NOTE]
>
>元件 `Journal` 和 `Journal Sidebar` 標題 `Blog` 和 `Blog Sidebar`。
>
>在6.0和早期版本AEM中找到的部落格功能現在已刪除。 它基於模板，只允許作者在作者環境中建立內容。

## 將部落格元件添加到頁面 {#adding-blog-components-to-a-page}

如果希望在作者模式下將部落格添加到頁面，請使用元件瀏覽器查找

* `Communities / Blog`
* `Communities / Blog Sidebar`

將它們拖到部落格應出現的頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

當 [所需的客戶端庫](/help/communities/blog-developer-basics.md#essentials-for-client-side) 包括，這是 `Blog` 元件將出現：

![Add-Blog元件](assets/add-blog-component.png)

### 配置部落格 {#configuring-blog}

選取已放置的 `Blog` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

![部落格設定](assets/blog-configure.png)

#### 「設定」頁籤 {#settings-tab}

在 **設定** 頁籤，指定部落格的基本功能：

* **允許附件縮圖**

   如果選中，則建立附加影像的縮覽圖。

* **附加縮圖最大尺寸**

   附件縮略圖影像的最大大小（以像素為單位）。 預設值為800 x 800。

* **最小縮圖影像大小**

   用於為內聯影像生成縮略圖的影像的最小大小（以位元組為單位）。 預設值為100000位元組(100kb)。

* **最大縮圖尺寸**

   內聯影像縮略圖的最大大小（以像素為單位）。 預設值為800 x 800。

* **允許有特殊權限的成員**

   如果選中，則僅允許特權成員建立內容。

* **允許擁有特殊權限的成員**

   添加允許建立內容的特權成員。

* **封鎖使用者在作者編輯模式中產生的內容**

   如果啟用，則在作者模式下編輯時阻止用戶生成的內容。

* **日誌標題**

   要在頁面上顯示的部落格標題。

>[!NOTE]
>
>日誌標題用於自動建立部落格的URL。
>
>您在此處指定的日誌標題中最多使用50個字元（唯一性附加5個字元）來為日誌建立URL。

* **日誌說明**

   部落格描述。

* **每頁主題**

   定義每頁顯示的部落格條目/注釋數。 預設值為10。

* **已審核**

   如果選中，則必須批准發佈部落格條目和評論，然後才能將它們顯示在發佈的網站上。 未選中預設值。

* **已關閉**

   如果選中，則將關閉日誌以查看新日誌和評論。 未選中預設值。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入部落格條目和注釋。 選中預設值。

* **允許標記**

   如果選中，允許成員將標籤標籤添加到其帖子(請參見 **標籤欄位** )的正平方根。 未選中預設值。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到部落格條目或注釋中。 未選中預設值。

* **最大檔案大小**

   僅在 `Allow File Uploads` 的子菜單。 此欄位將限制上載檔案的大小（以位元組為單位）。 預設為104857600(10 Mb)。

* **允許的檔案類型**

   僅在 `Allow File Uploads` 的子菜單。 以逗號分隔的檔案副檔名清單，其中帶有「點」分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許上載未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅當選中「允許檔案上載」時相關。 上載的影像檔案可能具有的最大位元組數。 預設為2097152(2 Mb)。

* **允許答復**

   如果選中，則允許對發佈到部落格條目的注釋作出答復。 未選中預設值。

* **允許投票**

   如果選中，則將「投票」功能與部落格條目一起包含。 未選中預設值。

* **允許使用者刪除評論和主題**

   如果選中，則允許成員刪除他們發佈的注釋和部落格條目。 未選中預設值。

* **允許關注**

   如果選中，則為部落格包括以下功能，允許成員 [通知](/help/communities/notifications.md) 新職位。 未選中預設值。

* **允許電子郵件訂閱**

   如果選中，則允許通過電子郵件通知成員新帖子([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 要檢查和 [電子郵件配置](/help/communities/email.md)。 未選中預設值。

* **顯示徽章**

   如果選中，則顯示已獲得和已分配 [徽章](/help/communities/implementing-scoring.md) 的日誌。 未選中預設值。

* **不在清單頁面上取得回覆**

* **允許主要內容**

   如果選中，該思想可被識別為 [特色內容](/help/communities/featured.md)。 未選中預設值。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他已註冊成員（使用名、姓、用戶名），並使用公用@user-name語法標籤他們。 標籤用戶收到有關其提及的通知。

* **最大提及數**

   限制帖子中允許的最大提及數。 預設值為10。

* **UI 提及模式**

   指定帖子中註冊用戶的標籤(@mention)所允許的模式字串。 例如~{{familyName}}{{givenName}}。

#### 「用戶審核」頁籤 {#user-moderation-tab}

在 **用戶審核** 頁籤，指定審核設定：

* **拒絕帖子**

   如果選中，則允許受信任的成員審核人拒絕帖子並阻止帖子出現在公共論壇中。 未選中預設值。

* **關閉/重新開啟主題**

   如果選中，受信任的成員審閱人可以關閉主題以進一步編輯和注釋，也可以重新開啟主題。 未選中預設值。

* **標誌帖子**

   如果選中，允許成員將其他主題或注釋標籤為不恰當。 未選中預設值。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇將主題或注釋標籤為不適當的原因。 未選中預設值。

* **自定義標誌原因**

   如果選中，允許成員輸入將主題或注釋標籤為不適當的自己原因。 未選中預設值。

* **審核閾值**

   輸入在通知審閱人之前必須由成員標籤主題或評論的次數。 預設值為1（一次）。

* **標籤限制**

   輸入主題或注釋在隱藏於公共視圖之前必須標籤的次數。 如果設定為–1，則標籤的主題或注釋永遠不會隱藏在公共視圖中。 否則，此數字必須大於或等於「審核閾值」。 預設值為5。

#### 「標籤」欄位頁籤 {#tag-field-tab}

在 **標籤欄位** 頁籤，指定在 **允許標籤** 檢查 **設定** 頁籤：

* **允許的命名空間**

   相關(如果 `Allow Tagging` 在 **設定** 頁籤。 可應用的標籤僅限於所檢查的命名空間類別中的標籤。 命名空間清單包括「標準標籤」（預設命名空間）和「包括所有標籤」。 預設值未選中，這意味著允許所有命名空間。

* **建議限制**

   輸入要作為對論壇成員過帳的建議顯示的標籤數。 值–1表示無限制。 預設值為0。

### 配置部落格提要欄 {#configuring-blog-sidebar}

按兩下 `Blog Sidebar` 元件，將開啟編輯對話框。

在 **日誌提要欄設定** 頁籤，指定存檔的日期格式以及要在邊欄中顯示的條目類型：

![部落格元件邊欄](assets/blog-component-sidebar.png)

* **日期格式**

   用於顯示部落格條目存檔的格式。 格式使用遵循Java約定的佔位符。

   * yyyy :全年，比如2015年
   * yy :短年，比如15
   * MMMMMM:整個月，就像6月
   * 嗯：短月，像君
   * 毫米：月號，大約06

   預設值為&quot;yyyy MMMM&quot;，將顯示例如&quot;2015 June&quot;

* **視圖類型**

   要顯示在提要欄中的部落格條目的標題和類型。 選擇是

   * 作者
   * 類別
   * 封存

* **Blopg元件路徑**

   *（可選）* 要從中列出部落格的部落格資源的位置。 如果留空，將使用resourceType的元件 `social/journal/components/hbs/journal` 顯示在同一頁。

   * 例如 `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **建議限制**

   要顯示的部落格數。 值–1表示無限制。 預設值為–1。

## 站點訪問者體驗 {#site-visitor-experience}

在發佈環境中，部落格功能將顯示最新的部落格，然後按照建立的降序顯示較舊的部落格。 部落格側欄允許站點訪問者應用篩選器以限制所顯示的部落格的選擇。

在部落格後面添加一個連結以發佈或查看評論。

選擇部落格後，將顯示部落格和注釋（如果已啟用）。

其他能力取決於站點訪問者是版主、管理員、社區成員、特權成員還是匿名。

### 使用文章 {#working-with-articles}

建立新部落格時，可以選擇：

1. 立即發佈
1. 發佈草稿
1. 在計畫日期和時間發佈

部落格將出現在相應的頁籤（「已發佈」、「草稿」或「已計畫」）下，顯示給能夠在發佈時建立作者的成員。

#### 審閱人和管理員 {#moderators-and-administrators}

當登錄用戶具有版主或管理員權限時，他們能夠執行 [緩和任務](/help/communities/moderate-ugc.md) （元件配置允許）發佈到部落格上的所有部落格和評論。

![版首頁](assets/moderator-homepage.png)

#### 成員 {#members}

當登錄用戶是社區成員或 [特權成員](/help/communities/users.md#privileged-members-group) （視配置而定），他們可以選擇 `New Article` 建立並發佈新部落格。

具體而言，它們可：

* 建立新部落格
* 代表其他成員發佈新部落格
* 將注釋發佈到部落格
* 編輯自己的部落格或評論
* 刪除其自己的部落格或評論
* 標籤其他部落格或評論

![成員首頁](assets/member-homepage.png)

![建立部落格](assets/create-blog.png)

#### 匿名 {#anonymous}

未登錄的網站訪問者只能閱讀已發佈的部落格和評論，如果支援，可以翻譯，但不得添加部落格或評論，不得標籤他人的文章或評論。

![匿名用戶視圖](assets/anonymous-user-view.png)

## 其他資訊 {#additional-information}

有關 [部落格要點](/help/communities/blog-developer-basics.md) 頁面。

有關審核部落格條目和評論，請參閱 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

有關為日誌條目和注釋添加標籤，請參見 [標籤用戶生成的內容](/help/communities/tag-ugc.md)。

有關部落格條目和注釋的翻譯，請參見 [翻譯用戶生成的內容](/help/communities/translate-ugc.md)。
