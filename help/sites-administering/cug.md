---
title: 建立已關閉的使用者群組
seo-title: 建立已關閉的使用者群組
description: 瞭解如何建立已關閉的使用者群組。
seo-description: 瞭解如何建立已關閉的使用者群組。
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c

---


# 建立已關閉的使用者群組{#creating-a-closed-user-group}

已關閉的使用者群組(CUG)可用來限制對已發佈網際網路網站中特定頁面的存取。 這些頁面需要指派的成員登入並提供安全憑證。

若要在您的網站中設定此區域，請：

* [建立實際關閉的用戶組並分配成員](#creating-the-user-group-to-be-used)。

* [將此群組套用至所需頁面](#applying-your-closed-user-group-to-content-pages) ，並選取（或建立）登入頁面供CUG成員使用；也會在套用CUG至內容頁面時指定。

* [建立連結，以某種形式連結至保護區內的至少一個頁面](#linking-to-the-realm)，否則將無法顯示。
* [配置Dispatcher](#configure-dispatcher-for-cugs) （如果正在使用）。

>[!CAUTION]
>
>在建立封閉使用者群組時，一律應考量效能。
>
>雖然CUG中的使用者和群組數目不受限制，但頁面上的大量CUG可能會降低演算效能。
>
>執行效能測試時，應始終考慮CUG的影響。

## 建立要使用的使用者群組 {#creating-the-user-group-to-be-used}

要建立已關閉的用戶組，請執行以下操作：

1. 前往「工 **具——來自AEM** 在家螢幕的安全性」。

   >[!NOTE]
   >
   >如需 [建立和設定使用者和群組的完整資訊](/help/sites-administering/security.md#managing-users-and-groups) ，請參閱管理使用者和群組。

1. 從下一 **個畫面** ，選取「群組」卡片。

   ![screenshop_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右上 **角的** 「建立」按鈕，以建立新群組。
1. 命名新群組；例如， `cug_access`。

   ![screenshop_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 前往「成 **員** 」標籤，並指派必要的使用者至此群組。

   ![screenshop_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 啟動您指派給CUG的任何使用者；在本例中，所有成員 `cug_access`。
1. 啟動關閉的使用者群組，以便在發佈環境中使用；在此示例中，為 `cug_access`。

## 將已關閉的使用者群組套用至內容頁面 {#applying-your-closed-user-group-to-content-pages}

要將CUG應用於頁面：

1. 導覽至您要指派給CUG之受限制區段的根頁面。
1. 按一下頁面的縮圖，然後按一下頂端面 **板中的** 「屬性」，以選取頁面。

   ![screenshop_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，轉至「高 **級** 」頁籤。
1. 向下捲動並啟用「驗證要求」區 **段中的選** 項框。

1. 在下面添加配置路徑，然後按保存。
1. 接著，前往「權限」 **標籤** ，然後按「編 **輯已關閉的使用者群組」按鈕** 。

   ![screenshop_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[注意!]
   >
   > 請注意，「權限」標籤中的CUG無法從「藍圖」回滾到「即時副本」。 設定即時副本時，請針對此進行規劃。
   >
   > 如需詳細資訊，請參 [閱本頁](closed-user-groups.md#aem-livecopy)。

1. 在以下窗口中查找並添加CUG —— 在本例中添加名為 **cug_access的組**。 最後，按「 **儲存」**。
1. 按一 **下「啟用** 」以定義此頁面（及任何子頁面）屬於CUG。
1. 指定 **群組成員** 將使用的登入頁面；例如：

   `/content/geometrixx/en/toolbar/login.html`

   如果保留為空白，則使用標準登入頁面。

1. 新增已接 **納的群組**。 使用+可新增群組或——可移除。 僅允許這些群組的成員登入並存取頁面。
1. 指定 **領域** （頁面群組的名稱）（如有需要）。 留空將使用頁面標題。
1. 按一下 **確定** ，保存規範。

如需 [發佈環境中的設定檔](/help/sites-administering/identity-management.md) ，以及提供登入和登出表單的相關資訊，請參閱身分管理。

## 連結至領域 {#linking-to-the-realm}

由於匿名使用者看不到任何CUG領域連結的目標，所以連結檢查程式會移除這些連結。

為避免此問題，建議您建立指向「CUG領域」內頁面的未受保護重新導向頁面。 然後，在不引起連結檢查器任何問題的情況下呈現導航條目。 只有在實際存取重新導向頁面時，使用者才會在CUG領域內重新導向——成功提供其登入認證後。

## 配置CUG的Dispatcher {#configure-dispatcher-for-cugs}

如果您使用Dispatcher，則需要定義具有以下屬性的Dispatcher群：

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts):與CUG所套用之頁面的路徑相符。
* \sessionmanagement:請參閱以下內容。
* [快取](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):專用於CUG所應用檔案的快取目錄。

### 為CUG配置Dispatcher會話管理 {#configuring-dispatcher-session-management-for-cugs}

在 [dispatcher.any檔案中為CUG配置會話管理](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 。 在CUG頁面要求存取時使用的驗證處理常式，會決定您如何設定工作階段管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher群啟用會話管理時，群處理的所有頁面都不會進行快取。 若要快取CUG以外的頁面，請在dispatcher.any中建立第二個群
>處理非CUG頁面。

1. 通過定 [義配置／會話](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 管理 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 將 [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) 設定為 `0`。

