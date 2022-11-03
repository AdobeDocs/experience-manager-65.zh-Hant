---
title: 建立封閉的使用者群組
seo-title: Creating a Closed User Group
description: 了解如何建立封閉使用者群組。
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

# 建立封閉的使用者群組{#creating-a-closed-user-group}

封閉使用者群組(CUG)可用來限制對已發佈網際網路網站中特定頁面的存取。 這些頁面需要指派的成員來登入並提供安全憑證。

若要在網站內設定此類區域，請：

* [建立實際關閉的用戶組並分配成員](#creating-the-user-group-to-be-used).

* [將此群組套用至必要頁面](#applying-your-closed-user-group-to-content-pages) 並選擇（或建立）登錄頁供CUG成員使用；也會在將CUG套用至內容頁面時指定。

* [建立某種形式的連結，到受保護區域內的至少一個頁面](#linking-to-the-cug-pages)，否則將無法顯示。

* [設定Dispatcher](#configure-dispatcher-for-cugs) 若使用中。

>[!CAUTION]
>
>應一律以效能建立封閉使用者群組(CUG)。
>
>雖然CUG中的使用者和群組數目並不受限，但頁面上的大量CUG可能會降低呈現效能。
>
>執行效能測試時，應一律考慮CUG的影響。

## 建立要使用的使用者群組 {#creating-the-user-group-to-be-used}

要建立封閉用戶組，請執行以下操作：

1. 前往 **工具 — 安全性** 從AEM主畫面。

   >[!NOTE]
   >
   >請參閱 [管理使用者和群組](/help/sites-administering/security.md#managing-users-and-groups) 以取得建立和設定使用者和群組的完整資訊。

1. 選取 **群組** 下一個畫面的資訊卡。

   ![螢幕截圖_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按下 **建立** 按鈕，以建立新群組。
1. 為新組命名；例如， `cug_access`.

   ![螢幕截圖_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 前往 **成員** 索引標籤，並將必要的使用者指派至此群組。

   ![螢幕截圖_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您指派給CUG的任何使用者；在本例中， `cug_access`.
1. 啟動封閉的使用者群組，以便在發佈環境中使用；在本例中， `cug_access`.

## 將封閉的使用者群組套用至內容頁面 {#applying-your-closed-user-group-to-content-pages}

若要將CUG套用至頁面或頁面：

1. 導覽至您要指派給CUG之限制區段的根頁面。
1. 按一下頁面縮圖並選取，以選取頁面 **屬性** 的下一頁。

   ![螢幕截圖_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在下列視窗中，開啟 **進階** 標籤。

1. 向下捲動至 **驗證需求** 區段。

   1. 啟動 **啟用** tickbox。

   1. 將路徑新增至 **登入頁面**.
若將保留為空白，系統會使用標準登入頁面，此為選用項目。

   ![新增CUG](assets/cug-authentication-requirement.png)

1. 接下來，前往 **權限** 索引標籤和選取 **編輯已關閉的用戶組**.

   ![螢幕截圖_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >「權限」頁簽中的CUG無法從Blueprint轉出到Live Copy。 設定Live Copy時，請針對此進行規劃。
   >
   >如需詳細資訊，請參閱 [本頁](closed-user-groups.md#aem-livecopy).

1. 此 **編輯已關閉的用戶組** 對話框將開啟。 您可以在此搜尋並選取您的CUG，然後使用確認群組選取項目 **儲存**.

   該組將被添加到清單中；例如，群組 **cug_access**.

   ![新增CUG](assets/cug-added.png)

1. 使用確認變更 **儲存並關閉**.

>[!NOTE]
>
>請參閱 [Identity Management](/help/sites-administering/identity-management.md) 以取得發佈環境中的設定檔以及提供登入和登出表單的相關資訊。

## 連結至CUG頁面 {#linking-to-the-cug-pages}

由於匿名用戶看不到指向CUG頁面的任何連結的目標，因此連結檢查器將刪除此類連結。

若要避免此問題，建議您建立未受保護的重新導向頁面，以指向CUG區域內的頁面。 然後，將呈現導航條目，而不會導致連結檢查器出現任何問題。 只有在實際存取重新導向頁面時，使用者才會在CUG區域內重新導向 — 成功提供登入憑證後。

## 為CUG設定Dispatcher {#configure-dispatcher-for-cugs}

如果您使用Dispatcher，則需要使用下列屬性來定義Dispatcher伺服器陣列：

* [虛擬主機](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts):匹配CUG應用的頁面路徑。
* \sessionmanagement:請參閱下方。
* [快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache):專用於CUG應用的檔案的快取目錄。

### 為CUG設定Dispatcher工作階段管理 {#configuring-dispatcher-session-management-for-cugs}

設定 [dispatcher.any檔案中的工作階段管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) CUG的。 為CUG頁面請求存取時使用的驗證處理常式，決定了如何設定工作階段管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher伺服器陣列已啟用工作階段管理時，系統不會快取伺服器陣列處理的所有頁面。 若要快取CUG以外的頁面，請在dispatcher.any中建立第二個伺服器陣列
>來處理非CUG頁面。

1. 設定 [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 定義 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 設定 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) to `0`.
