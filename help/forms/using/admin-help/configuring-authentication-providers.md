---
title: 配置身份驗證提供程式
seo-title: Configuring authentication providers
description: 添加、編輯或刪除身份驗證提供程式、更改身份驗證設定，以及閱讀有關用戶的及時配置的資訊。
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 配置身份驗證提供程式 {#configuring-authentication-providers}

混合域需要至少一個身份驗證提供程式，而企業域需要至少一個身份驗證提供程式或目錄提供程式。

如果使用SPNEGO啟用SSO，請添加啟用SPNEGO的Kerberos身份驗證提供程式和LDAP提供程式作為備份。 如果SPNEGO不工作，則此配置允許使用用戶ID和口令進行用戶身份驗證。 (請參閱 [使用SPNEGO啟用SSO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)。)

## 添加身份驗證提供程式 {#add-an-authentication-provider}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下清單中的現有域。 如果要為新域添加身份驗證，請參見 [添加企業域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) 或 [添加混合域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)。
1. 按一下添加驗證，然後在驗證提供程式清單中，根據您的組織使用的驗證機制選擇一個提供程式。
1. 提供頁面上所需的任何其他資訊。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings)。)
1. （可選）按一下「Test」test配置。
1. 按一下「OK（確定）」 ，然後再次按一下「OK（確定）」。

## 編輯現有身份驗證提供程式 {#edit-an-existing-authentication-provider}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下清單中的相應域。
1. 在顯示的頁面上，從清單中選擇相應的身份驗證提供程式並根據需要進行更改。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings)。)
1. 按一下「確定」。

## 刪除驗證提供程式 {#delete-an-authentication-provider}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下清單中的相應域。
1. 選中要刪除的驗證提供程式的複選框，然後按一下刪除。
1. 在顯示的確認頁面上按一下「確定」，然後再次按一下「確定」。

## 驗證設定 {#authentication-settings}

以下設定可用，具體取決於您選擇的域類型和身份驗證類型。

### LDAP設定 {#ldap-settings}

如果要為企業域或混合域配置身份驗證並選擇LDAP身份驗證，則可以選擇使用目錄配置中指定的LDAP伺服器，也可以選擇其他LDAP伺服器來進行身份驗證。 如果您選擇其他伺服器，則用戶必須同時存在於兩個LDAP伺服器上。

要使用在目錄配置中指定的LDAP伺服器，請選擇LDAP作為驗證提供程式，然後按一下「確定」。

要使用其他LDAP伺服器執行身份驗證，請選擇LDAP作為身份驗證提供程式，然後選擇「自定義LDAP身份驗證」複選框。 將顯示以下配置設定。

**伺服器：** （必需）目錄伺服器的完全限定域名(FQDN)。 例如，對於example.com網路上名為x的電腦，FQDN為x.example.com。 可以使用IP地址代替FQDN伺服器名。

**埠：** （必需）目錄伺服器使用的埠。 通常為389或636(如果安全套接字層(SSL)協定用於通過網路發送驗證資訊)。

**SSL:** （必需）指定在通過網路發送資料時目錄伺服器是否使用SSL。 預設值為No。 如果設定為「是」，則應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （必需）指定如何訪問目錄。

**匿名：** 不需要用戶名或密碼。

**用戶：** 需要身份驗證。 在「名稱」框中，指定可以訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整可分辨名稱(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」框中，指定關聯的密碼。 選擇「用戶」作為「綁定」選項時，需要這些設定。

**檢索基本DN:** （非必需）檢索基本DN並在下拉清單中顯示它們。 當您有多個基本DN且需要選擇值時，此設定非常有用。

**基本DN:** （必需）用作從LDAP層次結構同步用戶和組的起點。 最好在層次結構的最低級別指定一個基本DN，該DN包括需要同步服務的所有用戶和組。 不要在此設定中包括用戶的DN。 要同步特定用戶，請使用「搜索篩選器」設定。

**使用以下內容填充頁面：** （非必需）選中後，使用相應的預設LDAP值填充「用戶」和「組」設定頁上的屬性。

**搜索篩選器：** （必需）用於查找與用戶關聯的記錄的搜索篩選器。 請參閱搜索篩選器語法。

### Kerberos設定 {#kerberos-settings}

如果您正在為企業域或混合域配置身份驗證並選擇Kerberos身份驗證，則可以使用以下設定。

**DNS IP:** 運行表單的伺服器的DNS IPAEM地址。 在Windows上，可以通過在命令行運行ipconfig /all來確定此IP地址。

**KDC主機：** 用於身份驗證的Active Directory伺服器的完全限定主機名或IP地址。

**服務用戶：** 如果使用Active Directory 2003，則此值是為窗體中的服務主體建立的映射 `HTTP/<server name>`。 如果使用Active Directory 2008，則此值是服務主體的登錄ID。 例如，假定服務主體名為um spnego，用戶ID為spnegodemo，映射為HTTP/example.yourcompany.com。 使用Active Directory 2003，可將服務用戶設定為HTTP/example.yourcompany.com。 使用Active Directory 2008，可將「服務用戶」設定為spnegodemo。 （請參閱使用SPNEGO啟用SSO。）

**服務領域：** Active Directory的域名

**服務密碼：** 服務用戶密碼

**啟用SPNEGO:** 啟用SPNEGO用於單一登錄(SSO)。 （請參閱使用SPNEGO啟用SSO。）

### SAML設定 {#saml-settings}

如果您正在為企業域或混合域配置身份驗證並選擇SAML身份驗證，則以下設定可用。 有關其他SAML設定的資訊，請參見 [配置SAML服務提供程式設定](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)。

**請選擇要導入的SAML標識提供程式元資料檔案：** 按一下瀏覽以選擇從IDP生成的SAML標識提供程式元資料檔案，然後按一下導入。 將顯示來自IDP的詳細資訊。

**標題：** 由EntityID表示的URL的別名。 標題也顯示在企業和本地用戶的登錄頁上。

**Identity Provider支援客戶端基本身份驗證：** 當IDP使用SAML項目解析配置檔案時，將使用客戶端基本身份驗證。 在此配置檔案中，用戶管理將連接回在IDP上運行的Web服務，以檢索實際的SAML斷言。 IDP可能需要驗證。 如果IDP確實需要驗證，請選擇此選項，並在提供的框中指定用戶名和密碼。

**自定義屬性：** 允許您指定其他屬性。 附加屬性是由新行分隔的name=value對。

如果使用項目綁定，則需要以下自定義屬性。

* 添加以下自定義屬性以指定表示表單服務提供AEM程式的用戶名，該用戶名將用於向IDP項目解決服務進行身份驗證。
   `saml.idp.resolve.username=<username>`

* 添加以下自定義屬性以指定在中指定的用戶的口令 `saml.idp.resolve.username`。
   `saml.idp.resolve.password=<password>`

* 添加以下自定義屬性，以允許服務提供程式在通過SSL建立與項目解析服務的連接時忽略證書驗證。
   `saml.idp.resolve.ignorecert=true`

### 自定義設定 {#custom-settings}

如果要為企業域或混合域配置身份驗證並選擇自定義身份驗證，請選擇自定義身份驗證提供程式的名稱。

## 用戶的即時配置 {#just-in-time-provisioning-of-users}

在用戶通過身份驗證提供程式成功進行身份驗證後，即時設定會在用戶管理資料庫中自動建立用戶。 相關角色和組也動態地分配給新用戶。 您可以為企業域和混合域啟用即時資源調配。

此過程描述了傳統身份驗證在表單中的工AEM作方式：

1. 當用戶嘗試登錄表單時，AEM用戶管理會按順序將其憑據傳遞給所有可用的身份驗證提供程式。 （登錄憑據包括用戶名/密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供程式驗證憑據。
1. 然後，驗證提供程式檢查用戶是否存在於用戶管理資料庫中。 可能有以下狀態：

   **存在** 如果用戶是最新的且未鎖定，則用戶管理將返回驗證成功。 但是，如果用戶不是當前用戶或已鎖定用戶，則用戶管理將返回驗證失敗。

   **不存在** 用戶管理返回身份驗證失敗。

   **無效** 用戶管理返回身份驗證失敗。

1. 評估驗證提供程式返回的結果。 如果驗證提供程式返回驗證成功，則允許用戶登錄。 否則，「用戶管理」會與下一個身份驗證提供程式進行檢查（步驟2-3）。
1. 如果沒有可用的身份驗證提供程式驗證用戶憑據，則返回身份驗證失敗。

啟用即時設定後，如果其中一個身份驗證提供程式驗證其憑據，則會在用戶管理中動態建立新用戶。 （在上述步驟的步驟3之後。）

如果沒有及時預配，當用戶成功通過身份驗證但在用戶管理資料庫中找不到時，身份驗證將失敗。 即時預配在驗證過程中添加了一個步驟，以建立用戶並為用戶分配角色和組。

### 為域啟用即時配置 {#enable-just-in-time-provisioning-for-a-domain}

1. 編寫實現IdentityCreator和AssignmentProvider介面的服務容器。 (請參閱 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。)
1. 將服務容器部署到表單伺服器。
1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。

   選擇現有域，或按一下新建企業域。

1. 要建立域，請按一下「新建企業域」或「新建混合域」。 要編輯現有域，請按一下域的名稱。
1. 選擇「Enable Just In Time Provisioning（啟用及時預配）」。

   ***附註&#x200B;**:如果缺少「啟用及時預配」複選框，請按一下「首頁」>「設定」>「用戶管理」>「配置」>「高級系統屬性」，然後按一下「重新載入」。*

1. 添加身份驗證提供程式。 添加身份驗證提供程式時，在「新建身份驗證」螢幕上，選擇已註冊的身份建立者和分配提供程式。 (請參閱 [配置身份驗證提供程式](configuring-authentication-providers.md#configuring-authentication-providers)。)
1. 保存域。
