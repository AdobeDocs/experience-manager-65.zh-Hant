---
title: 在JEE環境中強化AEM Forms
seo-title: Hardening Your AEM Forms on JEE Environment
description: 了解各種安全性強化設定，以增強AEM Forms在企業內部網路中執行的JEE安全性。
seo-description: Learn a variety of security-hardening settings to enhance the security of AEM Forms on JEE running in a corporate intranet.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: d2661ee6614261179b5e8d2d9ffb7c240ce676dc
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 0%

---

# 在JEE環境中強化AEM Forms {#hardening-your-aem-forms-on-jee-environment}

了解各種安全性強化設定，以增強AEM Forms在企業內部網路中執行的JEE安全性。

本文說明在JEE上執行AEM Forms時，保護伺服器安全的建議和最佳實務。 這不是適用於作業系統和應用程式伺服器的全面的主機強化文檔。 相反地，本文說明您應實作的各種安全性強化設定，以增強在企業內部網路中執行之JEE上AEM Forms的安全性。 不過，為了確保JEE應用程式伺服器上的AEM Forms保持安全，您也應實作安全性監控、偵測和回應程式。

本文描述了在安裝和配置生命週期的以下階段應應用的硬化技術：

* **安裝前：** 在JEE上安裝AEM Forms之前，請先使用這些技巧。
* **安裝：** 在AEM Forms on JEE安裝程式中使用這些技術。
* **安裝後：** 安裝後使用這些技術，之後定期使用。

AEM Forms on JEE可提供高度自訂功能，且可在多種不同環境中運作。 有些建議可能不符合您組織的需求。

## 預安裝 {#preinstallation}

在JEE上安裝AEM Forms之前，您可以將安全性解決方案套用至網路層和作業系統。 本節介紹一些問題，並就減少這些領域的安全漏洞提出建議。

**在UNIX和Linux上安裝和配置**

您不應在JEE上使用根殼層安裝或設定AEM Forms。 預設情況下，檔案安裝在/opt目錄下，執行安裝的用戶需要/opt下的所有檔案權限。 或者，可以在個別使用者已擁有所有檔案權限的/user目錄下執行安裝。

**在Windows上安裝和配置**

如果您是在JBoss上使用統包方法在JEE上安裝AEM Forms，或是安裝PDF產生器，您應以管理員身分在Windows上執行安裝。 此外，在具有本機應用程式支援的Windows上安裝PDF產生器時，您必須以安裝Microsoft Office的相同Windows使用者身分執行安裝。 如需安裝權限的詳細資訊，請參閱*在JEE*上安裝和部署AEM Forms檔案，了解您的應用程式伺服器。

### 網路層安全 {#network-layer-security}

網路安全漏洞是任何面向網際網路或面向內聯網的應用伺服器面臨的首要威脅之一。 本節介紹針對這些漏洞強化網路上主機的過程。 它解決了網路分段、傳輸控制協定/網際網路協定(TCP/IP)棧強化以及使用防火牆進行主機保護等問題。

下表介紹了減少網路安全漏洞的常見過程。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非軍事區(DMZ)</p> </td> 
   <td><p>在非軍事區(DMZ)中部署表單伺服器。 區段至少應存在於兩個層級，內部防火牆後面應用程式伺服器用來在JEE上執行AEM Forms。 將外部網路與包含Web伺服器的DMZ分開，而Web伺服器又必須與內部網路分開。 使用防火牆來實施分離層。 對通過每個網路層的流量進行分類和控制，以確保僅允許絕對最小的所需資料。</p> </td> 
  </tr> 
  <tr> 
   <td><p>專用IP地址</p> </td> 
   <td><p>在AEM Forms應用程式伺服器上，使用網路位址轉譯(NAT)與RFC 1918專用IP位址。 分配專用IP地址(10.0.0.0/8 、 172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難通過Internet將通信路由到NAT內部主機和從內部主機發送。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火牆</p> </td> 
   <td><p>使用以下條件選擇防火牆解決方案：</p> 
    <ul> 
     <li><p>實作支援Proxy伺服器和/或的防火牆 <em>有狀態檢查</em> 而非簡單的封包篩選解決方案。</p> </li> 
     <li><p>使用支援 <em>拒絕除明確允許外的所有服務</em> 安全范式。</p> </li> 
     <li><p>實作雙本位或多本位的防火牆解決方案。 此體系結構提供最高級別的安全性，並有助於防止未經授權的用戶繞過防火牆安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>資料庫埠</p> </td> 
   <td><p>請勿使用資料庫的預設監聽埠(MySQL - 3306、Oracle- 1521、MS SQL - 1433)。 有關更改資料庫埠的資訊，請參閱資料庫文檔。</p> <p>使用不同的資料庫埠會影響JEE上的整體AEM Forms設定。 如果您變更預設連接埠，則必須在其他設定區域進行對應的修改，例如JEE上AEM Forms的資料來源。</p> <p>如需有關在JEE版AEM Forms中設定資料來源的資訊，請參閱在JEE上安裝和升級AEM Forms，或在JEE版升級至AEM Forms，以取得您的應用程式伺服器的位置： <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms使用手冊</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 作業系統安全性 {#operating-system-security}

下表說明一些將作業系統中發現的安全漏洞最小化的潛在方法。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p></th> 
   <th><p>說明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全補丁</p></td> 
   <td><p>如果未及時應用供應商安全補丁程式和升級，則未經授權的用戶可能獲得對應用程式伺服器的訪問的風險增加。 先測試安全補丁程式，然後再將其應用到生產伺服器。</p><p>此外，建立策略和過程以定期檢查和安裝修補程式。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防護軟體</p></td> 
   <td><p>病毒掃描程式可以通過掃描簽名或監視異常行為來識別受感染的檔案。 掃描程式會將其病毒簽名保存在檔案中，該檔案通常儲存在本地硬碟上。 由於新病毒經常被發現，因此您應經常更新此檔案，以便病毒掃描器識別所有當前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>網路時間協定(NTP)</p></td> 
   <td><p>要進行法證分析，請在表單伺服器上保持準確的時間。 使用NTP來同步所有直接連接到Internet的系統上的時間。</p></td> 
  </tr> 
 </tbody> 
</table>

有關作業系統的其他安全資訊，請參閱 [&quot;作業系統安全資訊&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## 安裝 {#installation}

本節說明在AEM Forms安裝程式期間，您可使用哪些技術來減少安全性弱點。 在某些情況下，這些技術會使用屬於安裝流程一部分的選項。 下表說明這些技術。

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
   <td><p>使用安裝軟體所需的最少權限數。 使用不在「管理員」組中的帳戶登錄到電腦。 在Windows上，您可以使用「執行方式」命令，以管理使用者身分在JEE安裝程式上執行AEM Forms。 在UNIX和Linux系統上，使用命令，如 <code>sudo</code> 安裝軟體。</p> </td> 
  </tr> 
  <tr> 
   <td><p>軟體源</p> </td> 
   <td><p>請勿從不受信任的來源在JEE上下載或執行AEM Forms。</p> <p>惡意程式可能包含數種違反安全的代碼，包括資料竊取、修改和刪除以及拒絕服務。 從AdobeDVD或僅從信任的來源在JEE上安裝AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁碟分區</p> </td> 
   <td><p>將AEM Forms放在JEE上的專用磁碟分區上。 磁碟分段是一種過程，它將伺服器上的特定資料保留在單獨的物理磁碟上，以增加安全性。 以此方式排列資料可降低目錄遍歷攻擊的風險。 計畫建立與系統分區分開的分區，您可以在JEE內容目錄上安裝AEM Forms。 （在Windows上，系統分區包含system32目錄或引導分區。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>元件</p> </td> 
   <td><p>評估現有服務，並停用或解除安裝任何不需要的服務。 請勿安裝不必要的元件和服務。</p> <p>應用程式伺服器的預設安裝可能包含您使用時不需要的服務。 在部署之前，應禁用所有不必要的服務，以盡量減少攻擊的入口點。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符檔案中注釋不必要的服務。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略檔案</p> </td> 
   <td><p>存在 <code>crossdomain.xml</code> 伺服器上的檔案可能會立即削弱該伺服器。 建議您盡可能限制網域清單。 請勿將 <code>crossdomain.xml</code> 使用參考線時，在開發到生產環境期間使用的檔案 <em>（已過時）</em>. 對於使用Web服務的指南，如果服務位於提供指南的相同伺服器上，則 <code>crossdomain.xml</code> 完全不需要檔案。 但是，如果服務位於另一台伺服器上，或如果涉及群集，則存在 <code>crossdomain.xml</code> 需要檔案。 請參閱 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>，以取得crossdomain.xml檔案的詳細資訊。</p> </td> 
  </tr> 
  <tr> 
   <td><p>作業系統安全設定</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，請確保安裝 <code>pkcs11_softtoken_extra.so</code> 而非 <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安裝後步驟 {#post-installation-steps}

在JEE上成功安裝AEM Forms後，請務必從安全性的角度定期維護環境。

以下部分詳細說明了為保護已部署的表單伺服器而建議執行的不同任務。

### AEM Forms安全性 {#aem-forms-security}

下列建議的設定適用於JEE伺服器上管理Web應用程式以外的AEM Forms。 若要降低伺服器的安全風險，請在JEE上安裝AEM Forms後立即套用這些設定。

**安全補丁**

如果未及時應用供應商安全補丁程式和升級，則未經授權的用戶可能會獲得對應用程式伺服器的訪問權，這一風險增加。 在將安全補丁程式應用到生產伺服器之前測試這些補丁程式，以確保應用程式的相容性和可用性。 此外，建立策略和過程以定期檢查和安裝修補程式。 AEM Forms on JEE更新位於企業產品下載網站。

**服務帳戶（僅Windows上的JBoss統包）**

AEM Forms on JEE依預設會使用LocalSystem帳戶來安裝服務。 內置的LocalSystem用戶帳戶具有高級別的可訪問性；它是管理員組的一部分。 如果工作進程標識以LocalSystem用戶帳戶的形式運行，則該工作進程可以完整訪問整個系統。

若要使用特定的非管理帳戶，執行部署JEE上AEM Forms的應用程式伺服器，請遵循下列指示：

1. 在Microsoft管理控制台(MMC)中，建立表單伺服器服務的本機使用者以下列方式登入：

   * 選擇 **用戶無法更改密碼**.
   * 在 **成員** 標籤，確保 **使用者** 已列出群組。

   >[!NOTE]
   >
   >您無法為PDF產生器變更此設定。

1. 選擇 **開始** > **設定** > **管理工具** > **服務**.
1. 在JEE上連按兩下適用於AEM Forms的JBoss ，然後停止服務。
1. 在 **登入** 索引標籤，選取 **此帳戶**，瀏覽您建立的使用者帳戶，然後輸入帳戶的密碼。
1. 在MMC中，開啟 **本機安全設定** 選取 **本地策略** > **用戶權限分配**.
1. 將下列權限指派給表單伺服器所執行的使用者帳戶：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄
   * 以服務身份登錄（應已設定）

1. 授予新用戶帳戶對以下目錄的修改權限：
   * **全局文檔儲存(GDS)目錄**:在AEM Forms安裝過程中，會手動配置GDS目錄的位置。 如果安裝期間位置設定保持空，則位置預設為應用程式伺服器安裝下的目錄，位置位於 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目錄**:預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登錄用戶的主目錄在基於UNIX的系統上，非根用戶可以將以下目錄用作臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄授予新用戶帳戶的寫入權限：
   * [JBoss-directory]\dastanale\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的預設安裝位置：
   >
   >* 窗口：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux:/opt/jboss/


1. 啟動應用程式伺服器。

**禁用Configuration Manager引導Servlet**

配置管理器使用部署在應用程式伺服器上的servlet，在JEE資料庫上執行AEM Forms的引導。 由於設定管理員在設定完成前即存取了此servlet，因此授權使用者的存取權限並未受到保護，且在您成功使用Configuration Manager在JEE上設定AEM Forms後，應停用此servlet。

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
1. 註解adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 戰爭模組如下：

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

1. 保存並關閉META-INF/application.xml檔案。
1. 壓縮EAR檔案，並將其重新部署至應用程式伺服器。
1. 啟動AEM Forms伺服器。
1. 在瀏覽器中輸入下列URL以測試變更，並確認變更不再有效。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**鎖定對信任儲存的遠程訪問**

Configuration Manager可讓您將Acrobat Reader DC擴充功能憑證上傳至JEE信任存放區上的AEM Forms。 這意味著預設情況下，已啟用通過遠程協定（SOAP和EJB）訪問信任儲存憑據服務。 使用Configuration Manager上載權限憑據後，或者如果您決定稍後使用管理控制台來管理憑據，則不再需要此訪問。

您可以按照一節中的步驟禁用對所有信任儲存服務的遠程訪問 [禁用對服務的非必需遠程訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**禁用所有非必需的匿名訪問**

某些表單伺服器服務具有可由匿名調用者調用的操作。 如果不需要匿名訪問這些服務，請按照 [禁用對服務的非必需匿名訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### 更改預設管理員密碼 {#change-the-default-administrator-password}

當安裝JEE上的AEM Forms時，會為使用者Super Administrator/ login-id Administrator設定單一預設使用者帳戶，其預設密碼為 *密碼*. 您應使用Configuration Manager立即更改此密碼。

1. 在網頁瀏覽器中輸入下列URL:

   ```java
   https://[host name]:[port]/adminui
   ```

   預設埠號為以下之一：

   **JBoss:** 8080

   **WebLogic伺服器：** 7001

   **WebSphere:** 9080。

1. 在 **使用者名稱** 欄位，類型 `administrator` 和 **密碼** 欄位，類型 `password`.
1. 按一下 **設定** > **使用者管理** > **使用者和群組**.
1. 類型 `administrator` 在 **查找** 欄位，然後按一下 **查找**.
1. 按一下 **超級管理員** 從用戶清單中。
1. 按一下 **更改密碼** 在「編輯用戶」頁上。
1. 指定新密碼，然後按一下 **儲存**.

此外，建議您執行下列步驟，更改CRX管理員的預設密碼：

1. 登入 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 使用預設的使用者名稱/密碼。
1. 在搜索欄位中鍵入Administrator ，然後按一下 **開始**.
1. 選擇 **管理員** 按一下搜尋結果中的 **編輯** 圖示。
1. 在 **新密碼** 欄位和 **密碼** 欄位。
1. 按一下使用者介面右下角的「儲存」圖示。

#### 禁用WSDL生成 {#disable-wsdl-generation}

只應為開發環境啟用Web服務定義語言(WSDL)生成，其中開發人員使用WSDL生成來構建其客戶端應用程式。 您可以選擇在生產環境中禁用WSDL生成，以避免顯示服務的內部詳細資訊。

1. 在網頁瀏覽器中輸入下列URL:

   ```java
   https://[host name]:[port]/adminui
   ```

1. 按一下 **設定>核心繫統設定>配置**.
1. 取消選擇 **啟用WSDL** 按一下 **確定**.

### 應用程式伺服器安全性 {#application-server-security}

下表說明在安裝JEE應用程式上的AEM Forms後，保護應用程式伺服器的一些技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>應用程式伺服器管理控制台</p> </td> 
   <td><p>在應用程式伺服器上於JEE安裝、設定和部署AEM Forms後，您應停用應用程式伺服器管理主控台的存取權。 如需詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>應用程式伺服器Cookie設定</p> </td> 
   <td><p>應用程式Cookie由應用程式伺服器控制。 部署應用程式時，應用程式伺服器管理員可以指定伺服器範圍或應用程式特定的Cookie偏好設定。 依預設，伺服器設定會優先使用。</p> <p>應用程式伺服器產生的所有工作階段Cookie都應包含 <code>HttpOnly</code> 屬性。 例如，使用JBoss Application Server時，您可以將SessionCookie元素修改為 <code>httpOnly="true"</code> 在 <code>WEB-INF/web.xml</code> 檔案。</p> <p>您可以限制僅使用HTTPS傳送的Cookie。 因此，系統不會透過HTTP以未加密方式傳送。 應用程式伺服器管理員應在全域基礎上為伺服器啟用安全Cookie。 例如，使用JBoss Application Server時，您可以將連接器元素修改為 <code>secure=true</code> 在 <code>server.xml</code> 檔案。</p> <p>如需Cookie設定的詳細資訊，請參閱應用程式伺服器檔案。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目錄瀏覽</p> </td> 
   <td><p>當有人請求不存在的頁面或請求控制器名稱時(請求字串以斜線(/)結尾)，應用程式伺服器不應返回該目錄的內容。 要防止此情況，可以禁用應用程式伺服器上的目錄瀏覽。 您應為管理控制台應用程式和伺服器上運行的其他應用程式執行此操作。</p> <p>針對JBoss，設定 <code>DefaultServlet</code> 屬性 <code>false</code> 在web.xml檔案中，如以下範例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;預設&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;清單&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>若為WebSphere，請設定 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi檔案中的屬性 <code>false</code>.</p> <p>對於WebLogic，請將weblogic.xml檔案中的index-directories屬性設定為 <code>false</code>，如以下範例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 資料庫安全 {#database-security}

保護資料庫時，應實施資料庫供應商描述的度量。 您應將資料庫使用者配置為JEE上AEM Forms所授予之最低必要資料庫權限。 例如，請勿使用具有資料庫管理員權限的帳戶。

在Oracle上，您使用的資料庫帳戶僅需要CONNECT、資源和建立視圖權限。 如需其他資料庫的類似需求，請參閱 [準備在JEE上安裝AEM Forms（單一伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### 為JBoss在Windows上的SQL Server配置整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml}要添加 `integratedSecurity=true` 至連線URL，如以下範例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起位置。
1. 將「從本機系統登入」的JBoss Windows服務(JBoss for AEM Forms on JEE)屬性修改為具有AEM Forms資料庫且具有最低特權集的登入帳戶。 如果您是從命令列執行JBoss而非以Windows服務的形式執行，則不需要執行此步驟。
1. 從 **混合** 模式 **僅限Windows驗證**.

#### 為Windows上的SQL Server配置WebLogic的整合安全 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 在Web瀏覽器的URL行中鍵入以下URL，以啟動WebLogic Server管理控制台：

   ```java
   https://[host name]:7001/console
   ```

1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯**.
1. 在「域結構」(Domain Structure)下，按一下 *[base_domain]* > **服務** > **JDBC** > **資料來源** 在右窗格中，按一下 **IDP_DS**.
1. 在下一個畫面上， **設定** ，按一下 **連接池** ，在 **屬性** 框，類型 `integratedSecurity=true`.
1. 在「域結構」(Domain Structure)下，按一下 **[base_domain]** > **服務** > **JDBC** > **資料來源** 在右窗格中，按一下 **RM_DS**.
1. 在下一個畫面上， **設定** ，按一下 **連接池** ，在 **屬性** 框，類型 `integratedSecurity=true`.
1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 6.2.1.0驅動程式安裝一起位置。
1. 從 **混合** 模式 **僅限Windows驗證**.

#### 為Windows上的SQL Server配置WebSphere的整合安全 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有使用外部SQL Server JDBC驅動程式時，才能配置整合安全，而不是使用嵌入WebSphere的SQL Server JDBC驅動程式。

1. 登入WebSphere管理控制台。
1. 在導覽樹中，按一下 **資源** > **JDBC** > **資料來源** 在右窗格中，按一下 **IDP_DS**.
1. 在右窗格的「Additional Properties（其他屬性）」下，按一下 **自訂屬性**，然後按一下 **新增**.
1. 在 **名稱** 框，類型 `integratedSecurity` 和 **值** 框，類型 `true`.
1. 在導覽樹中，按一下 **資源** > **JDBC** > **資料來源** 在右窗格中，按一下 **RM_DS**.
1. 在右窗格的「Additional Properties（其他屬性）」下，按一下 **自訂屬性**，然後按一下 **新增**.
1. 在 **名稱** 框，類型 `integratedSecurity` 和 **值** 框，類型 `true`.
1. 在安裝WebSphere的電腦上，將sqljdbc_auth.dll檔案添加到Windows系統路徑(C:\Windows)。 sqljdbc_auth.dll檔案與Microsoft SQL JDBC 1.2驅動程式安裝位置相同(預設為 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86)。
1. 選擇 **開始** > **控制面板** > **服務**，按一下右鍵WebSphere適用的Windows服務(IBM WebSphere應用程式伺服器) &lt;version> - &lt;node>)，然後選取 **屬性**.
1. 在「屬性」對話方塊中，按一下 **登入** 標籤。
1. 選擇 **此帳戶** 並提供設定您要使用的登入帳戶所需的資訊。
1. 從 **混合** 模式 **僅限Windows驗證**.

### 保護對資料庫中敏感內容的訪問 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms資料庫架構包含有關係統配置和業務流程的敏感資訊，應隱藏在防火牆後。 應將資料庫視為與表單伺服器相同的信任邊界內。 為防止資訊洩漏和業務資料失竊，資料庫管理員(DBA)必須配置該資料庫，以僅允許授權管理員訪問。

為了增加預防措施，您應考慮使用資料庫供應商專用工具來加密包含以下資料的表中的列：

* Rights Management文檔鍵
* 信任儲存HSM PIN加密密鑰
* 本地用戶密碼哈希

有關特定於供應商的工具的資訊，請參閱 [&quot;資料庫安全資訊&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP安全性 {#ldap-security}

輕型目錄存取通訊協定(LDAP)目錄通常由JEE上的AEM Forms用作企業使用者和群組資訊的來源，以及執行密碼驗證的方式。 您應確保LDAP目錄已設定為使用安全通訊端層(SSL)，且JEE上的AEM Forms已設定為使用其SSL埠存取您的LDAP目錄。

#### LDAP拒絕服務 {#ldap-denial-of-service}

使用LDAP的常見攻擊涉及攻擊者故意多次無法驗證。 這會強制LDAP目錄伺服器從所有依賴LDAP的服務中鎖定用戶。

您可以設定當使用者重複無法向AEM Forms驗證時，AEM Forms會實作的失敗嘗試次數和後續鎖定時間。 在管理控制台中，選擇低值。 在選擇失敗嘗試次數時，請務必了解，在進行所有嘗試之後，AEM Forms會在LDAP目錄伺服器發生之前鎖定使用者。

#### 設定自動帳戶鎖定 {#set-automatic-account-locking}

1. 登入管理控制台。
1. 按一下 **設定** > **使用者管理** > **網域管理**.
1. 在自動帳戶鎖定設定下，設定 **最大連續身份驗證故障數** 數字較低，例如3。
1. 按一下「**儲存**」。

### 審核和記錄 {#auditing-and-logging}

正確且安全地使用應用程式稽核和記錄有助於確保盡快追蹤和偵測安全及其他異常事件。 在應用程式內有效使用審核和日誌記錄包括跟蹤成功和失敗的登錄以及關鍵應用程式事件（如建立或刪除關鍵記錄）等項。

您可以使用審計來檢測許多類型的攻擊，包括：

* 暴力密碼攻擊
* 拒絕服務攻擊
* 注入惡意輸入和指令碼攻擊的相關類

此表介紹了可用於減少伺服器漏洞的審核和日誌記錄技術。

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
   <td><p>在JEE記錄檔存取控制清單(ACL)上設定適當的AEM Forms 。</p> <p>設定適當的憑據有助於防止攻擊者刪除檔案。</p> <p>日誌檔案目錄的安全權限應為管理員和系統組的完全控制。 AEM Forms使用者帳戶應僅具有讀取和寫入權限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日誌檔案冗餘</p> </td> 
   <td><p>如果資源允許，則通過使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他機制將日誌即時發送到攻擊者無法訪問的其他伺服器（僅寫）。</p> <p>以這種方式保護日誌有助於防止篡改。 此外，將日誌儲存在中央儲存庫中有助於關聯和監控（例如，如果使用了多個表單伺服器，並且在多台電腦中對每台電腦進行密碼查詢時發生了密碼猜測攻擊）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 使非管理員用戶能夠運行PDF生成器

您可以讓非管理員使用者使用PDF產生器。 通常，只有具有管理權限的使用者才能使用PDF產生器。 執行下列步驟，讓非管理員使用者執行PDF產生器：

1. 建立環境變數名稱PDFG_NON_ADMIN_ENABLED。

1. 將變數的值設為TRUE。

1. 重新啟動AEM Forms執行個體。

## 在JEE上設定AEM Forms以存取企業以外的項目 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安裝AEM Forms後，請務必定期維護您環境的安全性。 本節說明建議哪些工作可維護JEE生產伺服器上AEM Forms的安全性。

### 設定反向代理以訪問Web {#setting-up-a-reverse-proxy-for-web-access}

A *反向代理* 可用來確保外部和內部使用者都能使用JEE網頁應用程式上AEM Forms的一組URL。 此設定比讓使用者直接連線至JEE上AEM Forms所執行的應用程式伺服器更安全。 反向代理會針對在JEE上執行AEM Forms的應用程式伺服器執行所有HTTP要求。 使用者只能透過網路存取反向代理，且只能嘗試反向代理支援的URL連線。

**AEM Forms（JEE根URL上）以與反向Proxy伺服器搭配使用**

JEE Web應用程式上每個AEM Forms的下列應用程式根URL。 您應僅設定反向代理，以公開要提供給使用者之Web應用程式功能的URL。

某些URL會反白顯示為面向使用者的Web應用程式。 您應避免透過反向代理公開Configuration Manager的其他URL以存取外部使用者。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和/或相關的Web應用程式</p> </th> 
   <th><p>基於Web的介面</p> </th> 
   <th><p>一般使用者存取權</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC擴充功能一般使用者Web應用程式，將使用權套用至PDF檔案</p> </td> 
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
   <td><p>Rights Management的Web服務URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF生成器管理Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>工作區最終用戶Web應用程式</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>工作區用戶端應用程式需要的工作區servlet和資料服務</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>在JEE存放庫上引導AEM Forms的Servlet</p> </td> 
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
   <td><p>/TruststoreComponent/</p> <p>有擔保/*</p> </td> 
   <td><p>「信任儲存管理」頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Forms IVS應用程式，用於測試和偵錯表單轉譯</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>用於測試和調試輸出服務的輸出IVS應用</p> </td> 
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
   <td><p>Forms web應用程式檔案</p> </td> 
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
   <td><p>WebDAV（調試）訪問的URL</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>應用程式和服務用戶介面</p> </td> 
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
   <td><p>重設支援頁面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms on JEE核心組態設定頁面</p> </td> 
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
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>上載和下載在訪問遠程端點、SOAP WSDL端點和通過SOAP傳輸或啟用HTTP文檔的EJB傳輸的Java SDK時要處理的文檔。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨網站請求偽造攻擊 {#protecting-from-cross-site-request-forgery-attacks}

跨站請求偽造(CSRF)攻擊利用網站對用戶的信任來傳輸用戶未授權和無意的命令。 攻擊的設定方式是在網頁中包括連結或指令碼，或在電子郵件中包括URL，以訪問用戶已經通過身份驗證的其他站點。

例如，您可能在同時瀏覽其他網站時登入Administration Console。 其中一個網頁可以包括HTML影像標籤，其具有 `src` 屬性，其目標為受害網站上的伺服器端指令碼。 利用Web瀏覽器提供的基於Cookie的會話身份驗證機制，攻擊網站可以向該受害伺服器端指令碼發送惡意請求，偽裝成合法用戶。 如需更多範例，請參閱 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

CSRF共有下列特性：

* 涉及依賴使用者身分的網站。
* 利用站點對該身份的信任。
* 誘使使用者的瀏覽器將HTTP要求傳送至目標網站。
* 涉及具有副作用的HTTP要求。

AEM Forms on JEE使用反向連結篩選功能來封鎖CSRF攻擊。 本節使用下列詞語來說明反向連結篩選機制：

* **允許的反向連結：** 反向連結是將請求傳送至伺服器之來源頁面的位址。 對於JSP頁面或表單，反向連結通常是瀏覽歷史記錄中的上一頁。 影像的反向連結通常是顯示影像的頁面。 您可以將允許的反向連結新增至允許的反向連結清單，借此識別可存取您伺服器資源的反向連結。
* **允許的反向連結例外狀況：** 您可能會想要限制您允許的反向連結清單中特定反向連結的存取範圍。 若要強制執行此限制，您可以將該反向連結的個別路徑新增至允許的反向連結例外清單。 「允許反向連結例外」清單中源自路徑的請求無法叫用表單伺服器上的任何資源。 您可以定義特定應用程式的允許反向連結例外，也可以使用套用至所有應用程式的例外全域清單。
* **允許的URI:** 這是可在不勾選「反向連結標題」的情況下提供的資源清單。 不會導致伺服器狀態變更的資源（例如說明頁面）可以新增至此清單。 「允許的URI」清單中的資源不會遭到「反向連結篩選器」的封鎖，無論反向連結是誰。
* **Null反向連結：** 未與上層網頁相關聯或並非源自上層網頁的伺服器要求，視為來自Null反向連結的要求。 例如，當您開啟新的瀏覽器視窗並輸入位址，然後按Enter鍵時，傳送至伺服器的反向連結為null。 向Web伺服器發出HTTP請求的案頭應用程式（.NET或SWING）也會向伺服器發送Null反向連結。

### 反向連結篩選 {#referer-filtering}

反向連結篩選程式可說明如下：

1. 表單伺服器會檢查用於呼叫的HTTP方法：

   1. 如果是POST，表單伺服器會執行反向連結標題檢查。
   1. 如果是GET，表單伺服器會略過反向連結檢查，除非 *CSRF_CHECK_GETS* 設為true，則會執行反向連結標題檢查。 *CSRF_CHECK_GETS* 在中指定 *web.xml* 檔案。

1. 表單伺服器會檢查請求的URI是否存在於允許清單中：

   1. 如果允許列出URI，則伺服器接受請求。
   1. 如果未允許列出請求的URI，則伺服器會擷取請求的反向連結。

1. 如果請求中有反向連結，伺服器會檢查它是否為允許的反向連結。 如果允許，伺服器會檢查反向連結例外狀況：

   1. 如果是例外，則會封鎖要求。
   1. 如果不是例外，則會傳送要求。

1. 如果請求中沒有反向連結，則伺服器會檢查是否允許空反向連結：

   1. 如果允許Null反向連結，則會傳遞要求。
   1. 如果不允許Null反向連結，則伺服器會檢查所請求的URI是否為Null反向連結的例外，並相應地處理該請求。

### 管理反向連結篩選 {#managing-referer-filtering}

AEM Forms on JEE提供「反向連結篩選器」，用以指定可存取您伺服器資源的反向連結。 依預設，反向連結篩選器不會篩選使用安全HTTP方法(例如GET)的請求，除非 *CSRF_CHECK_GETS* 設為true時，退出連結才會受到追蹤。 如果「允許的反向連結」項目的連接埠號設為0，無論連接埠號為何，JEE上的AEM Forms都會允許來自該主機的所有具有反向連結的請求。 如果未指定埠號，則僅允許來自預設埠80(HTTP)或埠443(HTTPS)的請求。 如果刪除允許的反向連結清單中的所有項目，則會停用反向連結篩選。

首次安裝Document Services時，「允許的反向連結」清單會以安裝Document Services的伺服器的地址更新。 伺服器的條目包括伺服器名稱、IPv4地址、啟用IPv6時的IPv6地址、環回地址和本地主機條目。 主機作業系統會傳回新增至允許反向連結清單的名稱。 例如，IP位址為10.40.54.187的伺服器將包含下列項目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 對於主機作業系統重新調整的任何不合格名稱（沒有IPv4地址、 IPv6地址或合格域名的名稱）允許清單不會更新。 修改「允許的反向連結」清單以符合您的業務環境。 請勿使用預設的「允許反向連結」清單，在生產環境中部署表單伺服器。 修改任何「允許的反向連結」、「反向連結例外」或URI後，請務必重新啟動伺服器，讓變更生效。

**管理允許的反向連結清單**

您可以從管理控制台的使用者管理介面管理允許的反向連結清單。 使用者管理介面可讓您建立、編輯或刪除清單。 請參閱* [防止CSRF攻擊](/help/forms/using/admin-help/preventing-csrf-attacks.md)* *管理說明* 以取得使用允許反向連結清單的詳細資訊。

**管理允許的反向連結例外和允許的URI清單**

AEM Forms on JEE提供API來管理「允許的反向連結例外狀況」清單和「允許的URI」清單。 您可以使用這些API來擷取、建立、編輯或刪除清單。 以下是可用API的清單：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

如需API的詳細資訊，請參閱* AEM Forms on JEE API參考*。

使用 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 全域層級的允許反向連結例外清單，即定義適用於所有應用程式的例外。 此清單僅包含具有絕對路徑(例如 `/index.html`)或相對路徑(例如 `/sample/`)。 您也可以將規則運算式附加至相對URI的結尾，例如 `/sample/(.)*`.

此 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 清單ID在 `UMConstants` 類別 `com.adobe.idp.um.api` 命名空間，在中找到 `adobe-usermanager-client.jar`. 您可以使用AEM Forms API建立、修改或編輯此清單。 例如，若要建立「全域允許反向連結例外」清單，請使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用 ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** 特定於應用程式的例外的清單。

**停用反向連結篩選**

如果反向連結篩選器完全封鎖對表單伺服器的存取，且您無法編輯允許的反向連結清單，您可以更新伺服器啟動指令碼並停用反向連結篩選。

納入 `-Dlc.um.csrffilter.disabled=true` 啟動指令碼中的JAVA參數，然後重新啟動伺服器。 請務必在適當重新設定「允許的反向連結」清單後刪除JAVA引數。

**自訂WAR檔案的反向連結篩選**

您可能已建立自訂WAR檔案以搭配JEE上的AEM Forms使用，以符合您的業務需求。 若要為自訂WAR檔案啟用反向連結篩選，請包括 ***adobe-usermanager-client.jar*** 在WAR的類路徑中，並在* web.xml*檔案中包含一個篩選器條目，該條目包含以下參數：

**CSRF_CHECK_GETS** 控制對GET要求的反向連結檢查。 如果未定義此參數，則預設值設為false。 只有在您想要篩選GET請求時，才納入此參數。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是「允許的反向連結例外狀況」清單的ID。 「反向連結篩選」可防止清單ID所識別清單中源自反向連結的請求叫用表單伺服器上的任何資源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是「允許的URI」清單的ID。 反向連結篩選器不會封鎖清單ID所識別清單中任何資源的請求，無論請求中反向連結標題的值為何。

**CSRF_ALLOW_NULL_REFERER** 當反向連結為null或不存在時，控制反向連結篩選行為。 如果未定義此參數，則預設值設為false。 只有在您要允許Null反向連結時，才納入此參數。 允許null反向連結可能允許某些類型的跨網站請求偽造攻擊。

**CSRF_NULL_REFERER_EXCEPTIONS** 是URI的清單，當反向連結為null時，不會對其執行反向連結檢查。 只有在 *CSRF_ALLOW_NULL_REFERER* 設為false時，退出連結才會受到追蹤。 使用逗號在清單中分隔多個URI。

以下是 *web.xml* 檔案 ***範例*** WAR檔案：

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

如果CSRF篩選器正在阻止合法的伺服器請求，請嘗試以下操作之一：

* 如果拒絕的請求有「反向連結」標題，請謹慎考慮將它新增至「允許的反向連結」清單。 僅新增您信任的反向連結。
* 如果拒絕的請求沒有反向連結標題，請修改您的用戶端應用程式以包含反向連結標題。
* 如果客戶端可以在瀏覽器中工作，請嘗試該部署模型。
* 您最後可以將資源添加到「允許的URI」清單。 這不是建議的設定。

## 安全網路配置 {#secure-network-configuration}

本節說明AEM Forms on JEE所需的通訊協定和連接埠，並提供在JEE上以安全網路設定部署AEM Forms的建議。

### AEM Forms在JEE上使用的網路通訊協定 {#network-protocols-used-by-aem-forms-on-jee}

如前一節所述，當您設定安全的網路架構時，若要在JEE上的AEM Forms與企業網路中的其他系統進行互動，需要下列網路通訊協定。

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
     <li><p>瀏覽器顯示Configuration Manager和最終用戶Web應用程式</p> </li> 
     <li><p>所有SOAP連接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服務客戶端應用程式，如.NET應用程式</p> </li> 
     <li><p>Adobe Reader®在JEE伺服器網站服務上使用AEM Forms適用的SOAP</p> </li> 
     <li><p>AdobeFlash®應用程式使用SOAP來處理表單伺服器Web服務</p> </li> 
     <li><p>AEM Forms on JEE SDK呼叫在SOAP模式中使用時</p> </li> 
     <li><p>Workbench設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>AEM Forms on JEE SDK在Enterprise JavaBeans(EJB)模式中使用時呼叫</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>以電子郵件為基礎的服務輸入（電子郵件端點）</p> </li> 
     <li><p>電子郵件上的使用者任務通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC檔案IO</p> </td> 
   <td><p>AEM Forms on JEE監控監看的資料夾以輸入至服務（觀看的資料夾端點）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>目錄中組織用戶和組資訊的同步</p> </li> 
     <li><p>互動式使用者的LDAP驗證</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>在使用JDBC服務執行進程期間對外部資料庫進行的查詢和過程調用</p> </li> 
     <li><p>JEE存放庫上的AEM Forms內部存取</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>可讓任何WebDAV用戶端在JEE設計時存放庫（表單、片段等）上遠端瀏覽AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash應用程式，其中JEE伺服器服務上的AEM Forms會以遠端端點設定</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms on JEE公開MBean以使用JMX進行監控</p> </td> 
  </tr> 
 </tbody> 
</table>

### 應用程式伺服器的埠 {#ports-for-application-servers}

本節介紹支援的每種應用程式伺服器類型的預設埠（和備用配置範圍）。 內部防火牆上必須啟用或停用這些埠，具體取決於您要允許的網路功能，允許連接到在JEE上執行AEM Forms的應用程式伺服器的用戶端。

>[!NOTE]
>
>依預設，伺服器會在adobe.com命名空間下公開數個JMX MBean。 只有對伺服器運行狀況監視有用的資訊才會公開。 但是，為防止資訊洩漏，您應防止不受信任的網路中的呼叫者查找JMX MBean並訪問運行狀況度量。

**JBoss埠**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>訪問Web應用程式</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1連接器埠8080</p> <p>AJP 1.3連接器埠8009</p> <p>SSL/TLS連接器埠8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支援</p> </td> 
   <td><p>[JBoss根]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic埠**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>訪問Web應用程式</p> </td> 
   <td> 
    <ul> 
     <li><p>管理伺服器偵聽埠：預設為7001</p> </li> 
     <li><p>管理伺服器SSL偵聽埠：預設為7002</p> </li> 
     <li><p>為托管伺服器配置的埠，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>存取JEE上的AEM Forms不需要WebLogic管理埠</p> </td> 
   <td> 
    <ul> 
     <li><p>受控伺服器偵聽埠：可從1到65534配置</p> </li> 
     <li><p>托管伺服器SSL偵聽埠：可從1到65534配置</p> </li> 
     <li><p>節點管理器偵聽埠：預設為5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere埠**

有關AEM Forms在JEE上需要的WebSphere埠的資訊，請轉至WebSphere應用程式伺服器UI中的埠號設定。

### 設定SSL {#configuring-ssl}

指一節中所述的物理架構 [AEM Forms on JEE物理架構](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您應為您打算使用的所有連線設定SSL。 具體來說，所有SOAP連線都必須透過SSL進行，以防止網路上曝光使用者憑證。

如需如何在JBoss、WebLogic和WebSphere上設定SSL的指示，請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_64).

有關如何將憑證匯入為AEM Forms伺服器設定的JVM(Java Virtual Machine)的說明，請參閱 [AEM Forms Workbench說明](http://www.adobe.com/go/learn_aemforms_workbench_65).

### 設定SSL重新導向 {#configuring-ssl-redirect}

配置應用程式伺服器以支援SSL後，必須確保向應用程式和服務發送的所有HTTP通信都強制使用SSL埠。

若要為WebSphere或WebLogic配置SSL重新導向，請參閱應用程式伺服器檔案。

1. 開啟命令提示符，導航至/JBOSS_HOME/standalone/configuration目錄，然後執行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 開啟JBOSS_HOME/standalone/configuration/standalone.xml檔案進行編輯。

   在 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />網域:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素，新增下列詳細資訊：:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https連接器元素中新增下列程式碼：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存並關閉standalone.xml檔案。

## 特定於Windows的安全性建議 {#windows-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，Windows專屬的安全性建議。

### JBoss Service帳戶 {#jboss-service-accounts}

JEE上的AEM Forms統包安裝預設會使用本機系統帳戶來設定服務帳戶。 內建的本機系統使用者帳戶具備高水準的協助功能；它是管理員組的一部分。 如果工作進程標識以本地系統用戶帳戶的形式運行，則該工作進程可以完全訪問整個系統。

#### 使用非管理帳戶運行應用程式伺服器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，建立表單伺服器服務的本機使用者以下列方式登入：

   * 選擇 **用戶無法更改密碼**.
   * 在 **成員** 頁簽，確保列出「用戶」組。

1. 選擇 **設定** > **管理工具** > **服務**.
1. 按兩下應用程式伺服器服務並停止該服務。
1. 在 **登入** 索引標籤，選取 **此帳戶**，瀏覽您建立的使用者帳戶，然後輸入帳戶的密碼。
1. 在「本地安全設定」窗口的「用戶權限分配」下，為窗體伺服器正在運行的用戶帳戶提供以下權限：

   * 通過終端服務拒絕登錄
   * 拒絕本地登錄xx
   * 以服務身份登錄（應已設定）

1. 授予新用戶帳戶對以下目錄的修改權限：
   * **全局文檔儲存(GDS)目錄**:在AEM Forms安裝過程中，會手動配置GDS目錄的位置。 如果安裝期間位置設定保持空，則位置預設為應用程式伺服器安裝下的目錄，位置位於 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository目錄**:預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登錄用戶的主目錄在基於UNIX的系統上，非根用戶可以將以下目錄用作臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄授予新用戶帳戶的寫入權限：
   * [JBoss-directory]\dastanale\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server的預設安裝位置：
   >
   >* 窗口：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux:/opt/jboss/。


1. 啟動應用程式伺服器服務。

### 檔案系統安全 {#file-system-security}

AEM Forms on JEE使用檔案系統的方式如下：

* 儲存處理文檔輸入和輸出時使用的臨時檔案
* 將用於支援已安裝的解決方案元件的檔案儲存在全局存檔儲存中
* 監視資料夾儲存從檔案系統資料夾位置輸入服務時丟棄的檔案

使用觀看的資料夾作為通過表單伺服器服務發送和接收文檔的方式時，請對檔案系統安全性採取額外的預防措施。 當使用者丟棄已觀看資料夾中的內容時，該內容會透過已觀看資料夾公開。 在這種情況下，服務不會驗證實際的最終用戶。 相反，它依賴在資料夾級別設定的ACL和共用級別安全性，以確定哪些人可以有效調用服務。

## JBoss專屬安全性建議 {#jboss-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，專屬於JBoss 7.0.6的應用程式伺服器設定建議。

### 停用JBoss管理控制台和JMX主控台 {#disable-jboss-management-console-and-jmx-console}

使用統包安裝方法在JBoss上於JEE安裝AEM Forms時，已設定存取JBoss管理主控台和JMX主控台的權限（已停用JMX監控）。 如果您使用自己的JBoss Application Server，請確保JBoss Management Console和JMX監控主控台的存取權受到保護。 對JMX監控控制台的訪問設定在名為jmx-invoker-service.xml的JBoss配置檔案中。

### 禁用目錄瀏覽 {#disable-directory-browsing}

登入管理控制台後，可修改URL以瀏覽控制台的目錄清單。 例如，如果您將URL變更為下列其中一個URL，則可能會顯示目錄清單：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic專屬安全性建議 {#weblogic-specific-security-recommendations}

本節包含在JEE上執行AEM Forms時，用於保護WebLogic 9.1的應用程式伺服器設定建議。

### 禁用目錄瀏覽 {#disable_directory_browsing-1}

將weblogic.xml檔案中的index-directories屬性設定為 `false`，如以下範例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 啟用WebLogic SSL埠 {#enable-weblogic-ssl-port}

預設情況下，WebLogic不啟用預設SSL偵聽埠7002。 在配置SSL之前，請在WebLogic伺服器管理控制台中啟用此埠。

## WebSphere特定安全建議 {#websphere-specific-security-recommendations}

本節包含保護在JEE上執行AEM Forms之WebSphere的應用程式伺服器設定建議。

### 禁用目錄瀏覽 {#disable_directory_browsing-2}

設定 `directoryBrowsingEnabled` ibm-web-ext.xml檔案中的屬性 `false`.

### 啟用WebSphere管理安全 {#enable-websphere-administrative-security}

1. 登入WebSphere管理控制台。
1. 在導航樹中，轉到 **安全性** > **全球安全**
1. 選擇 **啟用管理安全**.
1. 取消選擇兩者 **啟用應用程式安全性** 和 **使用Java 2安全性**.
1. 按一下 **確定** 或 **套用**.
1. 在 **訊息** 按一下 **直接儲存至主配置**.
