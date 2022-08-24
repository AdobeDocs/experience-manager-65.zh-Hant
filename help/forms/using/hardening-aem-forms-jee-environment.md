---
title: 在JEE環境上強化您的AEM Forms
seo-title: Hardening Your AEM Forms on JEE Environment
description: 瞭解各種安全強化設定，以增強在公司內部網中運行的JEE上的AEM Forms的安全性。
seo-description: Learn a variety of security-hardening settings to enhance the security of AEM Forms on JEE running in a corporate intranet.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 0%

---

# 在JEE環境上強化您的AEM Forms {#hardening-your-aem-forms-on-jee-environment}

瞭解各種安全強化設定，以增強在公司內部網中運行的JEE上的AEM Forms的安全性。

文章介紹了在JEE上安全運行AEM Forms的伺服器的建議和最佳做法。 這不是適用於您的作業系統和應用程式伺服器的全面的主機強化文檔。 相反，本文描述了您應實施的各種安全強化設定，以增強在公司內部網內運行的JEE上AEM Forms的安全性。 但是，為了確保JEE應用程式伺服器上的AEM Forms保持安全，您還應實施安全監控、檢測和響應過程。

本文描述了在安裝和配置生命週期的以下階段應應用的硬化技術：

* **預安裝：** 在JEE上安裝AEM Forms之前，請使用這些技術。
* **安裝：** 在AEM Forms的JEE安裝過程中使用這些技術。
* **安裝後：** 安裝後使用這些技術，並在安裝後定期使用。

AEM FormsJEE是高度可定製的，可在多種不同的環境中工作。 有些建議可能不符合您組織的需要。

## 預安裝 {#preinstallation}

在JEE上安裝AEM Forms之前，您可以將安全解決方案應用到網路層和作業系統。 本節介紹了一些問題，並就減少這些領域的安全漏洞提出建議。

**在UNIX和Linux上安裝和配置**

您不應使用根外殼程式在JEE上安裝或配置AEM Forms。 預設情況下，檔案安裝在/opt目錄下，執行安裝的用戶需要在/opt下擁有所有檔案權限。 或者，可以在單個用戶的/user目錄下執行安裝，在該目錄下，他們已經擁有所有檔案權限。

**在Windows上安裝和配置**

如果要在JBoss上的JEE上使用統包方法安裝AEM Forms，或者要安裝PDF生成器，則應以管理員身份在Windows上執行安裝。 此外，在具有本機應用程式支援的Windows上安裝PDF生成器時，必須以安裝MicrosoftOffice的同一Windows用戶身份運行安裝。 有關安裝權限的詳細資訊，請參閱應用程式伺服器的*在JEE*上安裝和部署AEM Forms文檔。

### 網路層安全 {#network-layer-security}

網路安全漏洞是任何面向Internet或面向Intranet的應用程式伺服器面臨的首批威脅之一。 本節介紹針對這些漏洞加強網路上主機的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧加固以及使用防火牆保護主機的問題。

下表介紹了減少網路安全漏洞的常用進程。

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
   <td><p>在非軍事區(DMZ)內部署表單伺服器。 分段應至少在兩個級別中存在，在位於內部防火牆後面的JEE上運行AEM Forms的應用程式伺服器。 將外部網路與包含Web伺服器的DMZ分離，而Web伺服器又必須與內部網路分離。 使用防火牆實現分層。 對通過每個網路層的流量進行分類和控制，以確保只允許絕對最小的所需資料。</p> </td> 
  </tr> 
  <tr> 
   <td><p>專用IP地址</p> </td> 
   <td><p>將網路地址轉換(NAT)與RFC 1918專用IP地址一起使用在AEM Forms應用伺服器上。 分配專用IP地址(10.0.0.0/8 、 172.16.0.0/12和192.168.0.0/16)，使得攻擊者更難通過Internet將流量路由到NAT內部主機和從NAT內部主機路由通信。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火牆</p> </td> 
   <td><p>使用以下條件選擇防火牆解決方案：</p> 
    <ul> 
     <li><p>實施支援代理伺服器和/或 <em>狀態檢查</em> 而不是簡單的包過濾解決方案。</p> </li> 
     <li><p>使用支援 <em>拒絕除明確允許外的所有服務</em> 安全范式。</p> </li> 
     <li><p>實施雙宿主或多宿主防火牆解決方案。 此體系結構提供了最高級別的安全性，並有助於防止未經授權的用戶繞過防火牆安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>資料庫埠</p> </td> 
   <td><p>請勿對資料庫使用預設監聽埠(MySQL - 3306、Oracle- 1521、MS SQL - 1433)。 有關更改資料庫埠的資訊，請參閱資料庫文檔。</p> <p>使用不同的資料庫埠會影響JEE配置的整體AEM Forms。 如果更改預設埠，則必須在其他配置區域(如JEE上的AEM Forms資料源)中進行相應的修改。</p> <p>有關在JEE上的AEM Forms配置資料源的資訊，請參閱在JEE上安裝和升級AEM Forms或在JEE上升級到AEM Forms，以便您的應用程式伺服器在 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms使用手冊</a>。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 作業系統安全 {#operating-system-security}

下表介紹了一些可能的方法，以最大限度地減少作業系統中發現的安全漏洞。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p></th> 
   <th><p>說明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全修補程式</p></td> 
   <td><p>如果供應商安全補丁程式和升級未及時應用，則未經授權的用戶可能獲得對應用程式伺服器的訪問權限的風險增加。 Test安全修補程式，然後將其應用到生產伺服器。</p><p>此外，建立策略和過程以定期檢查和安裝修補程式。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防護軟體</p></td> 
   <td><p>病毒掃描程式可以通過掃描簽名或監視異常行為來識別受感染的檔案。 掃描程式將其病毒簽名保留在檔案中，該檔案通常儲存在本地硬碟上。 由於經常發現新病毒，因此您應經常更新此檔案以識別所有當前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>網路時間協定(NTP)</p></td> 
   <td><p>要進行取證分析，請在表單伺服器上保留準確的時間。 使用NTP來同步所有直接連接到Internet的系統上的時間。</p></td> 
  </tr> 
 </tbody> 
</table>

有關作業系統的其他安全資訊，請參閱 [&quot;作業系統安全資訊&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安裝 {#installation}

本節介紹在AEM Forms安裝過程中可以使用的技術，以減少安全漏洞。 在某些情況下，這些技術使用的是作為安裝過程一部分的選項。 下表介紹了這些技術。

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
   <td><p>使用安裝軟體所需的最少權限數。 使用不在Administrators組中的帳戶登錄到電腦。 在Windows上，可以使用「運行方式」命令以管理用戶身份在JEE安裝程式上運行AEM Forms。 在UNIX和Linux系統上，使用命令，如 <code>sudo</code> 安裝軟體。</p> </td> 
  </tr> 
  <tr> 
   <td><p>軟體源</p> </td> 
   <td><p>不要從不受信任的源下載或運行JEE上的AEM Forms。</p> <p>惡意程式可以包含多種違反安全性的代碼，包括資料竊取、修改和刪除，以及拒絕服務。 從AdobeDVD或僅從受信任的源在JEE上安裝AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁碟分區</p> </td> 
   <td><p>將AEM Forms置於JEE上的專用磁碟分區上。 磁碟分段是一種過程，它將伺服器上的特定資料保留在單獨的物理磁碟上，以增加安全性。 以這種方式排列資料降低了目錄遍歷攻擊的風險。 計畫建立與系統分區分開的分區，您可以在其上在JEE內容目錄上安裝AEM Forms。 （在Windows上，系統分區包含system32目錄或引導分區。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>元件</p> </td> 
   <td><p>評估現有服務並禁用或卸載任何不需要的服務。 不要安裝不必要的元件和服務。</p> <p>應用程式伺服器的預設安裝可能包括您使用時不需要的服務。 在部署之前，應禁用所有不必要的服務，以盡量減少攻擊的入口點。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符檔案中注釋掉不必要的服務。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略檔案</p> </td> 
   <td><p>存在 <code>crossdomain.xml</code> 伺服器上的檔案可能會立即削弱該伺服器。 建議您盡可能限制域清單。 不要放置 <code>crossdomain.xml</code> 在開發到生產時使用的檔案 <em>（不建議使用）</em>。 對於使用Web服務的指南，如果服務位於提供該指南的同一伺服器上，則 <code>crossdomain.xml</code> 根本不需要檔案。 但是，如果服務位於另一台伺服器上，或者如果涉及群集，則 <code>crossdomain.xml</code> 需要檔案。 請參閱 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>，以獲取有關crossdomain.xml檔案的詳細資訊。</p> </td> 
  </tr> 
  <tr> 
   <td><p>作業系統安全設定</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，請確保安裝 <code>pkcs11_softtoken_extra.so</code> 而不是 <code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安裝後步驟 {#post-installation-steps}

在JEE上成功安裝AEM Forms後，從安全形度定期維護環境非常重要。

以下部分詳細描述了建議保護已部署的表單伺服器的不同任務。

### AEM Forms安全 {#aem-forms-security}

以下建議的設定適用於管理Web應用程式外的JEE伺服器上的AEM Forms。 要降低伺服器的安全風險，請在JEE上安裝AEM Forms後立即應用這些設定。

**安全修補程式**

如果供應商安全補丁程式和升級未能及時應用，則未經授權的用戶可能獲得對應用程式伺服器的訪問權限的風險增加。 Test安全補丁程式，然後再將它們應用到生產伺服器，以確保應用程式的相容性和可用性。 此外，建立策略和過程以定期檢查和安裝修補程式。 AEM Forms的JEE更新位於企業產品下載站點上。

**服務帳戶（僅限Windows上的JBoss交鑰匙）**

AEM Forms在JEE上使用LocalSystem帳戶安裝服務。 內置的LocalSystem用戶帳戶具有高度的可訪問性；它是「管理員」組的一部分。 如果工作進程標識以LocalSystem用戶帳戶的身份運行，則該工作進程對整個系統具有完全訪問權限。

要使用特定非管理帳戶運行部署JEE上的AEM Forms的應用程式伺服器，請遵循以下說明：

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶以以下方式登錄：

   * 選擇 **用戶無法更改密碼**。
   * 在 **成員** 頁籤，確保 **用戶** 列出組。

   >[!NOTE]
   >
   >不能更改PDF生成器的此設定。

1. 選擇 **開始** > **設定** > **管理工具** > **服務**。
1. 按兩下JEE上的JBoss forAEM Forms並停止服務。
1. 在 **登錄** 頁籤 **此帳戶**，瀏覽您建立的用戶帳戶，並輸入帳戶的密碼。
1. 在MMC中，開啟 **本地安全設定** 選擇 **本地策略** > **用戶權限分配**。
1. 將以下權限分配給Forms伺服器正在運行的用戶帳戶：

   * 拒絕通過終端服務登錄
   * 拒絕本地登錄
   * 以服務身份登錄（應已設定）

1. 授予新用戶帳戶對以下目錄的修改權限：
   * **全局文檔儲存(GDS)目錄**:GDS目錄的位置是在AEM Forms安裝過程中手動配置的。 如果安裝期間位置設定仍為空，則該位置預設為應用程式伺服器安裝下的目錄，位置位於 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX — 儲存庫目錄**:預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)在環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登錄用戶的主目錄在基於UNIX的系統上，非根用戶可以將以下目錄用作臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄賦予新用戶帳戶寫入權限：
   * [JBoss目錄]\獨立\部署
   * [JBoss目錄]\獨立\
   * [JBoss目錄]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的預設安裝位置：
   > * 窗口：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/

1. 啟動應用程式伺服器。

**禁用Configuration Manager引導Servlet**

Configuration Manager使用部署在應用程式伺服器上的Servlet在JEE資料庫上執行AEM Forms的引導。 由於Configuration Manager在配置完成前訪問此Servlet，因此未確保授權用戶對其的訪問安全，並且在您成功使用Configuration Manager在JEE上配置AEM Forms後應禁用它。

1. 解壓縮adobe-livecycle-[appserver(appserver)].ear檔案。
1. 開啟META-INF/application.xml檔案。
1. 搜索adobe-bootstrapper.war節：

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
1. 注釋掉adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 戰爭模組如下：

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
1. 壓縮EAR檔案並將其重新部署到應用程式伺服器。
1. 啟動AEM Forms伺服器。
1. 在瀏覽器中鍵入以下URL以test更改並確保其不再有效。

   https://&lt;localhost>:&lt;port>/adobe bootstrapper/bootstrap

**鎖定對信任儲存的遠程訪問**

Configuration Manager允許您將Acrobat Reader DC擴展憑據上載到JEE信任儲存上的AEM Forms。 這意味著預設情況下已啟用通過遠程協定（SOAP和EJB）訪問信任儲存憑據服務。 使用Configuration Manager上載權限憑據後，或者如果您決定以後使用管理控制台管理憑據，則不再需要此訪問。

您可以按照一節中的步驟禁用對所有信任儲存服務的遠程訪問 [禁用對服務的非基本遠程訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)。

**禁用所有非必需的匿名訪問**

某些表單伺服器服務具有可由匿名調用者調用的操作。 如果不需要匿名訪問這些服務，請按照中的步驟禁用它 [禁用對服務的非必需匿名訪問](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)。

#### 更改預設管理員密碼 {#change-the-default-administrator-password}

安裝JEE上的AEM Forms時，將為用戶超級管理員/登錄ID管理員配置一個預設用戶帳戶，預設密碼為 *密碼*。 您應立即使用Configuration Manager更改此密碼。

1. 在Web瀏覽器中鍵入以下URL:

   ```java
   https://[host name]:[port]/adminui
   ```

   預設埠號為以下之一：

   **JBoss:** 8080

   **WebLogic伺服器：** 7001

   **WebSphere:** 9080。

1. 在 **用戶名** 欄位，類型 `administrator` 在 **密碼** 欄位，類型 `password`。
1. 按一下 **設定** > **用戶管理** > **用戶和組**。
1. 類型 `administrator` 的 **查找** ，然後按一下 **查找**。
1. 按一下 **超級管理員** 的子菜單。
1. 按一下 **更改密碼** 在「編輯用戶」頁上。
1. 指定新密碼，然後按一下 **保存**。

此外，建議通過執行以下步驟來更改CRX管理員的預設密碼：

1. 登錄 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 使用預設用戶名/密碼。
1. 在搜索欄位中鍵入Administrator ，然後按一下 **開始**。
1. 選擇 **管理員** 從搜索結果中按一下 **編輯** 表徵圖。
1. 在 **新密碼** 的 **您的密碼** 的子菜單。
1. 按一下用戶介面右下角的「保存」表徵圖。

#### 禁用WSDL生成 {#disable-wsdl-generation}

只應為開發環境啟用Web服務定義語言(WSDL)生成，在開發環境中，開發人員使用WSDL生成來構建其客戶端應用程式。 您可以選擇在生產環境中禁用WSDL生成，以避免暴露服務的內部詳細資訊。

1. 在Web瀏覽器中鍵入以下URL:

   ```java
   https://[host name]:[port]/adminui
   ```

1. 按一下 **設定>核心繫統設定>配置**。
1. 取消選擇 **啟用WSDL** 按一下 **確定**。

### 應用程式伺服器安全 {#application-server-security}

下表介紹了在JEE應用程式上安裝AEM Forms後保護應用程式伺服器的一些技術。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>說明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>應用伺服器管理控制台</p> </td> 
   <td><p>在應用程式伺服器上的JEE上安裝、配置和部署AEM Forms後，應禁用對應用程式伺服器管理控制台的訪問。 有關詳細資訊，請參閱應用程式伺服器文檔。</p> </td> 
  </tr> 
  <tr> 
   <td><p>應用程式伺服器Cookie設定</p> </td> 
   <td><p>應用程式Cookie由應用程式伺服器控制。 部署應用程式時，應用程式伺服器管理員可以指定伺服器範圍或特定於應用程式的cookie首選項。 預設情況下，伺服器設定是首選設定。</p> <p>應用程式伺服器生成的所有會話Cookie都應包括 <code>HttpOnly</code> 屬性。 例如，在使用JBoss Application Server時，可以將SessionCookie元素修改為 <code>httpOnly="true"</code> 的 <code>WEB-INF/web.xml</code> 的子菜單。</p> <p>您可以限制使用僅HTTPS發送Cookie。 因此，不會通過HTTP發送未加密的檔案。 應用程式伺服器管理員應全局為伺服器啟用安全Cookie。 例如，在使用JBoss Application Server時，可以將連接器元素修改為 <code>secure=true</code> 的 <code>server.xml</code> 的子菜單。</p> <p>有關Cookie設定的詳細資訊，請參閱應用程式伺服器文檔。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目錄瀏覽</p> </td> 
   <td><p>當有人請求不存在的頁面或請求控制器名稱(請求字串以正斜槓(/)結尾)時，應用程式伺服器不應返回該目錄的內容。 為防止出現此情況，可以禁用應用程式伺服器上的目錄瀏覽。 您應該為管理控制台應用程式和伺服器上運行的其他應用程式執行此操作。</p> <p>對於JBoss，設定 <code>DefaultServlet</code> 屬性 <code>false</code> 在web.xml檔案中，如以下示例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;預設&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;清單&lt;/param-name&gt;</p> <p>&lt;param-value&gt;假&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>對於WebSphere，設定 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi檔案中的屬性 <code>false</code>。</p> <p>對於WebLogic，將weblogic.xml檔案中的index-directories屬性設定為 <code>false</code>，如下例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;假</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 資料庫安全 {#database-security}

保護資料庫時，應實施資料庫供應商描述的度量。 您應分配資料庫用戶，其資料庫權限應為AEM Forms授予的在JEE上使用的最低要求。 例如，不要使用具有資料庫管理員權限的帳戶。

在Oracle中，您使用的資料庫帳戶只需要CONNECT、資源和CREATE VIEW權限。 有關其他資料庫的類似要求，請參見 [準備在JEE（單伺服器）上安裝AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上為JBoss配置SQL Server的整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml}要添加 `integratedSecurity=true` 連接URL，如本示例所示：

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與MicrosoftSQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 將本地系統中登錄身份的JBoss Windows服務(JBoss forAEM Forms在JEE上)屬性修改為具有AEM Forms資料庫和最小權限集的登錄帳戶。 如果從命令行而不是作為Windows服務運行JBoss，則無需執行此步驟。
1. 從中設定SQL Server的安全性 **混合** 模式 **僅Windows身份驗證**。

#### 為Windows上的SQL Server配置WebLogic的整合安全 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 在Web瀏覽器的URL行中鍵入以下URL，啟動WebLogic Server管理控制台：

   ```java
   https://[host name]:7001/console
   ```

1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯**。
1. 在「域結構」(Domain Structure)下，按一下 *[基域]* > **服務** > **JDBC** > **資料源** 在右窗格中，按一下 **IDP_DS**。
1. 在下一個螢幕上，在 **配置** 頁籤 **連接池** ，在 **屬性** 框，類型 `integratedSecurity=true`。
1. 在「域結構」(Domain Structure)下，按一下 **[基域]** > **服務** > **JDBC** > **資料源** 在右窗格中，按一下 **RM_DS**。
1. 在下一個螢幕上，在 **配置** 頁籤 **連接池** ，在 **屬性** 框，類型 `integratedSecurity=true`。
1. 將sqljdbc_auth.dll檔案添加到運行應用程式伺服器的電腦上的Windows系統路徑。 sqljdbc_auth.dll檔案與MicrosoftSQL JDBC 6.2.1.0驅動程式安裝一起使用。
1. 從中設定SQL Server的安全性 **混合** 模式 **僅Windows身份驗證**。

#### 為Windows上的SQL Server配置WebSphere的整合安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有使用外部SQL Server JDBC驅動程式，而不是嵌入WebSphere的SQL Server JDBC驅動程式時，才能配置整合安全性。

1. 登錄到WebSphere管理控制台。
1. 在導航樹中，按一下 **資源** > **JDBC** > **資料源** 在右窗格中，按一下 **IDP_DS**。
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下 **自定義屬性**，然後按一下 **新建**。
1. 在 **名稱** 框，類型 `integratedSecurity` 在 **值** 框，類型 `true`。
1. 在導航樹中，按一下 **資源** > **JDBC** > **資料源** 在右窗格中，按一下 **RM_DS**。
1. 在右窗格中的「Additional Properties（其他屬性）」下，按一下 **自定義屬性**，然後按一下 **新建**。
1. 在 **名稱** 框，類型 `integratedSecurity` 在 **值** 框，類型 `true`。
1. 在安裝WebSphere的電腦上，將sqljdbc_auth.dll檔案添加到Windows系統路徑(C:\Windows)。 sqljdbc_auth.dll檔案與MicrosoftSQL JDBC 1.2驅動程式安裝位置相同(預設為 *[安裝目錄]*/sqljdbc_1.2/enu/auth/x86)。
1. 選擇 **開始** > **控制面板** > **服務**，按一下右鍵WebSphere的Windows服務(IBMWebSphere應用程式伺服器) &lt;version> - &lt;node>) **屬性**。
1. 在「屬性」對話框中，按一下 **登錄** 頁籤。
1. 選擇 **此帳戶** 並提供設定要使用的登錄帳戶所需的資訊。
1. 在SQL Server上設定安全性 **混合** 模式 **僅Windows身份驗證**。

### 保護對資料庫中敏感內容的訪問 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms資料庫架構包含有關係統配置和業務流程的敏感資訊，應隱藏在防火牆後面。 應將資料庫考慮在與表單伺服器相同的信任邊界內。 為防止資訊洩露和業務資料被盜，資料庫必須由資料庫管理員(DBA)配置，才能僅允許授權管理員訪問。

作為附加的預防措施，您應考慮使用資料庫供應商特定的工具來加密包含以下資料的表中的列：

* Rights Management文檔密鑰
* 信任儲存HSM PIN加密密鑰
* 本地用戶密碼哈希

有關供應商特定工具的資訊，請參見 [&quot;資料庫安全資訊&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全 {#ldap-security}

輕型目錄訪問協定(LDAP)目錄通常由AEM Forms在JEE上用作企業用戶和組資訊的源，以及執行密碼驗證的方法。 您應確保將LDAP目錄配置為使用安全套接字層(SSL)，並且將JEE上的AEM Forms配置為使用SSL埠訪問LDAP目錄。

#### LDAP拒絕服務 {#ldap-denial-of-service}

使用LDAP的常見攻擊涉及攻擊者故意多次無法進行身份驗證。 這將強制LDAP目錄伺服器將用戶從所有依賴LDAP的服務中鎖定。

您可以設定當用戶多次無法向AEM Forms進行身份驗證時，AEM Forms執行的失敗嘗試次數和後續鎖定時間。 在管理控制台中，選擇低值。 在選擇失敗嘗試次數時，必須瞭解，在進行所有嘗試後，AEM Forms會在LDAP目錄伺服器之前鎖定用戶。

#### 設定自動帳戶鎖定 {#set-automatic-account-locking}

1. 登錄到Administration Console。
1. 按一下 **設定** > **用戶管理** > **域管理**。
1. 在自動帳戶鎖定設定下，設定 **最大連續身份驗證失敗數** 到3這樣的低數。
1. 按一下「**儲存**」。

### 審核和記錄 {#auditing-and-logging}

正確、安全地使用應用程式審核和日誌記錄有助於確保盡快跟蹤和檢測安全和其他異常事件。 在應用程式內有效使用審計和日誌記錄包括跟蹤成功登錄和失敗登錄等項目，以及關鍵應用程式事件，如建立或刪除關鍵記錄。

您可以使用審計來檢測多種類型的攻擊，包括：

* 暴力密碼攻擊
* 拒絕服務攻擊
* 注入惡意輸入和相關類的指令碼攻擊

此表介紹了可用於減少伺服器漏洞的審計和日誌記錄技術。

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
   <td><p>在JEE日誌檔案訪問控制清單(ACL)上設定相應的AEM Forms。</p> <p>設定適當的憑據有助於防止攻擊者刪除檔案。</p> <p>日誌檔案目錄上的安全權限應為管理員和SYSTEM組的完全控制權限。 AEM Forms用戶帳戶應僅具有讀和寫權限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日誌檔案冗餘</p> </td> 
   <td><p>如果資源允許，則使用Syslog 、 Tivoli 、MicrosoftOperations Manager(MOM)Server或其他機制將日誌即時發送到攻擊者無法訪問的另一個伺服器（僅寫入）。</p> <p>這樣保護日誌有助於防止篡改。 此外，將日誌儲存在中央儲存庫中有助於關聯和監控（例如，如果正在使用多個表單伺服器，並且正在多台電腦上進行密碼猜測攻擊，而每台電腦都在這些電腦上查詢密碼）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 啟用非管理員用戶運行PDF生成器

您可以啟用非管理員用戶使用PDF生成器。 通常，只有具有管理權限的用戶才能使用PDF生成器。 執行以下步驟，使非管理員用戶能夠運行PDF生成器：

1. 建立環境變數名稱PDFG_NON_ADMIN_ENABLED。

1. 將變數的值設定為TRUE。

1. 重新啟動AEM Forms實例。

## 在JEE上配置AEM Forms以訪問企業以外的 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安裝AEM Forms後，定期維護您環境的安全性非常重要。 本節介紹建議在JEE生產伺服器上維護AEM Forms的安全性的任務。

### 設定Web訪問的反向代理 {#setting-up-a-reverse-proxy-for-web-access}

A *反向代理* 可用於確保JEE Web應用程式上AEM Forms的一組URL可供外部和內部用戶使用。 此配置比允許用戶直接連接到JEE上的AEM Forms正在運行的應用程式伺服器更安全。 反向代理對在JEE上運行AEM Forms的應用程式伺服器執行所有HTTP請求。 用戶只能對反向代理進行網路訪問，並且只能嘗試反向代理支援的URL連接。

**AEM Forms在JEE根URL上，用於反向代理伺服器**

JEE Web應用程式上每個AEM Forms的以下應用程式根URL。 您應僅配置反向代理以向最終用戶公開要提供的Web應用程式功能的URL。

某些URL會突出顯示為面向最終用戶的Web應用程式。 您應避免暴露Configuration Manager的其他URL，以便通過反向代理訪問外部用戶。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和/或關聯的Web應用程式</p> </th> 
   <th><p>基於Web的介面</p> </th> 
   <th><p>最終用戶訪問</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC擴展最終用戶Web應用程式，用於對PDF文檔應用使用權</p> </td> 
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
   <td><p>用於Rights Management的Web服務URL</p> </td> 
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
   <td><p>Workspace客戶端應用程式需要的Workspace Servlet和資料服務</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe bootstrapper/*</p> </td> 
   <td><p>用於在JEE儲存庫上引導AEM Forms的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>表單伺服器Web服務的資訊頁面</p> </td> 
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
   <td><p>/TruststoreComponent/</p> <p>已抵押/*</p> </td> 
   <td><p>信任儲存管理頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>FormsIVS在表單繪製測試調試中的應用</p> </td> 
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
   <td><p>用於Rights Management的REST URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>輸出管理頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>FormsWeb應用程式檔案</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>用於在HTML轉換期間獲取JavaScript</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms管理頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/資料庫/*</p> </td> 
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
   <td><p>工作區管理頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>剩餘支援頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms在JEE核心配置設定頁</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>用戶管理身份驗證</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>用戶管理管理介面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>上載和下載在啟用HTTP文檔的情況下訪問遠程端點、SOAP WSDL端點和SOAP傳輸或EJB傳輸時要處理的文檔。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨站點請求偽造攻擊 {#protecting-from-cross-site-request-forgery-attacks}

跨站點請求偽造(CSRF)攻擊利用網站對用戶的信任來傳輸未經用戶授權和無意的命令。 通過在網頁中包括連結或指令碼，或在電子郵件消息中包括URL來設定攻擊，以訪問用戶已經通過身份驗證的其他站點。

例如，您可能在同時瀏覽其他網站時登錄到管理控制台。 其中一個網頁可以包括帶有HTML影像標籤的 `src` 針對受攻擊網站上的伺服器端指令碼的屬性。 通過利用Web瀏覽器提供的基於cookie的會話認證機制，攻擊網站可以將惡意請求發送到該受攻擊伺服器端指令碼，偽裝成合法用戶。 有關更多示例，請參見 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples)。

CSRF共有以下特點：

* 涉及依賴用戶身份的站點。
* 利用站點對該身份的信任。
* 欺騙用戶瀏覽器將HTTP請求發送到目標站點。
* 涉及具有副作用的HTTP請求。

AEM Forms在JEE上使用Referer Filter功能來阻止CSRF攻擊。 本節中使用以下術語來描述引用過濾機制：

* **允許的引用者：** 引用程式是向伺服器發送請求的源頁的地址。 對於JSP頁或表單，「引用」通常是瀏覽歷史記錄中的上一頁。 影像的引用者通常是顯示影像的頁面。 通過將伺服器資源添加到允許的引用清單，可以標識允許訪問伺服器資源的引用者。
* **允許的引用者例外：** 您可能希望限制「允許的引用」清單中特定引用的訪問範圍。 要強制實施此限制，可以將該引用者的單個路徑添加到允許的引用者例外清單。 禁止從允許引用者例外清單中的路徑發出的請求調用表單伺服器上的任何資源。 您可以為特定應用程式定義允許的參考例外，還可以使用適用於所有應用程式的例外的全局清單。
* **允許的URI:** 這是要提供的資源清單，但不檢查引用標題。 例如，幫助頁不會導致伺服器上的狀態更改的資源可以添加到此清單中。 「允許的URI」清單中的資源不會被引用者篩選器阻止，而不管引用者是誰。
* **空引用者：** 未與父網頁關聯或不源於父網頁的伺服器請求被視為來自空引用者的請求。 例如，當您開啟新的瀏覽器窗口，鍵入一個地址，然後按Enter鍵時，發送到伺服器的引用器為空。 案頭應用程式（.NET或SWING）向Web伺服器發出HTTP請求，還向伺服器發送空引用。

### 引用篩選 {#referer-filtering}

「引用者篩選」過程可以如下所述：

1. 表單伺服器檢查用於調用的HTTP方法：

   1. 如果是POST，則表單伺服器將執行「引用」標題檢查。
   1. 如果是GET，則表單伺服器會繞過「引用」檢查，除非 *CSRF_CHECK_GETS* 設定為true時，它會執行「引用」標題檢查。 *CSRF_CHECK_GETS* 在 *web.xml* 檔案。

1. 表單伺服器檢查允許清單中是否存在請求的URI:

   1. 如果允許列出URI，則伺服器接受該請求。
   1. 如果未允許列出請求的URI，則伺服器將檢索請求的引用者。

1. 如果請求中有引用者，伺服器將檢查它是否是允許的引用者。 如果允許，伺服器將檢查引用者異常：

   1. 如果是異常，則會阻止請求。
   1. 如果不是例外，則會傳遞請求。

1. 如果請求中沒有引用者，伺服器將檢查是否允許空引用者：

   1. 如果允許空引用，則會傳遞該請求。
   1. 如果不允許空引用，伺服器將檢查請求的URI是否是空引用的異常，並相應地處理該請求。

### 管理引用篩選 {#managing-referer-filtering}

AEM Forms在JEE上提供引用程式篩選器，以指定允許訪問伺服器資源的引用程式。 預設情況下，引用過濾器不會過濾使用安全HTTP方法的請求，如GET，除非 *CSRF_CHECK_GETS* 設定為true。 如果允許引用項的埠號設定為0，則JEE上的AEM Forms將允許來自該主機的所有具有引用項的請求，而不考慮埠號。 如果未指定埠號，則僅允許來自預設埠80(HTTP)或埠443(HTTPS)的請求。 如果「允許的引用」清單中的所有條目都被刪除，則禁用「引用過濾」。

首次安裝Document Services時，將使用安裝Document Services的伺服器的地址更新「允許引用」清單。 伺服器的條目包括伺服器名稱、IPv4地址、啟用IPv6時的IPv6地址、環回地址和localhost條目。 添加到允許引用清單的名稱由主機作業系統返回。 例如，IP地址為10.40.54.187的伺服器將包括以下條目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`。 對於主機作業系統重新調整的任何未限定名稱（沒有IPv4地址、 IPv6地址或限定域名的名稱）允許清單不會更新。 修改「允許引用者」清單以適應您的業務環境。 請勿使用預設的允許引用清單在生產環境中部署表單伺服器。 修改任何允許的引用程式、引用程式異常或URI後，請確保重新啟動伺服器以使更改生效。

**管理允許的引用者清單**

可以從管理控制台的用戶管理介面管理允許的引用清單。 用戶管理介面提供了建立、編輯或刪除清單的功能。 請參閱* [防止CSRF攻擊](/help/forms/using/admin-help/preventing-csrf-attacks.md)* *管理幫助* 的子菜單。

**管理允許的引用者異常和允許的URI清單**

AEM Forms在JEE上提供API來管理允許引用的異常清單和允許的URI清單。 您可以使用這些API來檢索、建立、編輯或刪除清單。 以下是可用API的清單：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

有關API的詳細資訊，請參閱*AEM FormsJEE API參考*。

使用 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 全局層允許的引用者例外清單，即定義適用於所有應用程式的例外。 此清單僅包含具有絕對路徑(例如 `/index.html`)或相對路徑(例如 `/sample/`)。 您還可以將規則運算式附加到相對URI的末尾，例如 `/sample/(.)*`。

的 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 清單ID在 `UMConstants` 類 `com.adobe.idp.um.api` 命名空間，在 `adobe-usermanager-client.jar`。 可以使用AEM FormsAPI建立、修改或編輯此清單。 例如，要建立「允許的全局引用者例外」清單，請使用：

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

使用 ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** 特定於應用程式的異常。

**禁用引用篩選器**

如果引用者篩選器完全阻止對表單伺服器的訪問，並且您無法編輯允許的引用者清單，則可以更新伺服器啟動指令碼並禁用引用者篩選。

包括 `-Dlc.um.csrffilter.disabled=true` 啟動指令碼中的JAVA參數並重新啟動伺服器。 確保在正確重新配置「允許引用」清單後刪除JAVA參數。

**自定義WAR檔案的引用篩選**

您可能已建立了自定義WAR檔案，以便與AEM Forms在JEE上合作，以滿足您的業務要求。 要為自定義WAR檔案啟用引用篩選，請包括 ***adobe usermanager-client.jar*** 在WAR的類路徑中，並在* web.xml*檔案中包含具有以下參數的篩選器項：

**CSRF_CHECK_GETS** 控制「引用者」(Referrer)對GET請求的檢查。 如果未定義此參數，則預設值將設定為false。 僅當要篩選GET請求時才包括此參數。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是允許引用者例外清單的ID。 「引用者過濾器」可防止從清單ID標識的清單中的引用者發起的請求調用表單伺服器上的任何資源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是「允許的URI」清單的ID。 引用者篩選器不會阻止對清單ID標識的清單中任何資源的請求，而不管請求中引用者標頭的值如何。

**CSRF_ALLOW_NULL_REFERER** 當引用者為空或不存在時，控制引用者過濾器行為。 如果未定義此參數，則預設值將設定為false。 僅當要允許空引用項時才包括此參數。 允許空引用站點可能允許某些類型的跨站點請求偽造攻擊。

**CSRF_NULL_REFERER_EXCEPTIONS** 是當引用者為空時不執行引用者檢查的URI的清單。 僅當 *CSRF_ALLOW_NULL_REFERER* 設定為false。 用逗號分隔清單中的多個URI。

下面是中篩選器條目的示例 *web.xml* 檔案 ***示例*** WAR檔案：

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

如果CSRF篩選器正在阻止合法伺服器請求，請嘗試下列操作之一：

* 如果拒絕的請求具有「引用者」標題，請仔細考慮將其添加到「允許的引用者」清單。 只添加您信任的引用者。
* 如果拒絕的請求沒有引用者標頭，請修改客戶端應用程式以包括引用者標頭。
* 如果客戶端可以在瀏覽器中工作，請嘗試該部署模型。
* 作為最後的選擇，您可以將資源添加到「允許的URI」清單。 這不是建議的設定。

## 安全網路配置 {#secure-network-configuration}

本節介紹AEM Forms在JEE上所需的協定和埠，並提供在安全網路配置中部署AEM Forms在JEE上的建議。

### AEM Forms在JEE上使用的網路協定 {#network-protocols-used-by-aem-forms-on-jee}

如上節所述，在配置安全網路體系結構時，JEE上的AEM Forms與企業網路中的其他系統之間的交互需要以下網路協定。

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
     <li><p>瀏覽器顯示Configuration Manager和最終用戶Web應用程式</p> </li> 
     <li><p>所有SOAP連接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服務客戶端應用程式，如.NET應用程式</p> </li> 
     <li><p>Adobe Reader®在JEE伺服器Web服務上使用AEM Forms的SOAP</p> </li> 
     <li><p>AdobeFlash®應用程式使用SOAP來表單伺服器Web服務</p> </li> 
     <li><p>AEM Forms在SOAP模式下使用JEE SDK調用</p> </li> 
     <li><p>工作台設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>AEM Forms在Enterprise JavaBeans(EJB)模式下使用時的JEE SDK調用</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>基於電子郵件的服務輸入（電子郵件終結點）</p> </li> 
     <li><p>通過電子郵件發送用戶任務通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC檔案IO</p> </td> 
   <td><p>AEM Forms: JEE監視受監視資料夾以輸入服務（受監視資料夾終結點）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>目錄中組織用戶和組資訊的同步</p> </li> 
     <li><p>互動式用戶的LDAP身份驗證</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>在使用JDBC服務執行進程期間對外部資料庫執行的查詢和過程調用</p> </li> 
     <li><p>內部訪問JEE資料庫上的AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>允許任何WebDAV客戶端在JEE設計時儲存庫（表單、片段等）上遠程瀏覽AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlash應用程式，其中JEE伺服器服務上的AEM Forms配置了遠程處理終結點</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms在JEE上公開MBean以使用JMX進行監控</p> </td> 
  </tr> 
 </tbody> 
</table>

### 應用程式伺服器的埠 {#ports-for-application-servers}

本節介紹支援的每種類型應用程式伺服器的預設埠（和備用配置範圍）。 必須在內部防火牆上啟用或禁用這些埠，這取決於您希望允許的網路功能，這些客戶端連接到在JEE上運行AEM Forms的應用程式伺服器。

>[!NOTE]
>
>預設情況下，伺服器會在adobe.com命名空間下顯示多個JMX MBean。 只有對伺服器運行狀況監視有用的資訊才會公開。 但是，為防止資訊洩露，您應防止不受信任的網路中的呼叫者查找JMX MBean並訪問運行狀況度量。

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
   <td><p>訪問Web應用程式</p> </td> 
   <td><p>[JBOSS_Root]/獨立/configuration/lc_[database].xml</p> <p>HTTP/1.1連接器埠8080</p> <p>AJP 1.3連接器埠8009</p> <p>SSL/TLS連接器埠8443</p> </td> 
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
   <th><p>目的</p> </th> 
   <th><p>埠</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>訪問Web應用程式</p> </td> 
   <td> 
    <ul> 
     <li><p>管理伺服器偵聽埠：預設值為7001</p> </li> 
     <li><p>管理伺服器SSL偵聽埠：預設值為7002</p> </li> 
     <li><p>為受控伺服器配置的埠，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>訪問JEE上的AEM Forms不需要WebLogic管理埠</p> </td> 
   <td> 
    <ul> 
     <li><p>受控伺服器偵聽埠：可配置從1到65534</p> </li> 
     <li><p>受控伺服器SSL偵聽埠：可配置從1到65534</p> </li> 
     <li><p>節點管理器偵聽埠：預設值為5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere埠**

有關JEE上的AEM Forms需要的WebSphere埠的資訊，請轉至WebSphere應用程式伺服器UI中的埠號設定。

### 配置SSL {#configuring-ssl}

參考本節中介紹的物理體系結構 [AEM FormsJEE物理架構](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您應為計畫使用的所有連接配置SSL。 具體來說，所有SOAP連接都必須通過SSL進行，以防止用戶憑據在網路上暴露。

有關如何在JBoss、WebLogic和WebSphere上配置SSL的說明，請參見中的「配置SSL」 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_64)。

有關如何將證書導入為AEM Forms伺服器配置的JVM（Java虛擬機）的說明，請參閱中的「相互驗證」部分 [AEM FormsWorkbench幫助](http://www.adobe.com/go/learn_aemforms_workbench_65)。

### 配置SSL重定向 {#configuring-ssl-redirect}

在將應用程式伺服器配置為支援SSL後，必須確保向應用程式和服務發送的所有HTTP通信都強制使用SSL埠。

要為WebSphere或WebLogic配置SSL重定向，請參閱應用伺服器文檔。

1. 開啟命令提示符，導航到/JBOSS_HOME/standalone/configuration目錄，然後執行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 開啟JBOSS_HOME/standalone/configuration/standalone.xml檔案進行編輯。

   在 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />域:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素，添加以下詳細資訊：:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https連接器元素中添加以下代碼：

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存並關閉standalone.xml檔案。

## 特定於Windows的安全建議 {#windows-specific-security-recommendations}

本節包含在JEE上運行AEM Forms時特定於Windows的安全建議。

### JBoss服務帳戶 {#jboss-service-accounts}

預設情況下，AEM FormsJEE統包安裝使用本地系統帳戶設定服務帳戶。 內置的本地系統用戶帳戶具有高度的可訪問性；它是「管理員」組的一部分。 如果工作進程標識作為本地系統用戶帳戶運行，則該工作進程對整個系統具有完全訪問權限。

#### 使用非管理帳戶運行應用程式伺服器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，為表單伺服器服務建立一個本地用戶以以下方式登錄：

   * 選擇 **用戶無法更改密碼**。
   * 在 **成員** 頁籤，確保列出「用戶」組。

1. 選擇 **設定** > **管理工具** > **服務**。
1. 按兩下應用程式伺服器服務並停止該服務。
1. 在 **登錄** 頁籤 **此帳戶**，瀏覽您建立的用戶帳戶，並輸入帳戶的密碼。
1. 在「本地安全設定」窗口的「用戶權限分配」下，為窗體伺服器運行的用戶帳戶授予以下權限：

   * 拒絕通過終端服務登錄
   * 拒絕本地登錄
   * 以服務身份登錄（應已設定）

1. 授予新用戶帳戶對以下目錄的修改權限：
   * **全局文檔儲存(GDS)目錄**:GDS目錄的位置是在AEM Forms安裝過程中手動配置的。 如果安裝期間位置設定仍為空，則該位置預設為應用程式伺服器安裝下的目錄，位置位於 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX — 儲存庫目錄**:預設位置為 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms臨時目錄**:
      * (Windows)在環境變數中設定的TMP或TEMP路徑
      * （AIX、Linux或Solaris）登錄用戶的主目錄在基於UNIX的系統上，非根用戶可以將以下目錄用作臨時目錄：
      * (Linux)/var/tmp或/usr/tmp
      * (AIX)/tmp或/usr/tmp
      * (Solaris)/var/tmp或/usr/tmp
1. 為以下目錄賦予新用戶帳戶寫入權限：
   * [JBoss目錄]\獨立\部署
   * [JBoss目錄]\獨立\
   * [JBoss目錄]\bin\

   >[!NOTE]
   >
   > JBoss Application Server的預設安裝位置：
   > * 窗口：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux:/opt/jboss/。


1. 啟動應用程式伺服器服務。

### 檔案系統安全 {#file-system-security}

AEM Forms在JEE上使用檔案系統的方式如下：

* 儲存在處理文檔輸入和輸出時使用的臨時檔案
* 將用於支援已安裝的解決方案元件的檔案儲存在全局存檔儲存中
* 受監視的資料夾儲存從檔案系統資料夾位置輸入到服務的已刪除檔案

使用受監視的資料夾作為使用表單伺服器服務發送和接收文檔的方式時，請在檔案系統安全性方面採取額外的預防措施。 當用戶刪除受監視資料夾中的內容時，該內容將通過受監視資料夾公開。 在這種情況下，服務不會驗證實際的最終用戶。 相反，它依賴在資料夾級別設定的ACL和共用級別安全性來確定哪些人可以有效地調用服務。

## 特定於JBoss的安全建議 {#jboss-specific-security-recommendations}

本節包含在JEE上運行AEM Forms時特定於JBoss 7.0.6的應用程式伺服器配置建議。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

在JBoss上使用交鑰匙安裝方法在JEE上安裝AEM Forms時，已配置對JBoss管理控制台和JMX控制台的訪問（JMX監視已禁用）。 如果您使用自己的JBoss Application Server，請確保對JBoss Management Console和JMX監控控制台的訪問是安全的。 在名為jmx-invoker-service.xml的JBoss配置檔案中設定對JMX監控控制台的訪問。

### 禁用目錄瀏覽 {#disable-directory-browsing}

登錄到管理控制台後，可以通過修改URL來瀏覽控制台的目錄清單。 例如，如果將URL更改為以下URL之一，則可能會顯示目錄清單：

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## 特定於WebLogic的安全建議 {#weblogic-specific-security-recommendations}

本節包含在JEE上運行AEM Forms時保護WebLogic 9.1的應用程式伺服器配置建議。

### 禁用目錄瀏覽 {#disable_directory_browsing-1}

將weblogic.xml檔案中的index-directories屬性設定為 `false`，如下例所示：

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 啟用WebLogic SSL埠 {#enable-weblogic-ssl-port}

預設情況下，WebLogic不啟用預設的SSL偵聽埠7002。 在配置SSL之前，請在WebLogic伺服器管理控制台中啟用此埠。

## 特定於WebSphere的安全建議 {#websphere-specific-security-recommendations}

本節包含用於保護在JEE上運行AEM Forms的WebSphere的應用程式伺服器配置建議。

### 禁用目錄瀏覽 {#disable_directory_browsing-2}

設定 `directoryBrowsingEnabled` ibm-web-ext.xml檔案中的屬性 `false`。

### 啟用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登錄到WebSphere管理控制台。
1. 在導航樹中，轉到 **安全** > **全球安全**
1. 選擇 **啟用管理安全性**。
1. 取消選擇兩者 **啟用應用程式安全性** 和 **使用Java 2安全**。
1. 按一下 **確定** 或 **應用**。
1. 在 **消息** 框中，按一下 **直接保存到主配置**。
