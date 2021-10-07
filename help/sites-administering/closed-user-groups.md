---
title: AEM中的封閉使用者群組
seo-title: Closed User Groups in AEM
description: 了解AEM中封閉的使用者群組。
seo-description: Learn about Closed User Groups in AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '6872'
ht-degree: 0%

---

# AEM中的封閉使用者群組{#closed-user-groups-in-aem}

## 簡介 {#introduction}

自AEM 6.3起，推出新的封閉使用者群組實作，旨在解決現有實作中存在的效能、延展性和安全性問題。

>[!NOTE]
>
>為了簡單起見，本檔案中將使用CUG縮寫。

新實作的目標是視需要涵蓋現有功能，同時解決舊版的問題和設計限制。 結果為新的CUG設計，具有以下特點：

* 可以單獨或組合使用的身份驗證和授權元素的明確分離；
* 專用授權模型，在配置的CUG樹上反映受限讀取訪問，而不干擾其他訪問控制設定和權限要求；
* 在編寫實例時通常需要的受限讀取訪問的訪問控制設定與通常只在發佈時才需要的權限評估之間分離；
* 編輯受限讀取訪問而不升級權限；
* 專用節點類型擴展標籤認證要求；
* 與身份驗證要求關聯的可選登錄路徑。

### 新的自訂使用者群組實作 {#the-new-custom-user-group-implementation}

AEM內容中稱為CUG的步驟如下：

* 在需要保護的樹上限制讀訪問，並且只允許讀取帶有指定CUG實例的清單主體或完全排除在CUG評估之外的主體。 這稱為&#x200B;**authorization**&#x200B;元素。
* 在指定的樹上強制驗證，並可選地為該樹指定一個專用的登錄頁，該登錄頁隨後被排除。 這稱為&#x200B;**authentication**&#x200B;元素。

新的實施旨在在驗證和授權元素之間划出一條線。 自AEM 6.3起，可在不明確新增驗證要求的情況下限制讀取存取。 例如，如果給定實例完全需要身份驗證，或給定樹已駐留在要求身份驗證的子樹中。

同樣，在不更改有效權限設定的情況下，可以用驗證要求來標籤給定的樹。 組合和結果列在[Combining CUG Policies and the Authentication Requirement](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)部分中。

## 概覽 {#overview}

### 授權：限制讀取訪問 {#authorization-restricting-read-access}

CUG的主要功能是限制除了所選主體之外，所有人在內容存放庫的指定樹狀結構上的讀取存取。 新實施採用的方法不是即時操作預設訪問控制內容，而是定義代表CUG的專用類型的訪問控制策略。

#### CUG的訪問控制策略 {#access-control-policy-for-cug}

這種新型策略具有以下特點：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定義）的存取控制原則；
* PrincipalSetPolicy授予可修改的主體集的權限；
* 授予的權限和策略的範圍是實施詳細資訊。

此外，用於表示CUG的PrincipalSetPolicy的實施還定義了：

* CUG策略僅授予對常規JCR項的讀取訪問權（例如，排除訪問控制內容）;
* 該範圍由保存CUG策略的訪問控制節點定義；
* CUG策略可以嵌套，嵌套的CUG啟動新CUG而不繼承「parent」CUG的主集；
* 如果啟用了評估，則策略的效果將繼承到整個子樹下到下一個嵌套CUG。

這些CUG原則會透過名為oak-authorization-cug的個別授權模組部署至AEM執行個體。 本模組隨附其自己的訪問控制管理和權限評估。 換句話說，預設AEM設定會提供結合多個授權機制的Oak內容存放庫設定。 如需詳細資訊，請參閱Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)上的[本頁。

在此複合設定中，新CUG不會替換附加到目標節點的現有訪問控制內容，而是設計為補充內容，以後也可以刪除，而不會影響原始訪問控制，預設情況下，AEM中的訪問控制清單是該內容。

與前一實施不同，新的CUG策略始終被識別並視為訪問控制內容。 這表示使用JCR存取控制管理API來建立和編輯這些API。 有關詳細資訊，請參閱[管理CUG策略](#managing-cug-policies)部分。

#### CUG策略的權限評估 {#permission-evaluation-of-cug-policies}

除了CUG專用的訪問控制管理之外，新授權模型允許有條件地啟用對其策略的權限評估。 這可讓您在預備環境中設定CUG原則，並且只有在將有效權限複製到生產環境後，才能啟用評估。

CUG政策的權限評估以及與預設或任何其他授權模型的互動，會遵循Apache Jackrabbit Oak中為多個授權機制所設計的模式：只有在所有模型都授予存取權時，才會授予指定的一組權限。 如需詳細資訊，請參閱[此頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

下列特性適用於與用於處理和評估CUG策略的授權模型相關的權限評估：

* 它只處理常規節點和屬性的讀取權限，而不處理讀取訪問控制內容
* 它不處理寫權限或修改受保護的JCR內容（訪問控制、節點類型資訊、版本設定、鎖定或用戶管理等）所需的任何類型的權限；這些權限不受CUG策略的影響，並且不會由關聯的授權模型評估。 是否授予這些權限取決於安全設定中配置的其他模型。

單個CUG策略對權限評估的影響可概括如下：

* 除策略中列出的包含被排除的主體或主體的主體外，所有人都拒絕讀取權限；
* 該策略對保存該策略及其屬性的訪問控制節點生效；
* 此效果在層次結構中被附加，即由訪問控制節點定義的項目樹；
* 但是，它不影響訪問控制節點的兄弟和祖先；
* 給定CUG的繼承將停止在嵌套CUG處。

#### 最佳作法 {#best-practices}

在定義通過CUG的受限讀取權限時，應考慮以下最佳做法：

* 有意識地決定您對CUG的需求是限制讀取存取還是驗證需求。 若是後者或兩者皆需，請參閱最佳實務一節，以取得有關驗證要求的詳細資訊
* 為需要保護的資料或內容建立威脅模型，以識別威脅界限並清楚了解資料的敏感性以及與授權訪問相關聯的角色
* 為儲存庫內容和CUG建立模型，同時銘記與一般授權相關的方面和最佳做法：

   * 請記住，只有當給定CUG和評估設定授予中部署的其他模組允許給定主體讀取給定的儲存庫項目時，才授予讀取權限
   * 避免建立冗餘CUG，其中讀取訪問已被其他授權模組限制
   * 過度需要巢狀CUG可能會突顯內容設計中的問題
   * 對CUG的過度需求（例如，在每一頁上）可能表示需要定制授權模型，這可能更適合於滿足應用程式和現有內容的特定安全需求。

* 將CUG策略支援的路徑限制為儲存庫中的幾個樹，以實現最佳效能。 例如，僅允許在/content節點下方的CUG，因為自AEM 6.3以來，預設值為已發運。
* CUG策略旨在授予對一小組主體的讀取訪問權限。 需要大量原則可能會突出內容或應用程式設計中的問題，應重新考慮。

### 驗證：定義驗證需求 {#authentication-defining-the-auth-requirement}

CUG功能的認證相關部分允許標籤需要認證的樹並可選地指定專用的登錄頁。 根據前一版本，新實現允許標籤需要在內容儲存庫中進行身份驗證的樹，並有條件地啟用與`Sling org.apache.sling.api.auth.Authenticator`的同步，該負責最終執行該要求並重定向到登錄資源。

通過提供`sling.auth.requirements`註冊屬性的OSGi服務向驗證器註冊這些要求。 然後，這些屬性將用於動態擴展驗證需求。 如需詳細資訊，請參閱[Sling檔案](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用專用混頻類型定義驗證需求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

基於安全理由，新實施會以名為`granite:AuthenticationRequired`的專用混合類型取代剩餘JCR屬性的使用，該類型定義登入路徑`granite:loginPath`的單一選用屬性類型為STRING。 只有與此混合類型相關的內容變更才會更新Apache Sling Authenticator註冊的需求。 持續保留任何暫時性修改時就會追蹤修改，因此需要`javax.jcr.Session.save()`呼叫才能生效。

`granite:loginPath`屬性也是如此。 只有由驗證要求相關的mixin類型定義時，才會接受它。 在非結構化JCR節點上添加具有此名稱的剩餘屬性將不會顯示所需的效果，而負責更新OSGi註冊的處理程式將忽略該屬性。

>[!NOTE]
>
>設定登錄路徑屬性是可選的，並且僅當需要身份驗證的樹不能回復為預設或繼承的登錄頁時才需要。 請參閱下方的[登入路徑評估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling Authenticator註冊驗證要求和登錄路徑 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由於此類型的身份驗證需求預計將限於某些運行模式以及內容儲存庫內的一小部分樹，因此，對需求混合類型和登錄路徑屬性的跟蹤是有條件的，並綁定到定義受支援路徑的相應配置（請參閱下面的配置選項）。 因此，只有這些受支援路徑範圍內的更改才會觸發OSGi註冊的更新，在其他地方，mixin類型和屬性都將被忽略。

預設AEM設定現在可允許在製作執行模式中設定mixin，但只讓mixin在復寫至發佈執行個體時生效，以利用此設定。 如需Sling如何強制執行驗證要求的詳細資訊，請參閱[本頁面](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)。

在配置的支援路徑中添加`granite:AuthenticationRequired` mixin類型將導致更新負責處理程式的OSGi註冊，該註冊包含具有`sling.auth.requirements`屬性的新的附加條目。 如果給定的驗證要求指定了可選的`granite:loginPath`屬性，則該值將以「 — 」前置詞向驗證器附加註冊，以便從驗證要求中排除。

#### 認證需求的評價與繼承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling驗證需求應透過頁面或節點階層繼承。 繼承和驗證要求評估的詳細資訊（如順序和優先順序）被視為實施詳細資訊，本文不予記錄。

#### 登錄路徑評估 {#evaluation-of-login-path}

驗證時評估登入路徑並重新導向至對應資源的目前是AdobeGranite登入選取器驗證處理常式(`com.day.cq.auth.impl.LoginSelectorHandler`)的實作詳細資料，此處理常式是預設為AEM的Apache Sling AuthenticationHandler。

呼叫`AuthenticationHandler.requestCredentials`時，此處理常式會嘗試判斷要將使用者重新導向的對應登入頁面。 這包括下列步驟：

* 區分過期的密碼以及需要定期登入作為重新導向的原因；
* 若是一般登入，會測試登入路徑是否可依下列順序取得：

   * 從新`com.adobe.granite.auth.requirement.impl.RequirementService`實作的LoginPathProvider,
   * 從舊有已棄用的CUG實作，
   * （如`LoginSelectorHandler`所定義）
   * 最後，依`LoginSelectorHandler`所定義，回復至預設登入頁面。

* 一旦透過上述呼叫取得有效的登入路徑，系統就會將使用者的要求重新導向至該頁面。

本檔案的目標是評估內部`LoginPathProvider`介面公開的登入路徑。 自AEM 6.3起提供的實作如下：

* 登錄路徑的註冊取決於密碼過期和需要定期登錄作為重定向原因之間的區別
* 若是一般登入，會測試登入路徑是否可依下列順序取得：

   * 從由新`com.adobe.granite.auth.requirement.impl.RequirementService`實作的`LoginPathProvider`,
   * 從舊有已棄用的CUG實作，
   * 從以`LoginSelectorHandler`定義的「登入頁面對應」，
   * 最後，依`LoginSelectorHandler`所定義，回復至預設登入頁面。

* 一旦透過上述呼叫取得有效的登入路徑，系統就會將使用者的要求重新導向至該頁面。

Granite中新驗證需求支援實作的`LoginPathProvider`會公開`granite:loginPath`屬性所定義的登入路徑，而這些屬性又由如上所述的mixin類型所定義。 保存登錄路徑的資源路徑和屬性值本身的映射被保存在記憶體中，並將被評估以為層次中的其他節點尋找合適的登錄路徑。

>[!NOTE]
>
>僅對與配置的支援路徑中的資源關聯的請求執行評估。 對於任何其他請求，將評估判斷登入路徑的替代方式。

#### 最佳作法 {#best-practices-1}

定義驗證需求時，應考量下列最佳實務：

* 避免嵌套身份驗證要求：在樹的開頭放置單個驗證需求標籤應足夠，並繼承至目標節點定義的整個子樹。 該樹狀結構中的其他驗證需求應視為備援，且在評估Apache Sling中的驗證需求時，可能會導致效能問題。 通過將授權和認證相關的CUG區域分開，可以通過CUG或其他類型的策略來限制讀取訪問，同時強制對整個樹進行認證。
* 模型儲存庫內容，使得驗證要求適用於整個樹，而不需要再次排除嵌套的子樹。
* 要避免指定，然後註冊冗餘登錄路徑：

   * 依賴繼承並避免定義巢狀登入路徑，
   * 請勿將選用的登入路徑設定為與預設值或繼承值相對應的值，
   * 應用程式開發人員應識別應在與`LoginSelectorHandler`關聯的全域登入路徑配置（預設和映射）中配置哪些登入路徑。

## 在儲存庫中的表示 {#representation-in-the-repository}

### CUG在儲存庫中的策略表示 {#cug-policy-representation-in-the-repository}

Oak檔案涵蓋新CUG原則在存放庫內容中的反映方式。 如需詳細資訊，請參閱[本頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 儲存庫中的驗證需求 {#authentication-requirement-in-the-repository}

在存放庫內容中反映了對單獨驗證需求的需求，其中目標節點處放置了專用的混合節點類型。 mixin類型定義了可選屬性，用於為目標節點定義的樹指定專用的登錄頁。

與登錄路徑相關聯的頁面可以位於該樹內或外部。 它將從驗證需求中排除。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份驗證要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR訪問控制管理API管理用於限制CUG讀訪問的新類型的訪問控制策略，並遵循[JCR 2.0規範](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)中描述的機制。

#### 設定新的CUG策略 {#set-a-new-cug-policy}

在以前沒有設定CUG的節點應用新CUG策略的代碼。 請注意，`getApplicablePolicies`只會傳回之前未設定的新原則。 最後，政策需要回復，而且需要持續進行變更。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 編輯現有的CUG策略 {#edit-an-existing-cug-policy}

編輯現有CUG策略需要執行以下步驟。 請注意，修改後的策略需要回復，並且需要使用`javax.jcr.Session.save()`保留更改。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 檢索有效的CUG策略 {#retrieve-effective-cug-policies}

JCR訪問控制管理定義了檢索在給定路徑生效的策略的最佳工作方法。 由於評估CUG策略是有條件的，並且取決於要啟用的相應配置，呼叫`getEffectivePolicies`是驗證給定CUG策略是否在給定安裝中生效的一種方便方法。

>[!NOTE]
>
>請注意`getEffectivePolicies`與後續程式碼範例之間的差異，該範例會向上游走階層，以尋找指定路徑是否已屬於現有CUG的一部分。

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 檢索繼承的CUG策略 {#retrieve-inherited-cug-policies}

無論CUG是否生效，都會在指定路徑上找到已定義的所有巢狀CUG。 如需詳細資訊，請參閱[設定選項](/help/sites-administering/closed-user-groups.md#configuration-options)區段。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### 按主管管理CUG策略 {#managing-cug-policies-by-pincipal}

`JackrabbitAccessControlManager`定義的允許按主體編輯訪問控制策略的擴展沒有通過CUG訪問控制管理來實現，因為根據定義，CUG策略始終影響所有主體：與`PrincipalSetPolicy`一起列出的主體被授予讀取訪問權限，而所有其他主體將被阻止讀取目標節點定義的樹中的內容。

相應的方法始終返回空策略陣列，但不會引發異常。

### 管理驗證需求 {#managing-the-authentication-requirement}

通過改變目標節點的有效節點類型來實現新認證需求的建立、修改或移除。 然後，可使用一般JCR API寫入選用的登入路徑屬性。

>[!NOTE]
>
>如果已設定`RequirementHandler`且目標包含在受支援路徑所定義的樹狀結構中，則上述對指定目標節點的修改僅會反映在Apache Sling Authenticator上（請參閱設定選項一節）。
>
>有關詳細資訊，請參閱[分配混合節點類型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配混合節點類型)和[添加節點和設定屬性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加節點和設定屬性)

#### 新增驗證需求 {#adding-a-new-auth-requirement}

建立新驗證需求的步驟如下所述。 請注意，如果`RequirementHandler`已針對包含目標節點的樹狀結構進行配置，則此需求將僅向Apache Sling Authenticator註冊。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登入路徑新增驗證需求 {#add-a-new-auth-requirement-with-login-path}

建立新驗證需求的步驟，包括登入路徑。 請注意，如果`RequirementHandler`已針對包含目標節點的樹狀結構進行設定，則登入路徑的需求和排除項目僅會向Apache Sling Authenticator註冊。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改現有登入路徑 {#modify-an-existing-login-path}

變更現有登入路徑的步驟於下文詳細說明。 只有為包含目標節點的樹狀結構配置了`RequirementHandler`，才會向Apache Sling Authenticator註冊修改。 先前的登錄路徑值將從註冊中刪除。 與目標節點相關聯的驗證要求不會受此修改影響。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 移除現有登入路徑 {#remove-an-existing-login-path}

移除現有登入路徑的步驟。 如果`RequirementHandler`已針對包含目標節點的樹狀結構進行配置，則登入路徑項目將僅從Apache Sling Authenticator中解除註冊。 與目標節點相關聯的驗證需求不受影響。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

或者，您可以使用下列方法來達到相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 移除驗證需求 {#remove-an-auth-requirement}

移除現有驗證需求的步驟。 如果`RequirementHandler`已針對包含目標節點的樹狀結構進行配置，則只能從Apache Sling Authenticator中取消註冊此要求。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 檢索有效驗證要求 {#retrieve-effective-auth-requirements}

沒有專用的公用API可讀取向Apache Sling Authenticator註冊的所有有效驗證需求。 但是，該清單在系統控制台的「**Authentication Requirement Configuration**」部分下`https://<serveraddress>:<serverport>/system/console/slingauth`公開。

下圖顯示AEM發佈例項的驗證需求及示範內容。 社群頁面的醒目提示路徑說明本檔案所述實施所新增的需求如何反映在Apache Sling Authenticator中。

>[!NOTE]
>
>在此示例中，未設定可選登錄路徑屬性。 因此，沒有向驗證器註冊第二條。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 檢索有效登錄路徑 {#retrieve-the-effective-login-path}

目前沒有公用API可擷取要求驗證的資源匿名存取時生效的登入路徑。 如需如何擷取登入路徑的實作詳細資訊，請參閱登入路徑評估一節。

但請注意，除了使用此功能定義的登入路徑外，還有其他方法可指定重新導向至登入，這在設計內容模型和指定AEM安裝的驗證需求時應納入考量。

#### 檢索繼承的驗證要求 {#retrieve-the-inherited-auth-requirement}

如同登入路徑，沒有公用API可擷取內容中定義的繼承驗證需求。 以下示例說明如何列出已使用指定層次結構定義的所有身份驗證要求（無論這些要求是否有效）。 有關詳細資訊，請參閱[配置選項](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建議您同時依賴繼承機制來滿足驗證需求和登入路徑，並避免建立巢狀驗證需求。
>
>有關詳細資訊，請參閱[驗證要求的評估和繼承](#evaluation-and-inheritance-of-the-authentication-requirement)、[登錄路徑評估](#evaluation-of-login-path)和[最佳實踐](#best-practices)。

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### 結合CUG策略和身份驗證要求 {#combining-cug-policies-and-the-authentication-requirement}

下表列出了AEM實例中CUG策略的有效組合和驗證要求，該實例通過配置啟用了兩個模組。

| **需要驗證** | **登入路徑** | **受限讀取** | **預期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 只有在有效權限評估授予訪問權限時，給定用戶才能查看標籤為CUG策略的子樹。 未驗證的使用者會重新導向至指定的登入頁面。 |
| 是 | 否 | 是 | 只有在有效權限評估授予訪問權限時，給定用戶才能查看標籤為CUG策略的子樹。 未驗證的使用者會重新導向至繼承的預設登入頁面。 |
| 是 | 是 | 否 | 未驗證的使用者會重新導向至指定的登入頁面。 是否允許它查看標有驗證要求的樹取決於該子樹中包含的各個項目的有效權限。 沒有專用的CUG限制讀取訪問。 |
| 是 | 否 | 否 | 未驗證的使用者會重新導向至繼承的預設登入頁面。 是否允許它查看標有驗證要求的樹取決於該子樹中包含的各個項目的有效權限。 沒有專用的CUG限制讀取訪問。 |
| 否 | 否 | 是 | 只有在有效權限評估授予訪問權限時，給定的已驗證或未驗證用戶才能查看標籤為CUG策略的子樹。 未驗證的使用者會受到同等對待，不會被重新導向至登入。 |

>[!NOTE]
>
>上方未列出「驗證需求」=「否」和「登入路徑」=「是」的組合，因為「登入路徑」是與驗證需求相關聯的選用屬性。 指定具有該名稱的JCR屬性而不添加定義的mixin類型將無效，並且將被相應的處理程式忽略。

## OSGi元件和配置 {#osgi-components-and-configuration}

本節概述OSGi元件，以及新CUG實作引入的個別設定選項。

另請參閱CUG對應檔案，以取得舊實作與新實作之間組態選項的完整對應。

### 授權：設定與設定 {#authorization-setup-and-configuration}

新的授權相關部件包含在&#x200B;**Oak CUG授權**&#x200B;套件組合(`org.apache.jackrabbit.oak-authorization-cug`)中，此套件是AEM預設安裝的一部分。 該捆綁定義了一個分離的授權模型，該授權模型旨在作為管理讀取訪問的一種附加方法進行部署。

#### 設定CUG授權 {#setting-up-cug-authorization}

[相關Apache檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)中詳細說明了設定CUG授權。 依預設，AEM在所有執行模式中都部署了CUG授權。 該逐步指令還可用於在那些需要不同授權設定的安裝中禁用CUG授權。

#### 設定反向連結篩選 {#configuring-the-referrer-filter}

您也需要設定[Sling反向連結篩選器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) ，包含所有可用來存取AEM的主機名稱；例如，透過CDN、負載平衡器等。

如果未設定反向連結篩選器，則當使用者嘗試登入CUG網站時，會出現類似下列的錯誤：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi元件的特性 {#characteristics-of-osgi-components}

引入下列兩個OSGi元件，以定義驗證需求並指定專用的登入路徑：

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>Apache Jackrabbit Oak CUG設定</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>專用於設定和評估CUG權限的授權配置。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另請參閱下方的<a href="#configuration-options">配置選項</a>。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>Apache Jackrabbit Oak CUG排除清單</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>允許從CUG評估中排除具有配置名稱的主體。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另請參閱下方的設定選項一節。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

#### 配置選項 {#configuration-options}

關鍵配置選項是：

* `cugSupportedPaths`:指定可能包含CUG的子樹。未設定預設值
* `cugEnabled`:配置選項，以啟用當前CUG策略的權限評估。

如需與CUG授權模組相關聯的可用設定選項，請參閱[Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)以取得詳細說明。

#### 將主體排除在CUG評估之外 {#excluding-principals-from-cug-evaluation}

在前一實施中，個人負責人免予進行CUG評估。 新的CUG授權透過名為CugExclude的專用介面涵蓋此資訊。 Apache Jackrabbit Oak 1.4隨附預設實作，排除固定的承擔者集合，以及可設定個別承擔者名稱的延伸實作。 後者是在AEM發佈執行個體中設定。

自AEM 6.3以來的預設值可防止下列主體受到CUG原則的影響：

* 管理主體（管理員用戶、管理員組）
* 服務用戶主體
* 儲存系統內部主體

如需詳細資訊，請參閱下方[自AEM 6.3](#default-configuration-since-aem)以來的預設設定一節中的表格。

「管理員」群組的排除可在系統主控台中的&#x200B;**Apache Jackrabbit Oak CUG Exclude List**&#x200B;設定區段進行變更或展開。

或者，您也可以提供並部署CugExclude介面的自訂實作，以因應特殊需求調整排除的主體集合。 如需詳細資訊和範例實作，請參閱[CUG增效性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)上的檔案。

### 驗證：設定與設定 {#authentication-setup-and-configuration}

新的身份驗證相關部件包含在&#x200B;**AdobeGranite身份驗證處理程式**&#x200B;捆綁包中（`com.adobe.granite.auth.authhandler`版本5.6.48）。 此套件組合是AEM預設安裝的一部分。

為了為已棄用的CUG支援設定驗證需求替換，在指定的AEM安裝中，某些OSGi元件必須存在且處於活動狀態。 如需更多詳細資訊，請參閱下方的&#x200B;**OSGi元件的特性**。

>[!NOTE]
>
>由於RequirementHandler的強制配置選項，只有通過指定一組受支援的路徑來啟用該功能時，驗證相關部件才會處於活動狀態。 在標準AEM安裝中，此功能會在製作執行模式中停用，並在發佈執行模式中針對/content啟用。

**OSGi元件的特性**

導入下列2個OSGi元件，以定義驗證需求並指定專用的登入路徑：

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>-</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>針對驗證需求的專用OSGi服務，該服務會針對影響驗證需求的內容變更（透過<code>granite:AuthenticationRequirement</code> mixin類型）向觀察者註冊，而使用的登入路徑則會向<code>LoginSelectorHandler</code>公開。 </td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>-</td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 標籤 | AdobeGranite驗證需求和登入路徑處理常式 |
|---|---|
| 說明 | `RequirementHandler` 更新Apache Sling驗證需求和相關登入路徑之對應排除的實作。 |
| 組態屬性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | 不適用 |

#### 配置選項 {#configuration-options-1}

CUG重寫的身份驗證相關部分僅附帶與AdobeGranite身份驗證要求和登錄路徑處理程式關聯的單個配置選項：

**&quot;驗證要求和登錄路徑處理程式&quot;**

<table>
 <tbody>
  <tr>
   <td>屬性</td>
   <td>類型</td>
   <td>預設值</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><p>標籤=支援的路徑</p> <p>名稱= 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>此處理常式將接受驗證要求的路徑。 如果您想要將<code>granite:AuthenticationRequirement</code> mixin類型新增至節點，但未強制執行（例如在製作執行個體上），請保留此設定未設定。 如果缺少，則禁用該功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3起的預設設定 {#default-configuration-since-aem}

依預設，新安裝的AEM會將新實施用於CUG功能的授權和驗證相關部分。 舊版實作「AdobeGranite封閉使用者群組(CUG)支援」已淘汰，並預設會在所有AEM安裝中停用。 將改為啟用新實施，如下所示：

### 製作例項 {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **說明** |
|---|---|
| 支援的路徑`/content` | 已啟用CUGpolicies的訪問控制管理。 |
| CUG評估已啟用FALSE | 禁用權限評估。 CUG政策沒有生效。 |
| 等級 | 200 | 請參閱Oak檔案。 |

>[!NOTE]
>
>預設製作執行個體上沒有&#x200B;**Apache Jackrabbit Oak CUG Exclude List**&#x200B;和&#x200B;**AdobeGranite驗證需求和登入路徑處理常式**&#x200B;的設定。

### 發佈例項 {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **說明** |
|---|---|
| 支援的路徑`/content` | CUG策略的訪問控制管理在配置的路徑下啟用。 |
| 啟用CUG評估TRUE | 權限評估會在已設定的路徑下方啟用。 CUG策略對`Session.save()`生效。 |
| 等級 | 200 | 請參閱Oak檔案。 |

| **&quot;Apache Jackrabbit Oak CUG Exclude List&quot;** | **說明** |
|---|---|
| 主體名稱管理員 | 不包括管理員主體（CUG評估）。 |

| **「AdobeGranite驗證需求和登入路徑處理常式」** | **說明** |
|---|---|
| 支援的路徑`/content` | 儲存庫中通過`granite:AuthenticationRequired` mixin類型定義的身份驗證要求在`Session.save()`上生效，在`/content`下。 Sling Authenticator會更新。 在支援的路徑之外新增mixin類型會遭忽略。 |

## 禁用CUG授權和身份驗證要求 {#disabling-cug-authorization-and-authentication-requirement}

如果給定的安裝沒有使用CUG或使用不同的方法來驗證和授權，則可完全禁用新實施。

### 禁用CUG授權 {#disable-cug-authorization}

有關如何從複合授權設定中刪除CUG授權模型的詳細資訊，請參閱[CUG可插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)文檔。

### 禁用身份驗證要求 {#disable-the-authentication-requirement}

為了禁用`granite.auth.authhandler`模組提供的對驗證要求的支援，足夠刪除與&#x200B;**AdobeGranite驗證要求和登錄路徑處理程式**&#x200B;關聯的配置。

>[!NOTE]
>
>但是，請注意，刪除配置將不會取消註銷混合類型，該類型仍適用於未生效的節點。

## 與其他模組的互動 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

為了反映CUG授權模型所使用的新類型存取控制政策，已擴充Apache Jackrabbit所定義的API。 由於`jackrabbit-api`模組的2.11.0版定義了一個名為`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新介面，該介面從`javax.jcr.security.AccessControlPolicy`擴展。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的匯入機制已調整，以處理`PrincipalSetPolicy`類型的存取控制政策。

### Apache Sling Content Distribution {#apache-sling-content-distribution}

請參閱上述[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)一節。

### AdobeGranite復寫 {#adobe-granite-replication}

復寫模組已稍作調整，以便能夠在不同AEM執行個體之間複製CUG原則：

* `DurboImportConfiguration.isImportAcl()` 按字面方式解釋，並且只會影響訪問控制策略的實施  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 只會遵守此配置，以使用真ACL
* CUG授權模型建立的`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`實例等其他策略將始終被複製，配置選項`DurboImportConfiguration.isImportAcl`()將被忽略。

複製CUG策略有一個限制。 如果在刪除給定的CUG策略時未刪除相應的混合節點類型`rep:CugMixin,`，則複製時不會反映刪除。 此問題已通過始終在刪除策略時刪除mixin來解決。 不過，如果手動新增混合類型，則可能會顯示限制。

### AdobeGranite驗證處理常式 {#adobe-granite-authentication-handler}

`com.adobe.granite.auth.authhandler`套件組合隨附的驗證處理程式&#x200B;**AdobeGranite HTTP標題驗證處理程式**&#x200B;包含對相同模組所定義`CugSupport`介面的引用。 它用於在某些情況下計算「領域」，並回退到配置有處理程式的領域。

這已調整，讓`CugSupport`的參考成為選用項目，以確保當指定設定決定重新啟用已棄用的實施時，回溯相容性達到最大。 使用實作的安裝將不再取得從CUG實作擷取的領域，而一律會依照&#x200B;**AdobeGranite HTTP Header Authentication Handler**&#x200B;的定義來顯示領域。

>[!NOTE]
>
>預設情況下，**AdobeGranite HTTP標題驗證處理常式**&#x200B;僅在發佈運行模式下配置，並啟用「禁用登錄頁」(`auth.http.nologin`)選項。

### AEM LiveCopy {#aem-livecopy}

配置CUG與LiveCopy結合時，會添加一個額外節點和一個額外屬性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

這兩個元素都會在`cq:Page`下建立。 使用當前設計時，MSM僅處理`cq:PageContent`(`jcr:content`)節點下的節點和屬性。

因此，CUG組無法從Blueprint轉出到Live Copy。 設定Live Copy時，請針對此進行規劃。

## 新CUG實作的變更 {#changes-with-the-new-cug-implementation}

本節旨在概述對CUG功能所做的變更，並比較舊實作和新實作。 它列出了影響CUG支援配置方式的更改，並描述了在儲存庫內容中管理CUG的方式和方式。

### CUG設定和配置方面的差異 {#differences-in-cug-setup-and-configuration}

已棄用的OSGi元件&#x200B;**AdobeGranite封閉用戶組(CUG)支援**(`com.day.cq.auth.impl.cug.CugSupportImpl`)已被新元件替換，以便能夠分別處理前CUG功能的授權和驗證相關部分。

## 管理儲存庫內容中CUG的差異 {#differences-in-managing-cugs-in-the-repository-content}

以下各節將從實作和安全性觀點，說明舊實作與新實作之間的差異。 雖然新實作旨在提供相同的功能，但在使用新CUG時，有些細微的變更非常重要。

### 授權方面的差異 {#differences-with-regards-to-authorization}

從授權角度來看，主要差異概述於下表：

**CUG專用的存取控制內容**

在舊實施中，預設授權模型用於在發佈時操縱訪問控制清單策略，由CUG授權的設定替換任何現有ACE。 觸發此動作的方式為撰寫會在發佈時解譯的一般、剩餘JCR屬性。

在新實施中，預設授權模型的訪問控制設定不受正在建立、修改或刪除的任何CUG的影響。 而是應用名為`PrincipalSetPolicy`的新策略類型作為對目標節點的附加訪問控制內容。 此附加策略將作為目標節點的子節點定位，如果存在，則為預設策略節點的同級。

**在訪問控制管理中編輯CUG策略**

從剩餘JCR屬性移至專用的存取控制原則，會影響建立或修改CUG功能授權部分所需的權限。 由於這被視為訪問控制內容的修改，因此它需要`jcr:readAccessControl`和`jcr:modifyAccessControl`權限才能寫入儲存庫。 因此，只有有權修改頁面存取控制內容的內容作者才能設定或修改此內容。 這與舊版實作不同，舊版實作中寫入一般JCR屬性的能力已足夠，導致權限提升。

**由策略定義的目標節點**

CUG策略應在JCR節點建立，該節點定義要受限制讀取訪問限制的子樹。 這可能是AEM頁面，以防CUG影響整個樹。

請注意，將CUG原則僅放在指定頁面下方的jcr:content節點，只會限制對指定頁面內容s.str的存取，但不會對任何同層頁面或子頁面生效。 這可能是有效的使用案例，而且可以使用允許套用微調存取內容內容的存放庫編輯器來達成。 不過，它會與前一個實施作比較，前者將cq:cugEnabled屬性放置在jcr:content節點上，會在內部重新對應至頁面節點。 不再執行此對應。

**使用CUG策略進行權限評估**

從舊的CUG支援移至其他授權模型，會變更評估有效讀取權限的方式。 如[Jackrabbit檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)所述，只有在Oak存放庫中所設定模型的權限評估已授予讀取存取權時，才授予可檢視`CUGcontent`的指定主體讀取存取權。

換言之，在評估有效權限時，將同時考慮`CUGPolicy`和預設訪問控制項，並且只有當CUG內容被兩種策略授予時，才授予對CUG內容的讀訪問權。 在預設的AEM發佈安裝中，每個人都有權讀取完整`/content`樹狀結構，CUG原則的效果將與舊實作相同。

**按需評估**

CUG授權模型允許單獨開啟訪問控制管理和權限評估：

* 如果模組有一或多個可建立CUG的支援路徑，則啟用訪問控制管理
* 只有在已另外檢查選項&#x200B;**CUG Evaluation Enabled**&#x200B;時，才啟用權限評估。

在新的AEM預設CUG策略設定評估中，它只會以「發佈」執行模式啟用。 如需詳細資訊，請參閱自AEM 6.3](#default-configuration-since-aem)以來的[預設設定的詳細資訊。 這可以通過將給定路徑的有效策略與儲存在內容中的策略進行比較來驗證。 只有在啟用CUG的權限評估時，才會顯示有效策略。

如上所述，CUG存取控制原則現在一律會儲存在內容中，但只有在Apache Jackrabbit Oak **CUG Configuration的系統主控台中開啟「**&#x200B;已啟用CUG評估&#x200B;**」時，才會強制評估這些原則產生的有效權限。** 依預設，僅以「發佈」執行模式啟用。

### 與驗證的差異 {#differences-with-regards-to-authentication}

與驗證有關的差異如下。

#### 用於認證需求的專用混合類型 {#dedicated-mixin-type-for-authentication-requirement}

在前一實施中，CUG的授權和驗證方面都由單個JCR屬性(`cq:cugEnabled`)觸發。 就驗證而言，這會導致更新Apache Sling Authenticator實作所儲存的驗證需求清單。 通過使用專用混合類型(`granite:AuthenticationRequired`)標籤目標節點，實現了相同的結果。

#### 用於排除登錄路徑的屬性 {#property-for-excluding-login-path}

mixin類型定義了名為`granite:loginPath`的單個可選屬性，該屬性基本上與`cq:cugLoginPage`屬性相對應。 與先前的實施相反，只有在其聲明節點類型為上述mixin時，登入路徑屬性才會受到尊重。 在未設定mixin類型的情況下添加具有該名稱的屬性將無效，並且不會向驗證器報告登錄路徑的新要求或排除。

#### 身份驗證要求的權限 {#privilege-for-authentication-requirement}

添加或刪除混合類型需要授予`jcr:nodeTypeManagement`權限。 在上一實施中， `jcr:modifyProperties`權限用於編輯剩餘屬性。

就`granite:loginPath`而言，添加、修改或刪除該屬性需要相同的權限。

#### 由Mixin類型定義的目標節點 {#target-node-defined-by-mixin-type}

驗證需求應建立在JCR節點，定義要受強制登入約束的子樹。 如果CUG預計會影響整個樹狀結構，則這可能是AEM頁面，而新實作的UI隨後會在頁面節點上新增驗證需求mixin類型。

將CUG原則僅放在指定頁面下方的jcr:content節點，只會限制對內容的存取，但不會影響頁面節點本身或任何子頁面。

這可能是有效的案例，而且使用允許將mixin放置在任何節點的儲存庫編輯器是可能的。 不過，此行為與前一個實作有所差異，即將cq:cugEnabled或cq:cugLoginPage屬性放置於jcr:content節點上，最終會在內部重新對應至頁面節點。 不再執行此對應。

#### 配置的支援路徑 {#configured-supported-paths}

`granite:AuthenticationRequired` mixin類型和granite:loginPath屬性僅在&#x200B;******AdobeGranite身份驗證要求和登錄路徑處理程式**&#x200B;中的受支援路徑配置選項集所定義的範圍內受允許。 如果未指定路徑，則完全禁用身份驗證要求功能。 在此情況下，mixin類型或屬性在添加到給定JCR節點或設定該節點時生效。

### JCR內容、OSGi服務和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下檔案提供舊實作與新實作之間OSGi服務、設定和存放庫內容的完整對應。

自AEM 6.3以來的CUG對應

[取得檔案](assets/cug-mapping.pdf)

## 升級CUG {#upgrade-cug}

### 使用已棄用的CUG的現有安裝 {#existing-installations-using-the-deprecated-cug}

舊版CUG支援實作已淘汰，並將在未來版本中移除。 從AEM 6.3以前的版本升級時，建議改用新實作。

對於升級的AEM安裝，請務必確保僅啟用一個CUG實作。 新的和舊的、過時的CUG支援的組合不會經過測試，並且可能會導致不適當的行為：

* Sling驗證器中與驗證需求的衝突
* 當與舊CUG關聯的ACL設定與新CUG策略衝突時，拒絕讀取訪問。

### 移轉現有CUG內容 {#migrating-existing-cug-content}

Adobe提供移轉至新CUG實作的工具。 若要使用，請執行下列步驟：

1. 前往`https://<serveraddress>:<serverport>/system/console/cug-migration`以存取工具。
1. 輸入要檢查CUG的根路徑，然後按&#x200B;**執行乾式運行**&#x200B;按鈕。 這會掃描所選位置中符合轉換資格的CUG。
1. 檢閱結果後，按&#x200B;**執行移轉**&#x200B;按鈕以移轉至新實作。

>[!NOTE]
>
>如果您遇到問題，可以在`com.day.cq.auth.impl.cug`的&#x200B;**DEBUG**&#x200B;層級上設定特定記錄器，以取得移轉工具的輸出。 有關如何執行此操作的詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)。
