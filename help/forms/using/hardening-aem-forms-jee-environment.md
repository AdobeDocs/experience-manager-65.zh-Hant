---
title: 在JEE環境中強化AEM Forms
description: 瞭解各種安全性強化設定，以增強在公司內部網路中執行的JEE上的AEM Forms安全性。
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '7608'
ht-degree: 1%

---

# 在JEE環境中強化AEM Forms {#hardening-your-aem-forms-on-jee-environment}

瞭解各種安全性強化設定，以增強在公司內部網路中執行的JEE上的AEM Forms安全性。

本文會說明保護伺服器安全的建議與最佳實務，這些伺服器會在JEE上執行AEM Forms。 這不是針對您的作業系統和應用程式伺服器的完整主機強化檔案。 本文改為說明各種安全性強化設定，您應實作這些設定以增強在公司內部網路中執行的JEE上的AEM Forms安全性。 不過，為了確保JEE應用程式伺服器上的AEM Forms保持安全，您也應該實作安全性監控、偵測和回應程式。

本文說明在下列階段中，安裝及組態生命週期期間應套用的強化技術：

* **預先安裝：** 在JEE上安裝AEM Forms前，請先運用這些技術。
* **安裝：** 在AEM Forms on JEE安裝程式中使用這些技術。
* **安裝後：** 安裝後及之後定期使用這些技巧。

JEE上的AEM Forms可高度自訂，可在許多不同的環境中運作。 部分建議可能不符合您組織的需求。

## 預先安裝 {#preinstallation}

在JEE上安裝AEM Forms之前，您可以將安全性解決方案套用至網路層和作業系統。 本節說明一些問題，並提出減少這些區域安全性弱點的建議。

**在UNIX和Linux上的安裝和設定**

您不應使用根殼層在JEE上安裝或設定AEM Forms。 依預設，檔案會安裝在/opt目錄下，而執行安裝的使用者需要/opt下的所有檔案許可權。 或者，也可以在個別使用者的/user目錄下執行安裝，該目錄下使用者已經擁有所有檔案許可權。

**在Windows上的安裝和設定**

如果您在JBoss上的JEE上使用turnkey方法安裝AEM Forms或安裝PDF Generator，您應該以管理員身分在Windows上執行安裝。 此外，在具有原生應用程式支援的Windows上安裝PDF Generator時，您必須以安裝Microsoft Office的同一Windows使用者身分執行安裝。 如需有關安裝許可權的詳細資訊，請參閱*在JEE上安裝和部署AEM Forms*檔案，以瞭解您的應用程式伺服器。

### 網路層安全性 {#network-layer-security}

網路安全漏洞是任何面對網際網路或面對內部網路的應用程式伺服器所面臨的首要威脅之一。 本節說明針對這些弱點強化網路上主機的程式。 它可處理網路細分、傳輸控制通訊協定/網際網路通訊協定(TCP/IP)棧疊強化，以及使用防火牆保護主機等問題。

下表說明減少網路安全漏洞的常見程式。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非軍事區域(DMZ)</p> </td> 
   <td><p>在非軍事區域(DMZ)中部署Forms伺服器。 區段應至少存在於兩個層級，而且用於在JEE上執行AEM Forms的應用程式伺服器應置於內部防火牆之後。 將外部網路與包含Web伺服器的DMZ分開，而後者則必須與內部網路分開。 使用防火牆來實作分隔層。 將流經每個網路層的流量分類並加以控制，確保只允許絕對最低必要資料。</p> </td> 
  </tr> 
  <tr> 
   <td><p>私人IP位址</p> </td> 
   <td><p>在AEM Forms應用程式伺服器上使用網路位址轉譯(NAT)搭配RFC 1918私人IP位址。 指派私人IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，讓攻擊者更難以透過網際網路路由往來於NAT的內部主機的流量。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火牆</p> </td> 
   <td><p>請使用下列條件來選取防火牆解決方案：</p> 
    <ul> 
     <li><p>實作支援Proxy伺服器的防火牆及/或 <em>狀態檢查</em> 而不是簡單的封包篩選解決方案。</p> </li> 
     <li><p>使用支援 <em>拒絕所有服務，但明確允許的除外</em> 安全性範例。</p> </li> 
     <li><p>實作雙主機或多主機防火牆解決方案。 此架構提供最高層級的安全性，並有助於防止未經授權的使用者繞過防火牆安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>資料庫連線埠</p> </td> 
   <td><p>請勿使用資料庫的預設監聽連線埠(MySQL - 3306、Oracle- 1521、MS SQL - 1433)。 如需有關變更資料庫連線埠的資訊，請參閱您的資料庫檔案。</p> <p>使用不同的資料庫連線埠會影響JEE設定的整體AEM Forms。 如果您變更預設連線埠，則必須在設定的其他區域進行對應的修改，例如JEE上AEM Forms的資料來源。</p> <p>如需有關在JEE上設定AEM Forms資料來源的資訊，請參閱在JEE上安裝和升級AEM Forms，或在JEE上升級至您的應用程式伺服器的AEM Forms ，網址為 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms使用手冊</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 作業系統安全性 {#operating-system-security}

下表說明將作業系統中發現的安全性弱點降至最低的一些可能方法。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p></th> 
   <th><p>說明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全性修補程式</p></td> 
   <td><p>如果未及時套用廠商安全性修補程式和升級，未經授權的使用者可能會取得應用程式伺服器的存取權，此風險會增加。 請先測試安全性修補程式，再將其套用至生產伺服器。</p><p>此外，建立原則和程式，以定期檢查並安裝修補程式。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防護軟體</p></td> 
   <td><p>病毒掃描程式可透過掃描簽名或監視異常行為來識別受感染的檔案。 掃描器會將病毒簽章儲存在檔案中，檔案通常儲存在本機硬碟上。 因為經常會發現新的病毒，所以您應該經常更新這個檔案，讓病毒掃描程式識別所有目前的病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>網路時間通訊協定(NTP)</p></td> 
   <td><p>為了進行鑑證分析，請務必在表單伺服器上保持準確的時間。 使用NTP同步所有直接連線到網際網路的系統上的時間。</p></td> 
  </tr> 
 </tbody> 
</table>

如需作業系統的其他安全性資訊，請參閱 [作業系統安全性資訊](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## 安裝 {#installation}

本節說明在AEM Forms安裝程式期間可用來減少安全漏洞的技術。 在某些情況下，這些技術會使用安裝流程中的選項。 下表說明這些技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>權限</p> </td> 
   <td><p>使用安裝軟體所需的最少許可權。 使用不在Administrators群組中的帳戶登入電腦。 在Windows上，您可以使用「執行身分」命令，以系統管理使用者的身分，在JEE安裝程式上執行AEM Forms 。 在UNIX和Linux系統上，使用命令，例如 <code>sudo</code> 以安裝軟體。</p> </td> 
  </tr> 
  <tr> 
   <td><p>軟體來源</p> </td> 
   <td><p>請勿在JEE上從不受信任的來源下載或執行AEM Forms。</p> <p>惡意程式可能包含程式碼，以數種方式違反安全性，包括資料竊取、修改和刪除，以及拒絕服務。 從AdobeDVD或僅從信任的來源在JEE上安裝AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁碟分割</p> </td> 
   <td><p>將AEM Forms放在JEE的專用磁碟分割上。 磁碟分段是將伺服器上的特定資料保留在個別實體磁碟上的程式，以提高安全性。 以這種方式排列資料可降低目錄周遊攻擊的風險。 計畫建立獨立於系統分割區的分割區，您可以在其中在JEE內容目錄上安裝AEM Forms。 （在Windows上，系統分割區包含system32目錄或開機分割區。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>元件</p> </td> 
   <td><p>評估現有的服務，並停用或解除安裝任何不需要的服務。 請勿安裝不必要的元件和服務。</p> <p>應用程式伺服器的預設安裝可能包含您不需要使用的服務。 您應在部署前停用所有不必要的服務，將攻擊的進入點減至最少。 例如，在JBoss上，您可以在META-INF/jboss-service.xml描述項檔案中註解不必要的服務。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨網域原則檔案</p> </td> 
   <td><p>存在 <code>crossdomain.xml</code> 伺服器上的檔案可能會立即削弱該伺服器。 建議您儘可能限制網域清單。 請勿放置 <code>crossdomain.xml</code> 使用Guides時，在開發至生產環境期間使用的檔案 <em>（已棄用）</em>. 對於使用Web服務的指南，如果服務位在提供指南的同一伺服器上，則 <code>crossdomain.xml</code> 完全不需要檔案。 但是，如果服務是在其他伺服器上，或如果涉及叢集，則會出現 <code>crossdomain.xml</code> 需要檔案。 請參閱 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>，以取得有關crossdomain.xml檔案的詳細資訊。</p> </td> 
  </tr> 
  <tr> 
   <td><p>作業系統安全性設定</p> </td> 
   <td><p>如果您需要在Solaris平台上使用192位元或256位元的XML加密，請務必安裝 <code>pkcs11_softtoken_extra.so</code> 而非 <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安裝後步驟 {#post-installation-steps}

在JEE上成功安裝AEM Forms後，請務必從安全性角度定期維護環境。

下節將詳細描述建議用來保護已部署Forms伺服器的各種工作。

### AEM Forms安全性 {#aem-forms-security}

下列建議的設定適用於管理Web應用程式以外的JEE伺服器上的AEM Forms。 為降低伺服器的安全風險，請在JEE上安裝AEM Forms後立即套用這些設定。

**安全性修補程式**

如果未及時套用廠商安全性修補程式和升級，未經授權的使用者可能會取得應用程式伺服器的存取權，此風險會增加。 請先測試安全性修補程式，再將其套用至生產伺服器，以確保應用程式的相容性和可用性。 此外，建立原則和程式，以定期檢查並安裝修補程式。 JEE上的AEM Forms更新位在企業產品下載網站上。

**服務帳戶（僅適用於Windows上的JBoss整套作業）**

JEE上的AEM Forms預設會使用LocalSystem帳戶安裝服務。 內建的LocalSystem使用者帳戶具有高度協助工具；它屬於Administrators群組的一部分。 如果工作者處理序識別以LocalSystem使用者帳戶執行，則該工作者處理序具有整個系統的完整存取權。

若要使用特定的非管理帳戶，執行已部署AEM Forms on JEE的應用程式伺服器，請遵循下列指示：

1. 在Microsoft管理主控台(MMC)中，建立Forms伺服器服務的本機使用者，以以下身分登入：

   * 選取 **使用者無法變更密碼**.
   * 在 **成員隸屬於** 標籤，確認 **使用者** 群組已列出。

   >[!NOTE]
   >
   >您無法變更PDF Generator的這個設定。

1. 選取 **開始** > **設定** > **管理工具** > **服務**.
1. 在JEE上連按兩下AEM Forms的JBoss並停止服務。
1. 在 **登入** 索引標籤，選取 **此帳戶**，瀏覽您建立的使用者帳戶，然後輸入帳戶的密碼。
1. 在MMC中，開啟 **本機安全性設定** 並選取 **本機原則** > **使用者許可權指派**.
1. 將下列許可權指派給Forms伺服器執行所在的使用者帳戶：

   * 拒絕透過終端機服務登入
   * 拒絕本機登入
   * 以服務登入（應已設定）

1. 為新的使用者帳戶提供修改下列目錄的許可權：
   * **全域檔案儲存(GDS)目錄**：GDS目錄的位置是在AEM Forms安裝過程中手動設定的。 如果在安裝期間位置設定保持空白，則該位置會預設為應用程式伺服器安裝下的目錄： `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目錄**：預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**：
      * (Windows)在環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登入使用者的主目錄在UNIX系統上，非根使用者可以使用以下目錄作為暫存目錄：
      * (Linux) /var/tmp或/usr/tmp
      * (AIX) /tmp或/usr/tmp
      * (Solaris) /var/tmp或/usr/tmp
1. 為新的使用者帳戶提供下列目錄的寫入許可權：
   * [JBoss-directory]\standalone\部署
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的預設安裝位置：
   >
   >* Windows： C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux： /opt/jboss/

1. 啟動應用程式伺服器。

**停用Configuration Manager啟動程式servlet**

Configuration Manager會使用部署在應用程式伺服器上的servlet，執行JEE資料庫上AEM Forms的啟動程式。 由於Configuration Manager在設定完成之前會存取此servlet，因此未保護授權使用者的存取權，而且在您成功使用Configuration Manager在JEE上設定AEM Forms後，應該停用它。

1. 解壓縮adobe-livecycle-[appserver].ear檔案。
1. 開啟META-INF/application.xml檔案。
1. 搜尋adobe-bootstrapper.war區段：

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. 停止AEM Forms伺服器。
1. 註解adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 war模組，如下所示：

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. 儲存並關閉META-INF/application.xml檔案。
1. 壓縮EAR檔案，並將其重新部署到應用程式伺服器。
1. 啟動AEM Forms伺服器。
1. 在瀏覽器中輸入下列URL以測試變更，確保變更不再運作。

   https://&lt;localhost>：&lt;port>/adobe-bootstrapper/bootstrap

**鎖定對信任存放區的遠端存取**

Configuration Manager可讓您將Acrobat Reader DC擴充功能認證上傳至JEE信任存放區上的AEM Forms。 這表示透過遠端通訊協定（SOAP和EJB）存取「信任存放區認證服務」已預設啟用。 使用Configuration Manager上傳許可權認證後，或決定稍後使用Administration Console管理認證後，不再需要此存取權。

您可以依照一節中的步驟，停用所有信任存放區服務的遠端存取 [停用非必要的服務遠端存取](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**停用所有非必要的匿名存取**

有些Forms Server服務具有可由匿名呼叫者叫用的操作。 如果不需要匿名存取這些服務，請依照中的步驟加以停用 [停用對服務的非必要匿名存取](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### 變更預設的管理員密碼 {#change-the-default-administrator-password}

安裝JEE上的AEM Forms時，會為使用者「超級管理員/登入ID管理員」設定單一預設使用者帳戶，預設密碼為 *密碼*. 您應立即使用Configuration Manager變更此密碼。

1. 在網頁瀏覽器中輸入下列URL：

   ```java
   https://[host name]:[port]/adminui
   ```

   預設連線埠號碼為下列其中一項：

   **JBoss：** 8080

   **WebLogic伺服器：** 7001

   **WebSphere：** 9080。

1. 在 **使用者名稱** 欄位，型別 `administrator` 而且，在 **密碼** 欄位，型別 `password`.
1. 按一下 **設定** > **User Management** > **使用者和群組**.
1. 型別 `administrator` 在 **尋找** 欄位，然後按一下 **尋找**.
1. 按一下 **超級管理員** 從使用者清單中。
1. 按一下 **變更密碼** 在編輯使用者頁面上。
1. 指定新密碼，然後按一下 **儲存**.

此外，建議透過執行以下步驟來變更CRX管理員的預設密碼：

1. 登入 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 使用預設的使用者名稱/密碼。
1. 在搜尋欄位中鍵入Administrator ，然後按一下 **前往**.
1. 選取 **管理員** ，然後按一下 **編輯** 圖示加以存取（位於使用者介面的右下方）。
1. 在「 」中指定新密碼 **新密碼** 欄位和中的舊密碼 **您的密碼** 欄位。
1. 按一下使用者介面右下方的儲存圖示。

#### 停用WSDL產生 {#disable-wsdl-generation}

Web服務定義語言(WSDL)產生應該只針對開發環境啟用，在這些環境中，開發人員會使用WSDL產生來建置他們的使用者端應用程式。 您可以選擇在生產環境中停用WSDL產生，以避免公開服務的內部詳細資料。

1. 在網頁瀏覽器中輸入下列URL：

   ```java
   https://[host name]:[port]/adminui
   ```

1. 選取 **設定>核心系統設定>設定**.
1. 取消選取 **啟用WSDL**，然後選取 **確定**.

### 應用程式伺服器安全性 {#application-server-security}

下表說明安裝JEE應用程式上的AEM Forms後保護應用程式伺服器安全的一些技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>應用程式伺服器管理主控台</p> </td> 
   <td><p>在應用程式伺服器上的JEE上安裝、設定和部署AEM Forms後，您應該停用對應用程式伺服器管理主控台的存取權。 如需詳細資訊，請參閱您的應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>應用程式伺服器Cookie設定</p> </td> 
   <td><p>應用程式Cookie由應用程式伺服器控制。 部署應用程式時，應用程式伺服器管理員可指定全伺服器或應用程式特定的Cookie偏好設定。 依預設，伺服器設定會偏好。</p> <p>應用程式伺服器產生的所有工作階段Cookie應包含 <code>HttpOnly</code> 屬性。 例如，使用JBoss Application Server時，您可以將SessionCookie元素修改為 <code>httpOnly="true"</code> 在 <code>WEB-INF/web.xml</code> 檔案。</p> <p>您可以限制僅使用HTTPS傳送Cookie。 因此，它們不會經由HTTP以未加密的方式傳送。 應用程式伺服器管理員應在全域為伺服器啟用安全Cookie。 例如，使用JBoss Application Server時，您可以將聯結器元素修改為 <code>secure=true</code> 在 <code>server.xml</code> 檔案。</p> <p>如需Cookie設定的詳細資訊，請參閱您的應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目錄瀏覽</p> </td> 
   <td><p>當有人請求不存在的頁面或請求導向器名稱(請求字串以正斜線(/)結尾)時，應用程式伺服器不應傳回該目錄的內容。 若要避免此問題，您可以停用應用程式伺服器上的目錄瀏覽。 您應該針對管理控制檯應用程式以及伺服器上執行的其他應用程式執行此動作。</p> <p>針對JBoss，請設定 <code>DefaultServlet</code> 屬性至 <code>false</code> 在web.xml檔案中，如下列範例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;預設&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;清單&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>針對WebSphere，設定 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi檔案中的屬性 <code>false</code>.</p> <p>對於WebLogic，請將weblogic.xml檔案中的index-directories屬性設定為 <code>false</code>，如下列範例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 資料庫安全性 {#database-security}

保護資料庫安全時，您應該實施資料庫供應商所述的措施。 您應該配置資料庫使用者，使其具有AEM Forms on JEE授權使用的最低必要資料庫許可權。 例如，請勿使用具有資料庫管理員許可權的帳戶。

在Oracle時，您使用的資料庫帳戶只需要CONNECT、RESOURCE和CREATE VIEW許可權。 如需其他資料庫的類似需求，請參閱 [準備在JEE （單一伺服器）上安裝AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### 為Windows for JBoss上的SQL Server設定整合式安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]要新增的\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 連線URL，如以下範例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 將sqljdbc_auth.dll檔案新增至執行應用程式伺服器之電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案位於Microsoft SQL JDBC 6.2.1.0驅動程式安裝中。
1. 將本機系統登入身分的JBoss Windows服務(JEE上AEM Forms的JBoss)屬性修改為具有AEM Forms資料庫和最低許可權集的登入帳戶。 如果您是從命令列執行JBoss，而不是以Windows服務的形式執行，則不需要執行此步驟。
1. 設定SQL Server的安全性，從 **混合** 模式至 **僅限Windows驗證**.

#### 為Windows for WebLogic的SQL Server設定整合式安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 在網頁瀏覽器的URL行中輸入下列URL，啟動「WebLogic伺服器管理主控台」：

   ```java
   https://[host name]:7001/console
   ```

1. 在「變更中心」下，按一下 **鎖定和編輯**.
1. 在「領域結構」下，按一下 *[base_domain]* > **服務** > **JDBC** > **資料來源** 然後在右窗格中，按一下 **IDP_DS**.
1. 在下一個畫面，在 **設定** 索引標籤，按一下 **連線集區** 標籤，然後在 **屬性** 方塊，輸入 `integratedSecurity=true`.
1. 在「領域結構」下，按一下 **[base_domain]** > **服務** > **JDBC** > **資料來源** 然後在右窗格中，按一下 **RM_DS**.
1. 在下一個畫面，在 **設定** 索引標籤，按一下 **連線集區** 標籤，然後在 **屬性** 方塊，輸入 `integratedSecurity=true`.
1. 將sqljdbc_auth.dll檔案新增至執行應用程式伺服器之電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案位於Microsoft SQL JDBC 6.2.1.0驅動程式安裝中。
1. 設定SQL Server的安全性，從 **混合** 模式至 **僅限Windows驗證**.

#### 為Windows for WebSphere的SQL Server設定整合式安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有在使用外部SQL Server JDBC驅動程式，而非內嵌於WebSphere的SQL Server JDBC驅動程式時，才能設定整合式安全性。

1. 登入WebSphere管理主控台。
1. 在導覽樹狀結構中，按一下 **資源** > **JDBC** > **資料來源** 然後在右窗格中，按一下 **IDP_DS**.
1. 在右窗格的「其他屬性」下方，按一下 **自訂屬性**，然後按一下 **新增**.
1. 在 **名稱** 方塊，輸入 `integratedSecurity` 而且，在 **值** 方塊，輸入 `true`.
1. 在導覽樹狀結構中，按一下 **資源** > **JDBC** > **資料來源** 然後在右窗格中，按一下 **RM_DS**.
1. 在右窗格的「其他屬性」下方，按一下 **自訂屬性**，然後按一下 **新增**.
1. 在 **名稱** 方塊，輸入 `integratedSecurity` 而且，在 **值** 方塊，輸入 `true`.
1. 在安裝WebSphere的電腦上，將sqljdbc_auth.dll檔案新增至Windows系統路徑(C:\Windows)。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 1.2驅動程式安裝位於相同位置(預設為 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86)。
1. 選取 **開始** > **控制面板** > **服務**，以滑鼠右鍵按一下適用於WebSphere (IBM WebSphere Application Server)的Windows服務 &lt;version> - &lt;node>)並選取 **屬性**.
1. 在「屬性」對話方塊中，按一下 **登入** 標籤。
1. 選取 **此帳戶** 並提供設定您要使用的登入帳戶所需的資訊。
1. 設定SQL Server的安全性，從 **混合** 模式至 **僅限Windows驗證**.

### 保護對資料庫中敏感內容的存取 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms資料庫結構描述包含有關系統設定和業務流程的敏感資訊，應隱藏在防火牆之後。 系統應將資料庫視為與Forms伺服器位於相同的信任界限內。 為了防止資訊洩漏及商業資料遭竊，資料庫必須由資料庫管理員(DBA)設定為僅允許授權管理員存取。

作為新增的預防措施，您應該考慮使用資料庫廠商專用的工具，對包含以下資料的表格中的欄進行加密：

* Rights Management檔案索引鍵
* 信任存放區HSM PIN加密金鑰
* 本機使用者密碼雜湊

如需有關廠商特定工具的資訊，請參閱 [資料庫安全性資訊](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP安全性 {#ldap-security}

AEM Forms on JEE通常會使用輕量型目錄存取協定(LDAP)目錄作為企業使用者和群組資訊的來源，以及執行密碼驗證的方法。 您應該確保您的LDAP目錄已設定為使用Secure Socket Layer (SSL)，而AEM Forms on JEE已設定為使用其SSL連線埠存取您的LDAP目錄。

#### LDAP拒絕服務 {#ldap-denial-of-service}

使用LDAP的常見攻擊是指攻擊者故意多次無法驗證身分。 這會強制LDAP目錄伺服器鎖定所有LDAP相關服務的使用者。

您可以設定當使用者一再無法向AEM Forms驗證時，AEM Forms實施的失敗嘗試和後續鎖定時間。 在「管理主控台」中，選擇低值。 選取失敗嘗試次數時，請務必瞭解，在嘗試了所有失敗嘗試後，AEM Forms會在LDAP目錄伺服器嘗試之前鎖定使用者。

#### 設定自動帳戶鎖定 {#set-automatic-account-locking}

1. 登入管理主控台。
1. 按一下 **設定** > **User Management** > **網域管理**.
1. 在自動帳戶鎖定設定下，設定 **連續驗證失敗數上限** 變更為低數值，例如3。
1. 按一下「**儲存**」。

### 稽核與記錄 {#auditing-and-logging}

正確且安全地使用應用程式稽核和記錄，有助於確保儘快追蹤和偵測安全性和其他異常事件。 在應用程式中有效使用稽核和記錄功能包括追蹤成功和失敗的登入等專案，以及建立或刪除關鍵記錄等重要應用程式事件。

您可以使用稽核來偵測許多型別的攻擊，包括：

* 暴力密碼攻擊
* 拒絕服務攻擊
* 插入惡意輸入和相關的指令碼攻擊

此表格說明可用來減少伺服器弱點的稽核與記錄技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>記錄檔ACL</p> </td> 
   <td><p>在JEE記錄檔存取控制清單(ACL)上設定適當的AEM Forms 。</p> <p>設定適當的認證有助於防止攻擊者刪除檔案。</p> <p>記錄檔目錄的安全性許可權應該是Full Control for Administrators and SYSTEM groups。 AEM Forms使用者帳戶應僅具備讀取和寫入許可權。</p> </td> 
  </tr> 
  <tr> 
   <td><p>記錄檔備援</p> </td> 
   <td><p>如果資源允許，請使用Syslog、Tivoli、Microsoft Operations Manager (MOM)伺服器或其他機制，即時傳送記錄至攻擊者無法存取的其他伺服器（僅限寫入）。</p> <p>以這種方式保護記錄檔有助於防止竄改。 此外，將記錄儲存在中央存放庫有助於關聯和監控（例如，如果有多台表單伺服器在使用中，且在多台電腦上發生密碼猜測攻擊，而每台電腦都要求密碼）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 允許非系統管理員使用者執行PDF Generator

您可以讓非管理員使用者使用PDF Generator。 通常只有具有管理許可權的使用者才能使用PDF Generator。 執行以下步驟，讓非管理員使用者執行PDF Generator：

1. 建立環境變數名稱PDFG_NON_ADMIN_ENABLED。

1. 將變數的值設為TRUE。

1. 重新啟動AEM Forms執行個體。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

## 設定JEE上的AEM Forms以取得企業以外的存取權 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安裝AEM Forms後，請務必定期維護環境的安全性。 本節說明維護JEE生產伺服器上AEM Forms安全性的建議工作。

### 設定網頁存取的反向Proxy {#setting-up-a-reverse-proxy-for-web-access}

A *反向Proxy* 可用來確保外部和內部使用者均可使用JEE網頁應用程式上AEM Forms的一組URL。 此設定比允許使用者直接連線至AEM Forms on JEE執行所在的應用程式伺服器更安全。 反向Proxy會針對在JEE上執行AEM Forms的應用程式伺服器執行所有HTTP要求。 使用者只有反向Proxy的網路存取權，而且只能嘗試反向Proxy支援的URL連線。

**JEE根URL上的AEM Forms ，用於反向Proxy伺服器**

以下是JEE網頁應用程式上每個AEM Forms的應用程式根URL。 您應該只設定反向Proxy，以公開URL供您提供給使用者的網頁應用程式功能使用。

某些URL會醒目提示為面對使用者的網頁應用程式。 您應該避免公開Configuration Manager的其他URL，以便透過反向Proxy存取外部使用者。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途及/或相關的網頁應用程式</p> </th> 
   <th><p>Web式介面</p> </th> 
   <th><p>一般使用者存取權</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC擴充功能一般使用者Web應用程式，用於將使用許可權套用至PDF檔案</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management一般使用者Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Rights Management的Web服務URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator管理Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>Workspace一般使用者Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Workspace使用者端應用程式所需的Workspace servlet和資料服務</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>用於在JEE存放庫上啟動AEM Forms的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Forms Server Web服務的資訊頁</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>所有Forms Server服務的Web服務URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management管理Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>管理主控台首頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>secure/*</p> </td> 
   <td><p>信任存放區管理管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Forms IVS應用程式以進行表單轉譯的測試及偵錯</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>用於測試和偵錯輸出服務的輸出IVS應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>用於Rights Management的重設URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>輸出管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms網頁應用程式檔案</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>用於在HTML轉換期間擷取JavaScript</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV （偵錯）存取的URL</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>應用程式和服務使用者介面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>工作區管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Rest支援頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE核心組態設定頁面上的AEM Forms</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>User Management驗證</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>使用者管理管理介面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>透過已啟用HTTP檔案的SOAP傳輸或EJB傳輸，在存取遠端端點、SOAP WSDL端點及Java SDK時，上傳及下載要處理的檔案。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 避免跨網站請求偽造攻擊 {#protecting-from-cross-site-request-forgery-attacks}

跨網站請求偽造(CSRF)攻擊會利用網站對使用者的信任，傳輸未經授權且使用者未預期的命令。 將連結或指令碼包含在網頁中，或將URL包含在電子郵件訊息中，以存取使用者已驗證的其他網站，藉此設定攻擊。

例如，您可能在瀏覽其他網站的同時登入Administration Console。 其中一個網頁可能包含帶有的HTML影像標籤 `src` 鎖定受害者網站上伺服器端指令碼的屬性。 使用網頁瀏覽器提供的Cookie型工作階段驗證機制，攻擊網站可以傳送惡意要求給這個受到傷害的伺服器端指令碼，偽裝成合法使用者。 如需更多範例，請參閱 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

CSRF的通用特性如下：

* 涉及依賴使用者身分的網站。
* 利用網站信任該身分識別。
* 誘使使用者的瀏覽器傳送HTTP請求到目標網站。
* 涉及有副作用的HTTP要求。

JEE上的AEM Forms使用反向連結篩選功能來封鎖CSRF攻擊。 本節會使用下列辭彙來說明反向連結篩選機制：

* **允許的反向連結：** 反向連結是傳送請求至伺服器的來源頁面位址。 對於JSP頁面或表單，反向連結通常是瀏覽歷史記錄中的上一頁。 影像的反向連結通常是顯示影像的頁面。 您可以識別允許存取您伺服器資源的反向連結，方法是將其新增至允許的反向連結清單。
* **允許的反向連結例外：** 您可能想要限制允許的反向連結清單中特定反向連結的存取範圍。 若要強制執行此限制，您可以將該反向連結的個別路徑新增至「允許的反向連結例外」清單。 源自允許的反向連結例外清單中路徑的請求無法叫用Forms伺服器上的任何資源。 您可以為特定應用程式定義「允許的反向連結例外」，也可以使用適用於所有應用程式的例外全域清單。
* **允許的URI：** 這是在不勾選Referrer Header的情況下提供的資源清單。 可以將資源（例如說明頁面）新增至此清單，這些資源不會導致伺服器上的狀態變更。 無論反向連結為何，反向連結篩選器都不會封鎖允許URI清單中的資源。
* **Null查閱者：** 未關聯或並非源自上層網頁的伺服器要求會被視為來自Null反向連結的要求。 例如，當您開啟新的瀏覽器視窗、輸入位址並按Enter鍵時，傳送至伺服器的反向連結為Null。 案頭應用程式（.NET或SWING）向Web伺服器發出HTTP要求，也會將Null反向連結傳送至伺服器。

### 反向連結篩選 {#referer-filtering}

「反向連結篩選」程式的說明如下：

1. Forms伺服器會檢查用於叫用的HTTP方法：

   1. 如果是POST，Forms伺服器會執行反向連結標題檢查。
   1. 如果是GET，則Forms伺服器會略過反向連結檢查，除非 *CSRF_CHECK_GETS* 設為true，則會執行Referrer標題檢查。 *CSRF_CHECK_GETS* 指定於 *web.xml* 應用程式的檔案。

1. Forms伺服器會檢查要求的URI是否存在於允許清單中：

   1. 如果URI已加入允許清單，則伺服器會接受要求。
   1. 如果請求的URI未被加入允許清單，則伺服器會擷取請求的反向連結。

1. 如果請求中有Referrer，則伺服器會檢查其是否為Allowed Referrer。 如果允許，伺服器會檢查反向連結例外狀況：

   1. 若為例外狀況，則會封鎖要求。
   1. 如果不是例外，則會傳遞要求。

1. 如果請求中沒有反向連結，則伺服器會檢查是否允許Null反向連結：

   1. 如果允許Null反向連結，則會傳遞請求。
   1. 如果不允許空反向連結，則伺服器會檢查請求的URI是否為Null反向連結的例外狀況，並據此處理請求。

### 管理反向連結篩選 {#managing-referer-filtering}

JEE上的AEM Forms提供反向連結篩選條件，用以指定可存取您伺服器資源的反向連結。 依預設，反向連結篩選器不會篩選使用安全HTTP方法(例如GET)的請求，除非 *CSRF_CHECK_GETS* 設為true。 如果「允許的反向連結」專案的連線埠號碼設為0，則無論連線埠號碼為何，JEE上的AEM Forms都將允許從該主機傳送帶有「反向連結」的所有要求。 如果未指定連線埠號碼，則只允許來自預設連線埠80 (HTTP)或連線埠443 (HTTPS)的請求。 如果刪除「允許的反向連結」清單中的所有專案，則會停用反向連結篩選。

第一次安裝Document Services時，「允許的反向連結」清單會以安裝Document Services的伺服器位址更新。 伺服器的專案包括伺服器名稱、IPv4位址、啟用IPv6時的IPv6位址、回送位址以及localhost專案。 主機作業系統會傳回新增至「允許的反向連結」清單的名稱。 例如，IP位址為10.40.54.187的伺服器將包含下列專案： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 對於主機作業系統傳回的任何未限定名稱（沒有IPv4位址、IPv6位址或限定網域名稱的名稱），允許清單不會更新。 修改允許的反向連結清單以符合您的業務環境。 請勿使用預設的「允許的反向連結」清單，在生產環境中部署Forms伺服器。 修改任何「允許的反向連結」、「反向連結例外」或URI後，請確定您重新啟動伺服器，變更才會生效。

**管理允許的反向連結清單**

您可以從「管理主控台」的「使用者管理介面」管理「允許的反向連結」清單。 「使用者管理介面」提供您建立、編輯或刪除清單的功能。 請參閱* [防止CSRF攻擊](/help/forms/using/admin-help/preventing-csrf-attacks.md)*部分，屬於 *管理說明* 以取得使用「允許的反向連結」清單的詳細資訊。

**管理允許的反向連結例外和允許的URI清單**

JEE上的AEM Forms提供API來管理允許的反向連結例外清單和允許的URI清單。 您可以使用這些API來擷取、建立、編輯或刪除清單。 以下是可用API的清單：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

如需API的詳細資訊，請參閱* AEM Forms on JEE API參考資料* 。

使用 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 全域層次的「允許的反向連結例外」清單，也就是定義適用於所有應用程式的例外。 此清單僅包含具有絕對路徑的URI (例如 `/index.html`)或相對路徑(例如， `/sample/`)。 您也可以將規則運算式附加至相對URI的結尾，例如， `/sample/(.)*`.

此 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 清單ID在 `UMConstants` 的類別 `com.adobe.idp.um.api` 名稱空間，可在 `adobe-usermanager-client.jar`. 您可以使用AEM Forms API來建立、修改或編輯此清單。 例如，若要建立「允許的全域反向連結例外」清單，請使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用 ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** 應用程式特定例外清單。

**停用反向連結篩選**

如果反向連結篩選完全封鎖對Forms伺服器的存取，且您無法編輯允許的反向連結清單，您可以更新伺服器啟動指令碼並停用反向連結篩選。

包含 `-Dlc.um.csrffilter.disabled=true` 啟動指令碼中的JAVA引數並重新啟動伺服器。 請務必在適當重新設定「允許的反向連結」清單後，刪除JAVA引數。

**自訂WAR檔案的反向連結篩選**

您可能已建立自訂WAR檔案，以搭配AEM Forms on JEE使用來滿足您的業務需求。 若要為自訂WAR檔案啟用反向連結篩選，請包括 ***adobe-usermanager-client.jar*** 在WAR的類別路徑中，並在* web.xml*檔案中包含一個篩選專案，其中包含下列引數：

**CSRF_CHECK_GETS** 控制GET請求的反向連結檢查。 如果未定義此引數，預設值會設為false。 僅當您要篩選GET請求時才包含此引數。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是「允許的反向連結例外」清單的ID。 反向連結篩選器可防止來自清單ID所識別清單中反向連結的請求，從Forms伺服器上叫用任何資源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是「允許的URI」清單的ID。 無論請求中的Referrer標頭值為何， Referrer Filter都不會封鎖針對清單ID所識別清單中任何資源的請求。

**CSRF_ALLOW_NULL_REFERER** 控制反向連結為Null或不存在時的反向連結篩選行為。 如果未定義此引數，預設值會設為false。 只有在您想要允許Null反向連結時才包含此引數。 允許空反向連結可能會允許某些型別的跨網站請求偽造攻擊。

**CSRF_NULL_REFERER_EXCEPTIONS** 是URI清單，當反向連結為Null時，不會對其執行反向連結檢查。 此引數僅在 *CSRF_ALLOW_NULL_REFERER* 設為false。 請使用逗號分隔清單中的多個URI。

以下是 *web.xml* 的檔案 ***範例*** WAR檔案：

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**疑難排解**

如果CSRF篩選器封鎖合法的伺服器要求，請嘗試下列其中一個動作：

* 如果被拒絕的請求有反向連結標題，請仔細考慮將其新增至允許的反向連結清單。 僅新增您信任的反向連結。
* 如果拒絕的請求沒有Referrer標頭，請修改您的使用者端應用程式以包含Referrer標頭。
* 如果使用者端可在瀏覽器中運作，請嘗試該部署模式。
* 作為最後手段，您可以將資源新增到允許的URI清單中。 不建議使用此設定。

## 安全網路設定 {#secure-network-configuration}

本節說明AEM Forms on JEE所需的通訊協定和連線埠，並提供在安全網路設定中部署AEM Forms on JEE的建議。

### AEM Forms on JEE使用的網路通訊協定 {#network-protocols-used-by-aem-forms-on-jee}

如上節所述，當您設定安全的網路架構時，JEE上的AEM Forms與企業網路中的其他系統之間的互動需要下列網路通訊協定。

<table> 
 <thead> 
  <tr> 
   <th><p>通訊協定</p> </th> 
   <th><p>使用</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>瀏覽器會顯示Configuration Manager和一般使用者Web應用程式</p> </li> 
     <li><p>所有SOAP連線</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服務使用者端應用程式，例如.NET應用程式</p> </li> 
     <li><p>Adobe Reader®針對JEE伺服器Web服務上的AEM Forms使用SOAP</p> </li> 
     <li><p>AdobeFlash®應用程式使用SOAP進行Forms Server Web服務</p> </li> 
     <li><p>在SOAP模式中使用時，針對JEE SDK呼叫進行AEM Forms</p> </li> 
     <li><p>Workbench設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在Enterprise JavaBeans (EJB)模式中使用時，在JEE SDK呼叫上使用AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>以電子郵件為基礎的服務輸入（電子郵件端點）</p> </li> 
     <li><p>透過電子郵件傳送使用者任務通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC檔案IO</p> </td> 
   <td><p>AEM Forms on JEE監視watched資料夾以輸入服務（watched資料夾端點）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>同步目錄中的組織使用者和群組資訊</p> </li> 
     <li><p>互動式使用者的LDAP驗證</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>使用JDBC服務執行處理作業時，對外部資料庫進行的查詢和程式呼叫</p> </li> 
     <li><p>內部存取JEE存放庫上的AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>啟用任何WebDAV使用者端在JEE設計階段存放庫（表單、片段等）上遠端瀏覽AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash應用程式，其中JEE伺服器服務上的AEM Forms設定了遠端端點</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE上的AEM Forms公開MBean，以使用JMX進行監視</p> </td> 
  </tr> 
 </tbody> 
</table>

### 應用程式伺服器的連線埠 {#ports-for-application-servers}

本節說明各種支援的應用程式伺服器型別的預設連線埠（和替代組態範圍）。 這些連線埠必須在內部防火牆上啟用或停用，具體取決於您要允許使用者端連線到在JEE上執行AEM Forms的應用程式伺服器的網路功能。

>[!NOTE]
>
>依預設，伺服器會在adobe.com名稱空間下公開數個JMX MBean。 只會公開對伺服器健康狀態監視有用的資訊。 不過，若要防止資訊洩漏，您應該防止不受信任網路中的呼叫者尋找JMX MBean並存取健康狀態量度。

**JBoss連線埠**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>連接埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>存取網頁應用程式</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1聯結器連線埠8080</p> <p>AJP 1.3聯結器連線埠8009</p> <p>SSL/TLS聯結器連線埠8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支援</p> </td> 
   <td><p>[JBoss根]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic連線埠**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>連接埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>存取網頁應用程式</p> </td> 
   <td> 
    <ul> 
     <li><p>Admin Server監聽連線埠：預設值為7001</p> </li> 
     <li><p>Admin Server SSL接聽連線埠：預設為7002</p> </li> 
     <li><p>為受管理伺服器設定的連線埠，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>存取JEE上的AEM Forms不需要WebLogic管理連線埠</p> </td> 
   <td> 
    <ul> 
     <li><p>受管理的伺服器接聽連線埠：可從1到65534設定</p> </li> 
     <li><p>受管理伺服器SSL接聽連線埠：可從1到65534設定</p> </li> 
     <li><p>節點管理員接聽連線埠：預設值為5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere連線埠**

如需AEM Forms on JEE所需的WebSphere連線埠相關資訊，請前往WebSphere Application Server UI中的連線埠號碼設定。

### 設定SSL {#configuring-ssl}

請參考一節中所述的實體架構 [JEE實體架構上的AEM Forms](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您應該為計畫使用的所有連線設定SSL。 具體而言，所有SOAP連線都必須透過SSL執行，以防止在網路上洩露使用者認證。

如需有關如何在JBoss、WebLogic和WebSphere上設定SSL的說明，請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_64).

如需如何將憑證匯入為AEM Forms伺服器設定的JVM （Java虛擬機器器）的指示，請參閱以下連結中的相互驗證一節： [AEM Forms Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_65).

### 設定SSL重新導向 {#configuring-ssl-redirect}

將應用程式伺服器設定為支援SSL之後，您必須確保所有應用程式和服務的HTTP流量都已強制使用SSL連線埠。

若要設定WebSphere或WebLogic的SSL重新導向，請參閱您的應用程式伺服器檔案。

1. 開啟命令提示字元，瀏覽至/JBOSS_HOME/standalone/configuration目錄，然後執行下列命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 開啟JBOSS_HOME/standalone/configuration/standalone.xml檔案進行編輯。

   在 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />網域:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素，新增下列詳細資料：:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https聯結器元素中新增下列程式碼：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   儲存並關閉standalone.xml檔案。

## Windows專屬安全性建議 {#windows-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，特定於Windows的安全性建議。

### JBoss服務帳戶 {#jboss-service-accounts}

JEE上的AEM Forms整套金鑰安裝依預設會使用「本機系統」帳戶設定服務帳戶。 內建的本機系統使用者帳戶具有高度協助功能；它是管理員群組的一部分。 如果背景工作處理序識別以「本機系統」使用者帳戶執行，則該背景工作處理序具有對整個系統的完整存取權。

#### 使用非管理帳戶執行應用程式伺服器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理主控台(MMC)中，建立Forms伺服器服務的本機使用者，以以下身分登入：

   * 選取 **使用者無法變更密碼**.
   * 在 **成員隸屬於** 索引標籤中，確定已列出「使用者」群組。

1. 選取 **設定** > **管理工具** > **服務**.
1. 按兩下應用程式伺服器服務並停止該服務。
1. 在 **登入** 索引標籤，選取 **此帳戶**，瀏覽您建立的使用者帳戶，然後輸入帳戶的密碼。
1. 在「本機安全性設定」視窗的「使用者許可權指派」下，將下列許可權授與執行Forms伺服器的使用者帳戶：

   * 拒絕透過終端機服務登入
   * 拒絕登入locallyxx
   * 以服務登入（應已設定）

1. 為新的使用者帳戶提供修改下列目錄的許可權：
   * **全域檔案儲存(GDS)目錄**：GDS目錄的位置是在AEM Forms安裝過程中手動設定的。 如果在安裝期間位置設定保持空白，則該位置會預設為應用程式伺服器安裝下的目錄： `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目錄**：預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**：
      * (Windows)在環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登入使用者的主目錄在UNIX系統上，非根使用者可以使用以下目錄作為暫存目錄：
      * (Linux) /var/tmp或/usr/tmp
      * (AIX) /tmp或/usr/tmp
      * (Solaris) /var/tmp或/usr/tmp
1. 為新的使用者帳戶提供下列目錄的寫入許可權：
   * [JBoss-directory]\standalone\部署
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的預設安裝位置：
   >
   >* Windows： C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux： /opt/jboss/。

1. 啟動應用程式伺服器服務。

### 檔案系統安全性 {#file-system-security}

JEE上的AEM Forms透過下列方式使用檔案系統：

* 儲存處理檔案輸入和輸出時使用的暫存檔
* 將用來支援所安裝解決方案元件的檔案儲存在全域封存存放區
* Watched資料夾存放區會從檔案系統資料夾位置將用作服務輸入的捨棄檔案

當使用watched資料夾作為Forms伺服器服務傳送和接收檔案的方式時，應採取檔案系統安全性的額外預防措施。 當使用者將內容放入watched資料夾中時，該內容會透過watched資料夾公開。 在此情況下，服務不會驗證實際的一般使用者。 相反，它依賴在檔案夾層級設定的ACL和共用層級安全性，以確定誰能夠有效地叫用服務。

## JBoss專屬安全性建議 {#jboss-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，JBoss 7.0.6專屬的應用程式伺服器設定建議。

### 停用JBoss管理主控台和JMX主控台 {#disable-jboss-management-console-and-jmx-console}

使用全包安裝方法在JBoss上的JEE上安裝AEM Forms時，已設定存取JBoss管理主控台和JMX主控台（已停用JMX監視）。 如果您使用自己的JBoss Application Server，請確定對JBoss管理主控台和JMX監控主控台的存取是安全的。 JMX監視主控台的存取權是在名為jmx-invoker-service.xml的JBoss組態檔中設定。

### 停用目錄瀏覽 {#disable-directory-browsing}

登入Administration Console後，可以修改URL來瀏覽主控台的目錄清單。 例如，如果您將URL變更為下列URL之一，可能會出現目錄清單：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic專屬安全性建議 {#weblogic-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，用於保護WebLogic 9.1安全的應用程式伺服器設定建議。

### 停用目錄瀏覽 {#disable_directory_browsing-1}

將weblogic.xml檔案中的index-directories屬性設定為 `false`，如下列範例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 啟用WebLogic SSL連線埠 {#enable-weblogic-ssl-port}

依預設，WebLogic不會啟用預設的SSL監聽連線埠7002。 設定SSL之前，請在WebLogic伺服器管理主控台中啟用此連線埠。

## WebSphere專屬安全性建議 {#websphere-specific-security-recommendations}

本節包含應用程式伺服器組態建議，可保護在JEE上執行AEM Forms的WebSphere。

### 停用目錄瀏覽 {#disable_directory_browsing-2}

設定 `directoryBrowsingEnabled` ibm-web-ext.xml檔案中的屬性 `false`.

### 啟用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登入WebSphere管理主控台。
1. 在導覽樹狀結構中，前往 **安全性** > **全球安全性**
1. 選取 **啟用管理安全性**.
1. 取消選取兩者 **啟用應用程式安全性** 和 **使用Java 2安全性**.
1. 按一下 **確定** 或 **套用**.
1. 在 **訊息** 方塊，按一下 **直接儲存至主組態**.
