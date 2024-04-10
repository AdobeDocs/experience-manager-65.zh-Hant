---
title: 建立已關閉的使用者群組
description: 瞭解如何建立「已關閉的使用者群組」。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 建立已關閉的使用者群組{#creating-a-closed-user-group}

封閉式使用者群組(CUG)可用來限制對已發佈網際網路網站中特定頁面的存取。 這類頁面需要指派的成員登入並提供安全性認證。

若要在網站中設定這類區域，請：

* [建立實際的已關閉使用者群組並指派成員](#creating-the-user-group-to-be-used).

* [將此群組套用至所需頁面](#applying-your-closed-user-group-to-content-pages) 並選取（或建立）登入頁面，以供CUG的成員使用；也會在將CUG套用至內容頁面時指定。

* [建立連結，連結（以某種形式連結）到受保護區域內至少一個頁面](#linking-to-the-cug-pages)，否則不會顯示。

* [設定Dispatcher](#configure-dispatcher-for-cugs) 若正在使用中。

>[!CAUTION]
>
>建立封閉式使用者群組(CUG)時，一律應考量效能。
>
>雖然CUG中的使用者和群組數量並沒有限制，但單一頁面上大量的CUG可能會降低轉譯效能。
>
>進行效能測試時，應一律考慮CUG的影響。

## 建立要使用的使用者群組 {#creating-the-user-group-to-be-used}

若要建立已關閉的使用者群組：

1. 前往 **工具 — 安全性** 從AEM homescreen取得。

   >[!NOTE]
   >
   >另請參閱 [管理使用者和群組](/help/sites-administering/security.md#managing-users-and-groups) 以取得建立和設定使用者和群組的完整資訊。

1. 選取 **群組** 卡片。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按下 **建立** 按鈕來建立群組。
1. 為新的群組命名，例如， `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 前往 **成員** 標籤並將所需的使用者指派給此群組。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 啟動您已指派給您的CUG的任何使用者；在此案例中，是 `cug_access`.
1. 啟動已關閉的使用者群組，使其可在發佈環境中使用；在此範例中， `cug_access`.

## 將封閉使用者群組套用至內容頁面 {#applying-your-closed-user-group-to-content-pages}

若要將CUG套用至一或多個頁面：

1. 導覽至您要指派給CUG之受限制區段的根頁面。
1. 按一下頁面的縮圖並選取「 」，以選取頁面 **屬性** 在頂端工具列中。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在下列視窗中，開啟 **進階** 標籤。

1. 向下捲動至 **驗證需求** 區段。

   1. 啟動 **啟用** 勾選方塊。

   1. 將路徑新增至 **登入頁面**.
這是選用專案，如果保留為空白，系統會使用標準登入頁面。

   ![已新增CUG](assets/cug-authentication-requirement.png)

1. 接下來，前往 **許可權** 標籤並選取 **編輯已關閉的使用者群組**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >許可權索引標籤中的CUG無法從Blueprint轉出至即時副本。 設定即時副本時，請對此進行規劃。
   >
   >如需詳細資訊，請參閱 [此頁面](closed-user-groups.md#aem-livecopy).

1. 此 **編輯已關閉的使用者群組** 對話方塊開啟。 您可以在此處搜尋並選取您的CUG，然後確認群組選取專案 **儲存**.

   群組將新增至清單中；例如，群組 **cug_access**.

   ![已新增CUG](assets/cug-added.png)

1. 透過確認變更 **儲存並關閉**.

>[!NOTE]
>
>另請參閱 [Identity Management](/help/sites-administering/identity-management.md) 以取得發佈環境中設定檔的相關資訊，以及登入和登出的表單相關資訊。

## 連結至CUG頁面 {#linking-to-the-cug-pages}

由於匿名使用者看不到任何CUG頁面連結的目標，因此連結檢查器會移除這類連結。

若要避免此問題，建議您建立指向CUG區域中頁面的非受保護重新導向頁面。 然後轉譯導覽專案，而不會導致連結檢查器發生任何問題。 只有在實際存取重新導向頁面時，才會在CUG區域將使用者重新導向 — 在成功提供其登入憑證後。

## 為CUG設定Dispatcher {#configure-dispatcher-for-cugs}

如果您使用Dispatcher，則需要使用以下屬性定義Dispatcher陣列：

* [虛擬主機](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)：比對CUG套用至的頁面路徑。
* \sessionmanagement：請參閱下文。
* [快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)：專屬於CUG套用之檔案的快取目錄。

### 設定CUG的Dispatcher工作階段管理 {#configuring-dispatcher-session-management-for-cugs}

設定 [dispatcher.any檔案中的工作階段管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 用於CUG。 要求CUG頁面的存取權時所使用的驗證處理常式，會決定您設定工作階段管理的方式。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher陣列啟用工作階段管理時，不會快取陣列處理的所有頁面。 若要快取CUG以外的頁面，請在dispatcher.any中建立第二個陣列
>處理非CUG頁面的即時通訊協定。

1. 設定 [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 透過定義 `/directory`；例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 設定 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#caching-when-authentication-is-used) 至 `0`.
