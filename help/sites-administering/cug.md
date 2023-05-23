---
title: 建立關閉的用戶組
seo-title: Creating a Closed User Group
description: 瞭解如何建立已關閉的用戶組。
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 64d174cc824c8bf200cece4e29f60f946ee5560e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# 建立關閉的用戶組{#creating-a-closed-user-group}

關閉的用戶組(CUG)用於限制對駐留在已發佈網際網路站點中的特定頁面的訪問。 此類頁面要求分配的成員登錄並提供安全憑據。

要在網站中配置此區域，請執行以下操作：

* [建立實際關閉的用戶組並分配成員](#creating-the-user-group-to-be-used)。

* [將此組應用於所需頁](#applying-your-closed-user-group-to-content-pages) 選擇（或建立）登錄頁供CUG成員使用；在將CUG應用於內容頁面時指定。

* [建立到受保護區域內至少一個頁面的連結（某種形式的）](#linking-to-the-cug-pages)，否則它將不可見。

* [配置Dispatcher](#configure-dispatcher-for-cugs) 的下界。

>[!CAUTION]
>
>應始終在建立封閉用戶組時考慮效能。
>
>雖然CUG中的用戶和組數不受限制，但頁面上的大量CUG可能會降低呈現效能。
>
>在進行效能測試時，應始終考慮CUG的影響。

## 建立要使用的用戶組 {#creating-the-user-group-to-be-used}

要建立關閉的用戶組：

1. 轉到 **工具 — 安全性** 從自AEM殺中。

   >[!NOTE]
   >
   >請參閱 [管理用戶和組](/help/sites-administering/security.md#managing-users-and-groups) 的子菜單。

1. 選擇 **組** 下一螢幕的卡。

   ![screpton_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按 **建立** 的子菜單。
1. 將新組命名為：比如說， `cug_access`。

   ![screpton_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 轉到 **成員** 頁籤，並將所需用戶分配到此組。

   ![screpton_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配給CUG的所有用戶；在本例中，所有 `cug_access`。
1. 激活關閉的用戶組，使其在發佈環境中可用；在本例中， `cug_access`。

## 將關閉的用戶組應用於內容頁 {#applying-your-closed-user-group-to-content-pages}

要將CUG應用於頁面或頁面，請執行以下操作：

1. 導航到要分配給CUG的受限部分的根頁。
1. 通過按一下其縮略圖，然後選擇 **屬性** 的子菜單。

   ![screpton_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，開啟 **高級** 頁籤。

1. 向下滾動到 **身份驗證要求** 的子菜單。

   1. 激活 **啟用** 按鈕。

   1. 將路徑添加到 **登錄頁**。
這是可選的，如果留空，則將使用標準登錄頁。

   ![已添加CUG](assets/cug-authentication-requirement.png)

1. 下一步，轉到 **權限** 頁籤 **編輯關閉的用戶組**。

   ![screpton_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >無法從「權限」頁籤中的CUG展開到「藍圖中的即時副本」。 配置Live Copy時，請圍繞此進行規劃。
   >
   >有關詳細資訊，請參見 [此頁](closed-user-groups.md#aem-livecopy)。

1. 的 **編輯關閉的用戶組** 對話框。 在此，您可以搜索並選擇CUG，然後使用 **保存**。

   該組將被添加到清單中；例如，組 **cug_access**。

   ![已添加CUG](assets/cug-added.png)

1. 確認更改 **保存並關閉**。

>[!NOTE]
>
>請參閱 [Identity Management](/help/sites-administering/identity-management.md) 有關發佈環境中配置檔案的資訊，並提供用於登錄和註銷的表單。

## 連結到CUG頁 {#linking-to-the-cug-pages}

由於匿名用戶不能看到指向CUG頁的任何連結的目標，連結檢查器將刪除這些連結。

為避免這種情況，建議建立指向CUG區域內頁面的非受保護重定向頁面。 然後，在不引起連結檢查器任何問題的情況下呈現導航條目。 僅當實際訪問重定向頁面時，用戶才會在CUG區域內重定向 — 成功提供其登錄憑據後。

## 配置CUG的Dispatcher {#configure-dispatcher-for-cugs}

如果使用Dispatcher，則需要定義具有以下屬性的Dispatcher場：

* [虛擬主機](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts):與CUG所應用的頁面的路徑匹配。
* \sessionmanagement（會話管理）參見下面。
* [快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache):專用於CUG所應用檔案的快取目錄。

### 為CUG配置Dispatcher會話管理 {#configuring-dispatcher-session-management-for-cugs}

配置 [dispatcher.any檔案中的會話管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) CUG 請求訪問CUG頁時使用的身份驗證處理程式決定了如何配置會話管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher場啟用了會話管理時，該場處理的所有頁都不會快取。 要快取CUG之外的頁，請在dispatcher.any中建立第二個場
>處理非CUG頁面。

1. 配置 [/會話管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 通過定義 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 設定 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) 至 `0`。
