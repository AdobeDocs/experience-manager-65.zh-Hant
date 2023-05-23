---
title: 在表單中啟用單一登AEM錄
seo-title: Enabling single sign-on in AEM forms
description: 瞭解如何使用HTTP標頭和SPNEGO啟用單一登錄(SSO)。
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

# 在表單中啟用單一登AEM錄{#enabling-single-sign-on-in-aem-forms}

表AEM單提供了兩種啟用單一登錄(SSO)- HTTP標頭和SPNEGO的方法。

實施SSO時，表AEM單用戶登錄頁不是必需的，如果用戶已通過其公司門戶進行身份驗證，則不會顯示。

如AEM果表單無法使用其中一種方法驗證用戶，則會將用戶重定向到登錄頁。

## 使用HTTP標頭啟用SSO {#enable-sso-using-http-headers}

可以使用「入口配置」頁在應用程式和支援通過HTTP標頭傳送標識的任何應用程式之間啟用單一登錄(SSO)。 實施SSO時，表AEM單用戶登錄頁不是必需的，如果用戶已通過其公司門戶進行身份驗證，則不會顯示。

您也可以使用SPNEGO啟用SSO。 (請參閱 [使用SPNEGO啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)。)

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置門戶屬性」。
1. 選擇是以啟用SSO。 如果選擇「否」，則頁面上的其餘設定不可用。
1. 根據需要設定頁面上的其餘選項，然後按一下「確定」：

   * **SSO類型：** （必需）選擇HTTP標頭以使用HTTP標頭啟用SSO。
   * **用戶標識符的HTTP標頭：** （必需）其值包含登錄用戶的唯一標識符的標頭的名稱。 用戶管理使用此值在用戶管理資料庫中查找用戶。 從此標頭獲取的值應與從LDAP目錄同步的用戶的唯一標識符匹配。 (請參閱 [用戶設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)。)
   * **標識符值映射到用戶的用戶ID，而不是用戶的唯一標識符：** 將用戶的唯一標識符值映射到用戶ID。 如果用戶的唯一標識符是無法通過HTTP標頭輕鬆傳播的二進位值（例如，如果正在從Active Directory同步用戶，則選擇此選項）。
   * **域的HTTP標頭：** （非強制）其值包含域名的標頭的名稱。 僅當沒有單個HTTP標頭唯一標識用戶時才使用此設定。 對於存在多個域且唯一標識符僅在域內唯一的情況，請使用此設定。 在這種情況下，在此文本框中指定標題名稱，並在「域映射」框中為多個域指定域映射。 (請參閱 [編輯和轉換現有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。)
   * **域映射：** （必需）指定格式為多個域的映射 *標頭值=域名*。

      例如，請考慮一種情況：域的HTTP標頭為domainName，並且它可以具有domain1、domain2或domain3的值。 在這種情況下，使用域映射將domainName值映射到用戶管理域名。 每個映射必須位於不同的行上：

      域1=UMdomain1

      域2=UMdomain2

      域3=UMdomain3

### 配置允許的引用者 {#configure-allowed-referers}

有關配置允許的引用的步驟，請參見 [配置允許的引用者](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)。

## 使用SPNEGO啟用SSO {#enable-sso-using-spnego}

在Windows環境中將Active Directory用作LDAP伺服器時，可以使用簡單和受保護的GSSAPI協商機制(SPNEGO)啟用單一登錄(SSO)。 啟用SSO後，表AEM單用戶登錄頁不是必需的，也不顯示。

也可以使用HTTP標頭啟用SSO。 (請參閱 [使用HTTP標頭啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)。)

>[!NOTE]
>
>AEM Forms在JEE上不支援在多子域環境中使用Kerberos/SPNEGO配置SSO。

1. 確定要啟用SSO的域。 表AEM單伺服器和用戶必須是同一Windows域或受信任域的一部分。
1. 在Active Directory中，建立代表表單伺服器AEM的用戶。 (請參閱 [建立用戶帳戶](enabling-single-sign-on-aem.md#create-a-user-account)。) 如果要配置多個域以使用SPNEGO，請確保每個用戶的密碼不同。 如果密碼不是不同的，則SPNEGO SSO不起作用。
1. 映射服務主體名稱。 (請參閱 [映射服務主體名稱(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)。)
1. 配置域控制器。 (請參閱 [防止Kerberos完整性檢查失敗](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)。)
1. 添加或編輯企業域（如所述） [添加域](/help/forms/using/admin-help/adding-domains.md#adding-domains) 或 [編輯和轉換現有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。 建立或編輯企業域時，請執行以下任務：

   * 添加或編輯包含Active Directory資訊的目錄。
   * 將LDAP添加為身份驗證提供程式。
   * 將Kerberos添加為身份驗證提供程式。 在Kerberos的「新建」或「編輯驗證」頁上提供以下資訊：

      * **身份驗證提供程式：** Kerberos
      * **DNS IP:** 運行表單的伺服器的DNS IPAEM地址。 您可以通過運行 `ipconfig/all` 命令行上。
      * **KDC主機：** 用於身份驗證的Active Directory伺服器的完全限定主機名或IP地址
      * **服務用戶：** 傳遞給KtPass工具的服務主體名稱(SPN)。 在前面使用的示例中，服務用戶 `HTTP/lcserver.um.lc.com`。
      * **服務領域：** Active Directory的域名。 在前面使用的示例中，域名為 `UM.LC.COM.`
      * **服務密碼：** 服務用戶的密碼。 在前面使用的示例中，服務密碼為 `password`。
      * **啟用SPNEGO:** 啟用SPNEGO用於單一登錄(SSO)。 選擇此選項。

1. 配置SPNEGO客戶端瀏覽器設定。 (請參閱 [配置SPNEGO客戶端瀏覽器設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)。)

### 建立用戶帳戶 {#create-a-user-account}

1. 在SPNEGO中，將服務註冊為域控制器上的Active Directory中的用戶，以表示AEM表單。 在域控制器上，轉到「開始」菜單>「管理工具」>「Active Directory用戶和電腦」。 如果「管理工具」不在「開始」菜單中，請使用「控制面板」。
1. 按一下「用戶」資料夾以顯示用戶清單。
1. 按一下右鍵用戶資料夾，然後選擇「新建」>「用戶」。
1. 鍵入「First Name/Last Name（名稱/姓氏）」和「User Logon Name（用戶登錄名）」 ，然後按一下「Next（下一步）」。 例如，設定以下值：

   * **名字**:雨
   * **用戶登錄名**:spnegodemo

1. 鍵入密碼。 例如，將其設定為 *密碼*。 確保選中了「密碼永不過期」，並且未選擇其他選項。
1. 按一下「Next（下一步）」 ，然後按一下「Finish（完成）」。

### 映射服務主體名稱(SPN) {#map-a-service-principal-name-spn}

1. 獲取KtPass實用程式。 此實用程式用於將SPN映射到REALM。 您可以獲得KtPass實用程式作為Windows Server工具包或資源工具包的一部分。 (請參閱 [Windows Server 2003 Service Pack 1支援工具](https://support.microsoft.com/kb/892777)。)
1. 在命令提示符下，運行 `ktpass` 使用以下參數：

   `ktpass -princ HTTP/`*主機* `@`*領域* `-mapuser`*用戶*

   例如，鍵入以下文本：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   您必須提供的值說明如下：

   **主機：** 表單伺服器或任何唯一URL的完全限定名稱。 在本示例中，它設定為lcserver.um.lc.com。

   **領域：** 域控制器的Active Directory領域。 在本示例中，它設定為UM.LC.COM。 確保以大寫字元輸入領域。 要確定Windows 2003的領域，請完成以下步驟：

   * 按一下右鍵「My Computer（我的電腦）」並選擇「Properties（屬性）」
   * 按一下「Computer Name（電腦名稱）」頁籤。 域名值是領域名。

   **用戶：** 您在上一任務中建立的用戶帳戶的登錄名。 在本示例中，它設定為spnegodemo。

如果遇到以下錯誤：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

嘗試將用戶指定為spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性檢查失敗 {#prevent-kerberos-integrity-check-failures}

1. 在域控制器上，轉到「開始」菜單>「管理工具」>「Active Directory用戶和電腦」。 如果「管理工具」不在「開始」菜單中，請使用「控制面板」。
1. 按一下「用戶」資料夾以顯示用戶清單。
1. 按一下右鍵在上一任務中建立的用戶帳戶。 在本示例中，用戶帳戶為 `spnegodemo`。
1. 按一下「重置密碼」。
1. 鍵入並確認以前鍵入的密碼。 在本例中，它設定為 `password`。
1. 取消選擇「Change Password At Next Logon（下次登錄時更改密碼）」 ，然後按一下「OK（確定）」。

### 配置SPNEGO客戶端瀏覽器設定 {#configuring-spnego-client-browser-settings}

要使基於SPNEGO的驗證工作，客戶端電腦必須是在中建立用戶帳戶的域的一部分。 您還必須配置客戶端瀏覽器以允許基於SPNEGO的身份驗證。 此外，需要基於SPNEGO的身份驗證的站點必須是受信任的站點。

如果使用電腦名(如https://lcserver:8080)訪問伺服器，則Internet Explorer不需要設定。 如果輸入的URL不包含任何點(&quot;。&quot;),Internet Explorer將該站點視為本地Intranet站點。 如果您正在為站點使用完全限定的名稱，則必須將站點添加為受信任的站點。

**配置Internet Explorer 6.x**

1. 轉到「工具」>「Internet選項」，然後按一下「安全」頁籤。
1. 按一下「Local Intranet（本地Intranet）」表徵圖，然後按一下「Sites（站點）」。
1. 按一下「高級」，然後在「將此網站添加到區域」框中，鍵入表單伺服器的URL。 例如，鍵入 `https://lcserver.um.lc.com`
1. 按一下「確定」(OK)，直到關閉所有對話框。
1. Test配置，方法是訪問Forms服AEM務器的URL。 例如，在瀏覽器URL框中，鍵入 `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**配置Mozilla Firefox**

1. 在瀏覽器URL框中，鍵入 `about:config`

   出現about:config - Mozilla Firefox對話框。

1. 在「篩選器」框中，鍵入 `negotiate`
1. 在顯示的清單中，按一下network.negotiate-auth.trusted-uri ，然後鍵入以下適合您環境的命令之一：

   `.um.lc.com` — 將Firefox配置為允許SPNEGO訪問以um.lc.com結尾的任何URL。 確保包含點(&quot;。&quot;) 開始。

   `lcserver.um.lc.com`  — 將Firefox配置為僅允許特定伺服器使用SPNEGO。 不要以點(&quot;。&quot;)開頭此值。

1. 通過訪問應用程式test配置。 應出現目標應用程式的歡迎頁。
