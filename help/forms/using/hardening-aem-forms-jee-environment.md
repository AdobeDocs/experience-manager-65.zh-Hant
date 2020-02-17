---
title: 在JEE環境中強化您的AEM表格
seo-title: 在JEE環境中強化您的AEM表格
description: 瞭解各種安全性強化設定，以增強在企業內部網路中執行之JEE上AEM Forms的安全性。
seo-description: 瞭解各種安全性強化設定，以增強在企業內部網路中執行之JEE上AEM Forms的安全性。
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 在JEE環境中強化您的AEM表格 {#hardening-your-aem-forms-on-jee-environment}

瞭解各種安全性強化設定，以增強在企業內部網路中執行之JEE上AEM Forms的安全性。

文章說明在JEE上執行AEM Forms的伺服器保全建議和最佳實務。 對於您的作業系統和應用程式伺服器，此檔案並非完整的主機強化檔案。 相反地，本文說明您應實作的各種安全性強化設定，以增強在公司內部網路中執行的JEE上AEM Forms的安全性。 不過，為確保JEE應用程式伺服器上的AEM Forms保持安全，您也應實作安全性監控、偵測和回應程式。

本文描述在安裝和配置生命週期的以下階段應應用的強化技術：

* **** 預安裝：在JEE上安裝AEM Forms之前，請先使用這些技巧。
* **** 安裝：在AEM Forms on JEE安裝程式中使用這些技巧。
* **** 安裝後：安裝後及安裝後定期使用這些技術。

AEM Forms on JEE可高度自訂，可在許多不同的環境中運作。 有些建議可能不符合您組織的需求。

## 預安裝 {#preinstallation}

在JEE上安裝AEM Forms之前，您可以將安全性解決方案套用至網路層與作業系統。 本節將說明一些問題，並建議您減少這些領域的安全性弱點。

**在UNIX和Linux上安裝和配置**

您不應使用根殼層在JEE上安裝或設定AEM Forms。 依預設，檔案會安裝在/opt目錄下，而執行安裝的使用者需要/opt下的所有檔案權限。 或者，您也可以在個別使用者/user目錄下執行安裝，而使用者已擁有所有檔案權限。

**在Windows上安裝和配置**

如果您是使用統包方法或安裝PDF產生器，在JBoss的JEE上安裝AEM Forms，您應以管理員身分在Windows上執行安裝。 此外，在具備原生應用程式支援的Windows上安裝PDF產生器時，您必須與安裝Microsoft office的Windows使用者一樣執行安裝。 如需安裝權限的詳細資訊，請參 **閱您應用程式伺服器的「在JEE上安裝和部署AEM** Forms」檔案。

### 網路層安全性 {#network-layer-security}

網路安全漏洞是對任何面向網際網路或面向內聯網的應用程式伺服器的首批威脅之一。 本節介紹加強網路上主機抵御這些漏洞的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧強化以及使用防火牆保護主機的問題。

下表說明了減少網路安全漏洞的常見過程。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非軍事區</p> </td> 
   <td><p>在非軍事區(DMZ)內部署表單伺服器。 區段至少應存在於兩個層級，而應用程式伺服器則位於內部防火牆後方，用來在JEE上執行AEM Forms。 將外部網路與包含Web伺服器的DMZ分離，而Web伺服器又必須與內部網路分離。 使用防火牆來實現分層。 對流經每個網路層的流量進行分類和控制，以確保僅允許所需資料的絕對最小值。</p> </td> 
  </tr> 
  <tr> 
   <td><p>專用IP地址</p> </td> 
   <td><p>在AEM Forms應用程式伺服器上，搭配使用網路位址轉換(NAT)與RFC 1918專用IP位址。 指定私有IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難以透過網際網路將NAT內部主機的流量路由至網路。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火牆</p> </td> 
   <td><p>使用以下標準選擇防火牆解決方案：</p> 
    <ul> 
     <li><p>建置支援代理伺服器和／或狀態檢 <em>查的防火牆</em> ，而非簡單的封包篩選解決方案。</p> </li> 
     <li><p>使用防火牆，它支援拒絕 <em>除明確允許的安全范式外的所</em> 有服務。</p> </li> 
     <li><p>實作雙歸屬或多歸屬的防火牆解決方案。 此架構提供最高等級的安全性，並協助防止未經授權的使用者略過防火牆安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>資料庫埠</p> </td> 
   <td><p>請勿對資料庫使用預設監聽埠(MySQL - 3306、Oracle - 1521、MS SQL - 1433)。 有關更改資料庫埠的資訊，請參見資料庫文檔。</p> <p>使用不同的資料庫連接埠會影響JEE上的整體AEM Forms設定。 如果您變更預設埠，則必須在其他設定區域進行對應的修改，例如JEE上AEM Forms的資料來源。</p> <p>如需在JEE上的AEM Forms中設定資料來源的詳細資訊，請參閱 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms使用指南中的「在JEE上安裝並升級AEM Forms」或「在JEE上升級至AEM Forms」（適用於您的應用程式伺服器）</a>。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 作業系統安全性 {#operating-system-security}

下表說明將作業系統中發現的安全性弱點降至最低的一些潛在方法。

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
   <td><p>如果未及時應用供應商安全補丁和升級，未經授權的用戶可能會獲得對應用程式伺服器的訪問，這一風險增加。 在將安全修補程式套用至生產伺服器之前，請先加以測試。</p><p>此外，建立策略和程式以定期檢查和安裝修補程式。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防護軟體</p></td> 
   <td><p>病毒掃描器可以通過掃描簽名或監視異常行為來識別感染病毒的檔案。 掃描器將其病毒簽名保存在檔案中，該檔案通常儲存在本地硬碟上。 由於新病毒經常被發現，因此您應經常更新此檔案，以便病毒掃描程式識別所有當前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>網路時間協定(NTP)</p></td> 
   <td><p>若要取證分析，請在表單伺服器上維持正確的時間。 使用NTP來同步所有直接連接到Internet的系統上的時間。</p></td> 
  </tr> 
 </tbody> 
</table>

如需作業系統的其他安全性資訊，請參 [閱「作業系統安全性資訊」](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安裝 {#installation}

本節說明您在AEM Forms安裝程式期間可使用的技術，以降低安全性弱點。 在某些情況下，這些技術會使用屬於安裝程式一部分的選項。 下表說明這些技巧。

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
   <td><p>使用安裝軟體所需的最少權限數。 使用不在「管理員」群組中的帳戶登入您的電腦。 在Windows上，您可以使用「執行方式」命令，以管理使用者身分，在JEE安裝程式上執行AEM Forms。 在UNIX和Linux系統上，使用諸如命令 <code>sudo</code> 來安裝軟體。</p> </td> 
  </tr> 
  <tr> 
   <td><p>軟體源</p> </td> 
   <td><p>請勿從不受信任的來源下載或在JEE上執行AEM Forms。</p> <p>惡意程式可能包含數種違反安全性的程式碼，包括資料竊取、修改和刪除，以及拒絕服務。 從Adobe DVD或僅從受信任的來源，在JEE上安裝AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁碟分區</p> </td> 
   <td><p>將AEM Forms置於專用磁碟分區的JEE上。 磁碟分段是將伺服器上的特定資料保存在單獨的物理磁碟上，以增加安全性的過程。 以這種方式安排資料可降低目錄遍歷攻擊的風險。 計畫建立與系統分區分隔的分區，您可以在JEE內容目錄上安裝AEM Forms。 （在Windows上，系統分區包含system32目錄或引導分區。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>元件</p> </td> 
   <td><p>評估現有服務，並停用或解除安裝任何不需要的服務。 請勿安裝不必要的元件和服務。</p> <p>應用程式伺服器的預設安裝可能包含您使用時不需要的服務。 在部署之前，您應禁用所有不必要的服務，以最大限度地減少攻擊的入口點。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符檔案中注釋掉不必要的服務。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨網域原則檔案</p> </td> 
   <td><p>伺服器上存 <code>crossdomain.xml</code> 在檔案可能會立即削弱該伺服器。 建議您盡可能限制網域清單。 使用「參考 <code>crossdomain.xml</code> 線（已過時）」時，請勿將開發期間使用的檔 <em>案置入生產</em>。 對於使用web services的指南，如果服務位於提供該指南的同一台伺服器上，則根 <code>crossdomain.xml</code> 本不需要檔案。 但是，如果服務位於另一台伺服器上，或者如果涉及群集，則需要存 <code>crossdomain.xml</code> 在檔案。 如需 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">crossdomain.xml檔案的詳細資訊</a>，請參閱https://kb2.adobe.com/cps/142/tn_14213.html。</p> </td> 
  </tr> 
  <tr> 
   <td><p>作業系統安全性設定</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，請確保您安裝而不是 <code>pkcs11_softtoken_extra.so</code> 安裝 <code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安裝後步驟 {#post-installation-steps}

在JEE上成功安裝AEM Forms後，請務必從安全性角度定期維護環境。

下節詳細說明建議的保護已部署表單伺服器的不同任務。

### AEM Forms安全性 {#aem-forms-security}

下列建議的設定適用於JEE伺服器上的AEM Forms，而非管理Web應用程式。 若要降低伺服器的安全性風險，請在JEE上安裝AEM Forms後立即套用這些設定。

**安全性修補程式**

如果供應商未及時應用安全補丁和升級，未經授權的用戶可能會獲得對應用程式伺服器的訪問，這一風險增加。 在將安全性修補程式套用至生產伺服器之前，請先加以測試，以確保應用程式的相容性和可用性。 此外，建立策略和程式以定期檢查和安裝修補程式。 AEM Forms on JEE更新位於「企業版」產品下載網站。

**服務帳戶（僅Windows上的JBoss統包）**

AEM Forms on JEE依預設會使用LocalSystem帳戶來安裝服務。 內建的LocalSystem使用者帳戶具備高階的協助功能；它屬於管理員組。 如果工作進程身份作為LocalSystem用戶帳戶運行，則該工作進程可以完全訪問整個系統。

若要使用特定非管理帳戶，執行部署JEE上AEM Forms的應用程式伺服器，請依照下列指示進行：

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶，以以下方式登錄：

   * 選擇「 **用戶不能更改密碼**」。
   * 在「成 **員** 」標籤中，請確 **定已列出「使用者** 」群組。
   >[!NOTE]
   >
   >您無法變更PDF產生器的此設定。

1. 選擇 **「** > **Settings** > **Administrative Tools** > **** Services」。
1. 在JEE上按兩下JBoss for AEM Forms，然後停止服務。
1. 在「登 **錄** 」標籤上，選 **擇「此帳戶**」，瀏覽您建立的用戶帳戶，並輸入帳戶的密碼。
1. 在MMC中，開啟「本 **地安全設定」** ，然後選擇「 **本地策略** 」>「用 **戶權限分配」**。
1. 將下列權限指派給Forms伺服器所在之使用者帳戶：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄
   * 以服務身分登入（應已設定）

1. 為新使用者帳戶提供JEE網頁內容目錄上AEM Forms的「讀取與執行」、「清單資料夾內容」和「讀取」權限項目。
1. 啟動應用程式伺服器。

**禁用配置管理器引導Servlet**

Configuration manager使用部署在應用程式伺服器上的servlet，在JEE資料庫上執行AEM Forms的引導。 由於Configuration manager在配置完成前即存取此servlet，因此授權使用者尚未保護對其的存取，而且在您成功使用Configuration manager在JEE上設定AEM Forms後，應停用此Servlet。

1. 解壓縮adobe-livecycle-[appserver].ear檔案。
1. 開啟META-INF/application.xml檔案。
1. 搜尋adobe-bootstrapper.war區段：

   ```as3
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
1. 注釋adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 戰爭模組如下：

   ```as3
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
1. 壓縮EAR檔案，並將它重新部署至應用程式伺服器。
1. 啟動AEM Forms伺服器。
1. 在瀏覽器中輸入下列URL以測試變更，並確保其不再運作。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**鎖定對信任儲存的遠程訪問**

Configuration manager可讓您將Acrobat Reader DC擴充功能憑證上傳至JEE信任商店的AEM Forms。 這表示依預設，已啟用透過遠端通訊協定（SOAP和EJB）存取信任商店憑證服務的功能。 當您使用Configuration manager上傳權限憑證或您稍後決定使用Administration console管理憑證後，就不再需要此存取。

您可以按照禁用非基本服務遠程訪問一節中的步驟禁用對所有信任 [儲存服務的遠程訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)。

**禁用所有非必要的匿名訪問**

某些表單伺服器服務具有可由匿名呼叫者調用的操作。 如果不需要匿名訪問這些服務，請按照禁用服務的非必要匿名訪 [問中的步驟將其禁用](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)。

#### 更改預設管理員密碼 {#change-the-default-administrator-password}

當安裝JEE上的AEM Forms時，會針對使用者Super Administrator/ login-id Administrator設定單一預設使用者帳戶，並設定預設密碼為 *密碼*。 您應使用配置管理器立即更改此密碼。

1. 在網頁瀏覽器中輸入下列URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

   預設埠號是以下其中之一：

   **** JBoss:郵遞區號8080

   **** WebLogic伺服器：郵編：7001

   **** WebSphere:9080。

1. 在「用 **戶名** 」欄位中，鍵入 `administrator` 並在「密碼」字 **段中鍵入**`password`。
1. 按一 **下「設定** >使 **用者管理** >使 **用者和群組**」。
1. 在「尋 `administrator` 找」欄 **位中輸入** ，然後按一下「尋 **找」**。
1. 從使 **用者清單中按一下** 「超級管理員」。
1. 在「編 **輯用戶** 」頁上按一下更改密碼。
1. 指定新密碼，然後按一下「 **儲存**」。

此外，建議通過執行以下步驟來更改CRX管理員的預設密碼：

1. 使用預 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 設的使用者名稱／密碼登入。
1. 在搜尋欄位中鍵入Administrator，然後按一 **下Go**。
1. 從搜 **尋結果中選取** 「管理員」，然後按一下使用者介面右下方的「編輯 **** 」圖示。
1. 在「新密碼」欄位中 **指定新密碼** ，在「密碼」欄位中指 **定舊密碼** 。
1. 按一下使用者介面右下方的「儲存」圖示。

#### 禁用WSDL生成 {#disable-wsdl-generation}

Web服務定義語言(WSDL)產生只能用於開發環境，開發人員會使用WSDL產生來建立其用戶端應用程式。 您可以選擇在生產環境中停用WSDL產生功能，以避免暴露服務的內部詳細資訊。

1. 在網頁瀏覽器中輸入下列URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

1. 按一下 **設定>核心繫統設定>配置**。
1. 取消選 **擇「啟用WSDL** 」，然後單 **擊「確定」**。

### 應用程式伺服器安全性 {#application-server-security}

下表說明在安裝JEE應用程式上的AEM Forms後，保護您應用程式伺服器的一些技巧。

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
   <td><p>在您的應用程式伺服器上，在JEE上安裝、設定和部署AEM Forms後，您應停用對應用程式伺服器管理控制台的存取權。 如需詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>應用程式伺服器Cookie設定</p> </td> 
   <td><p>應用程式Cookie由應用程式伺服器控制。 部署應用程式時，應用程式伺服器管理員可以指定整個伺服器或特定應用程式的Cookie偏好設定。 依預設，伺服器設定會優先使用。</p> <p>您的應用程式伺服器產生的所有作業Cookie都應包含該 <code>HttpOnly</code> 屬性。 例如，使用JBoss Application Server時，可將SessionCookie元素修改為 <code>httpOnly="true"</code> 檔案 <code>WEB-INF/web.xml</code> 中。</p> <p>您可以限制使用僅HTTPS傳送的Cookie。 因此，不會透過HTTP傳送未加密的檔案。 應用程式伺服器管理員應全域啟用伺服器的安全Cookie。 例如，使用JBoss Application server時，可以將連接器元素修改為 <code>secure=true</code> 檔案 <code>server.xml</code> 中。</p> <p>如需Cookie設定的詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目錄瀏覽</p> </td> 
   <td><p>當有人請求不存在的頁面或請求控制器名稱(請求字串以斜線(/)結尾)時，應用程式伺服器不應傳回該目錄的內容。 為避免此問題，您可以停用應用程式伺服器上的目錄瀏覽。 您應針對管理控制台應用程式和伺服器上執行的其他應用程式執行此動作。</p> <p>對於JBoss，請將屬性的清單初始化參 <code>DefaultServlet</code> 數的值 <code>false</code> 設定為web.xml檔案中，如以下示例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>對於WebSphere，將ibm-web-ext.xmi <code>directoryBrowsingEnabled</code> 檔案中的屬性設定為 <code>false</code>。</p> <p>對於WebLogic，請將weblogic.xml檔案中的index-directories設定為 <code>false</code>，如以下示例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 資料庫安全性 {#database-security}

在保護資料庫時，應實施資料庫供應商描述的測量。 您應將AEM Forms在JEE上授與的最低必要資料庫權限配置給資料庫使用者。 例如，請勿使用具有資料庫管理員權限的帳戶。

在Oracle上，您使用的資料庫帳戶只需要CONNECT、RESOURCE和CREATE VIEW權限。 如需其他資料庫的類似需求，請 [參閱「準備在JEE(Single Server)上安裝AEM Forms」](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上為JBoss配置SQL server的整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 以新增至連線URL，如以下範例所示：

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 將「從本機系統登入為」的JBoss windows服務(JBoss for AEM Forms on JEE)屬性修改為具有AEM Forms資料庫和最低權限集的登入帳戶。 如果從命令行而不是作為Windows服務運行JBoss，則無需執行此步驟。
1. 將「SQL server的安全性」從「 **混合** 」模式設 **置為「Windows驗證」**。

#### 在Windows上為WebLogic配置SQL server的整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 在Web瀏覽器的URL行中鍵入以下URL，以啟動WebLogic Server管理控制台：

   ```as3
   https://[host name]:7001/console
   ```

1. 在「變更中心」下，按一下「 **鎖定與編輯」**。
1. 在「域結構」下，單 *[擊「base_domain]* > **Services** > **JDBC**********> Sources」資料，在右窗格中按一下右側的IDP_DS窗格。
1. 在下一個螢幕的「 **Configuration** （配置）」頁籤上，按一下「 **Connection Pool** （連接池）」頁籤，然後在「 **Properties** （屬性）」框中鍵入 `integratedSecurity=true`。
1. 在「域結構」下，單 **[擊「base_domain]** > **Services** > **JDBC**********> Sources」資料，在右窗格中按一下RightRm RM_DS Pane。
1. 在下一個螢幕的「 **Configuration** （配置）」頁籤上，按一下「 **Connection Pool** （連接池）」頁籤，然後在「 **Properties** （屬性）」框中鍵入 `integratedSecurity=true`。
1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 將「SQL server的安全性」從「 **混合** 」模式設 **置為「Windows驗證」**。

#### 在Windows上為WebSphere配置SQL server的整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有當使用外部SQL Server JDBC驅動程式時，才可配置整合安全性，而不是嵌入WebSphere的SQL Server JDBC驅動程式。

1. 登入WebSphere管理控制台。
1. 在導航樹中，按一下「 **資源** > **JDBC** > **Data Sources** 」 ，在右窗格中按一下「 **** IDP_DS Sources」。
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下「 **Custom Properties（自定義屬性）**」 ，然後按一下「 **New（新建）**」。
1. 在「名 **稱** 」(Name `integratedSecurity` )框中，鍵入 **並在「值」(** Value `true`)框中鍵入。
1. 在導航樹中，按一下 **資源** > **JDBC** > **Data Sources** ，然後在右窗格中按一下 **** RM_DS。
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下「 **Custom Properties（自定義屬性）**」 ，然後按一下「 **New（新建）**」。
1. 在「名 **稱** 」(Name `integratedSecurity` )框中，鍵入 **並在「值」(** Value `true`)框中鍵入。
1. 在安裝WebSphere的電腦上，將sqljdbc_auth.dll檔案添加到Windows系統路徑(C:\Windows)。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 1.2驅動程式安裝位置相同(預設為 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86)。
1. 選擇「 **開始** 」>「控制面板 **」>「服務」** ，按一下右鍵WebSphere的Windows服務(IBM webSphere Application Server &lt;version> - &lt;node>)，然後選擇 ******** PropertiesAldings。
1. 在「屬性」對話方塊中，按一下「登 **入」標籤** 。
1. 選 **擇此帳戶** ，並提供設定您要使用的登入帳戶所需的資訊。
1. 將SQL server上的安全性從「混 **合** 」模式設 **置為「Windows身份驗證」**。

### 保護對資料庫中敏感內容的訪問 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms資料庫架構包含有關係統設定和商業程式的敏感資訊，應隱藏在防火牆後方。 應將資料庫考慮在與表單伺服器相同的信任邊界內。 為防止資訊洩漏和業務資料失竊，資料庫必須由資料庫管理員(DBA)配置，才允許授權管理員訪問。

為避免出現這種情況，您應考慮使用資料庫供應商專用的工具來加密包含以下資料的表中的列：

* Rights Management檔案金鑰
* 信任儲存HSM PIN加密密鑰
* 本地用戶密碼散列

有關供應商特定工具的資訊，請參 [閱「資料庫安全資訊」](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全性 {#ldap-security}

輕量型目錄存取通訊協定(LDAP)目錄通常由JEE上的AEM Forms用作企業使用者和群組資訊的來源，以及執行密碼驗證的方式。 您應確定您的LDAP目錄已設定為使用安全通訊端層(SSL)，且JEE上的AEM Forms已設定為使用其SSL連接埠存取您的LDAP目錄。

#### LDAP拒絕服務 {#ldap-denial-of-service}

使用LDAP的常見攻擊涉及攻擊者故意多次驗證失敗。 這會強制LDAP目錄伺服器將用戶從所有依賴LDAP的服務中鎖定。

您可以設定當使用者多次無法向AEM Forms驗證時，AEM Forms實作的失敗嘗試次數和後續鎖定時間。 在管理控制台中，選擇低值。 在選取失敗嘗試次數時，請務必瞭解，在進行所有嘗試後，AEM Forms會先將使用者鎖定在LDAP目錄伺服器上。

#### 設定自動帳戶鎖定 {#set-automatic-account-locking}

1. 登入管理控制台。
1. 按一 **下「設定** >使 **用者管理** >網 **域管理**」。
1. 在「自動帳戶鎖定設定」下， **將「最大連續驗證失敗** 」設為低數目，例如3。
1. 按一下&#x200B;**「儲存」**。

### 審核和記錄 {#auditing-and-logging}

正確且安全地使用應用程式稽核和記錄功能有助於確保盡快追蹤和偵測安全性和其他異常事件。 在應用程式中有效使用稽核和記錄功能，包括追蹤成功登入和失敗登入的項目，以及重要應用程式事件，例如建立或刪除重要記錄。

您可以使用審計來檢測多種攻擊類型，包括：

* 暴力密碼攻擊
* 拒絕服務攻擊
* 植入惡意輸入及相關類的指令碼攻擊

下表說明您可以用來降低伺服器弱點的稽核和記錄技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>日誌檔案ACL</p> </td> 
   <td><p>在JEE記錄檔存取控制清單(ACL)上設定適當的AEM Forms。</p> <p>設定適當的憑證有助於防止攻擊者刪除檔案。</p> <p>日誌檔案目錄的安全權限應為管理員和SYSTEM組的完全控制權。 AEM Forms使用者帳戶應僅具有「讀取」和「寫入」權限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日誌檔案冗餘</p> </td> 
   <td><p>如果資源允許，請使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他機制，將日誌即時發送到攻擊者無法訪問的另一台伺服器（僅寫入）。</p> <p>以這種方式保護日誌有助於防止篡改。 此外，將記錄檔儲存在中央儲存庫有助於關聯和監控（例如，如果使用多個表單伺服器，而且在多部電腦上都會發生密碼猜測攻擊，而每部電腦都會查詢密碼）。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 在JEE上設定AEM Forms，以便在企業以外存取 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安裝AEM Forms後，請務必定期維護您環境的安全性。 本節說明建議的工作，以維護JEE生產伺服器上AEM Forms的安全性。

### 設定反向Proxy以進行Web存取 {#setting-up-a-reverse-proxy-for-web-access}

可 *以使用反向代理* ，以確保JEE網頁應用程式上的AEM Forms URL集可供外部和內部使用者使用。 此設定比讓使用者直接連線至JEE上AEM Forms執行的應用程式伺服器更安全。 反向代理會針對在JEE上執行AEM Forms的應用程式伺服器執行所有HTTP請求。 使用者只能透過網路存取反向代理，且只能嘗試反向代理支援的URL連線。

**AEM Forms on JEE root URLs，以用於反向代理伺服器**

JEE網頁應用程式上每個AEM Forms的下列應用程式根URL。 您只應設定反向代理，以公開您要提供給使用者之Web應用程式功能的URL。

某些URL會反白標示為使用者對應的Web應用程式。 您應避免暴露Configuration manager的其他URL，以便透過反向代理存取外部使用者。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和／或相關的Web應用程式</p> </th> 
   <th><p>網路介面</p> </th> 
   <th><p>使用者存取</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC擴充功能使用者網路應用程式，以套用PDF檔案的使用權</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management最終用戶Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Web服務URL，用於權限管理</p> </td> 
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
   <td><p>工作區一般使用者網頁應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>工作區客戶端應用程式需要的工作區servlet和資料服務</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>在JEE儲存庫上啟動AEM Forms的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>表單伺服器Web服務的資訊頁</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>所有表單伺服器服務的Web服務URL</p> </td> 
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
   <td><p>管理控制台首頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>安全/*</p> </td> 
   <td><p>信任商店管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Forms IVS應用程式，以測試和除錯表單轉換</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>輸出IVS應用於測試和調試輸出服務</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>REST URL for Rights Management</p> </td> 
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
   <td><p>表單Web應用程式檔案</p> </td> 
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
   <td><p>表單管理頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV（除錯）存取的URL</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>應用程式與服務使用者介面</p> </td> 
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
   <td><p>其餘支援頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms on JEE Core Configuration設定頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>使用者管理驗證</p> </td> 
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
   <td><p>上傳和下載在存取遠端端點、SOAP WSDL端點以及啟用HTTP檔案的Java SDK over SOAP傳輸或EJB傳輸時，要處理的檔案。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨網站偽造要求攻擊 {#protecting-from-cross-site-request-forgery-attacks}

跨網站偽造要求(CSRF)攻擊利用網站對使用者的信任來傳輸未經授權且由使用者無意的指令。 此攻擊的設定方式為：在網頁中加入連結或指令碼，或在電子郵件訊息中加入URL，以存取使用者已經驗證的其他網站。

例如，您可能登入Administration Console，同時瀏覽其他網站。 其中一個網頁可以包括HTML影像標籤，該HTML影像標籤具有 `src` 目標在受害者網站上的伺服器端指令碼的屬性。 攻擊網站利用網頁瀏覽器提供的Cookie作業驗證機制，將惡意要求傳送給此受攻擊伺服器端指令碼，偽裝成合法使用者。 如需更多範例，請參 [閱https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples)。

CSRF共有下列特性：

* 涉及依賴使用者身分的網站。
* 利用網站對該身份的信任。
* 誘使使用者的瀏覽器傳送HTTP要求至目標網站。
* 涉及具有副作用的HTTP請求。

AEM Forms on JEE使用「反向連結篩選」功能來封鎖CSRF攻擊。 本節使用下列詞語來說明「反向連結篩選」機制：

* **** 允許的反向連結：反向連結是傳送請求至伺服器之來源頁面的位址。 對於JSP頁面或表單，反向連結通常是瀏覽歷史記錄中的上一頁。 影像的反向連結通常是顯示影像的頁面。 您可以將允許的反向連結新增至允許的反向連結清單，以識別允許存取您伺服器資源的反向連結。
* **** 允許的反向連結例外：您可能想要限制「允許反向連結」清單中特定反向連結的存取範圍。 若要執行此限制，您可以將該反向連結的個別路徑新增至「允許的反向連結例外情況」清單。 「允許的反向連結例外」清單中的路徑所產生的請求無法叫用表單伺服器上的任何資源。 您可以為特定應用程式定義允許的反向連結例外，也可以使用套用至所有應用程式的例外狀況全域清單。
* **** 允許的URI:這是一份資源清單，不需勾選「反向連結標題」即可提供。 例如，不會導致伺服器狀態變更的資源（例如說說明頁面）可以新增至此清單。 「允許的URI」清單中的資源不會被「反向連結篩選器」封鎖，不論反向連結是誰。
* **** 空反向連結：未與父網頁關聯或未源自父網頁的伺服器要求被視為來自空反向連結的請求。 例如，當您開啟新的瀏覽器視窗，輸入位址並按Enter時，傳送至伺服器的反向連結為null。 對Web伺服器發出HTTP請求的案頭應用程式（.NET或SWING）也會向伺服器發送空反向連接。

### 反向連結篩選 {#referer-filtering}

「反向連結篩選」程式可說明如下：

1. Forms伺服器檢查用於調用的HTTP方法：

   1. 如果是POST，表單伺服器會執行「反向連結」標題檢查。
   1. 如果是GET，表單伺服器會略過「反向連結」檢查，除非 *CSRF_CHECK_GETS* 設定為true，否則會執行「反向連結」標題檢查。 *CSRF_CHECK_GETS* 是在應用程 *式的web.xml* 檔案中指定。

1. Forms伺服器檢查請求的URI是否為白名單：

   1. 如果URI已列入白名單，則伺服器接受請求。
   1. 如果請求的URI未列入白名單，則伺服器將檢索請求的反向連結。

1. 如果請求中有反向連結，伺服器會檢查它是否為「允許的反向連結」。 如果允許，伺服器會檢查反向連結例外：

   1. 如果是例外，則會封鎖請求。
   1. 如果不是例外，則會傳遞請求。

1. 如果請求中沒有反向連結，伺服器會檢查是否允許空反向連結：

   1. 如果允許空反向連結，則會傳遞請求。
   1. 如果不允許Null反向連結，伺服器會檢查請求的URI是否為Null反向連結的例外，並據以處理請求。

### 管理反向連結篩選 {#managing-referer-filtering}

JEE上的AEM Forms提供「反向連結篩選」，以指定允許存取您伺服器資源的反向連結。 依預設，反向連結篩選器不會篩選使用安全HTTP方法（例如GET）的請求，除非 *CSRF_CHECK_GETS* 設定為true。 如果「允許的反向連結」項目的埠號設定為0,JEE上的AEM Forms將允許來自該主機的所有具有反向連結的請求，而不論其埠號為何。 如果未指定埠號，則僅允許來自預設埠80(HTTP)或埠443(HTTPS)的請求。 如果「允許的反向連結」清單中的所有項目都已刪除，則會停用「反向連結篩選」。

首次安裝Document Services時，「允許反向連結」清單會更新為安裝Document services的伺服器位址。 伺服器的條目包括伺服器名、IPv4地址、IPv6地址（如果啟用了IPv6）、環回地址和localhost條目。 主機作業系統會傳回新增至「允許反向連結」清單的名稱。 例如，IP位址為10.40.54.187的伺服器將包含下列項目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`。 對於主機作業系統重新調整的任何不合格名稱（沒有IPv4地址、IPv6地址或限定域名的名稱），不更新白名單。 修改「允許的反向連結」清單以符合您的商業環境。 請勿使用預設的「允許反向連結」清單，在生產環境中部署表單伺服器。 修改任何「允許的反向連結」、「反向連結例外」或URI後，請確定您重新啟動伺服器，讓變更生效。

**管理允許的反向連結清單**

您可以從管理控制台的使用者管理介面管理允許的反向連結清單。 使用者管理介面提供您建立、編輯或刪除清單的功能。 如需使用「允 *[許的反向連結](/help/forms/using/admin-help/preventing-csrf-attacks.md)*」清單的詳細資訊，請&#x200B;*參閱管理說明的*「防止CSRF攻擊」一節。

**管理允許的反向連結例外和允許的URI清單**

JEE上的AEM Forms提供API來管理「允許的反向連結例外」清單和「允許的URI」清單。 您可以使用這些API來擷取、建立、編輯或刪除清單。 以下是可用API的清單：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

如需API的詳 *細資訊，請參閱JEE API參考上的AEM* Forms。

在全局級 ***別使用LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** list表示允許的反向連結例外，即定義適用於所有應用程式的例外。 此清單僅包含具有絕對路徑(如 `/index.html`)或相對路徑(例如 `/sample/`)。 您也可以將規則運算式附加至相對URI的結尾，例如 `/sample/(.)*`。

LC_ ***GLOBAL_ALLOWED_REFERER_EXCEPTION*** 清單ID在命名空間類中定義為常 `UMConstants` 數， `com.adobe.idp.um.api` 如中所示 `adobe-usermanager-client.jar`。 您可以使用AEM Forms API來建立、修改或編輯此清單。 例如，若要建立「允許的全域反向連結例外」清單，請使用：

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用 ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** 清單來查看特定於應用程式的異常。

**停用反向連結篩選**

如果「反向連結篩選」完全封鎖對表單伺服器的存取，而您無法編輯「允許的反向連結」清單，您可以更新伺服器啟動指令碼並停用「反向連結篩選」。

將 `-Dlc.um.csrffilter.disabled=true` JAVA引數加入啟動指令碼並重新啟動伺服器。 請確定您在正確重新設定「允許的反向連結」清單後刪除JAVA引數。

**自訂WAR檔案的反向連結篩選**

您可能已建立自訂WAR檔案，以便搭配AEM Forms on JEE運作，以符合您的業務需求。 若要為自訂WAR檔案啟用「反向連結篩選」，請在WAR的類別路徑中加入 ***adobe-usermanager-client.jar*** ，並在 ** web.xml檔案中加入篩選條目，並包含以下參數：

**CSRF_CHECK_GETS控制GET請求的** 「反向連結」檢查。 如果未定義此參數，則預設值設定為false。 只有在您要篩選GET請求時，才加入此參數。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是「允許的反向連結例外」清單的ID。 「反向連結篩選」可防止來自清單ID所識別清單中反向連結的請求在表單伺服器上叫用任何資源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是「允許的URI」清單的ID。 反向連結篩選器不會封鎖清單ID所識別清單中任何資源的請求，不論請求中反向連結標題的值為何。

**當反向連結為null或不存在時** ,CSRF_ALLOW_NULL_REFERER控制「反向連結篩選」行為。 如果未定義此參數，則預設值設定為false。 只有在您要允許空反向連結時，才加入此參數。 允許空反向連結可能允許某些類型的跨網站偽造要求攻擊。

**CSRF_NULL_REFERER_EXCEPTIONS** 是URI的清單，當反向連結為null時，不會對其執行反向連結檢查。 僅當 *CSRF_ALLOW_NULL_REFERER設定為false時* ，才啟用此參數。 以逗號分隔清單中的多個URI。

以下是 *SAMPLE* WAR檔案 ****** web.xml檔案中篩選條目的範例：

```as3
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

如果CSRF篩選器封鎖了合法的伺服器要求，請嘗試下列其中一項：

* 如果拒絕的請求有「反向連結」標題，請謹慎考慮將它新增至「允許的反向連結」清單。 只新增您信任的反向連結。
* 如果拒絕的請求沒有反向連結標題，請修改您的用戶端應用程式以包含反向連結標題。
* 如果用戶端可在瀏覽器中運作，請嘗試該部署模型。
* 作為最後的手段，您可以將資源添加到「允許的URI」清單。 這不是建議的設定。

## 安全的網路配置 {#secure-network-configuration}

本節說明AEM Forms on JEE所需的通訊協定和埠，並提供在JEE上部署AEM Forms以安全網路組態的建議。

### AEM Forms在JEE上使用的網路通訊協定 {#network-protocols-used-by-aem-forms-on-jee}

當您如上節所述設定安全網路架構時，JEE上的AEM Forms與企業網路中其他系統之間的互動需要下列網路通訊協定。

<table> 
 <thead> 
  <tr> 
   <th><p>協定</p> </th> 
   <th><p>使用</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>瀏覽器顯示配置管理器和最終用戶Web應用程式</p> </li> 
     <li><p>所有SOAP連接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服務客戶端應用程式，如。NET應用程式</p> </li> 
     <li><p>Adobe Reader®在JEE伺服器網站服務上使用SOAP for AEM Forms</p> </li> 
     <li><p>Adobe Flash®應用程式使用SOAP來建立表單伺服器web services</p> </li> 
     <li><p>在SOAP模式中使用AEM Forms on JEE SDK呼叫</p> </li> 
     <li><p>工作台設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在「企業版JavaBeans(EJB)」模式中使用AEM Forms on JEE SDK呼叫</p> </td> 
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
   <td><p>AEM Forms on JEE監控受監視的資料夾，以輸入至服務（受監視的資料夾端點）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>目錄中組織用戶和組資訊的同步</p> </li> 
     <li><p>適用於互動式使用者的LDAP驗證</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>使用JDBC服務執行進程期間對外部資料庫進行的查詢和過程調用</p> </li> 
     <li><p>JEE存放庫上的內部存取AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>可讓任何WebDAV用戶端在JEE設計時儲存庫（表單、片段等）上遠端瀏覽AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe Flash應用程式，其中JEE伺服器服務上的AEM Forms設定有Remoting端點</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms on JEE公開MBeans以使用JMX進行監控</p> </td> 
  </tr> 
 </tbody> 
</table>

### 應用程式伺服器的埠 {#ports-for-application-servers}

本節介紹每種支援的應用程式伺服器類型的預設埠（和備用配置範圍）。 這些埠必須在內部防火牆上啟用或停用，視您要允許在JEE上執行AEM Forms的應用程式伺服器上連線的網路功能而定。

>[!NOTE]
>
>依預設，伺服器會在adobe.com命名空間下公開數個JMX MBean。 僅公開對伺服器運行狀況監視有用的資訊。 不過，為防止資訊洩漏，您應防止不受信任網路中的呼叫者尋找JMX MBeans並存取健康度量。

**JBoss埠**

<table> 
 <thead> 
  <tr> 
   <th><p>目的</p> </th> 
   <th><p>埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>存取Web應用程式</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1連接器埠8080</p> <p>AJP 1.3介面埠8009</p> <p>SSL/TLS連接器埠8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支援</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic埠**

<table> 
 <thead> 
  <tr> 
   <th><p>目的</p> </th> 
   <th><p>埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>存取Web應用程式</p> </td> 
   <td> 
    <ul> 
     <li><p>管理伺服器偵聽埠：預設值為7001</p> </li> 
     <li><p>管理伺服器SSL監聽埠：預設值為7002</p> </li> 
     <li><p>為受控伺服器配置的埠，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>在JEE上存取AEM Forms不需要WebLogic管理埠</p> </td> 
   <td> 
    <ul> 
     <li><p>受控伺服器偵聽埠：可配置從1到65534</p> </li> 
     <li><p>受控伺服器SSL偵聽埠：可配置從1到65534</p> </li> 
     <li><p>節點管理器偵聽埠：預設為5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere埠**

如需AEM Forms on JEE需要的WebSphere埠相關資訊，請至WebSphere Application Server UI中的「Port number」（埠號）設定。

### 設定SSL {#configuring-ssl}

參照JEE上的 [AEM Forms物理架構一節所述的物理架構](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您應針對您計畫使用的所有連線設定SSL。 具體來說，所有SOAP連線都必須透過SSL進行，以防止使用者憑證暴露在網路上。

如需如何在JBoss、WebLogic和WebSphere上配置SSL的說明，請參閱管理幫助中的「配置SSL [」](https://www.adobe.com/go/learn_aemforms_admin_64)。

### 設定SSL重新導向 {#configuring-ssl-redirect}

在將應用程式伺服器設定為支援SSL後，您必須確保所有應用程式和服務的HTTP流量都強制使用SSL連接埠。

若要設定WebSphere或WebLogic的SSL重新導向，請參閱您的應用程式伺服器檔案。

1. 開啟命令提示符，導航至/JBOSS_HOME/standalone/configuration目錄，然後執行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 開啟JBOSS_HOME/standalone/configuration/standalone.xml檔案以進行編輯。

   在&lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素之後，添加以下詳細資訊：

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https連接器元素中新增下列程式碼：

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   儲存並關閉standalone.xml檔案。

## Windows特定的安全性建議 {#windows-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，Windows專屬的安全性建議。

### JBoss服務帳戶 {#jboss-service-accounts}

依預設，AEM Forms on JEE統包安裝會使用本機系統帳戶來設定服務帳戶。 內建的本機系統使用者帳戶具備高度的協助功能；它屬於管理員組。 如果工作進程身份作為本地系統用戶帳戶運行，則該工作進程具有對整個系統的完全訪問權限。

#### 使用非管理帳戶運行應用程式伺服器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶，以以下方式登錄：

   * 選擇「 **用戶不能更改密碼**」。
   * 在「成 **員** 」標籤上，請確定已列出「使用者」群組。

1. 選擇「 **設定** >管 **理工具** >服 **務」**。
1. 連按兩下應用程式伺服器服務並停止服務。
1. 在「登 **錄** 」標籤上，選 ****&#x200B;擇「此帳戶」，瀏覽您建立的用戶帳戶，並輸入帳戶的密碼。
1. 在「本地安全設定」窗口的「用戶權限分配」下，為運行表單伺服器的用戶帳戶提供以下權限：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄
   * 以服務身分登入（應已設定）

1. 為JEE網頁內容目錄上的AEM Forms提供新使用者帳戶的「讀取與執行」、「清單資料夾內容」和「讀取」權限。
1. 啟動應用程式伺服器服務。

### 檔案系統安全性 {#file-system-security}

AEM Forms on JEE使用檔案系統的方式如下：

* 儲存處理檔案輸入與輸出時使用的暫存檔案
* 將用於支援已安裝的解決方案元件的檔案儲存在全局存檔儲存中
* 受監視的資料夾儲存被丟棄的檔案，這些檔案用作從檔案系統資料夾位置輸入到服務

當使用受監視的資料夾來傳送和接收使用表單伺服器服務的檔案時，請格外注意檔案系統的安全性。 當使用者將內容拖放至監看的資料夾時，該內容會透過觀看的資料夾公開。 在這種情況下，服務不會驗證實際的最終用戶。 相反，它依賴於在資料夾級別設定ACL和共用級別安全，以確定哪些人可以有效調用服務。

## JBoss特定的安全性建議 {#jboss-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，JBoss 7.0.6專屬的應用程式伺服器設定建議。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

當您使用完善的安裝方法在JBoss的JEE上安裝AEM Forms時，已設定JBoss管理主控台和JMX主控台的存取權（JMX監視已停用）。 如果您使用自己的JBoss Application Server，請確保對JBoss管理控制台和JMX監控控制台的訪問安全。 對JMX監控控制台的訪問權在名為jmx-invoker-service.xml的JBoss配置檔案中設定。

### 禁用目錄瀏覽 {#disable-directory-browsing}

登入Administration Console後，可修改URL，以瀏覽主控台的目錄清單。 例如，如果您將URL變更為下列其中一個URL，則可能會出現目錄清單：

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic特定的安全性建議 {#weblogic-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時保護WebLogic 9.1的應用程式伺服器設定建議。

### 禁用目錄瀏覽 {#disable_directory_browsing-1}

將weblogic.xml檔案中的index-directorys屬性設定為 `false`，如以下示例所示：

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 啟用WebLogic SSL埠 {#enable-weblogic-ssl-port}

依預設，WebLogic不會啟用預設的SSL監聽埠7002。 在配置SSL之前，請在WebLogic server管理控制台中啟用此埠。

## WebSphere特定的安全性建議 {#websphere-specific-security-recommendations}

本節包含應用程式伺服器設定建議，以保護在JEE上執行AEM Forms的WebSphere。

### 禁用目錄瀏覽 {#disable_directory_browsing-2}

將ibm- `directoryBrowsingEnabled` web-ext.xml檔案中的屬性設定為 `false`。

### 啟用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登入WebSphere管理控制台。
1. 在導覽樹狀結構中，前往「 **安全性** >全 **域安全性」**
1. 選擇 **啟用管理安全**。
1. 取消選 **取「啟用應用程式保全** 」 **和「使用Java 2保全」**。
1. 按一 **下「確定** 」或「 **套用」**。
1. 在「消 **息** 」框中，單 **擊「直接保存到主配置」**。

