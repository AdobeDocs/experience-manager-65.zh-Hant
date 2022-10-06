---
title: 為WebSphere應用程式伺服器配置SSL
seo-title: Configuring SSL for WebSphere Application Server
description: 了解如何為WebSphere應用程式伺服器配置SSL。
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# 為WebSphere應用程式伺服器配置SSL {#configuring-ssl-for-websphere-application-server}

本節包含下列步驟，以使用您的IBM WebSphere應用程式伺服器設定SSL。

## 在WebSphere上建立本地用戶帳戶 {#creating-a-local-user-account-on-websphere}

要啟用SSL,WebSphere需要訪問本地OS用戶註冊表中有權管理系統的用戶帳戶：

* (Windows)建立新的Windows用戶，該用戶屬於「管理員」組，並有權作為作業系統的一部分。 (請參閱 [為WebSphere建立Windows用戶](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux、UNIX)該用戶可以是根用戶，也可以是具有根權限的其他用戶。 在WebSphere上啟用SSL時，請使用此用戶的伺服器標識和密碼。

### 為WebSphere建立Linux或UNIX用戶 {#create-a-linux-or-unix-user-for-websphere}

1. 以根使用者身分登入。
1. 在命令提示符中輸入以下命令以建立用戶：

   * （Linux和Sun Solaris） `useradd`
   * (IBM AIX) `mkuser`

1. 通過輸入 `passwd` 在命令提示符中。
1. （Linux和Solaris）通過輸入 `pwconv` （沒有參數）。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere應用程式伺服器本地OS安全註冊表工作，必須存在卷影密碼檔案。 卷影密碼檔案通常名為 **/etc/shadow** 和以/etc/passwd檔案為基礎。 如果卷影密碼檔案不存在，則啟用全局安全並將用戶註冊表配置為本地作業系統後，將發生錯誤。

1. 在文本編輯器中從/etc目錄開啟組檔案。
1. 將您在步驟2建立的使用者新增至 `root` 群組。
1. 儲存並關閉檔案。
1. （啟用SSL的UNIX）啟動和停止WebSphere作為根用戶。

### 為WebSphere建立Windows用戶 {#create-a-windows-user-for-websphere}

1. 使用管理員用戶帳戶登錄到Windows。
1. 選擇 **「開始」>「控制面板」>「管理工具」>「電腦管理」>「本地用戶和組」**.
1. 按一下右鍵用戶並選擇 **新用戶**.
1. 在相應的框中鍵入用戶名和密碼，並在其餘框中鍵入您需要的任何其他資訊。
1. 取消選擇 **使用者必須在下次登入時變更密碼**，按一下 **建立**，然後按一下 **關閉**.
1. 按一下 **使用者**，按一下右鍵您剛建立的用戶並選擇 **屬性**.
1. 按一下 **成員** ，然後按一下 **新增**.
1. 在「輸入要選擇的對象名稱」(Enter The Object Names To Select)框中，鍵入 `Administrators`，按一下「檢查名稱」 ，確保群組名稱正確無誤。
1. 按一下 **確定** 然後按一下 **確定** 。
1. 選擇 **「開始」>「控制面板」>「管理工具」>「本地安全策略」>「本地策略」**.
1. 按一下「用戶權限分配」，然後按一下右鍵「作為作業系統的一部分」，然後選擇「屬性」。
1. 按一下 **新增使用者或群組**.
1. 在輸入要選擇的對象名稱框中，鍵入您在步驟4中建立的用戶的名稱，按一下 **檢查名稱** 以確保名稱正確，然後按一下 **確定**.
1. 按一下 **確定** 關閉作為作業系統屬性對話框的一部分。

### 配置WebSphere以將新建立的用戶用作管理員 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，選擇 **安全性>全球安全性**.
1. 在「管理安全」下，選擇 **管理使用者角色**.
1. 按一下「新增」 ，然後執行下列動作：

   1. 類型 **&amp;ast;** 在「搜索」框中，按一下「搜索」。
   1. 按一下 **管理員** 在角色下。
   1. 將新建立的用戶添加到「已映射到」角色，並將其映射到「管理員」。

1. 按一下 **確定** 並儲存您的變更。
1. 重新啟動WebSphere配置檔案。

## 啟用管理安全 {#enable-administrative-security}

1. 在WebSphere管理控制台中，選擇 **安全性>全球安全性**.
1. 按一下 **安全配置嚮導**.
1. 確保 **啟用應用程式安全性** 核取方塊已啟用。 按一下&#x200B;**下一步**。
1. 選擇 **聯合儲存庫** 按一下 **下一個**.
1. 指定您要設定的憑證，然後按一下 **下一個**.
1. 按一下 **完成**.
1. 重新啟動WebSphere配置檔案。

   WebSphere將開始使用預設密鑰庫和信任儲存。

## 啟用SSL（自訂金鑰和信任存放區） {#enable-ssl-custom-key-and-truststore}

可使用ikeyman公用程式或管理控制台來建立信任存放區和鑰匙存放區。 要使ikeyman正常工作，請確保WebSphere安裝路徑不包含括弧。

1. 在WebSphere管理控制台中，選擇 **安全性> SSL憑證和金鑰管理**.
1. 按一下 **鑰匙存放區和憑證** 在「相關項目」下。
1. 在 **金鑰存放區使用方式** 下拉式清單，確定 **SSL密鑰庫** 中所有規則的URL。 按一下 **新增**.
1. 輸入邏輯名稱和說明。
1. 指定要建立金鑰存放區的路徑。 如果已通過ikeyman建立密鑰庫，請指定密鑰庫檔案的路徑。
1. 指定並確認密碼。
1. 選擇金鑰存放區類型，然後按一下 **套用**.
1. 保存主配置。
1. 按一下 **個人證書**.
1. 如果您已使用ikeyman新增金鑰存放區，則會顯示憑證。 否則，您需要執行下列步驟來新增自行簽署的憑證：

   1. 選擇 **建立>自簽名證書**.
   1. 在憑證表單上指定適當的值。 請確保將別名和公用名稱保留為電腦的完全限定域名。
   1. 按一下 **套用**.

1. 重複步驟2到10以建立信任存放區。

## 將自定義密鑰庫和信任儲存應用於伺服器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，選擇 **安全性> SSL憑證和金鑰管理**.
1. 按一下 **管理端點安全配置**. 本地拓撲圖開啟。
1. 在入站下，選擇節點的直接子節點。
1. 在「相關項目」下，選擇 **SSL設定**.
1. 選擇 **NodeDefaultSSLSetting**.
1. 從truststore名稱和金鑰存放區名稱下拉式清單中，選取您建立的自訂truststore和金鑰存放區。
1. 按一下 **套用**.
1. 保存主配置。
1. 重新啟動WebSphere配置檔案。

   您的設定檔現在會在自訂SSL設定和憑證上執行。

## 啟用對AEM表單原生代的支援 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理控制台中，選擇 **安全性>全球安全性**.
1. 在驗證區段中，展開 **RMI/IIOP安全性** 按一下 **CSIv2入站通信**.
1. 確保 **SSL支援** 在「傳輸」下拉式清單中選取。
1. 重新啟動WebSphere配置檔案。

## 設定WebSphere以轉換以https開頭的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

若要轉換以https開頭的URL，請為該URL新增簽署者憑證至WebSphere伺服器。

**為啟用https的網站建立簽署者憑證**

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，導航到簽署者證書，然後按一下「安全」>「SSL證書和密鑰管理」>「密鑰儲存和證書」>「NodeDefaultTrustStore」>「簽署者證書」。
1. 按一下「從埠檢索」並執行以下任務：

   * 在「主機」方塊中，輸入URL。 例如，輸入 `www.paypal.com`.
   * 在「Port（埠）」框中，鍵入 `443`. 此埠是預設的SSL埠。
   * 在「別名」框中，鍵入別名。

1. 按一下「檢索簽名者資訊」 ，然後驗證是否檢索了該資訊。
1. 按一下「套用」 ，然後按一下「儲存」 。

從已新增憑證的網站進行HTML對PDF轉換，現在可從「產生PDF」服務運作。

>[!NOTE]
>
>若要讓應用程式從WebSphere內連線至SSL網站，需要簽署者憑證。 Java安全套接字擴展(JSSE)使用它來驗證在SSL握手期間發送的連接的遠程端的證書。

## 配置動態埠 {#configuring-dynamic-ports}

IBM WebSphere在啟用全域安全性時不允許對ORB.init()進行多次呼叫。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704閱讀永久限制的相關資訊。

執行下列步驟將埠設定為動態並解決問題：

1. 在WebSphere管理控制台中，選擇 **伺服器** > **伺服器類型** > **WebSphere應用程式伺服器**.
1. 在「首選項」部分，選擇伺服器。
1. 在 **設定** 標籤下 **通訊** 區段，展開 **埠**，然後按一下 **詳細資料**.
1. 按一下以下埠名稱，更改 **埠號** 設為0，然後按一下 **確定**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 設定sling.properties檔案 {#configure-the-sling-properties-file}

1. 開啟 `[aem-forms_root]`\crx-repository\launchpad\sling.properties檔案進行編輯。
1. 找出 `sling.bootdelegation.ibm` 屬性和新增 `com.ibm.websphere.ssl.*`至其值欄位。 更新後的欄位如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 儲存檔案並重新啟動伺服器。
