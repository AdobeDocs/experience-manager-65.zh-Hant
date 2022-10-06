---
title: 在OSGi環境中強化和保護AEM表單
seo-title: Hardening and Securing AEM forms on OSGi environment
description: 了解在OSGi伺服器上保護AEM Forms的建議和最佳實務。
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

# 在OSGi環境中強化和保護AEM表單 {#hardening-and-securing-aem-forms-on-osgi-environment}

了解在OSGi伺服器上保護AEM Forms的建議和最佳實務。

保護伺服器環境對於組織至關重要。 本文說明保護執行AEM Forms之伺服器的建議與最佳作法。 這不是適用於作業系統的全面的主機強化文檔。 相反地，本文介紹了您應實施的各種安全強化設定，以增強已部署應用程式的安全性。 但是，為了確保應用程式伺服器保持安全，除了本文中提供的建議外，您還應實施安全監控、檢測和響應過程。 本檔案也包含保護PII（個人識別資訊）的最佳作法和准則。

本文旨在為顧問、安全專家、系統架構師以及負責規劃AEM Forms應用程式或基礎架構開發與部署的IT專業人員提供。 這些角色包括下列常見角色：

* IT和運營工程師必須在自己或客戶組織中部署安全的Web應用程式和伺服器。
* 負責為組織中的客戶規劃建築工作的建築師和規劃師。
* 專注於在組織內跨平台提供安全性的IT安全專家。
* 需要客戶和合作夥伴詳細資源的Adobe和合作夥伴的顧問。

下面的映像顯示典型AEM Forms部署中使用的元件和協定，包括相應的防火牆拓撲：

![典型體系結構](assets/typical-architecture.png)

AEM Forms可高度自訂，且可在多種不同環境中運作。 有些建議可能不適用於您的組織。

## 安全傳輸層 {#secure-transport-layer}

傳輸層安全漏洞是任何面向網際網路或面向內聯網的應用伺服器面臨的首要威脅之一。 本節介紹針對這些漏洞強化網路上主機的過程。 它解決了網路分段、傳輸控制協定/網際網路協定(TCP/IP)棧強化以及使用防火牆進行主機保護等問題。

### 限制開啟的端點  {#limit-open-endpoints}

組織可以有外部防火牆，以限制一般使用者和AEM Forms發佈伺服器陣列之間的存取權。 組織也可以有內部防火牆，以限制發佈伺服器陣列與組織元素內其他元素（例如，製作例項、處理例項、資料庫）之間的存取。 允許防火牆為一般使用者和組織元素內啟用有限數量的AEM Forms URL:

#### 配置外部防火牆  {#configure-external-firewall}

您可以設定外部防火牆，以允許特定AEM Forms URL存取網際網路。 填寫或提交最適化表單、HTML5、通信管理信函或登入AEM Forms伺服器時，必須存取以下URL:

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
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5表單</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
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

您可以設定內部防火牆，以允許某些AEM Forms元件（例如製作例項、處理例項、資料庫）與發佈伺服器陣列和拓撲圖中提到的其他內部元件通訊：

<table> 
 <tbody>
  <tr>
   <td>主機<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>發佈伺服器陣列（發佈節點）</td> 
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

依預設，發佈節點上的可用資產可供所有人存取。 所有資產都會啟用唯讀存取權。 必須啟用匿名訪問。 如果您打算限制表單檢視並僅向已驗證的使用者提交存取權，則使用通用群組，讓已驗證的使用者僅能以唯讀方式存取發佈節點上可用的資產。 以下位置/目錄包含需要強化（已驗證使用者只讀存取權）的表單資產：

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 安全地處理表單資料  {#securely-handle-forms-data}

AEM Forms會將資料儲存至預先定義的位置和臨時資料夾。 您應保護資料安全，以防止未經授權的使用。

### 設定臨時資料夾的定期清理 {#setup-periodic-cleanup-of-temporary-folder}

配置檔案附件、驗證或預覽元件的表單時，相應的資料儲存在位於/tmp/fd/的發佈節點上。 會定期清除資料。 您可以修改預設資料清除作業，使其更具攻擊性。 要修改計劃清除資料的作業，請開啟AEM Web Console、開啟AEM Forms臨時儲存清除任務，並修改Cron表達式。

在上述情況中，僅會為已驗證的使用者儲存資料。 此外，資料還受到訪問控制清單(ACL)的保護。 因此，修改資料清除是保護資訊的額外步驟。

### 保護由表單入口網站儲存的資料提交動作 {#secure-data-saved-by-forms-portal-submit-action}

依預設，適用性表單的表單入口網站提交動作會將資料儲存在發佈節點的本機存放庫中。 資料儲存在/content/forms/fp。 **不建議將資料儲存在發佈執行個體上。**

您可以設定儲存服務以透過連線傳送至處理叢集，而不需在發佈節點上將任何項目儲存於本機。 處理群集位於私有防火牆後的安全區域，資料保持安全。

使用AEM DS設定服務處理伺服器的認證，將資料從發佈節點發佈到處理伺服器。 建議使用具有處理伺服器儲存庫讀寫權限的受限非管理用戶的憑據。 如需詳細資訊，請參閱 [配置草稿和提交的儲存服務](/help/forms/using/configuring-draft-submission-storage.md).

### 由表單資料模型(FDM)處理的安全資料 {#secure-data-handled-by-form-data-model-fdm}

使用具有最低所需權限的使用者帳戶來設定表單資料模型(FDM)的資料來源。 使用管理帳戶可以為未經授權的用戶提供對元資料和架構實體的開放訪問。\
資料整合也提供授權FDM服務要求的方法。 您可以插入執行前和執行後授權機制來驗證請求。 在預填表單、提交表單和通過規則調用服務時生成服務請求。

**處理前授權：** 您可以使用預先處理授權，在執行請求之前驗證請求的真實性。 您可以使用輸入、服務和請求詳細資訊來允許或停止執行請求。 如果停止執行，則可以返回資料整合異常OPERATION_ACCESS_DENIED。 您也可以在傳送用戶端請求以供執行之前加以修改。 例如，變更輸入並新增其他資訊。

**進程後授權：** 在將結果返回給請求者之前，可以使用後處理授權來驗證和控制結果。 您也可以篩選、修剪及插入其他資料至結果。

### 限制使用者存取權 {#limit-user-access}

製作、發佈和處理例項需要不同的使用者角色集。 不運行具有管理員憑據的任何實例。

**在發佈例項上：**

* 只有表單使用者群組的使用者才能預覽、建立草稿和提交表單。
* 只有cm-user-agent組的用戶才能預覽通信管理信函。
* 禁用所有非必需的匿名訪問。

**在製作例項上：**

* 有一組不同的預先定義群組，具有每個角色的特定權限。 將使用者指派至群組。

   * 表單使用者群組的使用者：

      * 可以建立、填寫、發佈和提交表單。
      * 無法建立XDP型最適化表單。
      * 沒有編寫最適化表單指令碼的權限。
      * 無法匯入XDP或包含XDP的任何套件
   * 表單功能使用者群組的使用者可建立、填寫、發佈和提交所有類型的表單、撰寫最適化表單的指令碼、匯入包含XDP的套件。
   * 範本作者和範本使用者可預覽和建立範本。
   * fdm作者的使用者可以建立和修改表單資料模型。
   * cm-user-agent組的用戶可以建立、預覽和發佈通信管理信函。
   * 工作流編輯器組的用戶可以建立收件箱應用程式和工作流模型。


**處理作者時：**

* 若要遠端儲存並提交使用案例，請建立擁有crx-repository內容/表單/fp路徑之讀取、建立和修改權限的使用者。
* 將使用者新增至工作流程使用者群組，讓使用者能使用AEM收件匣應用程式。

## AEM Forms環境的安全內聯網元素 {#secure-intranet-elements-of-an-aem-forms-environment}

一般而言，處理叢集和Forms Workflow附加元件(JEE上的AEM Forms)會在防火牆後執行。 因此，這些都被認為是安全的。 您仍可執行一些步驟來強化這些環境：

### 安全處理群集 {#secure-processing-cluster}

處理叢集會在製作模式中執行，但不會用於開發活動。 請勿將一般使用者納入處理叢集的內容作者和表單使用者群組中。

### 使用AEM最佳實務來保護AEM Forms環境 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

本檔案提供AEM Forms環境的特定指示。 您應採取措施，確保部署時基礎AEM安裝安全無虞。 如需詳細指示，請參閱 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md) 檔案。
