---
title: OSGi環境AEM的強化與固定
seo-title: Hardening and Securing AEM forms on OSGi environment
description: 瞭解在OSGi伺服器上保護AEM Forms的建議和最佳做法。
seo-description: Learn recommendations and best practices for securing AEM Forms on OSGi server.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# OSGi環境AEM的強化與固定 {#hardening-and-securing-aem-forms-on-osgi-environment}

瞭解在OSGi伺服器上保護AEM Forms的建議和最佳做法。

保護伺服器環境對組織來說至關重要。 本文介紹保護運行AEM Forms的伺服器的建議和最佳做法。 這不是適用於您的作業系統的全面的主機強化文檔。 相反，本文描述了您應實施的各種安全強化設定，以增強已部署應用程式的安全性。 但是，為確保應用程式伺服器保持安全，除了本文中提供的建議之外，您還應實施安全監控、檢測和響應過程。 該文檔還包含保護PII（個人身份資訊）的最佳做法和指導原則。

本文面向負責規劃AEM Forms應用程式或基礎架構開發和部署的顧問、安全專家、系統架構師和IT專業人員。 這些角色包括以下常見角色：

* IT和運營部門的工程師必須在其自己或客戶組織中部署安全的Web應用程式和伺服器。
* 負責為組織中的客戶規劃建築工作的建築師和規劃師。
* IT安全專家，他們專注於跨組織內的平台提供安全保護。
* 需要客戶和合作夥伴詳細資源的Adobe和合作夥伴的顧問。

以下映像顯示典型AEM Forms部署中使用的元件和協定，包括相應的防火牆拓撲：

![典型體系結構](assets/typical-architecture.png)

AEM Forms具有高度的可定製性，可在多種不同的環境中工作。 某些建議可能不適用於您的組織。

## 安全傳輸層 {#secure-transport-layer}

傳輸層安全漏洞是任何面向Internet或面向Intranet的應用程式伺服器面臨的首批威脅之一。 本節介紹針對這些漏洞加強網路上主機的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧加固以及使用防火牆保護主機的問題。

### 限制開啟的終結點  {#limit-open-endpoints}

組織可以具有外部防火牆來限制最終用戶和AEM Forms發佈場之間的訪問。 組織還可以具有內部防火牆，以限制發佈場與組織元素內的其他元素（例如，作者實例、處理實例、資料庫）之間的訪問。 允許防火牆允許訪問有限數量的最終用戶和組織元素內的AEM FormsURL:

#### 配置外部防火牆  {#configure-external-firewall}

您可以配置外部防火牆以允許某個AEM FormsURL訪問Internet。 要填寫或提交自適應表單、HTML5、信件管理信件或登錄AEM Forms伺服器，需要訪問以下URL:

<table> 
 <tbody>
  <tr>
   <td>Component</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>調適型表單</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr：內容</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML表</td> 
   <td>
    <ul> 
     <li>/content/forms/forms/forms/profiles///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createterge* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表單入口網站 </td> 
   <td>
    <ul> 
     <li>/content/forms/portal</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms 應用程式</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 配置內部防火牆  {#configure-internal-firewall}

您可以配置內部防火牆，以允許某些AEM Forms元件（例如，作者實例、處理實例、資料庫）與發佈伺服器場和拓撲圖中提到的其他內部元件通信：

<table> 
 <tbody>
  <tr>
   <td>主機<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>發佈場（發佈節點）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>處理伺服器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow附加伺服器(JEE伺服器上的AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 設定儲存庫權限和訪問控制清單(ACL) {#setup-repository-permissions-and-access-control-lists-acls}

預設情況下，發佈節點上的可用資產可供所有人訪問。 所有資產都啟用只讀訪問。 需要啟用匿名訪問。 如果您計畫限制表單視圖並僅向經過身份驗證的用戶提交訪問權限，則使用公用組只允許經過身份驗證的用戶對發佈節點上的可用資產具有只讀訪問權限。 以下位置/目錄包含需要硬化的表單資產（對已驗證的用戶進行只讀訪問）:

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 安全地處理表單資料  {#securely-handle-forms-data}

AEM Forms將資料儲存到預定義的位置和臨時資料夾。 您應保護資料以防止未經授權的使用。

### 設定臨時資料夾的定期清理 {#setup-periodic-cleanup-of-temporary-folder}

在為檔案附件、驗證或預覽元件配置表單時，相應的資料將儲存在/tmp/fd/的發佈節點上。 定期清除資料。 您可以將預設資料清除作業修改為更激進。 要修改計劃清除資料的作業，請打AEM開Web控制台，開啟AEM Forms臨時儲存清理任務，並修改Cron表達式。

在上述情形中，資料僅保存給經過驗證的用戶。 此外，還使用訪問控制清單(ACL)保護資料。 因此，修改資料清除是保護資訊的附加步驟。

### 通過表單門戶提交操作保存的資料安全 {#secure-data-saved-by-forms-portal-submit-action}

預設情況下，自適應表單的表單門戶提交操作會將資料保存到發佈節點的本地儲存庫中。 資料保存在/content/forms/fp。 **建議不要在發佈實例上儲存資料。**

您可以配置儲存服務以通過線向處理群集發送，而無需在發佈節點上本地保存任何內容。 處理群集位於專用防火牆後的安全區域中，資料保持安全。

使用DS設定服務的處理服AEM務器的憑據將資料從發佈節點發佈到處理伺服器。 建議使用對處理伺服器儲存庫具有讀寫訪問權限的受限非管理用戶的憑據。 有關詳細資訊，請參見 [為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

### 通過表單資料模型(FDM)處理的安全資料 {#secure-data-handled-by-form-data-model-fdm}

使用具有所需最低權限的用戶帳戶為表單資料模型(FDM)配置資料源。 使用管理帳戶可以為未經授權的用戶提供元資料和架構實體的開放訪問。\
資料整合還提供了授權FDM服務請求的方法。 您可以插入執行前和執行後授權機制來驗證請求。 在預填表單、提交表單和通過規則調用服務時生成服務請求。

**預處理授權：** 您可以在執行請求之前使用預處理授權來驗證請求的真實性。 您可以使用輸入、服務和請求詳細資訊來允許或停止執行請求。 如果停止執行，則可以返回資料整合異常OPERATION_ACCESS_DENIED。 您還可以在發送客戶端請求以執行之前修改它。 例如，更改輸入並添加附加資訊。

**後處理授權：** 您可以使用後處理授權在將結果返回給請求者之前驗證和控制結果。 您還可以過濾、修剪和向結果插入附加資料。

### 限制用戶訪問 {#limit-user-access}

建立、發佈和處理實例需要另一組用戶角色。 不運行任何具有管理員憑據的實例。

**在發佈實例上：**

* 只有表單用戶組的用戶才能預覽、建立草稿和提交表單。
* 只有cm-user-agent組的用戶才能預覽通信管理信函。
* 禁用所有非必需的匿名訪問。

**在作者實例上：**

* 對於每個角色，都有一組不同的預定義組，具有特定權限。 將用戶分配給組。

   * 表單用戶組的用戶：

      * 可以建立、填寫、發佈和提交表單。
      * 無法建立基於XDP的自適應表單。
      * 沒有為自適應表單編寫指令碼的權限。
      * 無法導入XDP或包含XDP的任何包
   * 表單 — 超級用戶組的用戶建立、填充、發佈和提交所有類型的表單，編寫自適應表單的指令碼，導入包含XDP的包。
   * 模板作者和模板權用戶的用戶可以預覽和建立模板。
   * fdm作者的用戶可以建立和修改表單資料模型。
   * cm-user-agent組的用戶可以建立、預覽和發佈通信管理信函。
   * 工作流編輯器組的用戶可以建立收件箱應用程式和工作流模型。


**在處理作者時：**

* 對於遠程保存和提交使用案例，請建立具有對crx-repository的內容/表單/fp路徑的讀取、建立和修改權限的用戶。
* 將用戶添加到工作流用戶組，以使用戶能夠使用收件箱AEM應用程式。

## AEM Forms環境的安全內聯網要素 {#secure-intranet-elements-of-an-aem-forms-environment}

通常，處理群集和Forms Workflow附加模組(JEE上的AEM Forms)在防火牆後運行。 所以，這些是安全的。 您仍然可以執行幾個步驟來強化這些環境：

### 安全處理群集 {#secure-processing-cluster}

處理群集以作者模式運行，但不將其用於開發活動。 不允許將普通用戶包括在處理群集的內容作者和表單用戶組中。

### 使用AEM最佳做法保護AEM Forms環境 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

本檔案提供了針對AEM Forms環境的具體說明。 您應確保在部署時基礎AEM安裝是安全的。 有關詳細說明，請參見 [安AEM全核對表](/help/sites-administering/security-checklist.md) 文檔。
