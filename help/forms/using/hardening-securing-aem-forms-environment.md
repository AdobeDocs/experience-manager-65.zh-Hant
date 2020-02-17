---
title: 在OSGi環境上強化和保護AEM表單
seo-title: 在OSGi環境上強化和保護AEM表單
description: 瞭解在OSGi伺服器上保護AEM Forms的建議和最佳實務。
seo-description: 瞭解在OSGi伺服器上保護AEM Forms的建議和最佳實務。
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 在OSGi環境上強化和保護AEM表單 {#hardening-and-securing-aem-forms-on-osgi-environment}

瞭解在OSGi伺服器上保護AEM Forms的建議和最佳實務。

保護伺服器環境對組織至關重要。 本文說明如何保護執行AEM Forms的伺服器的安全建議和最佳實務。 這不是針對您作業系統的完整主機強化檔案。 相反地，本文說明您應實作的各種安全強化設定，以增強已部署應用程式的安全性。 不過，為了確保應用程式伺服器保持安全，除了本文中提供的建議外，您還應實作安全性監控、偵測和回應程式。 本檔案也包含保護PII（個人識別資訊）的最佳實務和准則。

本文的適用對象為負責規劃AEM Forms應用程式或基礎架構開發與部署的顧問、安全性專家、系統架構設計人員和IT專業人員。 這些角色包括以下常見角色：

* IT和營運部門的工程師必須在自己或客戶組織中部署安全的Web應用程式和伺服器。
* 負責規劃組織中客戶的建築工作的建築師和規劃師。
* IT安全專家，他們專注於在組織內跨平台提供安全性。
* 需要客戶和合作夥伴詳細資源的Adobe顧問和合作夥伴。

下列影像顯示一般AEM Forms部署中使用的元件和通訊協定，包括適當的防火牆拓撲：

![典型體系結構](assets/typical-architecture.png)

AEM Forms具備高度自訂性，可在許多不同的環境中運作。 有些建議可能不適用於您的組織。

## 安全傳輸層 {#secure-transport-layer}

傳輸層安全漏洞是對任何面向網際網路或面向內部網的應用程式伺服器的首批威脅之一。 本節介紹加強網路上主機抵御這些漏洞的過程。 它解決了網路分段、傳輸控制協定/Internet協定(TCP/IP)棧強化以及使用防火牆保護主機的問題。

### 限制開放端點 {#limit-open-endpoints}

組織可以有外部防火牆，以限制使用者與AEM Forms發佈群之間的存取。 組織也可以有內部防火牆，以限制發佈群與組織元素內的其他元素（例如，作者例項、處理例項、資料庫）之間的存取。 允許防火牆為使用者和組織元素啟用有限數量的AEM Forms URL存取：

#### 配置外部防火牆 {#configure-external-firewall}

您可以設定外部防火牆，以允許特定AEM Forms URL存取網際網路。 您必須存取這些URL，才能填寫或送出最適化表單、HTML5、信件管理信件，或登入AEM Forms伺服器：

<table> 
 <tbody>
  <tr>
   <td>元件</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>最適化表單</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5表格</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorresponces* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表單入口網站 </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms應用程式</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/authenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 配置內部防火牆 {#configure-internal-firewall}

您可以設定內部防火牆，以允許某些AEM Forms元件（例如，作者例項、處理例項、資料庫）與發佈群組及其他拓撲圖中提及的內部元件通訊：

<table> 
 <tbody>
  <tr>
   <td>主機<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>發佈群（發佈節點）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>處理伺服器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow add-on server（AEM Forms on JEE伺服器）</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 設定儲存庫權限和訪問控制清單(ACL) {#setup-repository-permissions-and-access-control-lists-acls}

依預設，每個人都可存取發佈節點上可用的資產。 所有資產都啟用唯讀存取。 必須啟用匿名存取。 如果您打算限制表單檢視並僅將存取權提交給已驗證的使用者，則使用通用群組只允許已驗證的使用者擁有發佈節點上可用資產的唯讀存取權。 下列位置／目錄包含需要強化的表單資產（已驗證使用者的唯讀存取權）:

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 安全地處理表單資料 {#securely-handle-forms-data}

AEM Forms會將資料儲存至預先定義的位置和暫存資料夾。 您應保護資料的安全，以防止未經授權的使用。

### 設定臨時資料夾的定期清理 {#setup-periodic-cleanup-of-temporary-folder}

當您為檔案附件、驗證或預覽元件配置表單時，相應的資料將儲存在位於/tmp/fd/的發佈節點上。 系統會定期清除資料。 您可以將預設資料清除作業修改為更具攻擊性。 若要修改排程為清除資料的工作，請開啟AEM Web Console、開啟AEM Forms Temporary Storage Cleaning Task，並修改Cron運算式。

在上述案例中，資料僅會儲存給已驗證的使用者。 此外，資料還受到訪問控制清單(ACL)的保護。 因此，修改資料清除是保護資訊安全的另外一個步驟。

### 保護表單入口網站提交動作所儲存的資料 {#secure-data-saved-by-forms-portal-submit-action}

預設情況下，最適化表單的表單門戶提交操作會將資料保存到發佈節點的本地儲存庫中。 資料儲存於/content/forms/fp。 **建議不要將資料儲存在發佈例項上。**

您可以配置儲存服務以通過線路向處理群集發送，而無需在發佈節點上本地保存任何內容。 處理群集位於私有防火牆後的安全區域，資料保持安全。

使用AEM DS設定服務的處理伺服器認證，將資料從發佈節點張貼至處理伺服器。 建議使用受限非管理用戶的憑據，並具有對處理伺服器儲存庫的讀寫訪問權。 有關詳細資訊，請參 [閱為草稿和提交配置儲存服務](/help/forms/using/configuring-draft-submission-storage.md)。

### 表單資料模型(FDM)處理的安全資料 {#secure-data-handled-by-form-data-model-fdm}

使用具有最低所需權限的用戶帳戶為表單資料模型(FDM)配置資料源。 使用管理帳戶可讓未經授權的使用者開放存取中繼資料和架構實體。\
資料整合還提供了授權FDM服務請求的方法。 您可以插入執行前和執行後授權機制來驗證請求。 服務請求是在預先填寫表單、提交表單及透過規則叫用服務時產生的。

**** 預處理授權：您可以使用處理前授權來驗證請求的真實性，然後再執行請求。 您可以使用輸入、服務和請求詳細資訊來允許或停止執行請求。 如果停止執行，則可以返回資料整合例外OPERATION_ACCESS_DENIED。 您也可以在傳送用戶端要求以執行之前加以修改。 例如，變更輸入並新增其他資訊。

**** 處理後授權：在將結果返回給請求者之前，可以使用後處理授權來驗證和控制結果。 您也可以篩選、修剪及插入其他資料至結果。

### 限制使用者存取權 {#limit-user-access}

作者、發佈和處理例項需要一組不同的使用者角色。 請勿使用管理員認證執行任何例項。

**在發佈例項上：**

* 只有表單使用者群組的使用者才能預覽、建立草稿及提交表單。
* 只有cm-user-agent組的用戶才能預覽通信管理信件。
* 停用所有非必要的匿名存取。

**在作者實例上：**

* 每個角色都有一組不同的預先定義群組，具有特定權限。 指派使用者至群組。

   * 表單使用者群組的使用者：

      * 可以建立、填寫、發佈及提交表格。
      * 無法建立以XDP為基礎的調適性表單。
      * 沒有編寫最適化表單指令碼的權限。
      * 無法導入XDP或包含XDP的任何包
   * 表單使用者——強大的使用者群組——建立、填寫、發佈和送出所有類型的表單、編寫最適化表單的指令碼、匯入包含XDP的封裝。
   * 範本作者和範本強大使用者的使用者可以預覽並建立範本。
   * fdm-authors的用戶可以建立和修改表單資料模型。
   * cm-user-agent組的用戶可以建立、預覽和發佈通信管理信件。
   * 工作流編輯組的用戶可以建立收件箱應用程式和工作流模型。


**在處理作者時：**

* 對於遠程保存和提交使用案例，請建立對crx-repository的content/form/fp路徑具有讀取、建立和修改權限的用戶。
* 將使用者新增至工作流程使用者群組，讓使用者能夠使用AEM收件匣應用程式。

## AEM Forms環境的安全內部網路元素 {#secure-intranet-elements-of-an-aem-forms-environment}

一般而言，「處理叢集」和「表單工作流程」附加元件(AEM Forms on JEE)會在防火牆後執行。 因此，這些都被認為是安全的。 您仍然可以執行幾個步驟來強化這些環境：

### 安全處理群集 {#secure-processing-cluster}

處理群集在作者模式下運行，但不用於開發活動。 請勿允許一般使用者納入處理叢集的內容作者和表單使用者群組。

### 使用AEM最佳實務來保護AEM Forms環境 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

本檔案提供AEM Forms環境的特定指示。 您應該負責確保在部署時，您的基礎AEM安裝是安全的。 如需詳細指示，請參閱 [AEM安全性檢查清單檔案](/help/sites-administering/security-checklist.md) 。
