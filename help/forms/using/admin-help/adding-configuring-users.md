---
title: 添加和配置用戶
seo-title: Adding and configuring users
description: 管理控制台中的「用戶管理」設定允許您建立或刪除用戶以及配置其他用戶設定。
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# 添加和配置用戶 {#adding-and-configuring-users}

用戶和組資訊被維護在第三方儲存系統中，如LDAP目錄。 用戶管理不寫入第三方儲存系統。 相反，用戶管理會將用戶和組資訊與其自己的資料庫同步

## 建立用戶 {#create-a-user}

在建立用戶時，可以將用戶添加到組並為其分配角色。

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>用戶和組]**，然後按一下 **[!UICONTROL 新用戶]**。。
1. 下 **[!UICONTROL 常規設定]**，根據需要提供資訊，然後按一下 **[!UICONTROL 下一個]**。 有關設定的詳細資訊，請參閱 [用戶設定](adding-configuring-users.md#user-settings)。
1. （可選）要將用戶添加到組，請按一下 **[!UICONTROL 查找組]**，執行以下任務：

   * 在 **[!UICONTROL 查找]** 框中，鍵入組名稱的全部或部分。
   * 選擇要搜索的域，選擇要顯示的項數，然後按一下 **[!UICONTROL 查找]**。
   * （可選）要查看組詳細資訊，請選擇組名稱，然後按一下 **[!UICONTROL 確定]** 的子菜單。
   * 選中組的複選框，然後按一下 **[!UICONTROL 確定]**。
   * 按一下&#x200B;**[!UICONTROL 下一步]**。

1. （可選）要為用戶分配角色，請按一下 **[!UICONTROL 查找角色]**，選中要分配的角色的複選框，然後按一下 **[!UICONTROL 確定]**。
1. 按一下 **[!UICONTROL 完成]**。

   >[!NOTE]
   >
   >如果您遇到用戶的登錄問題，請參閱 [AEM FormsJEE用戶無法在OSGi端登錄AEM Forms](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html)。

## 用戶設定 {#user-settings}

在建立或編輯用戶時指定以下設定。

**規範名稱：** （必需）用戶的唯一標識符。 域中的每個用戶和組必須具有唯一的規範名稱。 選中「系統生成」複選框，讓用戶管理分配一個唯一值，或清除該複選框並為規範名稱指定自定義值。

避免在規範名稱中使用下划線字元(_)，例如， `sample_user`。 當您根據用戶的規範名稱搜索用戶時，不會返回包含下划線字元的用戶。

**名字：** （必需）用戶的指定名稱

**姓氏：** （必需）用戶的姓

**公用名：** 用戶的全名或顯示名。 例如，如果名字= Gloria，而姓氏= Rios，則公用名= Gloria Rios。

**電子郵件：** 用戶的電子郵件地址

**電話：** 用戶的電話號碼

**描述：** 可選說明。 使用此欄位以滿足您組織的需要。

**地址：** 用戶的郵件地址

**組織：** 用戶所屬的組織

**電子郵件別名：** 用戶的電子郵件別名。 用逗號分隔電子郵件別名。

**域：** 用戶所屬的域

**區域設定：** 用戶的ISO區域設定

**業務日曆密鑰：** 允許您根據此設定的值將業務日曆映射到用戶。 業務日曆定義業務日和非業務日。 在計AEM算提醒、截止日期和升級等事件的將來日期和時間時，表單可以使用業務日曆。 您為用戶分配業務日曆密鑰的方式取決於您是使用企業域、本地域還是混合域。 (請參閱 [添加域](/help/forms/using/admin-help/adding-domains.md#adding-domains)。)

如果使用本地域或混合域，則有關用戶的資訊僅儲存在用戶管理資料庫中。 對於這些用戶，將「業務日曆密鑰」設定為字串。 然後，在表單工作流中將業務日曆鍵（字串）映射到業務日曆。

如果使用的是企業域，則有關用戶的資訊將駐留在第三方儲存系統中，如LDAP目錄。 用戶管理將目錄中的用戶資訊與用戶管理資料庫同步。 此功能允許您將業務日曆鍵映射到LDAP目錄中的欄位。 例如，請考慮一個方案，其中目錄中的每個用戶記錄都包含一個國家/地區欄位，並且您要根據用戶所在的國家/地區分配業務日曆。 在這種情況下，將國家/地區欄位名稱指定為「業務日曆密鑰」設定的值。 然後，您可以將業務日曆鍵（為LDAP目錄中的國家/地區欄位定義的值）映射到表單工作流中的業務日曆。

有關業務日曆的附加資訊，包括如何將業務日曆鍵映射到業務日曆，請參閱 [配置業務日曆](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars)。

將名稱限制為少於53個字元。 名稱較短有助於防止在管理控制台的「流程管理」頁中顯示業務日曆鍵時出現問題。

**用戶ID:** （必需）用戶用於登錄的用戶ID。 用戶ID不區分大小寫，並且必須在整個域中唯一。

在企業域中，使用非DN屬性作為用戶ID，因為如果用戶的DN移到組織的其他部分，則其DN可以更改。 此設定取決於目錄伺服器。 值為 `objectGUID` 對於Active Directory 2003, `nsuniqueID` 用於Sun™ One和 `guid` 的子菜單。

確保用戶ID唯一。 不要使用分配給已刪除用戶的一個。

表AEM單無法區分具有相同用戶ID和密碼但屬於不同域的用戶帳戶。 要避免此問題，請不要在多個域上建立具有相同用戶ID的帳戶。

使用SQL Server作為資料庫時，無法建立超過255個字元的用戶ID。

使用MySQL時，用戶ID可以包含擴展字元。 但是，當在兩個字串（如abcde和abcdè）之間進行比較時，它們被視為相同。 例如，在同步時，如果將新用戶添加到資料庫，則會進行比較以檢查資料庫中是否存在具有相同用戶ID的用戶。 如果用戶 *禁用* 當新用戶 *布克德* 添加時，比較無法區分兩個名稱。 假定該用戶存在於資料庫中，並且新用戶被忽略且不被添加。

避免建立以數字元號(#)開頭的用戶名。 執行任務搜索不會返回這些用戶名的結果。 (請參閱 [處理任務](/help/forms/using/admin-help/tasks.md#working-with-tasks)。)

**密碼和確認密碼：** 用戶用於登錄的密碼。 它必須至少包含八個字元。 屬於混合域的用戶不需要密碼。

## 查看有關用戶的詳細資訊 {#view-details-about-a-user}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「用戶和組」。
1. 指定資訊以縮小搜索範圍，並在「在」清單中選擇「用戶」，然後按一下「查找」。 搜索結果列在頁面底部。 通過按一下任何列標題，可以對清單進行排序。
1. 按一下用戶名以顯示有關的詳細資訊。 「編輯用戶」頁顯示如下有關用戶的詳細資訊：

   * 一般標識資訊，如名稱、電子郵件、地址、域和組織
   * 分配給用戶的角色
   * 將用戶作為成員的組

## 更改本地用戶的密碼 {#change-the-password-for-a-local-user}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>用戶和組]**。
1. 指定資訊以縮小對特定用戶的搜索範圍，然後按一下 **[!UICONTROL 查找]**。 搜索結果列在頁面底部。 通過按一下任何列標題，可以對清單進行排序。
1. 按一下用戶名，然後按一下 **[!UICONTROL 更改密碼]**。
1. 鍵入並確認新密碼，然後按一下 **[!UICONTROL 確定]**。 密碼必須至少為8個字元。

## 編輯用戶的屬性 {#edit-a-user-s-properties}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>用戶和組]**。
1. 要查找要編輯的用戶，請執行以下任務：

   * 在 **[!UICONTROL 查找]** 框中，選擇「 CSV文本」。
   * 在 **[!UICONTROL 使用]** 清單，選擇 **[!UICONTROL 名稱]**。 **[!UICONTROL 電子郵件]**&#x200B;或 **[!UICONTROL 用戶ID]**。
   * 在 **[!UICONTROL 在清單中]**&#x200B;選中 **[!UICONTROL 用戶]**。
   * 選擇域，選擇要顯示的項數，然後按一下 **[!UICONTROL 查找]**。

1. 按一下要編輯的用戶。
1. 對於屬於本地或混合域的用戶， **[!UICONTROL 詳細資訊]** 頁籤 **[!UICONTROL 常規設定]** 和 **[!UICONTROL 登錄設定]**，然後按一下 **[!UICONTROL 保存]**。 有關設定的詳細資訊，請參閱 [用戶設定](adding-configuring-users.md#user-settings)。 不能編輯屬於企業域的用戶的常規和登錄設定。
1. 要編輯用戶的組設定，請按一下 **[!UICONTROL 組成員身份]** 頁籤，執行以下任務：

   * 按一下 **[!UICONTROL 查找組]** 並填寫搜索資訊。
   * 要將用戶添加到新組，請選中該組的複選框，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 保存]**。

   >[!NOTE]
   >
   >無法將本地用戶添加到目錄組。 但是，目錄用戶可以添加到本地組。

   * 要從組中刪除用戶，請選中該組的複選框，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 保存]**。


1. 要編輯用戶的角色，請按一下 **[!UICONTROL 角色分配]** 頁籤，執行以下任務：

   * 要顯示角色清單，請按一下 **[!UICONTROL 查找角色]**。
   * 要添加角色，請選中該角色的複選框，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 保存]**。
   * 要刪除角色，請選中該角色的複選框，按一下 **[!UICONTROL 取消分配]**，然後按一下 **[!UICONTROL 保存]**。

## 刪除用戶 {#delete-a-user}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>用戶和組]**。
1. 要查找要刪除的用戶，請執行以下任務：

   * 在 **[!UICONTROL 查找]** 框中，選擇「 CSV文本」。
   * 在 **[!UICONTROL 使用]** 清單，選擇 **[!UICONTROL 名稱]**。 **[!UICONTROL 電子郵件]**&#x200B;或 **[!UICONTROL 用戶ID]**。
   * 在 **[!UICONTROL 在清單中]**&#x200B;選中 **[!UICONTROL 用戶]**。
   * 選擇域，選擇要顯示的項數，然後按一下 **[!UICONTROL 查找]**。

1. 選中用戶的複選框，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**。

>[!NOTE]
>
>AEM Forms在JEE上還允AEM許在OSGi上運行的表單附加項的用戶被識別為AEM用戶。 對於需要在JEE上的AEM Forms和在OSGi上運行的表AEM單載入項(例如，HTML工作區)之間進行單一登錄的情況，這是必需的。 上述刪除操作僅從JEE上的AEM Forms刪除用戶。 未從OSGi環境上運行的AEM Forms載入項中刪除用戶。 但刪除用戶後進行的任何登錄嘗試(登錄到OSGi環境上的AEM Forms附加JEE伺服器或AEM Forms附加程式的嘗試)均被拒絕。

## 建立自定義登錄錯誤處理程式 {#create-custom-login-error-handler}

如果沒有所需AEM表單和CQ權限的用戶嘗試登錄到CQ中嵌入的以下應用程式，則用戶將被重定向到包含錯誤跟蹤的預設CQ 404頁：

* 通信管理解決方案
* 表AEM單工作區

   ***附註&#x200B;**:不建議使用Flex工AEM作空間。*

* 表單管理器
* 程序報告

CQ提供一種機制來覆蓋預設的404處理程式jsp。

有關如何自定義錯誤處理頁的詳細資訊，請參見 [自定義錯誤處理程式顯示的頁](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) 在Adobe Experience Manager檔案里。
