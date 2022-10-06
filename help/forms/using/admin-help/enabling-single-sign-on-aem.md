---
title: 在AEM Forms中啟用單一登入
seo-title: Enabling single sign-on in AEM forms
description: 了解如何使用HTTP標題和SPNEGO啟用單一登入(SSO)。
seo-description: Learn how to enable single sign-on (SSO) using HTTP headers and SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# 在AEM Forms中啟用單一登入{#enabling-single-sign-on-in-aem-forms}

AEM表單提供兩種啟用單一登入(SSO)的方式： HTTP標題和SPNEGO。

實作SSO時，若使用者已透過其公司入口網站驗證，則不需要AEM表單使用者登入頁面，也不會顯示。

如果AEM表單無法使用其中一種方法驗證使用者，系統會將使用者重新導向至登入頁面。

## 使用HTTP標頭啟用SSO {#enable-sso-using-http-headers}

您可以使用「門戶配置」頁在應用程式和任何支援通過HTTP標頭傳輸身份的應用程式之間啟用單一登錄(SSO)。 實作SSO時，若使用者已透過其公司入口網站驗證，則不需要AEM表單使用者登入頁面，也不會顯示。

您也可以使用SPNEGO啟用SSO。 (請參閱 [使用SPNEGO啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. 在管理控制台中，按一下「設定>使用者管理>設定>設定入口屬性」。
1. 選擇「是」以啟用SSO。 如果選擇「否」，則頁面上的其餘設定不可用。
1. 視需要設定頁面上的其餘選項，然後按一下「確定」 :

   * **SSO類型：** （必要）選取HTTP標題，以使用HTTP標題啟用SSO。
   * **使用者識別碼的HTTP標題：** （必要）其值包含登入使用者唯一識別碼的標題名稱。 用戶管理使用此值在用戶管理資料庫中查找用戶。 從此標題獲取的值應與從LDAP目錄同步的用戶的唯一標識符匹配。 (請參閱 [使用者設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **識別碼值會對應至使用者的使用者ID，而非使用者的唯一識別碼：** 將使用者的唯一識別碼值對應至使用者ID。 如果用戶的唯一標識符是無法通過HTTP標頭輕鬆傳播的二進位值（例如，如果要從Active Directory同步用戶，則選擇此選項）。
   * **域的HTTP標頭：** （非強制）其值包含網域名稱的標題名稱。 只有在沒有單一HTTP標題可唯一識別使用者時，才使用此設定。 若有多個網域，且唯一識別碼僅在網域內為唯一，請使用此設定。 在這種情況下，請在此文本框中指定標題名稱，並在「域映射」框中為多個域指定域映射。 (請參閱 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **域映射：** （必要）以格式指定多個網域的對應 *標題值=域名*.

      例如，假設網域的HTTP標題為domainName，且其值可能為domain1、domain2或domain3。 在此情況下，請使用域映射將domainName值映射到User Management域名。 每個映射必須位於不同的行：

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### 設定允許的反向連結 {#configure-allowed-referers}

如需設定允許的反向連結的步驟，請參閱 [設定允許的反向連結](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## 使用SPNEGO啟用SSO {#enable-sso-using-spnego}

在Windows環境中使用Active Directory作為LDAP伺服器時，可以使用簡單且受保護的GSSAPI協商機制(SPNEGO)來啟用單一登錄(SSO)。 啟用SSO時，AEM表單使用者登入頁面不是必要項目，也不會顯示。

您也可以使用HTTP標頭來啟用SSO。 (請參閱 [使用HTTP標頭啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>AEM Forms on JEE不支援在多個子網域環境中使用Kerberos/SPNEGO來設定SSO。

1. 決定要使用哪個網域來啟用SSO。 AEM表單伺服器和使用者必須屬於相同的Windows網域或受信任的網域。
1. 在Active Directory中，建立代表AEM表單伺服器的用戶。 (請參閱 [建立使用者帳戶](enabling-single-sign-on-aem.md#create-a-user-account).) 如果要配置多個域以使用SPNEGO，請確保每個用戶的密碼不同。 如果密碼不同，SPNEGO SSO將無法工作。
1. 映射服務主體名稱。 (請參閱 [映射服務主體名稱(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. 配置域控制器。 (請參閱 [防止Kerberos完整性檢查失敗](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. 添加或編輯企業域，如 [新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains) 或 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). 建立或編輯企業域時，請執行以下任務：

   * 添加或編輯包含Active Directory資訊的目錄。
   * 將LDAP添加為身份驗證提供程式。
   * 將Kerberos添加為身份驗證提供程式。 在Kerberos的「新建」或「編輯身份驗證」頁上提供以下資訊：

      * **驗證提供程式：** Kerberos
      * **DNS IP:** 運行AEM表單的伺服器的DNS IP地址。 您可以執行 `ipconfig/all` 在命令行上。
      * **KDC主機：** 用於身份驗證的Active Directory伺服器的完全限定的主機名或IP地址
      * **服務用戶：** 傳遞到KtPass工具的服務主體名稱(SPN)。 在先前使用的範例中，服務使用者為 `HTTP/lcserver.um.lc.com`.
      * **服務領域：** Active Directory的域名。 在先前使用的範例中，網域名稱為 `UM.LC.COM.`
      * **服務密碼：** 服務用戶密碼。 在先前使用的範例中，服務密碼為 `password`.
      * **啟用SPNEGO:** 啟用SPNEGO進行單一登入(SSO)。 選取此選項。

1. 配置SPNEGO客戶端瀏覽器設定。 (請參閱 [配置SPNEGO客戶端瀏覽器設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### 建立使用者帳戶 {#create-a-user-account}

1. 在SPNEGO中，以用戶身份註冊服務（在域控制器上的Active Directory中）以表示AEM表單。 在域控制器上，轉到「開始」菜單>「管理工具」>「Active Directory用戶和電腦」。 如果「管理工具」不在「開始」菜單中，請使用「控制面板」。
1. 按一下「使用者」資料夾以顯示使用者清單。
1. 按一下右鍵用戶資料夾，然後選擇「新建」>「用戶」。
1. 鍵入名字/姓氏和用戶登錄名，然後按一下下一步。 例如，設定下列值：

   * **名字**:umspnego
   * **用戶登錄名**:spnegodemo

1. 輸入密碼。 例如，將其設為 *密碼*. 確保已選擇「密碼永不過期」，並且未選擇其他選項。
1. 按「下一步」，然後按一下「完成」。

### 映射服務主體名稱(SPN) {#map-a-service-principal-name-spn}

1. 獲取KtPass實用程式。 此實用程式用於將SPN映射到領域。 您可以在Windows Server工具包或資源工具包中獲得KtPass實用程式。 (請參閱 [Windows Server 2003 Service Pack 1支援工具](https://support.microsoft.com/kb/892777).)
1. 在命令提示字元中，執行 `ktpass` 使用下列引數：

   `ktpass -princ HTTP/`*主機* `@`*領域* `-mapuser`*使用者*

   例如，輸入下列文字：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   您必須提供的值說明如下：

   **主機：** 表單伺服器或任何唯一URL的完全限定名稱。 在此範例中，已設為lcserver.um.lc.com。

   **領域：** 域控制器的Active Directory領域。 在此範例中，已設為UM.LC.COM。 確保輸入大寫字元的領域。 要確定Windows 2003的領域，請完成以下步驟：

   * 按一下右鍵「My Computer（我的電腦）」並選擇「Properties（屬性）」
   * 按一下「電腦名稱」頁簽。 域名值是領域名稱。

   **使用者：** 您在上一任務中建立的用戶帳戶的登錄名。 在此範例中，其設為spnegodemo。

如果您遇到此錯誤：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

請嘗試將使用者指定為spnegodemo@um.lc.com :

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性檢查失敗 {#prevent-kerberos-integrity-check-failures}

1. 在域控制器上，轉到「開始」菜單>「管理工具」>「Active Directory用戶和電腦」。 如果「管理工具」不在「開始」菜單中，請使用「控制面板」。
1. 按一下「使用者」資料夾以顯示使用者清單。
1. 按一下右鍵您在上一任務中建立的用戶帳戶。 在此範例中，使用者帳戶為 `spnegodemo`.
1. 按一下「重設密碼」。
1. 輸入並確認您先前輸入的相同密碼。 在此範例中，此值設為 `password`.
1. 取消選擇「Change Password At Next Logon（下次登錄時更改密碼）」 ，然後按一下「OK（確定）」。

### 配置SPNEGO客戶端瀏覽器設定 {#configuring-spnego-client-browser-settings}

要使基於SPNEGO的驗證工作正常，客戶端電腦必須是用戶帳戶建立的域的一部分。 您還必須配置客戶端瀏覽器以允許基於SPNEGO的驗證。 此外，需要基於SPNEGO的身份驗證的站點必須是受信任的站點。

如果使用電腦名稱(如https://lcserver:8080)訪問伺服器，則Internet Explorer無需任何設定。 如果您輸入的URL不包含任何點(&quot;。&quot;),Internet Explorer會將該網站視為本機內部網網站。 如果您對網站使用完全限定的名稱，則必須將網站新增為受信任的網站。

**配置Internet Explorer 6.x**

1. 轉至「工具」>「Internet選項」，然後按一下「安全」頁簽。
1. 按一下「Local Intranet（本地內部網）」表徵圖，然後按一下「Sites（站點）」。
1. 按一下「高級」，然後在「將此網站添加到區域」框中，鍵入表單伺服器的URL。 例如，輸入 `https://lcserver.um.lc.com`
1. 按一下「確定」(OK)，直到關閉所有對話框。
1. 存取AEM表單伺服器的URL以測試設定。 例如，在瀏覽器URL方塊中，輸入 `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**配置Mozilla Firefox**

1. 在瀏覽器URL方塊中，輸入 `about:config`

   隨即顯示about:config - Mozilla Firefox對話方塊。

1. 在「篩選」方塊中，輸入 `negotiate`
1. 在顯示的清單中，按一下network.negotiae-auth.trusted-uri ，然後根據您的環境鍵入以下任一命令：

   `.um.lc.com` — 將Firefox配置為允許以um.lc.com結尾的任何URL使用SPNEGO。 請務必加入點(&quot;。&quot;) 一開始。

   `lcserver.um.lc.com`  — 將Firefox配置為僅允許特定伺服器的SPNEGO。 請勿以點(&quot;。&quot;)開頭此值。

1. 存取應用程式以測試設定。 目標應用程式的歡迎頁面應隨即顯示。
