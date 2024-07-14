---
title: 為WebSphere Application Server設定SSL
description: 瞭解如何設定WebSphere Application Server的SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# 為WebSphere Application Server設定SSL {#configuring-ssl-for-websphere-application-server}

本節包含使用IBM WebSphere Application Server設定SSL的下列步驟。

## 在WebSphere上建立本機使用者帳戶 {#creating-a-local-user-account-on-websphere}

若要啟用SSL，WebSphere需要存取本機作業系統使用者登入中具有系統管理許可權的使用者帳戶：

* (Windows)建立屬於Administrators群組，並擁有做為作業系統一部分之許可權的Windows使用者。 （請參閱[為WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)建立Windows使用者。）
* (Linux、UNIX)使用者可以是root使用者或其他具有root許可權的使用者。 當您在WebSphere上啟用SSL時，請使用這個使用者的伺服器識別碼和密碼。

### 為WebSphere建立Linux或UNIX使用者 {#create-a-linux-or-unix-user-for-websphere}

1. 以根用戶用戶身分登入。
1. 通過在命令提示符下輸入以下命令來建立用戶：

   * （Linux 和 Sun Solaris） `useradd`
   * （IBM AIX） `mkuser`

1. 通過在命令提示符下輸入 `passwd` 來設置新用戶的密碼。
1. （Linux 和 Solaris）通過在命令提示符下輸入 `pwconv` （不帶參數）來建立影子密碼檔。

   >[!NOTE]
   >
   >（Linux 和 Solaris）要使 WebSphere Application Server Local OS 安全註冊表正常工作，必須存在影子密碼文件。 影子密碼文件通常名為 **/etc/shadow** ，並基於 /etc/passwd 文件。 如果影子密碼檔不存在，則在啟用全域安全性並將用戶註冊表配置為本地操作系統後會發生錯誤。

1. 在文本編輯者中從 /etc 目錄中打開群組文件。
1. 將您在步驟 2 `root` 中創建的用戶添加到群組。
1. 儲存並關閉檔案。
1. （啟用SSL的UNIX）以root使用者身分啟動和停止WebSphere。

### 為WebSphere建立Windows使用者 {#create-a-windows-user-for-websphere}

1. 使用系統管理員使用者帳戶登入Windows。
1. 選取&#x200B;**開始>控制檯>系統管理工具>電腦管理>本機使用者和群組**。
1. 用滑鼠右鍵按一下[使用者]並選取&#x200B;**新使用者**。
1. 在適當的方塊中輸入使用者名稱和密碼，並在其他方塊中輸入您需要的任何其他資訊。
1. 取消選取&#x200B;**使用者必須在下次登入時變更密碼**，按一下&#x200B;**建立**，然後按一下&#x200B;**關閉**。
1. 按一下&#x200B;**使用者**，用滑鼠右鍵按一下您建立的使用者並選取&#x200B;**內容**。
1. 按一下&#x200B;**的**&#x200B;成員標籤，然後按一下&#x200B;**新增**。
1. 在[輸入要選取的物件名稱]方塊中，輸入`Administrators`，按一下[檢查名稱]以確保群組名稱正確。
1. 按一下[確定]****，然後再按一下[確定]****。
1. 選取&#x200B;**開始>控制檯>系統管理工具>本機安全性原則>本機原則**。
1. 按一下「使用者許可權指派」，然後以滑鼠右鍵按一下「作為作業系統的一部分」，並選取「屬性」。
1. 按一下&#x200B;**新增使用者或群組**。
1. 在[輸入要選取的物件名稱]方塊中，輸入您在步驟4中建立的使用者名稱，按一下[檢查名稱]，確定名稱正確，然後按一下[確定]。****。****
1. 按一下&#x200B;**確定**，關閉作為作業系統內容對話方塊一部分的動作。

### 設定WebSphere以使用新建立的使用者作為管理員 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. 請確定WebSphere正在執行。
1. 在WebSphere管理主控台中，選取&#x200B;**安全性>全域安全性**。
1. 在管理安全性下，選取&#x200B;**管理使用者角色**。
1. 按一下「新增」並執行下列動作：

   1. 在搜尋方塊中輸入&#x200B;**&amp;amp；ast；**，然後按一下搜尋。
   1. 按一下角色底下的&#x200B;**管理員**。
   1. 將新建的使用者新增至對應至角色，並將其對應至管理員。

1. 按一下&#x200B;**確定**&#x200B;並儲存您的變更。
1. 重新啟動WebSphere設定檔。

## 啟用管理安全性 {#enable-administrative-security}

1. 在WebSphere管理主控台中，選取&#x200B;**安全性>全域安全性**。
1. 按一下&#x200B;**安全性設定精靈**。
1. 確定&#x200B;**啟用應用程式安全性**&#x200B;核取方塊已啟用。 按一下「**下一步**」。
1. 選取&#x200B;**同盟存放庫**&#x200B;並按一下&#x200B;**下一步**。
1. 指定您要設定的認證，然後按一下&#x200B;**下一步**。
1. 按一下&#x200B;**完成**。
1. 重新啟動WebSphere設定檔。

   WebSphere開始使用預設的金鑰存放區和信任存放區。

## 啟用SSL （自訂金鑰和信任庫） {#enable-ssl-custom-key-and-truststore}

信任存放區和金鑰存放區可以使用ikeyman公用程式或Admin Console來建立。 若要讓ikeyman正常運作，請確保WebSphere安裝路徑不包含括弧。

1. 在WebSphere管理主控台中，選取&#x200B;**安全性> SSL憑證和金鑰管理**。
1. 按一下「相關專案」下的&#x200B;**「金鑰存放區和憑證」**。
1. 在&#x200B;**金鑰存放區使用情況**&#x200B;下拉式清單中，確定已選取&#x200B;**SSL金鑰存放區**。 按一下&#x200B;**新增**。
1. 輸入邏輯名稱和說明。
1. 指定您要建立金鑰存放區的路徑。 如果您已透過ikeyman建立金鑰存放區，請指定金鑰存放區檔案的路徑。
1. 指定並確認密碼。
1. 選擇金鑰存放區型別並按一下&#x200B;**套用**。
1. 儲存主組態。
1. 按一下&#x200B;**個人憑證**。
1. 如果您已新增使用ikeyman建立的金鑰存放區，則會顯示您的憑證。 否則，您需要透過執行以下步驟來新增新的自我簽署憑證：

   1. 選擇 **建立 >自簽名證書**」。
   1. 在證書表單上指定適當的值。 確保將別名和公用名保留為計算機的完全限定功能變數名稱。
   1. 按一下「**套用**」。

1. 重複步驟 2 到 10 以創建信任庫。

## 將自訂金鑰庫和信任庫套用到伺服器 {#apply-custom-keystore-and-truststore-to-the-server}

1. 在 WebSphere 管理控制台中，選擇 **安全性> SSL 證書和密鑰管理**。
1. 按兩下管理 **端點安全配置**。 將打開本地拓撲圖。
1. 在“入站”下，選擇節點的直接子級。
1. 在「相關項」下，選擇「 **SSL 配置**」。
1. 選擇 **NodeDeafultSSLSetting**。
1. 從信任存放區名稱和金鑰存放區名稱下拉式清單中，選取您建立的自訂信任存放區和金鑰存放區。
1. 按一下「**套用**」。
1. 儲存主組態。
1. 重新啟動WebSphere設定檔。

   您的設定檔現在會在自訂SSL設定和您的憑證上執行。

## 啟用對AEM原生表單的支援 {#enabling-support-for-aem-forms-natives}

1. 在WebSphere管理主控台中，選取&#x200B;**安全性>全域安全性**。
1. 在[驗證]區段中，展開&#x200B;**RMI/IIOP安全性**&#x200B;並按一下&#x200B;**CSIv2輸入通訊**。
1. 確定已在[傳輸]下拉式清單中選取&#x200B;**SSL支援**。
1. 重新啟動WebSphere設定檔。

## 設定WebSphere以轉換以https開頭的URL {#configuring-websphere-to-convert-urls-that-begins-with-https}

若要轉換以https開頭的URL，請將該URL的簽署者憑證新增至WebSphere伺服器。

**為啟用https的網站建立簽署者憑證**

1. 請確定WebSphere正在執行。
1. 在WebSphere管理主控台中，瀏覽至簽署者憑證，然後按一下[安全性] > [SSL憑證和金鑰管理] > [金鑰存放區和憑證] > [NodeDefaultTrustStore] > [簽署者憑證]。
1. 按一下「從連線埠擷取」，然後執行下列工作：

   * 在「主機」方塊中，輸入URL。 例如，型別`www.paypal.com`。
   * 在[連線埠]方塊中，輸入`443`。 此連線埠是預設的SSL連線埠。
   * 在「別名」方塊中，鍵入別名。

1. 按一下「擷取簽署者資訊」，然後確認已擷取資訊。
1. 按一下套用，然後按一下儲存。

從已新增憑證的網站進行HTML至PDF的轉換，現在可以在產生PDF服務中運作。

>[!NOTE]
>
>應用程式若要從WebSphere內部連線至SSL網站，需要簽署者憑證。 Java Secure Socket Extensions (JSSE)會使用它來驗證連線的遠端端在SSL交握期間傳送的憑證。

## 設定動態連線埠 {#configuring-dynamic-ports}

啟用「全域安全性」時，IBM WebSphere不允許對ORB.init()進行多次呼叫。 您可以在https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704閱讀永久限制的相關資訊。

執行以下步驟，將連線埠設定為動態並解決問題：

1. 在WebSphere管理主控台中，選取&#x200B;**伺服器** > **伺服器型別** > **WebSphere應用程式伺服器**。
1. 在「偏好設定」區段中，選取您的伺服器。
1. 在&#x200B;**組態**&#x200B;標籤的&#x200B;**通訊**&#x200B;區段下，展開&#x200B;**連線埠**，然後按一下&#x200B;**詳細資料**。
1. 按一下下列連線埠名稱，將&#x200B;**連線埠號碼**&#x200B;變更為0，然後按一下&#x200B;**確定**。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## 設定sling.properties檔案 {#configure-the-sling-properties-file}

1. 開啟`[aem-forms_root]`\crx-repository\launchpad\sling.properties檔案以進行編輯。
1. 找到`sling.bootdelegation.ibm`屬性，並將`com.ibm.websphere.ssl.*`新增至其值欄位。 更新的欄位如下所示：

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 儲存檔案並重新啟動伺服器。
