---
title: 為WebSphere應用程式伺服器配置SSL
seo-title: 為WebSphere應用程式伺服器配置SSL
description: 瞭解如何為WebSphere應用程式伺服器設定SSL。
seo-description: 瞭解如何為WebSphere應用程式伺服器設定SSL。
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---


# 為WebSphere應用程式伺服器配置SSL {#configuring-ssl-for-websphere-application-server}

本節包含以下步驟，以便使用IBM WebSphere Application Server配置SSL。

## 在WebSphere上建立本地用戶帳戶{#creating-a-local-user-account-on-websphere}

要啟用SSL,WebSphere需要訪問本地OS用戶註冊表中有權管理系統的用戶帳戶：

* (Windows)建立屬於「管理員」群組的新Windows使用者，並具有作為作業系統一部分的權限。 （請參閱[建立WebSphere的Windows使用者](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)）。
* (Linux、UNIX)用戶可以是root用戶，也可以是具有root權限的其他用戶。 在WebSphere上啟用SSL時，請使用此用戶的伺服器標識和密碼。

### 為WebSphere {#create-a-linux-or-unix-user-for-websphere}建立Linux或UNIX用戶

1. 以root用戶身份登錄。
1. 在命令提示符下輸入以下命令以建立用戶：

   * （Linux和Sun Solaris）`useradd`
   * (IBM AIX)`mkuser`

1. 通過在命令提示符下輸入`passwd`來設定新用戶的口令。
1. （Linux和Solaris）通過在命令提示符下輸入`pwconv`（無參數）來建立卷影口令檔案。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere Application Server本地OS安全註冊表工作，卷影密碼檔案必須存在。 卷影密碼檔案通常名為&#x200B;**/etc/shadow** ，並基於/etc/passwd檔案。 如果卷影密碼檔案不存在，則在啟用全局安全性並將用戶註冊表配置為本地作業系統後會發生錯誤。

1. 在文本編輯器中從/etc目錄開啟組檔案。
1. 將您在步驟2中建立的使用者新增至`root`群組。
1. 儲存並關閉檔案。
1. （啟用SSL的UNIX）以root用戶身份啟動和停止WebSphere。

### 為WebSphere {#create-a-windows-user-for-websphere}建立Windows用戶

1. 使用管理員使用者帳戶登入Windows。
1. 選擇&#x200B;**開始>控制面板>管理工具>電腦管理>本地用戶和組**。
1. 按一下右鍵用戶，然後選擇&#x200B;**新建用戶**。
1. 在適當的方塊中輸入使用者名稱和密碼，並在其他方塊中輸入您需要的任何其他資訊。
1. 取消選擇&#x200B;**「使用者必須在下次登入時變更密碼」**，按一下「建立&#x200B;**」，然後按一下「關閉**」。****
1. 按一下&#x200B;**Users** ，按一下右鍵剛建立的用戶，然後選擇&#x200B;**Properties**。
1. 按一下&#x200B;**成員Of**&#x200B;頁籤，然後按一下&#x200B;**添加**。
1. 在輸入要選擇的對象名稱框中，鍵入`Administrators` ，按一下檢查名稱以確保組名稱正確。
1. 按一下&#x200B;**OK** ，然後再次按一下&#x200B;**OK**。
1. 選擇&#x200B;**開始>控制面板>管理工具>本地安全策略>本地策略**。
1. 按一下「使用者權限指派」，然後以滑鼠右鍵按一下「作為作業系統的一部分」，並選取「屬性」。
1. 按一下&#x200B;**添加用戶或組**。
1. 在「輸入要選擇的對象名稱」框中，鍵入在步驟4中建立的用戶名稱，按一下「檢查名稱」(Check Names)**以確保名稱正確，然後按一下「確定」(OK)**。****
1. 按一下&#x200B;**確定**&#x200B;以關閉作為作業系統屬性對話框一部分的操作。

### 將WebSphere配置為將新建立的用戶作為管理員{#configure-websphere-to-use-the-newly-created-user-as-administrator}使用

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，選擇&#x200B;**安全性>全域安全性**。
1. 在「管理安全性」下，選擇&#x200B;**管理用戶角色**。
1. 按一下「新增」並執行下列動作：

   1. 在搜索框中鍵入&#x200B;**&amp;ast;** ，然後按一下搜索。
   1. 按一下角色下的&#x200B;**管理員**。
   1. 將新建立的用戶添加到映射到角色，並將其映射到管理員。

1. 按一下&#x200B;**確定**&#x200B;並保存更改。
1. 重新啟動WebSphere描述檔。

## 啟用管理安全性{#enable-administrative-security}

1. 在WebSphere管理控制台中，選擇&#x200B;**安全性>全域安全性**。
1. 按一下&#x200B;**安全配置嚮導**。
1. 確保&#x200B;**啟用應用程式安全**&#x200B;複選框已啟用。 按一下&#x200B;**下一步**。
1. 選擇&#x200B;**聯合資料庫** ，然後按一下&#x200B;**Next**。
1. 指定要設定的憑據，然後按一下&#x200B;**Next**。
1. 按一下&#x200B;**完成**。
1. 重新啟動WebSphere描述檔。

   WebSphere將開始使用預設密鑰庫和信任儲存。

## 啟用SSL（自訂金鑰和信任庫）{#enable-ssl-custom-key-and-truststore}

您可以使用ikeyman公用程式或管理控制台來建立信任庫和keystore。 要使ikeyman正常運作，請確保WebSphere安裝路徑不包含括弧。

1. 在WebSphere管理控制台中，選擇&#x200B;**安全> SSL證書和密鑰管理**。
1. 按一下「相關項目」下方的「鑰匙圈和憑證」。****
1. 在&#x200B;**Key store usages**&#x200B;下拉式清單中，請確定已選取&#x200B;**SSL Keystores**。 按一下&#x200B;**新建**。
1. 鍵入邏輯名稱和說明。
1. 指定要在其中建立密鑰庫的路徑。 如果已通過ikeyman建立密鑰庫，請指定密鑰庫檔案的路徑。
1. 指定並確認密碼。
1. 選擇密鑰庫類型，然後按一下&#x200B;**Apply**。
1. 保存主配置。
1. 按一下&#x200B;**個人證書**。
1. 如果您已使用ikeyman新增已建立密鑰庫，則會出現憑證。 否則，您需要執行下列步驟來新增自簽證：

   1. 選擇&#x200B;**「建立」>「自簽名證書」**。
   1. 在憑證表單上指定適當的值。 確保將別名和公用名稱保留為電腦的完全限定域名。
   1. 按一下&#x200B;**Apply**。

1. 重複步驟2到10以建立信任庫。

## 將自定義密鑰庫和信任儲存應用到伺服器{#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，選擇&#x200B;**安全> SSL證書和密鑰管理**。
1. 按一下&#x200B;**管理端點安全配置**。 本地拓撲圖開啟。
1. 在「入站」下，選擇節點的直接子項。
1. 在「相關項目」下，選擇&#x200B;**SSL配置**。
1. 選擇&#x200B;**NodeDefaultSSLSetting**。
1. 從truststore名稱和keystore名稱下拉式清單中，選取您建立的自訂truststore和keystore。
1. 按一下&#x200B;**Apply**。
1. 保存主配置。
1. 重新啟動WebSphere描述檔。

   您的設定檔現在會在自訂SSL設定和憑證上執行。

## 啟用AEM表單原生代的支援{#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理控制台中，選擇&#x200B;**安全性>全域安全性**。
1. 在「驗證」部分中，展開&#x200B;**RMI/IIOP security** ，然後按一下&#x200B;**CSIv2入站通信**。
1. 確保在「傳輸」下拉清單中選擇了&#x200B;**SSL支援**。
1. 重新啟動WebSphere描述檔。

## 設定WebSphere以轉換以https {#configuring-websphere-to-convert-urls-that-begins-with-https}開頭的URL

若要轉換以https開頭的URL，請將該URL的簽署者憑證新增至WebSphere伺服器。

**為啟用https的網站建立簽署者憑證**

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，導覽至簽署者憑證，然後按一下「安全性> SSL憑證和金鑰管理>金鑰存放區和憑證> NodeDefaultTrustStore >簽署者憑證」。
1. 按一下「從埠檢索」並執行以下任務：

   * 在「主機」方塊中，輸入URL。 例如，鍵入`www.paypal.com`。
   * 在「Port（埠）」框中，鍵入`443`。 此埠是預設的SSL埠。
   * 在「別名」框中，鍵入別名。

1. 按一下「擷取簽署者資訊」，然後確認已擷取該資訊。
1. 按一下「套用」，然後按一下「儲存」。

從新增認證的網站轉換HTML至PDF，現在可從「產生PDF」服務運作。

>[!NOTE]
>
>若要從WebSphere內部連線至SSL網站的應用程式，則需要簽署者憑證。 Java安全套接字擴展(JSSE)使用它來驗證在SSL握手期間發送的連接遠程端的證書。

## 配置動態埠{#configuring-dynamic-ports}

IBM WebSphere不允許在啟用「全域安全性」時對ORB.init()進行多次呼叫。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704上閱讀永久限制的相關資訊。

執行以下步驟將埠設定為動態並解決問題：

1. 在WebSphere管理控制台中，選擇&#x200B;**Servers** > **Server Types** > **WebSphere應用程式伺服器**。
1. 在「首選項」部分，選擇您的伺服器。
1. 在&#x200B;**Configuration**&#x200B;頁籤的&#x200B;**Communications**&#x200B;部分下，展開&#x200B;**Ports** ，然後按一下&#x200B;**Details**。
1. 按一下以下埠名稱，將&#x200B;**埠號**&#x200B;更改為0，然後按一下&#x200B;**確定**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 設定sling.properties檔案{#configure-the-sling-properties-file}

1. 開啟`[aem-forms_root]`\crx-repository\launchpad\sling.properties檔案以進行編輯。
1. 找到`sling.bootdelegation.ibm`屬性，並將`com.ibm.websphere.ssl.*`新增至其值欄位。 更新的欄位如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 保存檔案並重新啟動伺服器。

