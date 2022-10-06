---
title: 新增和設定使用者
seo-title: Adding and configuring users
description: 管理控制台中的「使用者管理」設定可讓您建立或刪除使用者，以及設定其他使用者設定。
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# 新增和設定使用者 {#adding-and-configuring-users}

用戶和組資訊在第三方儲存系統（如LDAP目錄）中維護。 用戶管理不寫入第三方儲存系統。 相反，「用戶管理」會將用戶和組資訊與其自己的資料庫同步

## 建立使用者 {#create-a-user}

建立使用者時，您可以將使用者新增至群組，並為其指派角色。

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**，然後按一下 **[!UICONTROL 新用戶]**..
1. 在 **[!UICONTROL 一般設定]**，視需要提供資訊，然後按一下 **[!UICONTROL 下一個]**. 如需設定的詳細資訊，請參閱 [使用者設定](adding-configuring-users.md#user-settings).
1. （選用）若要新增使用者至群組，請按一下 **[!UICONTROL 查找組]**，並執行下列工作：

   * 在 **[!UICONTROL 查找]** 框中，鍵入組名稱的全部或部分。
   * 選取要搜尋的網域、選取要顯示的項目數，然後按一下 **[!UICONTROL 查找]**.
   * （可選）若要檢視群組詳細資訊，請選取群組名稱，然後按一下 **[!UICONTROL 確定]** 返回搜索結果頁。
   * 選取群組的核取方塊，然後按一下 **[!UICONTROL 確定]**.
   * 按一下&#x200B;**[!UICONTROL 下一步]**。

1. （可選）若要指派角色給使用者，請按一下 **[!UICONTROL 查找角色]**，選中要分配的角色的複選框，然後按一下 **[!UICONTROL 確定]**.
1. 按一下 **[!UICONTROL 完成]**.

   >[!NOTE]
   >
   >如果您發生使用者的任何登入問題，請參閱 [JEE上的AEM Forms使用者無法在OSGi端登入AEM Forms](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## 使用者設定 {#user-settings}

在建立或編輯使用者時指定下列設定。

**標準名稱：** （必要）使用者的唯一識別碼。 網域中的每個使用者和群組必須具有唯一的標準名稱。 選中「系統生成」複選框，使「用戶管理」可以指定一個唯一值，或清除該複選框，並為「規範名稱」指定自定義值。

請避免在標準名稱中使用底線字元(_)，例如 `sample_user`. 當您根據使用者的標準名稱來搜尋使用者時，系統不會傳回包含底線字元的使用者。

**名字：** （強制）使用者的指定名稱

**姓氏：** （強制）使用者的姓氏

**常用名稱：** 使用者的完整名稱或顯示名稱。 例如，如果名字= Gloria，姓氏= Rios，則常見名字= Gloria Rios。

**電子郵件：** 使用者的電子郵件地址

**電話：** 用戶的電話號碼

**說明：** 可選說明。 請依照組織的需求使用此欄位。

**地址：** 用戶的郵件地址

**組織：** 使用者所屬的組織

**電子郵件別名：** 使用者的電子郵件別名。 請使用逗號分隔電子郵件別名。

**域：** 用戶所屬的域

**地區：** 用戶的ISO地區設定

**業務日曆密鑰：** 允許您根據此設定的值將業務日曆映射到用戶。 業務日曆定義業務日和非業務日。 AEM表單可在計算提醒、截止日期和呈報等事件的未來日期和時間時使用商業日曆。 將業務日曆密鑰分配給用戶的方式取決於您使用的是企業、本地還是混合域。 (請參閱 [新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

如果您使用本機或混合網域，則有關使用者的資訊只會儲存在使用者管理資料庫中。 對於這些用戶，將「業務日曆」鍵設定為字串。 然後，在表單工作流程中將業務日曆鍵（字串）映射到業務日曆。

如果使用企業域，則有關用戶的資訊駐留在第三方儲存系統中，如LDAP目錄。 用戶管理將目錄中的用戶資訊與用戶管理資料庫同步。 此功能允許您將業務日曆密鑰映射到LDAP目錄中的欄位。 例如，假設目錄中的每個用戶記錄都包含國家欄位，並且您想根據用戶所在的國家分配業務日曆。 在此情況下，您指定國家欄位名稱作為「業務日曆鍵」設定的值。 然後，您可以將業務日曆鍵（為LDAP目錄中的國家欄位定義的值）映射到表單工作流中的業務日曆。

有關業務日曆的其他資訊，包括如何將業務日曆鍵映射到業務日曆，請參閱 [配置業務日曆](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

名稱限制為少於53個字元。 名稱較短有助於防止在管理控制台的「流程管理」頁面中顯示業務日曆鍵的問題。

**用戶ID:** （必要）使用者用來登入的使用者ID。 使用者ID不區分大小寫，且在整個網域中必須是唯一的。

在企業網域中，使用非DN屬性作為使用者ID，因為如果使用者移至組織的其他部分，其DN可能會變更。 此設定取決於目錄伺服器。 值為 `objectGUID` 對於Active Directory 2003, `nsuniqueID` Sun™ One的 `guid` （用於eDirectory）。

請確定使用者ID為唯一。 請勿使用指派給已刪除使用者的檔案。

AEM表單無法區分具有相同使用者ID和密碼但屬於不同網域的使用者帳戶。 若要避免此問題，請勿在多個網域上建立具有相同使用者ID的帳戶。

使用SQL Server作為資料庫時，無法建立超過255個字元的用戶ID。

使用MySQL時，用戶ID可以包含擴展字元。 不過，當在兩個字串（例如abcde和âbcdè）之間進行比較時，兩者會視為相同。 例如，同步時，如果新用戶被添加到資料庫，則會進行比較以檢查資料庫中是否存在具有相同用戶ID的用戶。 若使用者 *abcde* 當新用戶 *阿布奇* 新增，則比較無法區分這兩個名稱。 假設該用戶已存在於資料庫中，並且會忽略新用戶，而不會添加。

請避免建立以數字型大小(#)開頭的使用者名稱。 執行任務搜索不會返回這些用戶名的結果。 (請參閱 [使用任務](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**密碼和確認密碼：** 用戶用於登錄的密碼。 它至少必須有8個字元。 屬於混合域的用戶不需要密碼。

## 檢視使用者的詳細資訊 {#view-details-about-a-user}

1. 在管理控制台中，按一下「設定>使用者管理>使用者和群組」。
1. 指定要縮小搜索範圍的資訊，並在「輸入」清單中，選擇「用戶」，然後按一下「查找」。 搜尋結果會列在頁面底部。 您可以按一下任何欄標題來排序清單。
1. 按一下使用者的名稱以顯示相關詳細資訊。 「編輯使用者」頁面會顯示下列關於使用者的詳細資訊：

   * 一般識別資訊，例如名稱、電子郵件、地址、網域和組織
   * 指派給使用者的角色
   * 對用戶所屬的組

## 更改本地用戶的密碼 {#change-the-password-for-a-local-user}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 指定用於縮小搜索特定用戶範圍的資訊，然後按一下 **[!UICONTROL 查找]**. 搜尋結果會列在頁面底部。 您可以按一下任何欄標題來排序清單。
1. 按一下使用者的名稱，然後按一下 **[!UICONTROL 更改密碼]**.
1. 輸入並確認新密碼，然後按一下 **[!UICONTROL 確定]**. 密碼至少必須有8個字元。

## 編輯使用者的屬性 {#edit-a-user-s-properties}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 要查找要編輯的用戶，請執行以下任務：

   * 在 **[!UICONTROL 查找]** 框中，鍵入搜索條件。
   * 在 **[!UICONTROL 使用]** 清單，選擇 **[!UICONTROL 名稱]**, **[!UICONTROL 電子郵件]**，或 **[!UICONTROL 使用者ID]**.
   * 在 **[!UICONTROL 在清單中]**，選取 **[!UICONTROL 使用者]**.
   * 選取網域，選取要顯示的項目數，然後按一下 **[!UICONTROL 查找]**.

1. 按一下要編輯的使用者。
1. 若使用者屬於本機或混合網域，請在 **[!UICONTROL 詳細資料]** 頁簽，編輯 **[!UICONTROL 一般設定]** 和 **[!UICONTROL 登入設定]**，然後按一下 **[!UICONTROL 儲存]**. 如需設定的詳細資訊，請參閱 [使用者設定](adding-configuring-users.md#user-settings). 您無法編輯屬於企業域的用戶的一般設定和登錄設定。
1. 若要編輯使用者的群組設定，請按一下 **[!UICONTROL 群組成員資格]** 標籤，然後執行下列工作：

   * 按一下 **[!UICONTROL 查找組]** 填寫搜索資訊。
   * 若要將使用者新增至新群組，請選取該群組的核取方塊，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 儲存]**.

   >[!NOTE]
   >
   >無法將本地用戶添加到目錄組。 但是，目錄用戶可以添加到本地組。

   * 若要從群組中移除使用者，請選取該群組的核取方塊，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 儲存]**.


1. 若要編輯使用者的角色，請按一下 **[!UICONTROL 角色分配]** 標籤，然後執行下列工作：

   * 要顯示角色清單，請按一下 **[!UICONTROL 查找角色]**.
   * 若要新增角色，請選取角色的核取方塊，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 儲存]**.
   * 要刪除角色，請選中角色的複選框，按一下 **[!UICONTROL 取消指派]**，然後按一下 **[!UICONTROL 儲存]**.

## 刪除使用者 {#delete-a-user}

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 要查找要刪除的用戶，請執行以下任務：

   * 在 **[!UICONTROL 查找]** 框中，鍵入搜索條件。
   * 在 **[!UICONTROL 使用]** 清單，選擇 **[!UICONTROL 名稱]**, **[!UICONTROL 電子郵件]**，或 **[!UICONTROL 使用者ID]**.
   * 在 **[!UICONTROL 在清單中]**，選取 **[!UICONTROL 使用者]**.
   * 選取網域，選取要顯示的項目數，然後按一下 **[!UICONTROL 查找]**.

1. 選取使用者的核取方塊，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**.

>[!NOTE]
>
>AEM Forms on JEE也可讓在OSGi上執行的AEM forms附加元件使用者辨識為AEM使用者。 若是需要JEE上的AEM Forms和在OSGi上執行的AEM Forms附加元件之間的單一登入(例如HTML工作區)，則此為必要項目。 上述刪除操作僅會從JEE上的AEM Forms移除使用者。 未從在OSGi環境上執行的AEM Forms附加元件中刪除使用者。 但刪除使用者後進行的任何登入嘗試(登入AEM Forms附加JEE伺服器或OSGi環境上的AEM Forms附加元件)則遭拒。

## 建立自訂登入錯誤處理常式 {#create-custom-login-error-handler}

若使用者未具備必要的AEM表單和CQ權限，而嘗試登入內嵌於CQ中的下列應用程式，系統會將使用者重新導向至包含錯誤追蹤的預設CQ 404頁面：

* 通信管理解決方案
* AEM forms Workspace

   ***附註&#x200B;**:AEM Forms版本已不再使用Flex Workspace。*

* forms manager
* 程序報告

CQ提供覆寫預設404處理常式jsp的機制。

如需如何自訂錯誤處理頁面的詳細資訊，請參閱 [自訂由錯誤處理常式顯示的頁面](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) 在Adobe Experience Manager檔案中。
