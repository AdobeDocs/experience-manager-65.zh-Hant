---
title: 在JEE環境中強化您的AEM Forms
seo-title: 在JEE環境中強化您的AEM Forms
description: 瞭解各種安全性強化設定，以增強AEM Forms在企業內部網路中執行JEE時的安全性。
seo-description: 瞭解各種安全性強化設定，以增強AEM Forms在企業內部網路中執行JEE時的安全性。
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '7699'
ht-degree: 0%

---


# 在JEE環境中強化您的AEM Forms{#hardening-your-aem-forms-on-jee-environment}

瞭解各種安全性強化設定，以增強AEM Forms在企業內部網路中執行JEE時的安全性。

文章介紹了保護在JEE上運行AEM Forms的伺服器安全的建議和最佳做法。 對於您的作業系統和應用程式伺服器，此檔案並非完整的主機強化檔案。 相反，本文描述了您應實作的各種安全強化設定，以增強在公司內部網路內執行的JEE上AEM Forms的安全性。 不過，為確保JEE應用程式伺服器上的AEM Forms保持安全，您也應實作安全性監控、偵測和回應程式。

本文描述在安裝和配置生命週期的以下階段應用的強化技術：

* **預安裝：在** JEE上安裝AEM Forms之前，請先使用這些技巧。
* **安裝：在** AEM Forms的JEE安裝程式中使用這些技巧。
* **安裝後：安裝** 後請定期使用這些技巧。

AEM Forms的JEE可高度自訂，可在多種不同的環境中運作。 有些建議可能不符合您組織的需求。

## 預安裝{#preinstallation}

在JEE上安裝AEM Forms之前，您可以將安全解決方案應用到網路層和作業系統。 本節將說明一些問題，並建議您減少這些領域的安全性弱點。

**在UNIX和Linux上安裝和配置**

您不應使用根shell在JEE上安裝或配置AEM Forms。 依預設，檔案會安裝在/opt目錄下，而執行安裝的使用者需要/opt下的所有檔案權限。 或者，您也可以在個別使用者/user目錄下執行安裝，而使用者已擁有所有檔案權限。

**在Windows上安裝和配置**

如果您要在JBoss上使用統包方法在JEE上安裝AEM Forms，或者您要安裝PDF Generator，則您應以管理員身份在Windows上執行安裝。 此外，在具備原生應用程式支援的Windows上安裝PDF產生器時，您必須與安裝Microsoft Office的Windows使用者一樣執行安裝。 有關安裝權限的詳細資訊，請參閱*在JEE*上安裝和部署AEM Forms文檔，以瞭解您的應用伺服器。

### 網路層安全{#network-layer-security}

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
   <td><p>在非軍事區(DMZ)內部署表單伺服器。 區段至少應存在於兩個層級，而應用程式伺服器用來在JEE上執行位於內部防火牆後方的AEM Forms。 將外部網路與包含Web伺服器的DMZ分離，而Web伺服器又必須與內部網路分離。 使用防火牆來實現分層。 對流經每個網路層的流量進行分類和控制，以確保僅允許所需資料的絕對最小值。</p> </td> 
  </tr> 
  <tr> 
   <td><p>專用IP地址</p> </td> 
   <td><p>在AEM Forms應用程式伺服器上，將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用。 指定私有IP位址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難以透過網際網路將NAT內部主機的流量路由至網路。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火牆</p> </td> 
   <td><p>使用以下標準選擇防火牆解決方案：</p> 
    <ul> 
     <li><p>實施支援代理伺服器和／或<em>狀態檢查</em>的防火牆，而不是簡單的包過濾解決方案。</p> </li> 
     <li><p>使用支援<em>的防火牆拒絕除明確允許的</em>安全範例外的所有服務。</p> </li> 
     <li><p>實作雙歸屬或多歸屬的防火牆解決方案。 此架構提供最高等級的安全性，並協助防止未經授權的使用者略過防火牆安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>資料庫埠</p> </td> 
   <td><p>請勿對資料庫使用預設監聽埠(MySQL - 3306、Oracle- 1521、MS SQL - 1433)。 有關更改資料庫埠的資訊，請參見資料庫文檔。</p> <p>使用不同的資料庫埠會影響JEE配置上的整體AEM Forms。 如果更改了預設埠，則必須在其它配置區域進行相應的修改，如JEE上的AEM Forms資料源。</p> <p>有關在JEE上配置AEM Forms資料源的資訊，請參閱<a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms使用手冊</a>中的「在JEE上安裝並升級AEM Forms」或在JEE上升級到AEM Forms」。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 作業系統安全性{#operating-system-security}

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

有關作業系統的其他安全資訊，請參閱[「作業系統安全資訊」](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安裝{#installation}

本節說明在AEM Forms安裝過程中可使用的技術，以降低安全性弱點。 在某些情況下，這些技術會使用屬於安裝程式一部分的選項。 下表說明這些技巧。

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
   <td><p>使用安裝軟體所需的最少權限數。 使用不在「管理員」群組中的帳戶登入您的電腦。 在Windows上，您可以使用「執行方式」命令，以管理使用者身分，在JEE安裝程式上執行AEM Forms。 在UNIX和Linux系統上，使用<code>sudo</code>之類的命令來安裝軟體。</p> </td> 
  </tr> 
  <tr> 
   <td><p>軟體源</p> </td> 
   <td><p>請勿從不受信任的來源下載或執行JEE上的AEM Forms。</p> <p>惡意程式可能包含數種違反安全性的程式碼，包括資料竊取、修改和刪除，以及拒絕服務。 從AdobeDVD或僅從受信任的來源，將AEM Forms安裝在JEE上。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁碟分區</p> </td> 
   <td><p>將AEM Forms置於JEE上的專用磁碟分區。 磁碟分段是將伺服器上的特定資料保存在單獨的物理磁碟上，以增加安全性的過程。 以這種方式安排資料可降低目錄遍歷攻擊的風險。 計畫建立與系統分區分開的分區，您可以在其上將AEM Forms安裝在JEE內容目錄上。 （在Windows上，系統分區包含system32目錄或引導分區。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>元件</p> </td> 
   <td><p>評估現有服務，並停用或解除安裝任何不需要的服務。 請勿安裝不必要的元件和服務。</p> <p>應用程式伺服器的預設安裝可能包含您使用時不需要的服務。 在部署之前，您應禁用所有不必要的服務，以最大限度地減少攻擊的入口點。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符檔案中注釋掉不必要的服務。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨網域原則檔案</p> </td> 
   <td><p>伺服器上存在<code>crossdomain.xml</code>檔案可能會立即削弱該伺服器。 建議您盡可能限制網域清單。 使用「參考線<em>（不建議使用）</em>」時，請勿將開發期間使用的<code>crossdomain.xml</code>檔案置入生產環境。 對於使用web services的指南，如果服務位於提供該指南的同一伺服器上，則完全不需要<code>crossdomain.xml</code>檔案。 但是，如果服務位於另一台伺服器上，或如果涉及群集，則需要存在<code>crossdomain.xml</code>檔案。 有關crossdomain.xml檔案的詳細資訊，請參閱<a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p>作業系統安全性設定</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，請確保安裝<code>pkcs11_softtoken_extra.so</code>而不是<code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安裝後步驟{#post-installation-steps}

在JEE上成功安裝AEM Forms後，從安全形度定期維護環境非常重要。

下節詳細說明建議的保護已部署表單伺服器的不同任務。

### AEM Forms安全{#aem-forms-security}

下列建議的設定適用於JEE伺服器上的AEM Forms（非管理Web應用程式）。 要降低伺服器的安全風險，請在將AEM Forms安裝到JEE後立即應用這些設定。

**安全性修補程式**

如果供應商未及時應用安全補丁和升級，未經授權的用戶可能會獲得對應用程式伺服器的訪問，這一風險增加。 在將安全性修補程式套用至生產伺服器之前，請先加以測試，以確保應用程式的相容性和可用性。 此外，建立策略和程式以定期檢查和安裝修補程式。 AEM Forms的JEE更新位於企業產品下載網站。

**服務帳戶（僅Windows上的JBoss統包）**

AEM FormsJEE上預設會使用LocalSystem帳戶安裝服務。 內建的LocalSystem使用者帳戶具備高階的協助功能；它屬於管理員組。 如果工作進程身份作為LocalSystem用戶帳戶運行，則該工作進程可以完全訪問整個系統。

要運行部署JEE上的AEM Forms的應用程式伺服器，請使用特定的非管理帳戶，按照以下說明操作：

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶，以以下方式登錄：

   * 選擇&#x200B;**用戶不能更改密碼**。
   * 在&#x200B;**成員Of**&#x200B;標籤上，確保列出&#x200B;**用戶**&#x200B;組。

   >[!NOTE]
   >
   >您無法變更PDF產生器的此設定。

1. 選擇&#x200B;**開始** > **設定** > **管理工具** > **服務**。
1. 連按兩下JEE上的JBoss forAEM Forms並停止服務。
1. 在&#x200B;**登入**&#x200B;標籤上，選擇&#x200B;**此帳戶**，瀏覽您建立的使用者帳戶，並輸入帳戶的密碼。
1. 在MMC中，開啟&#x200B;**本地安全設定**&#x200B;並選擇&#x200B;**本地策略** > **用戶權限分配**。
1. 將下列權限指派給Forms伺服器所在之使用者帳戶：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄
   * 以服務身分登入（應已設定）

1. 為下列目錄授予新用戶帳戶修改權限：
   * **全域檔案儲存(GDS)目錄**:GDS目錄的位置是在AEM Forms安裝過程中手動配置的。如果位置設定在安裝期間保持空，則位置預設為`[JBoss root]/server/[type]/svcnative/DocumentStorage`應用程式伺服器安裝下的目錄
   * **CRX-Repository目錄**:預設位置為  `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登入使用者的首頁目錄
在基於UNIX的系統上，非根用戶可以使用以下目錄作為臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄提供新用戶帳戶的寫權限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的預設安裝位置：
   > * Windows:C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/

1. 啟動應用程式伺服器。

**禁用配置管理器引導Servlet**

配置管理器使用部署在應用程式伺服器上的servlet來執行JEE資料庫上的AEM Forms的引導。 由於配置管理器在配置完成之前訪問此servlet，因此對其的訪問尚未對授權用戶進行安全保護，並且在您成功使用配置管理器在JEE上配置AEM Forms後，應禁用它。

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
1. 注釋adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 戰爭模組如下：

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
1. 壓縮EAR檔案，並將它重新部署至應用程式伺服器。
1. 啟動AEM Forms伺服器。
1. 在瀏覽器中輸入下列URL以測試變更，並確保其不再運作。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**鎖定對信任儲存的遠程訪問**

Configuration Manager可讓您將Acrobat Reader DC擴充功能憑證上傳到JEE信任商店的AEM Forms。 這表示依預設，已啟用透過遠端通訊協定（SOAP和EJB）存取信任商店憑證服務的功能。 當您使用Configuration Manager上傳權限憑證或您稍後決定使用Administration Console管理憑證後，就不再需要此存取。

您可以按照[中的步驟禁用對所有信任儲存服務的遠程訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)禁用對服務的非基本遠程訪問。

**禁用所有非必要的匿名訪問**

某些表單伺服器服務具有可由匿名呼叫者調用的操作。 如果不需要匿名訪問這些服務，請按照[禁用對服務的非必要匿名訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)中的步驟禁用它。

#### 更改預設管理員密碼{#change-the-default-administrator-password}

安裝JEE上的AEM Forms時，將為用戶Super Administrator/ login-id Administrator配置一個預設用戶帳戶，預設密碼為&#x200B;*password*。 您應使用配置管理器立即更改此密碼。

1. 在網頁瀏覽器中輸入下列URL:

   ```java
   https://[host name]:[port]/adminui
   ```

   預設埠號是以下其中之一：

   **JBoss:** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080。

1. 在&#x200B;**用戶名**&#x200B;欄位中鍵入`administrator` ，在&#x200B;**密碼**&#x200B;欄位中鍵入`password`。
1. 按一下「**設定** > **使用者管理** > **使用者和群組**」。
1. 在&#x200B;**Find**&#x200B;欄位中鍵入`administrator`，然後按一下&#x200B;**Find**。
1. 從用戶清單中按一下&#x200B;**超級管理員**。
1. 按一下「編輯用戶」頁上的&#x200B;**更改密碼**。
1. 指定新密碼，然後按一下「保存」。****

此外，建議通過執行以下步驟來更改CRX管理員的預設密碼：

1. 使用預設的用戶名／密碼登錄到`https://[server]:[port]/lc/libs/granite/security/content/useradmin.html`。
1. 在搜索欄位中鍵入Administrator ，然後按一下&#x200B;**Go**。
1. 從搜索結果中選擇&#x200B;**管理員** ，然後按一下用戶介面右下方的&#x200B;**編輯**&#x200B;表徵圖。
1. 在&#x200B;**新密碼**&#x200B;欄位中指定新密碼，在&#x200B;**您的密碼**&#x200B;欄位中指定舊密碼。
1. 按一下使用者介面右下方的「儲存」圖示。

#### 禁用WSDL生成{#disable-wsdl-generation}

Web服務定義語言(WSDL)產生只能用於開發環境，開發人員會使用WSDL產生來建立其用戶端應用程式。 您可以選擇在生產環境中停用WSDL產生功能，以避免暴露服務的內部詳細資訊。

1. 在網頁瀏覽器中輸入下列URL:

   ```java
   https://[host name]:[port]/adminui
   ```

1. 按一下&#x200B;**設定>核心繫統設定>配置**。
1. 取消選擇「啟用WSDL **」，然後按一下「確定」。******

### 應用程式伺服器安全性{#application-server-security}

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
   <td><p>在應用程式伺服器上安裝、設定和部署JEE上的AEM Forms後，您應停用對應用程式伺服器管理主控台的存取。 如需詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>應用程式伺服器Cookie設定</p> </td> 
   <td><p>應用程式Cookie由應用程式伺服器控制。 部署應用程式時，應用程式伺服器管理員可以指定整個伺服器或特定應用程式的Cookie偏好設定。 依預設，伺服器設定會優先使用。</p> <p>您的應用程式伺服器產生的所有作業Cookie都應包含<code>HttpOnly</code>屬性。 例如，使用JBoss Application Server時，可以將SessionCookie元素修改為<code>WEB-INF/web.xml</code>檔案中的<code>httpOnly="true"</code>。</p> <p>您可以限制使用僅HTTPS傳送的Cookie。 因此，不會透過HTTP傳送未加密的檔案。 應用程式伺服器管理員應全域啟用伺服器的安全Cookie。 例如，使用JBoss Application Server時，可以將<code>server.xml</code>檔案中的連接器元素修改為<code>secure=true</code>。</p> <p>如需Cookie設定的詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目錄瀏覽</p> </td> 
   <td><p>當有人請求不存在的頁面或請求控制器名稱(請求字串以斜線(/)結尾)時，應用程式伺服器不應傳回該目錄的內容。 為避免此問題，您可以停用應用程式伺服器上的目錄瀏覽。 您應針對管理控制台應用程式和伺服器上執行的其他應用程式執行此動作。</p> <p>對於JBoss，請將web.xml檔案中<code>DefaultServlet</code>屬性的清單初始化參數的值設定為<code>false</code>，如以下示例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;預設&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;清單&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;3&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>對於WebSphere，將ibm-web-ext.xmi檔案中的<code>directoryBrowsingEnabled</code>屬性設定為<code>false</code>。</p> <p>對於WebLogic，請將weblogic.xml檔案中的index-directories屬性設定為<code>false</code>，如以下示例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 資料庫安全{#database-security}

在保護資料庫時，應實施資料庫供應商描述的測量。 您應該為資料庫用戶分配最低要求的資料庫權限，以供AEM Forms在JEE上使用。 例如，請勿使用具有資料庫管理員權限的帳戶。

在Oracle中，您使用的資料庫帳戶只需要CONNECT、資源和CREATE VIEW權限。 有關其他資料庫的類似要求，請參見[準備在JEE（單伺服器）上安裝AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上為JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}配置SQL Server的整合安全性

1. 修改[JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml}以將`integratedSecurity=true`新增至連線URL，如以下範例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 將「從本地系統登錄為」的JBoss Windows服務(JBoss forAEM Forms在JEE上)屬性修改為具有AEM Forms資料庫和最小權限集的登錄帳戶。 如果從命令行而不是作為Windows服務運行JBoss，則無需執行此步驟。
1. 將SQL Server的安全性從&#x200B;**Mixed**&#x200B;模式設定為&#x200B;**僅Windows身份驗證**。

#### 在Windows上為WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}配置SQL Server的整合安全性

1. 在Web瀏覽器的URL行中鍵入以下URL，以啟動WebLogic Server管理控制台：

   ```java
   https://[host name]:7001/console
   ```

1. 在「變更中心」下，按一下「鎖定與編輯」**。**
1. 在「域結構」下，按一下「*[base_domain]* > **服務** > **JDBC** > **資料源**」，在右窗格中按一下「**IDP_DS**」。
1. 在下一個螢幕上，在&#x200B;**Configuration**&#x200B;頁籤上，按一下&#x200B;**Connection Pool**&#x200B;頁籤，在&#x200B;**Properties**&#x200B;框中，鍵入`integratedSecurity=true`。
1. 在「域結構」下，按一下「**[base_domain]** > **服務** > **JDBC** > **資料源**」，在右窗格中按一下「**RM_DS**」。
1. 在下一個螢幕上，在&#x200B;**Configuration**&#x200B;頁籤上，按一下&#x200B;**Connection Pool**&#x200B;頁籤，在&#x200B;**Properties**&#x200B;框中，鍵入`integratedSecurity=true`。
1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 將SQL Server的安全性從&#x200B;**Mixed**&#x200B;模式設定為&#x200B;**僅Windows身份驗證**。

#### 在Windows上為WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}配置SQL Server的整合安全性

在WebSphere上，只有當使用外部SQL Server JDBC驅動程式時，才可配置整合安全性，而不是嵌入WebSphere的SQL Server JDBC驅動程式。

1. 登入WebSphere管理控制台。
1. 在導航樹中，按一下「資源」>「**「資源」>「** JDBC」>「**資料源」，在右窗格中按一下「** IDP_DS」**。******
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下「Custom Properties（自定義屬性）」**，然後按一下「New（新建）」**。****
1. 在&#x200B;**Name**&#x200B;方塊中，鍵入`integratedSecurity`，在&#x200B;**Value**&#x200B;方塊中鍵入`true`。
1. 在導航樹中，按一下「資源」>「**「資源」>「** JDBC」>「**資料源」，在右窗格中按一下「** RM_DS」**。******
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下「Custom Properties（自定義屬性）」**，然後按一下「New（新建）」**。****
1. 在&#x200B;**Name**&#x200B;方塊中，鍵入`integratedSecurity`，在&#x200B;**Value**&#x200B;方塊中鍵入`true`。
1. 在安裝WebSphere的電腦上，將sqljdbc_auth.dll檔案添加到Windows系統路徑(C:\Windows)。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 1.2驅動程式安裝位置相同（預設為&#x200B;*[InstallDir]*/sqljdbc_1.2/enu/auth/x86）。
1. 選擇&#x200B;**開始** > **控制面板** > **服務**，按一下右鍵WebSphere的Windows服務(IBM WebSphere Application Server &lt;version> - &lt;node>)，然後選擇&#x200B;**屬性**。
1. 在「屬性」對話框中，按一下「登錄」頁籤。****
1. 選擇&#x200B;**此帳戶**&#x200B;並提供設定您要使用的登錄帳戶所需的資訊。
1. 將SQL Server上的安全性從&#x200B;**Mixed**&#x200B;模式設定為&#x200B;**僅Windows身份驗證**。

### 保護對資料庫{#protecting-access-to-sensitive-content-in-the-database}中敏感內容的訪問

AEM Forms資料庫模式包含有關係統配置和業務流程的敏感資訊，應隱藏在防火牆後面。 應將資料庫考慮在與表單伺服器相同的信任邊界內。 為防止資訊洩漏和業務資料失竊，資料庫必須由資料庫管理員(DBA)配置，才允許授權管理員訪問。

為避免出現這種情況，您應考慮使用資料庫供應商專用的工具來加密包含以下資料的表中的列：

* Rights Management文檔鍵
* 信任儲存HSM PIN加密密鑰
* 本地用戶密碼散列

有關特定於供應商的工具的資訊，請參見[「資料庫安全資訊」](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全{#ldap-security}

輕量型目錄訪問協定(LDAP)目錄通常由JEE上的AEM Forms用作企業用戶和組資訊的源，以及執行密碼驗證的方法。 您應確保將LDAP目錄配置為使用安全套接字層(SSL)，並將JEE上的AEM Forms配置為使用其SSL埠訪問LDAP目錄。

#### LDAP拒絕服務{#ldap-denial-of-service}

使用LDAP的常見攻擊涉及攻擊者故意多次驗證失敗。 這會強制LDAP目錄伺服器將用戶從所有依賴LDAP的服務中鎖定。

您可以設定當使用者多次無法向AEM Forms驗證時，AEM Forms所實施的失敗嘗試次數和後續鎖定時間。 在管理控制台中，選擇低值。 在選擇失敗嘗試次數時，請務必瞭解，在進行所有嘗試後，AEM Forms會在LDAP目錄伺服器之前將用戶鎖定。

#### 設定自動帳戶鎖定{#set-automatic-account-locking}

1. 登入管理控制台。
1. 按一下「**設定** > **用戶管理** > **域管理**」。
1. 在「自動帳戶鎖定設定」下，將「最大連續驗證失敗數&#x200B;**」設定為低數，例如3。**
1. 按一下「**儲存**」。

### 審計和記錄{#auditing-and-logging}

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
   <td><p>在JEE日誌檔案訪問控制清單(ACL)上設定適當的AEM Forms。</p> <p>設定適當的憑證有助於防止攻擊者刪除檔案。</p> <p>日誌檔案目錄的安全權限應為管理員和SYSTEM組的完全控制權。 AEM Forms用戶帳戶應僅具有「讀取」和「寫入」權限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日誌檔案冗餘</p> </td> 
   <td><p>如果資源允許，請使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他機制，將日誌即時發送到攻擊者無法訪問的另一台伺服器（僅寫入）。</p> <p>以這種方式保護日誌有助於防止篡改。 此外，將記錄檔儲存在中央儲存庫有助於關聯和監控（例如，如果使用多個表單伺服器，而且在多部電腦上都會發生密碼猜測攻擊，而每部電腦都會查詢密碼）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 讓非管理員使用者可執行PDF產生器

您可以讓非管理員使用者使用PDF產生器。 一般而言，只有具有管理權限的使用者才能使用PDF產生器。 執行下列步驟，讓非管理員使用者執行PDF產生器：

1. 建立環境變數名稱PDFG_NON_ADMIN_ENABLED。

1. 將變數的值設為TRUE。

1. 重新啟動AEM Forms實例。

## 在JEE上配置AEM Forms，以便訪問企業以外的{#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安裝AEM Forms後，請務必定期維護您環境的安全性。 本節介紹為維護AEM Forms在JEE生產伺服器上的安全而建議的任務。

### 為Web訪問設定反向代理{#setting-up-a-reverse-proxy-for-web-access}

*reverse proxy*&#x200B;可用來確保JEE Web應用程式上的AEM FormsURL集可供外部和內部使用者使用。 此配置比允許用戶直接連接到JEE上的AEM Forms正在運行的應用程式伺服器更安全。 反向代理會對在JEE上運行AEM Forms的應用程式伺服器執行所有HTTP請求。 使用者只能透過網路存取反向代理，且只能嘗試反向代理支援的URL連線。

**AEM Forms的JEE根URL，可與反向代理伺服器搭配使用**

JEE Web應用程式上每個AEM Forms的下列應用程式根URL。 您只應設定反向代理，以公開您要提供給使用者之Web應用程式功能的URL。

某些URL會反白標示為使用者對應的Web應用程式。 您應避免暴露Configuration Manager的其他URL，以便透過反向代理存取外部使用者。

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
   <td><p>Acrobat Reader DC擴充功能使用者網頁應用程式，以套用PDF檔案的使用權</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management用戶Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>用於Rights Management的Web服務URL</p> </td> 
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
   <td><p>用於在JEE儲存庫上引導AEM Forms的Servlet</p> </td> 
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
   <td><p>FormsIVS應用程式，用於測試和除錯表單轉換</p> </td> 
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
   <td><p>Rights Management的REST URL</p> </td> 
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
   <td><p>Forms網路應用程式檔案</p> </td> 
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
   <td><p>AEM FormsJEE核心配置設定頁</p> </td> 
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

## 防止跨網站偽造要求攻擊{#protecting-from-cross-site-request-forgery-attacks}

跨網站偽造要求(CSRF)攻擊利用網站對使用者的信任來傳輸未經授權且由使用者無意的指令。 此攻擊的設定方式為：在網頁中加入連結或指令碼，或在電子郵件訊息中加入URL，以存取使用者已經驗證的其他網站。

例如，您可能登入Administration Console，同時瀏覽其他網站。 其中一個網頁可以包括具有`src`屬性的HTML影像標籤，該屬性針對受害網站上的伺服器端指令碼。 攻擊網站利用網頁瀏覽器提供的Cookie作業驗證機制，將惡意要求傳送給此受攻擊伺服器端指令碼，偽裝成合法使用者。 如需更多範例，請參閱[https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples)。

CSRF共有下列特性：

* 涉及依賴使用者身分的網站。
* 利用網站對該身份的信任。
* 誘使使用者的瀏覽器傳送HTTP要求至目標網站。
* 涉及具有副作用的HTTP請求。

AEM Forms的JEE使用反向連結篩選功能來封鎖CSRF攻擊。 本節使用下列詞語來說明「反向連結篩選」機制：

* **允許的反向連** 結：反向連結是傳送請求至伺服器之來源頁面的位址。對於JSP頁面或表單，反向連結通常是瀏覽歷史記錄中的上一頁。 影像的反向連結通常是顯示影像的頁面。 您可以將允許的反向連結新增至允許的反向連結清單，以識別允許存取您伺服器資源的反向連結。
* **允許的反向連結例** 外：您可能想要限制「允許的反向連結」清單中特定反向連結的存取範圍。若要執行此限制，您可以將該反向連結的個別路徑新增至「允許的反向連結例外情況」清單。 「允許的反向連結例外」清單中的路徑所產生的請求無法叫用表單伺服器上的任何資源。 您可以為特定應用程式定義允許的反向連結例外，也可以使用套用至所有應用程式的例外狀況全域清單。
* **允許的URI:** 這是要提供的資源清單，不需勾選「反向連結標題」。例如，不會導致伺服器狀態變更的資源（例如說明頁面）可以新增至此清單。 「允許的URI」清單中的資源不會被「反向連結篩選器」封鎖，不論反向連結是誰。
* **Null反向連** 結：未與父網頁關聯或未源自父網頁的伺服器要求被視為來自Null反向連結的請求。例如，當您開啟新的瀏覽器視窗，輸入位址並按Enter時，傳送至伺服器的反向連結為null。 對Web伺服器發出HTTP請求的案頭應用程式（.NET或SWING）也會向伺服器發送空反向連接。

### 反向連結篩選{#referer-filtering}

「反向連結篩選」程式可說明如下：

1. Forms伺服器檢查用於調用的HTTP方法：

   1. 如果是POST，表單伺服器會執行「反向連結」標題檢查。
   1. 如果是GET，表單伺服器會略過「反向連結」檢查，除非&#x200B;*CSRF_CHECK_GETS*&#x200B;設定為true，否則它會執行「反向連結」標題檢查。 *CSRF_CHECK_* GETS是在應用程 *式的web.* xmlfile中指定。

1. Forms伺服器檢查請求的URI是否存在於allowlist中：

   1. 如果允許列出URI，則伺服器接受請求。
   1. 如果未允許列出請求的URI，則伺服器會檢索請求的反向連結。

1. 如果請求中有反向連結，伺服器會檢查它是否為「允許的反向連結」。 如果允許，伺服器會檢查反向連結例外：

   1. 如果是例外，則會封鎖請求。
   1. 如果不是例外，則會傳遞請求。

1. 如果請求中沒有反向連結，伺服器會檢查是否允許空反向連結：

   1. 如果允許空反向連結，則會傳遞請求。
   1. 如果不允許Null反向連結，伺服器會檢查請求的URI是否為Null反向連結的例外，並據以處理請求。

### 管理反向連結篩選{#managing-referer-filtering}

AEM Forms在JEE上提供「反向連結篩選」，以指定允許存取您伺服器資源的反向連結。 依預設，反向連結篩選器不會篩選使用安全HTTP方法(例如GET)的請求，除非&#x200B;*CSRF_CHECK_GETS*&#x200B;設定為true。 如果「允許的反向連結」項目的埠號設為0,JEE上的AEM Forms將允許來自該主機的所有具有反向連結的請求，而不論其埠號為何。 如果未指定埠號，則僅允許來自預設埠80(HTTP)或埠443(HTTPS)的請求。 如果「允許的反向連結」清單中的所有項目都已刪除，則會停用「反向連結篩選」。

首次安裝Document Services時，「允許反向連結」清單會更新為安裝Document Services的伺服器位址。 伺服器的條目包括伺服器名、IPv4地址、IPv6地址（如果啟用了IPv6）、環回地址和localhost條目。 主機作業系統會傳回新增至「允許反向連結」清單的名稱。 例如，IP位址為10.40.54.187的伺服器將包含下列項目：`https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`。 對於主機作業系統重新調整的任何不合格名稱（沒有IPv4地址、IPv6地址或限定域名的名稱），不會更新允許清單。 修改「允許的反向連結」清單以符合您的商業環境。 請勿使用預設的「允許反向連結」清單，在生產環境中部署表單伺服器。 修改任何「允許的反向連結」、「反向連結例外」或URI後，請確定您重新啟動伺服器，讓變更生效。

**管理允許的反向連結清單**

您可以從管理控制台的使用者管理介面管理允許的反向連結清單。 使用者管理介面提供您建立、編輯或刪除清單的功能。 有關使用「允許反向連結」清單的詳細資訊，請參閱&#x200B;*管理說明*&#x200B;的「防止CSRF攻擊](/help/forms/using/admin-help/preventing-csrf-attacks.md)*」一節。[

**管理允許的反向連結例外和允許的URI清單**

AEM Forms在JEE上提供API來管理允許的反向連結例外清單和允許的URI清單。 您可以使用這些API來擷取、建立、編輯或刪除清單。 以下是可用API的清單：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

如需API的詳細資訊，請參閱*AEM Forms的JEE API參考*。

使用全局級別「允許的反向連結例外」的&#x200B;***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION***&#x200B;清單，即定義適用於所有應用程式的例外。 此清單僅包含具有絕對路徑(如`/index.html`)或相對路徑(例如`/sample/`)。 您也可以將規則運算式附加至相對URI的結尾，例如`/sample/(.)*`。

***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION***&#x200B;清單ID在`adobe-usermanager-client.jar`命名空間的`UMConstants`類中定義為常數。 `com.adobe.idp.um.api`您可以使用AEM FormsAPI來建立、修改或編輯此清單。 例如，若要建立「允許的全域反向連結例外」清單，請使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用&#x200B;***CSRF_ALLOWED_REFERER_EXCEPTIONS***&#x200B;清單來顯示應用程式特定的例外情況。

**停用反向連結篩選**

如果「反向連結篩選」完全封鎖對表單伺服器的存取，而您無法編輯「允許的反向連結」清單，您可以更新伺服器啟動指令碼並停用「反向連結篩選」。

將`-Dlc.um.csrffilter.disabled=true` JAVA參數包含在啟動指令碼中並重新啟動伺服器。 請確定您在正確重新設定「允許的反向連結」清單後刪除JAVA引數。

**自訂WAR檔案的反向連結篩選**

您可能已建立自訂的WAR檔案，以便與AEM Forms在JEE上合作，以符合您的業務需求。 要為自定義WAR檔案啟用反向連接過濾，請在WAR的類路徑中包含&#x200B;***adobe-usermanager-client.jar***，並在* web.xml*檔案中包含一個包含以下參數的過濾器條目：

**CSRF_CHECK_** GETS控制對GET請求的反向連結檢查。如果未定義此參數，則預設值設定為false。 只有在您要篩選您的GET請求時，才加入此參數。

**CSRF_ALLOWED_REFERER_** EXCEPTIONS是「允許的反向連結例外」清單的ID。「反向連結篩選」可防止來自清單ID所識別清單中反向連結的請求在表單伺服器上叫用任何資源。

**CSRF_ALLOWED_URIS_LIST_** NAME是「允許的URI」清單的ID。反向連結篩選器不會封鎖清單ID所識別清單中任何資源的請求，不論請求中反向連結標題的值為何。

**CSRF_ALLOW_NULL_** REFERER在反向連結為null或不存在時控制反向連結篩選器行為。如果未定義此參數，則預設值設定為false。 只有在您要允許空反向連結時，才加入此參數。 允許空反向連結可能允許某些類型的跨網站偽造要求攻擊。

**CSRF_NULL_REFERER_** EXCEPTIONS是URI的清單，當反向連結為null時，不會對其執行反向連結檢查。僅當&#x200B;*CSRF_ALLOW_NULL_REFERER*&#x200B;設定為false時，才啟用此參數。 以逗號分隔清單中的多個URI。

以下是&#x200B;***SAMPLE*** WAR檔案&#x200B;*web.xml*&#x200B;檔案中的篩選器條目示例：

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

如果CSRF篩選器封鎖了合法的伺服器要求，請嘗試下列其中一項：

* 如果拒絕的請求有「反向連結」標題，請謹慎考慮將它新增至「允許的反向連結」清單。 只新增您信任的反向連結。
* 如果拒絕的請求沒有反向連結標題，請修改您的用戶端應用程式以包含反向連結標題。
* 如果用戶端可在瀏覽器中運作，請嘗試該部署模型。
* 作為最後的手段，您可以將資源添加到「允許的URI」清單。 這不是建議的設定。

## 安全網路配置{#secure-network-configuration}

本節介紹AEM Forms在JEE上所需的協定和埠，並為在安全網路配置中部署AEM Forms在JEE上提供建議。

### AEM Forms在JEE上使用的網路協定{#network-protocols-used-by-aem-forms-on-jee}

如上節所述，當您設定安全網路架構時，JEE上的AEM Forms與您企業網路中其他系統之間的互動需要下列網路通訊協定。

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
     <li><p>Adobe Reader®在JEE伺服器web服務上使用AEM Forms的SOAP</p> </li> 
     <li><p>AdobeFlash®應用程式使用SOAP來建立表單伺服器web services</p> </li> 
     <li><p>AEM Forms在SOAP模式下使用JEE SDK呼叫</p> </li> 
     <li><p>工作台設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>AEM FormsJEE SDK呼叫(用於企業版JavaBeans(EJB)模式)</p> </td> 
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
   <td><p>AEM Forms:JEE監視受監視資料夾以輸入到服務（受監視資料夾端點）</p> </td> 
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
     <li><p>JEE儲存庫上的AEM Forms內部訪問</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>允許任何WebDAV客戶端在JEE設計時儲存庫（表單、片段等）上遠程瀏覽AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash應用程式，其中AEM FormsJEE伺服器服務上的服務配置了遠程端點</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM FormsJEE公開MBeans以使用JMX進行監控</p> </td> 
  </tr> 
 </tbody> 
</table>

### 應用程式伺服器{#ports-for-application-servers}的埠

本節介紹每種支援的應用程式伺服器類型的預設埠（和備用配置範圍）。 這些埠必須在內部防火牆上啟用或禁用，具體取決於您要允許連接到運行JEE上AEM Forms的應用程式伺服器的客戶端的網路功能。

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
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1連接器埠8080</p> <p>AJP 1.3連接器埠8009</p> <p>SSL/TLS連接器埠8443</p> </td> 
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
   <td><p>在JEE上訪問AEM Forms不需要WebLogic管理埠</p> </td> 
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

有關JEE上的AEM Forms需要的WebSphere埠的資訊，請轉至WebSphere Application Server UI中的「埠號」設定。

### 配置SSL {#configuring-ssl}

參照JEE物理體系結構](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)上的[AEM Forms一節中所述的物理體系結構，您應為您計畫使用的所有連接配置SSL。 具體來說，所有SOAP連線都必須透過SSL進行，以防止使用者憑證暴露在網路上。

有關如何在JBoss、WebLogic和WebSphere上配置SSL的說明，請參閱[管理幫助](https://www.adobe.com/go/learn_aemforms_admin_64)中的「配置SSL」。

如需如何將憑證匯入至為AEM Forms伺服器設定的JVM(Java Virtual Machine)的指示，請參閱[AEM Forms工作台說明](http://www.adobe.com/go/learn_aemforms_workbench_65)中的「相互驗證」一節。

### 配置SSL重定向{#configuring-ssl-redirect}

在將應用程式伺服器設定為支援SSL後，您必須確保所有應用程式和服務的HTTP流量都強制使用SSL連接埠。

若要設定WebSphere或WebLogic的SSL重新導向，請參閱您的應用程式伺服器檔案。

1. 開啟命令提示符，導航至/JBOSS_HOME/standalone/configuration目錄，然後執行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 開啟JBOSS_HOME/standalone/configuration/standalone.xml檔案以進行編輯。

   在&lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素之後，添加以下詳細資訊：

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. 在https連接器元素中新增下列程式碼：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   儲存並關閉standalone.xml檔案。

## Windows特定安全性建議{#windows-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，Windows專屬的安全性建議。

### JBoss服務帳戶{#jboss-service-accounts}

AEM Forms的JEE統包安裝預設會使用本機系統帳戶來設定服務帳戶。 內建的本機系統使用者帳戶具備高度的協助功能；它屬於管理員組。 如果工作進程身份作為本地系統用戶帳戶運行，則該工作進程具有對整個系統的完全訪問權限。

#### 使用非管理帳戶{#run-the-application-server-using-a-non-administrative-account}運行應用程式伺服器

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶，以以下方式登錄：

   * 選擇&#x200B;**用戶不能更改密碼**。
   * 在&#x200B;**成員**&#x200B;標籤上，確保列出「用戶」組。

1. 選擇「**設定** > **管理工具** > **服務**」。
1. 連按兩下應用程式伺服器服務並停止服務。
1. 在&#x200B;**登入**&#x200B;標籤上，選擇&#x200B;**此帳戶**，瀏覽您建立的使用者帳戶，並輸入帳戶的密碼。
1. 在「本地安全設定」窗口的「用戶權限分配」下，為運行表單伺服器的用戶帳戶提供以下權限：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄xx
   * 以服務身分登入（應已設定）

1. 為下列目錄授予新用戶帳戶修改權限：
   * **全域檔案儲存(GDS)目錄**:GDS目錄的位置是在AEM Forms安裝過程中手動配置的。如果位置設定在安裝期間保持空，則位置預設為`[JBoss root]/server/[type]/svcnative/DocumentStorage`應用程式伺服器安裝下的目錄
   * **CRX-Repository目錄**:預設位置為  `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登入使用者的首頁目錄
在基於UNIX的系統上，非根用戶可以使用以下目錄作為臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄提供新用戶帳戶的寫權限：
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的預設安裝位置：
   > * Windows:C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/。


1. 啟動應用程式伺服器服務。

### 檔案系統安全{#file-system-security}

AEM Forms在JEE上使用檔案系統的方式如下：

* 儲存處理檔案輸入與輸出時使用的暫存檔案
* 將用於支援已安裝的解決方案元件的檔案儲存在全局存檔儲存中
* 受監視的資料夾儲存被丟棄的檔案，這些檔案用作從檔案系統資料夾位置輸入到服務

當使用受監視的資料夾來傳送和接收使用表單伺服器服務的檔案時，請格外注意檔案系統的安全性。 當使用者將內容拖放至監看的資料夾時，該內容會透過觀看的資料夾公開。 在這種情況下，服務不會驗證實際的最終用戶。 相反，它依賴於在資料夾級別設定ACL和共用級別安全，以確定哪些人可以有效調用服務。

## JBoss特定的安全建議{#jboss-specific-security-recommendations}

本節包含在JEE上運行AEM Forms時特定於JBoss 7.0.6的應用程式伺服器配置建議。

### 禁用JBoss管理控制台和JMX控制台{#disable-jboss-management-console-and-jmx-console}

當您使用完善的安裝方法在JBoss的JEE上安裝AEM Forms時，已配置了對JBoss管理控制台和JMX控制台的訪問（JMX監視被禁用）。 如果您使用自己的JBoss Application Server，請確保對JBoss管理控制台和JMX監控控制台的訪問安全。 對JMX監控控制台的訪問權在名為jmx-invoker-service.xml的JBoss配置檔案中設定。

### 禁用目錄瀏覽{#disable-directory-browsing}

登入Administration Console後，可修改URL來瀏覽主控台的目錄清單。 例如，如果您將URL變更為下列其中一個URL，則可能會出現目錄清單：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic特定安全性建議{#weblogic-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時保護WebLogic 9.1的應用程式伺服器組態建議。

### 禁用目錄瀏覽{#disable_directory_browsing-1}

將weblogic.xml檔案中的index-directories屬性設定為`false` ，如以下示例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 啟用WebLogic SSL埠{#enable-weblogic-ssl-port}

依預設，WebLogic不會啟用預設的SSL監聽埠7002。 在配置SSL之前，請在WebLogic Server管理控制台中啟用此埠。

## WebSphere特定的安全性建議{#websphere-specific-security-recommendations}

本節包含應用程式伺服器組態建議，以保護在JEE上執行AEM Forms的WebSphere。

### 禁用目錄瀏覽{#disable_directory_browsing-2}

將ibm-web-ext.xml檔案中的`directoryBrowsingEnabled`屬性設為`false`。

### 啟用WebSphere管理安全性{#enable-websphere-administrative-security}

1. 登入WebSphere管理控制台。
1. 在導航樹中，轉至&#x200B;**Security** > **Global Security**
1. 選擇&#x200B;**啟用管理安全**。
1. 取消選擇&#x200B;**啟用應用程式安全**&#x200B;和&#x200B;**使用Java 2安全**。
1. 按一下&#x200B;**確定**&#x200B;或&#x200B;**應用**。
1. 在&#x200B;**消息**&#x200B;框中，按一下&#x200B;**直接保存到主配置**。