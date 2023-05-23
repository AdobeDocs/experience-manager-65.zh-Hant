---
title: 為WebSphere應用程式伺服器配置SSL
seo-title: Configuring SSL for WebSphere Application Server
description: 瞭解如何為WebSphere應用程式伺服器配置SSL。
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

本節包括以下步驟，以便使用您的IBMWebSphere應用程式伺服器配置SSL。

## 在WebSphere上建立本地用戶帳戶 {#creating-a-local-user-account-on-websphere}

要啟用SSL,WebSphere需要訪問本地作業系統用戶註冊表中具有管理系統權限的用戶帳戶：

* (Windows)建立新的Windows用戶，該用戶是Administrators組的一部分，並具有作為作業系統一部分的權限。 (請參閱 [為WebSphere建立Windows用戶](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)。)
* (Linux, UNIX)用戶可以是根用戶，也可以是具有根權限的其他用戶。 在WebSphere上啟用SSL時，請使用此用戶的伺服器標識和密碼。

### 為WebSphere建立Linux或UNIX用戶 {#create-a-linux-or-unix-user-for-websphere}

1. 以根用戶身份登錄。
1. 在命令提示符下輸入以下命令建立用戶：

   * （Linux和Sun Solaris） `useradd`
   * (IBM艾克斯) `mkuser`

1. 通過輸入 `passwd` 的子菜單。
1. （Linux和Solaris）通過輸入 `pwconv` （沒有參數）。

   >[!NOTE]
   >
   >（Linux和Solaris）要使WebSphere Application Server本地OS安全註冊表工作，必須存在卷影密碼檔案。 卷影密碼檔案通常被命名 **/etc/陰影** 並基於/etc/passwd檔案。 如果卷影密碼檔案不存在，則在啟用全局安全並將用戶註冊表配置為本地OS後將發生錯誤。

1. 在文本編輯器中從/etc目錄開啟組檔案。
1. 將您在步驟2中建立的用戶添加到 `root` 組。
1. 保存並關閉檔案。
1. （啟用SSL的UNIX）以根用戶身份啟動和停止WebSphere。

### 為WebSphere建立Windows用戶 {#create-a-windows-user-for-websphere}

1. 使用管理員用戶帳戶登錄Windows。
1. 選擇 **開始>控制面板>管理工具>電腦管理>本地用戶和組**。
1. 按一下右鍵用戶並選擇 **新用戶**。
1. 在相應的框中鍵入用戶名和密碼，並在其餘框中鍵入所需的任何其他資訊。
1. 取消選擇 **用戶必須在下次登錄時更改密碼**&#x200B;按一下 **建立**，然後按一下 **關閉**。
1. 按一下 **用戶**，按一下右鍵您剛建立的用戶，然後選擇 **屬性**。
1. 按一下 **成員** 按鈕 **添加**。
1. 在「輸入要選擇的對象名稱」(Enter the Object Names To Select)框中，鍵入 `Administrators`，按一下「檢查名稱」(Check Names)以確保組名正確。
1. 按一下 **確定** 然後按一下 **確定** 的雙曲餘切值。
1. 選擇 **「開始」>「控制面板」>「管理工具」>「本地安全策略」>「本地策略」**。
1. 按一下「用戶權限分配」，然後按一下右鍵「作為作業系統的一部分」並選擇「屬性」。
1. 按一下 **添加用戶或組**。
1. 在「輸入要選擇的對象名稱」(Enter The Object Names To Select)框中，鍵入您在步驟4中建立的用戶名稱，按一下 **檢查名稱** 以確保名稱正確，然後按一下 **確定**。
1. 按一下 **確定** 關閉「作為作業系統屬性」對話框的一部分。

### 將WebSphere配置為將新建立的用戶用作管理員 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，選擇 **安全性>全局安全性**。
1. 在「管理安全」下，選擇 **管理用戶角色**。
1. 按一下「添加」(Add)，然後執行以下操作：

   1. 類型 **&amp;ast;** ，然後按一下「搜索」。
   1. 按一下 **管理員** 的子菜單。
   1. 將新建立的用戶添加到映射到角色，並將其映射到管理員。

1. 按一下 **確定** 並保存更改。
1. 重新啟動WebSphere配置檔案。

## 啟用管理安全性 {#enable-administrative-security}

1. 在WebSphere管理控制台中，選擇 **安全性>全局安全性**。
1. 按一下 **安全配置嚮導**。
1. 確保 **啟用應用程式安全性** 複選框。 按一下&#x200B;**下一步**。
1. 選擇 **聯合資料庫** 按一下 **下一個**。
1. 指定要設定的憑據，然後按一下 **下一個**。
1. 按一下 **完成**。
1. 重新啟動WebSphere配置檔案。

   WebSphere將開始使用預設密鑰庫和信任儲存。

## 啟用SSL（自定義密鑰和信任儲存） {#enable-ssl-custom-key-and-truststore}

可以使用ikeyman實用程式或管理控制台建立信任儲存和密鑰儲存。 要使ikeyman正常工作，請確保WebSphere安裝路徑不包含括弧。

1. 在WebSphere管理控制台中，選擇 **安全性> SSL證書和密鑰管理**。
1. 按一下 **密鑰庫和證書** 的下界。
1. 在 **密鑰儲存用法** 下拉清單，確保 **SSL密鑰庫** 的子菜單。 按一下 **新建**。
1. 鍵入邏輯名稱和說明。
1. 指定要建立密鑰庫的路徑。 如果已通過ikeyman建立密鑰庫，請指定密鑰庫檔案的路徑。
1. 指定並確認密碼。
1. 選擇密鑰庫類型，然後按一下 **應用**。
1. 保存主配置。
1. 按一下 **個人證書**。
1. 如果已使用ikeyman添加了已建立密鑰庫的密鑰庫，則將顯示您的證書。 否則，您需要通過執行以下步驟添加新的自簽名證書：

   1. 選擇 **建立>自簽名證書**。
   1. 在證書窗體上指定相應的值。 確保將別名和公用名稱保留為電腦的完全限定域名。
   1. 按一下 **應用**。

1. 重複步驟2至10以建立信任儲存。

## 將自定義密鑰庫和信任儲存應用於伺服器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在WebSphere管理控制台中，選擇 **安全性> SSL證書和密鑰管理**。
1. 按一下 **管理終結點安全配置**。 本地拓撲圖開啟。
1. 在「入站」下，選擇節點的直接子級。
1. 在「相關項目」下，選擇 **SSL配置**。
1. 選擇 **節點預設SSLSetting**。
1. 從truststore名稱和密鑰庫名稱下拉清單中，選擇您建立的自定義信任儲存和密鑰庫。
1. 按一下 **應用**。
1. 保存主配置。
1. 重新啟動WebSphere配置檔案。

   您的配置檔案現在在自定義SSL設定和證書上運行。

## 支援本地AEM表格 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理控制台中，選擇 **安全性>全局安全性**。
1. 在「驗證」部分，展開 **RMI/IIOP安全** 按一下 **CSIv2入站通信**。
1. 確保 **支援SSL** 在「傳輸」下拉清單中選擇。
1. 重新啟動WebSphere配置檔案。

## 配置WebSphere以轉換以https開頭的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

要轉換以https開頭的URL，請將該URL的簽名者證書添加到WebSphere伺服器。

**為啟用https的站點建立簽名者證書**

1. 確保WebSphere正在運行。
1. 在WebSphere管理控制台中，導航到簽名者證書，然後按一下「安全性」>「SSL證書和密鑰管理」>「密鑰儲存和證書」>「節點預設信任儲存」>「簽名者證書」。
1. 按一下「從埠檢索」並執行以下任務：

   * 在「主機」框中，鍵入URL。 例如，鍵入 `www.paypal.com`。
   * 在「Port（埠）」框中，鍵入 `443`。 此埠是預設SSL埠。
   * 在「別名」框中，鍵入別名。

1. 按一下「檢索簽名者資訊」(Retrieve Signer Information)，然後驗證是否檢索了該資訊。
1. 按一下「Apply（應用）」 ，然後按一下「Save（保存）」。

添加證書的站點的HTML到PDF轉換現在將通過生成PDF服務工作。

>[!NOTE]
>
>要使應用程式從WebSphere內部連接到SSL站點，需要簽名者證書。 Java安全套接字擴展(JSSE)使用它來驗證在SSL握手期間連接的遠程端發送的證書。

## 配置動態埠 {#configuring-dynamic-ports}

IBMWebSphere不允許在啟用全局安全時對ORB.init()進行多次調用。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704上閱讀有關永久限制的資訊。

執行以下步驟將埠設定為動態並解決問題：

1. 在WebSphere管理控制台中，選擇 **伺服器** > **伺服器類型** > **WebSphere應用程式伺服器**。
1. 在「首選項」部分，選擇伺服器。
1. 在 **配置** 頁籤 **通信** 部分，展開 **埠**，然後按一下 **詳細資訊**。
1. 按一下以下埠名，更改 **埠號** 到0，然後按一下 **確定**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 配置sling.properties檔案 {#configure-the-sling-properties-file}

1. 開啟 `[aem-forms_root]`\crx-repository\launchpad\sling.properties檔案進行編輯。
1. 查找 `sling.bootdelegation.ibm` 屬性和添加 `com.ibm.websphere.ssl.*`值欄位。 更新後的欄位如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 儲存檔案並重新啟動伺服器。
