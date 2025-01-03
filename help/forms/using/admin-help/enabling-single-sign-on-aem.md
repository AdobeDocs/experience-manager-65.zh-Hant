---
title: 在AEM表單中啟用單一登入
description: 瞭解如何使用HTTP標題和SPNEGO啟用單一登入(SSO)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# 在AEM表單中啟用單一登入{#enabling-single-sign-on-in-aem-forms}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

AEM表單提供兩種啟用單一登入(SSO)的方式 — HTTP標題和SPNEGO。

實作SSO時，AEM Forms使用者登入頁面不是必要頁面，且若使用者已透過其公司入口網站驗證，也不會顯示。

如果AEM Forms無法使用其中一種方法來驗證使用者，系統會將使用者重新導向至登入頁面。

* [使用HTTP標頭啟用SSO](#enable-sso-using-http-headers)
* [使用SPNEGO啟用SSO](#enable-sso-using-spnego)
* [指派角色給使用者和群組](#assign-roles-to-users-groups)

## 使用HTTP標頭啟用SSO {#enable-sso-using-http-headers}

您可以使用「入口網站組態」頁面，在應用程式與任何支援透過HTTP標題傳送身分的應用程式之間，啟用單一登入(SSO)。 實作SSO時，AEM Forms使用者登入頁面不是必要頁面，且若使用者已透過其公司入口網站驗證，也不會顯示。

您也可以使用SPNEGO來啟用SSO。 （請參閱[使用SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)啟用SSO。）

1. 在管理控制檯中，按一下設定>使用者管理>設定>設定入口網站屬性。
1. 選取「是」以啟用SSO。 如果您選取「否」，頁面上的其餘設定將無法使用。
1. 視需要設定頁面上的其餘選項，然後按一下「確定」：

   * **SSO型別：** （必要）選取HTTP標頭以使用HTTP標頭啟用SSO。
   * 使用者識別碼的&#x200B;**HTTP標頭：** （必要）標頭的名稱，其值包含登入使用者的唯一識別碼。 「使用者管理」會使用此值在「使用者管理」資料庫中尋找使用者。 從此標頭取得的值應該與從LDAP目錄同步之使用者的唯一識別碼相符。 （請參閱[使用者設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)。）
   * **識別碼值對應到使用者的使用者識別碼，而不是使用者的唯一識別碼：**&#x200B;將使用者的唯一識別碼值對應到使用者識別碼。 如果使用者的唯一識別碼是無法透過HTTP標頭輕鬆傳播的二進位值（例如，如果您從Active Directory同步使用者，請選取objectGUID），請選取此選項。
   * 網域&#x200B;**的** HTTP標頭（非必要）其值包含網域名稱的標頭名稱。 只有在沒有單一HTTP標頭可唯一識別使用者時，才使用此設定。 如果有多個網域存在，且唯一識別碼僅在網域中是唯一的，請使用此設定。 在這種情況下，請在此文字方塊中指定標頭名稱，並在「網域對應」方塊中指定多個網域的網域對應。 （請參閱[編輯及轉換現有的網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。）
   * **網域對應：** （必要）指定多個網域的對應，格式為&#x200B;*標頭值=網域名稱*。

     例如，假設某個網域的HTTP標頭是domainName，而且它可以有domain1、domain2或domain3的值。 在這種情況下，請使用網域對應將domainName值對應到User Management網域名稱。 每個對應必須位於不同的行：

     domain1=UMdomain1

     domain2=UMdomain2

     domain3=UMdomain3

### 設定允許的反向連結 {#configure-allowed-referers}

如需設定允許的反向連結的步驟，請參閱[設定允許的反向連結](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)。

### 指派角色給使用者和群組

按一下以瞭解[將角色指派給使用者和群組](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups)的步驟。

## 使用SPNEGO啟用SSO {#enable-sso-using-spnego}

在Windows環境中使用Active Directory做為LDAP伺服器時，您可以使用簡單且受保護的GSSAPI交涉機制(SPNEGO)來啟用單一登入(SSO)。 啟用SSO時，AEM Forms使用者登入頁面不是必要專案，也不會出現。

您也可以使用HTTP標頭來啟用SSO。 （請參閱[使用HTTP標頭啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)。）

>[!NOTE]
>
>JEE上的AEM Forms不支援在多個子網域環境中使用Kerberos/SPNEGO來設定SSO。

1. 決定要使用哪個網域來啟用SSO。 AEM Forms Server和使用者必須屬於相同的Windows網域或受信任的網域。
1. 在Active Directory中，建立代表AEM Forms伺服器的使用者。 （請參閱[建立使用者帳戶](enabling-single-sign-on-aem.md#create-a-user-account)。）如果您要設定多個網域來使用SPNEGO，請確定每個使用者的密碼不同。 如果密碼不同，SPNEGO SSO將無法運作。
1. 對應服務主體名稱。 (請參閱[對應服務主要名稱(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)。)
1. 設定網域控制站。 （請參閱[防止Kerberos完整性檢查失敗](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)。）
1. 新增或編輯企業網域，如[新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains)或[編輯及轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)中所述。 當您建立或編輯企業網域時，請執行下列工作：

   * 新增或編輯包含Active Directory資訊的目錄。
   * 將LDAP新增為驗證提供者。
   * 將Kerberos新增為驗證提供者。 在Kerberos的「新增驗證」或「編輯驗證」頁面上提供下列資訊：

      * **驗證提供者：** Kerberos
      * **DNS IP：**&#x200B;執行AEM表單之伺服器的DNS IP位址。 您可以在命令列上執行`ipconfig/all`以判斷此IP位址。
      * **KDC主機：**&#x200B;用於驗證之Active Directory伺服器的完整主機名稱或IP位址
      * **服務使用者：**&#x200B;傳遞給KtPass工具的服務主要名稱(SPN)。 在先前使用的範例中，服務使用者為`HTTP/lcserver.um.lc.com`。
      * **服務領域：** Active Directory的網域名稱。 在先前使用的範例中，網域名稱為`UM.LC.COM.`
      * **服務密碼：**&#x200B;服務使用者的密碼。 在先前使用的範例中，服務密碼為`password`。
      * **啟用SPNEGO：**&#x200B;啟用單一登入(SSO)使用SPNEGO。 選取此選項。

1. 設定SPNEGO使用者端瀏覽器設定。 （請參閱[設定SPNEGO使用者端瀏覽器設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)。）

### 建立使用者帳戶 {#create-a-user-account}

1. 在SPNEGO中，將服務註冊為網域控制站上Active Directory中的使用者，以代表AEM表單。 在網域控制站上，移至[開始]功能表> [系統管理工具] > [Active Directory使用者和電腦]。 如果「管理工具」不在「開始」功能表中，請使用「控制面板」。
1. 按一下Users資料夾以顯示使用者清單。
1. 以滑鼠右鍵按一下使用者資料夾，然後選取「新增>使用者」。
1. 輸入「名字/姓氏」和「使用者登入名稱」，然後按「下一步」。 例如，設定下列值：

   * **名字**： umspnego
   * **使用者登入名稱**： spnegodemo

1. 輸入密碼。 例如，將其設定為&#x200B;*密碼*。 確保已選取「密碼永不過期」，且未選取其他選項。
1. 按一下「下一步」，然後按一下「完成」。

### 對應服務主要名稱(SPN) {#map-a-service-principal-name-spn}

1. 取得KtPass公用程式。 此公用程式用來將SPN對應至REALM。 您可以取得KtPass公用程式作為Windows Server Tool Pack或Resource Kit的一部分。 （請參閱[Windows Server 2003 Service Pack 1支援工具](https://support.microsoft.com/kb/892777)。）
1. 在命令提示字元中，使用下列引數執行`ktpass`：

   `ktpass -princ HTTP/`*主機* `@`*領域* `-mapuser`*使用者*

   例如，輸入下列文字：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   您必須提供的值說明如下：

   **主機：** Forms伺服器的完整名稱或任何唯一URL。 在此範例中，它被設為lcserver.um.lc.com。

   **領域：**&#x200B;網域控制站的Active Directory領域。 在此範例中，它被設為UM.LC.COM。 請確定您以大寫字元輸入範圍。 若要確定Windows 2003的範圍，請完成下列步驟：

   * 用滑鼠右鍵按一下「我的電腦」並選取「內容」
   * 按一下「電腦名稱」標籤。 「網域名稱」值是範圍名稱。

   **使用者：**&#x200B;您在前一個任務中建立的使用者帳戶登入名稱。 在此範例中，它被設定為spnegedemo。

如果您遇到此錯誤：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

嘗試將使用者指定為spnegodemo@um.lc.com：

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性檢查失敗 {#prevent-kerberos-integrity-check-failures}

1. 在網域控制站上，移至[開始]功能表> [系統管理工具] > [Active Directory使用者和電腦]。 如果「管理工具」不在「開始」功能表中，請使用「控制面板」。
1. 按一下Users資料夾以顯示使用者清單。
1. 以滑鼠右鍵按一下您在前一個任務中建立的使用者帳戶。 在此範例中，使用者帳戶為`spnegodemo`。
1. 按一下「重設密碼」。
1. 輸入並確認您先前輸入的密碼。 在此範例中，它被設定為`password`。
1. 取消選取「下次登入時變更密碼」，然後按一下「確定」。

### 正在設定SPNEGO使用者端瀏覽器設定 {#configuring-spnego-client-browser-settings}

若要讓SPNEGO式驗證能夠運作，使用者端電腦必須是建立使用者帳戶的網域的一部分。 您也必須設定使用者端瀏覽器以允許以SPNEGO為基礎的驗證。 此外，需要SPNEGO式驗證的網站必須是受信任的網站。

如果使用電腦名稱(例如https://lcserver:8080)存取伺服器，則Internet Explorer不需要任何設定。 如果您輸入的URL不含任何點(「。」)，Internet Explorer會將網站視為近端內部網路網站。 如果您使用網站的完整名稱，則必須將網站新增為信任的網站。

**設定Internet Explorer 6.x**

1. 前往「工具>網際網路選項」 ，然後按一下「安全性」標籤。
1. 按一下「近端內部網路」圖示，然後按一下「網站」。
1. 按一下「進階」，然後在「將此網站新增至區域」方塊中，輸入Forms伺服器的URL。 例如，型別`https://lcserver.um.lc.com`
1. 按一下「確定」，直到關閉所有對話方塊。
1. 存取AEM Forms伺服器的URL以測試設定。 例如，在瀏覽器URL方塊中，輸入`https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**設定Mozilla Firefox**

1. 在瀏覽器URL方塊中，輸入`about:config`

   這時會出現about：config - Mozilla Firefox對話方塊。

1. 在篩選方塊中，輸入`negotiate`
1. 在顯示的清單中，按一下network.negotiate-auth.trusted-uri，然後輸入下列適合您環境的命令：

   `.um.lc.com` — 設定Firefox允許任何以um.lc.com結尾的URL使用SPNEGO。 請務必加入點(「。」) 在開頭。

   `lcserver.um.lc.com` — 將Firefox設定為僅允許特定伺服器使用SPNEGO。 請勿以點(「。」)作為此值開頭。

1. 存取應用程式以測試設定。 目標應用程式的歡迎頁面應該會出現。

按一下以瞭解[將角色指派給使用者和群組](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups)的步驟。

## 指派角色給使用者和群組 {#assign-roles-to-users-groups}

1. 在JEE環境中登入您的AEM Forms 。
1. 在管理控制檯中，按一下「設定」>「使用者管理」>「網域管理」。
1. 選取您的網域設定，例如LDAP，然後按一下它。 您可以在「目錄」中找到所有已建立的使用者和群組。 如有需要，您可以建立新的使用者或群組。
   ![網域管理頁面](/help/forms/using/assets/domain-mgmt-page.png)
1. 按一下「驗證」，在新頁面上選取「驗證提供者」，例如LDAP。
1. 瀏覽至「網域管理」頁面，選取LDAP，然後按一下[立即同步] **，將目錄與您設定的驗證配置同步處理，以進行AEM存取。**
   ![同步LDAP](/help/forms/using/assets/sync-ldap.png)
1. 前往使用者管理，然後按一下使用者和群組。
1. 搜尋具有其名稱的使用者或群組，如下圖所示。
   ![搜尋使用者群組](/help/forms/using/assets/search-user-group.png)
1. 視需要指派角色給使用者或群組。
   ![使用者角色指派](/help/forms/using/assets/user-role-assign.png)

