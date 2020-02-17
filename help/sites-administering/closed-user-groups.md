---
title: AEM中的已關閉使用者群組
seo-title: AEM中的已關閉使用者群組
description: 瞭解AEM中的「關閉使用者群組」。
seo-description: 瞭解AEM中的「關閉使用者群組」。
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475

---


# AEM中的已關閉使用者群組{#closed-user-groups-in-aem}

## 簡介 {#introduction}

自從AEM 6.3起，就推出新的「封閉使用者群組」實作，旨在解決現有實作中的效能、延展性與安全性問題。

>[!NOTE]
>
>為了簡單起見，本檔案將使用CUG縮寫。

新實作的目標是視需要涵蓋現有功能，同時解決舊版的問題和設計限制。 其結果為具有以下特點的新CUG設計：

* 可單獨使用或組合使用的驗證和授權要素明確分開；
* 專用授權模型，在配置的CUG樹上反映受限讀取訪問，而不干擾其他訪問控制設定和權限要求；
* 在編寫實例時通常需要的受限讀訪問權限控制設定和發佈時通常需要的權限評估之間分離；
* 編輯受限讀取存取權，而無權限竊取；
* 專用節點類型擴展來標籤認證要求；
* 與驗證要求相關聯的可選登錄路徑。

### 新的自訂使用者群組實作 {#the-new-custom-user-group-implementation}

在AEM中稱為CUG的CUG包含下列步驟：

* 限制對需要保護的樹狀結構的讀取訪問權限，並且只允許讀取帶有給定CUG實例或完全排除在CUG評估之外的承擔者。 這稱為授 **權元** 素。
* 在指定樹上強制驗證，並可選擇指定該樹的專用登錄頁，該登錄頁隨後被排除。 這稱為驗 **證元** 素。

新的實施旨在在驗證和授權元素之間划出一條線。 自AEM 6.3起，您就可以限制讀取存取，而不需明確新增驗證要求。 例如，如果給定實例完全需要驗證，或者給定樹已駐留在需要驗證的子樹中。

同樣地，給定的樹可以用驗證要求標籤，而無需更改有效的權限設定。 組合和結果列在「組合CUG策 [略」和「驗證要求」部分](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 。

## 概覽 {#overview}

### 授權：限制讀取訪問 {#authorization-restricting-read-access}

CUG的主要功能是限制內容儲存庫中指定樹上除選定承擔者之外的所有人的讀取訪問。 新實施不會即時控制預設存取控制內容，而是採用不同的方法，定義代表CUG的專用存取控制策略類型。

#### CUG的訪問控制策略 {#access-control-policy-for-cug}

這種新型策略具有以下特點：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定義）類型的存取控制政策；
* PrincipalSetPolicy授予可修改的承擔者集的權限；
* 授予的權限和策略的範圍是實施詳細資訊。

用於表示CUG的PrincipalSetPolicy的實施還定義了：

* CUG策略僅授予對常規JCR項的讀訪問權限（例如，排除訪問控制內容）;
* 範圍由CUG策略的接入控制節點定義；
* CUG策略可以嵌套，嵌套CUG啟動新CUG而不繼承「父」CUG的主集；
* 如果啟用了評估，則策略的效果將繼承到整個子樹，並下移到下一個嵌套的CUG。

這些CUG原則會透過名為oak-authorization-cug的個別授權模組部署至AEM例項。 本模組具有自己的訪問控制管理和權限評估功能。 換言之，預設的AEM設定會提供結合多種授權機制的Oak內容存放庫設定。 如需詳細資訊，請 [參閱Apache Oak檔案上的本頁](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

在此複合設定中，新的CUG不會取代附加至目標節點的現有存取控制內容，但是其設計為增補內容，稍後也可移除，而不會影響原始的存取控制，在AEM中預設會是存取控制清單。

與以前的實施相比，新的CUG策略始終被識別和視為訪問控制內容。 這表示它們是使用JCR存取控制管理API來建立和編輯的。 如需詳細資訊，請參閱「管 [理CUG原則」一節](#managing-cug-policies) 。

#### CUG策略的權限評估 {#permission-evaluation-of-cug-policies}

除了CUG的專用訪問控制管理外，新的授權模型允許有條件地啟用其策略的權限評估。 這允許在測試環境中設定CUG策略，並且僅允許在複製到生產環境後評估有效權限。

CUG原則的權限評估以及與預設或任何額外授權模型的互動遵循Apache Jackrabbit Oak中針對多種授權機制所設計的模式：只有在所有模型都授與存取權時，才會授與特定的權限集。 如需詳 [細資訊](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) ，請參閱本頁。

與用於處理和評估CUG策略的授權模型相關的權限評估適用以下特徵：

* 它僅處理常規節點和屬性的讀取權限，但不處理讀取訪問控制內容
* 它不處理修改受保護JCR內容（訪問控制、節點類型資訊、版本修訂、鎖定或用戶管理等）所需的寫權限或任何類型的權限；這些權限不受CUG原則影響，且不會由相關的授權模型評估。 是否授予這些權限取決於安全設定中配置的其他模型。

單一CUG策略對權限評估的影響可總結如下：

* 除了包含策略中列出的已排除承擔者或承擔者的主體外，所有人都拒絕讀取權限；
* 策略對包含策略及其屬性的訪問控制節點生效；
* 這種效果還會沿著層次結構繼承，即由訪問控制節點定義的項目樹；
* 但是，它不影響接入控制節點的兄弟和祖先；
* 給定CUG的繼承將停止在嵌套CUG處。

#### Best Practices {#best-practices}

在通過CUG定義受限讀訪問權限時，應考慮以下最佳做法：

* 有意識地決定您對CUG的需求是限制讀取存取還是驗證要求。 如果是後者，或如果需要兩者，請參閱最佳實務一節，以取得有關驗證要求的詳細資訊
* 為需要保護的資料或內容建立威脅模型，以識別威脅界限並清楚瞭解資料的敏感性以及與授權存取相關的角色
* 為儲存庫內容和CUG建模，同時牢記與授權相關的一般方面和最佳做法：

   * 請記住，只有在給定的CUG和設定授權中部署的其他模組評估允許給定主體讀取給定儲存庫項目時，才授予讀取權限
   * 避免建立冗餘CUG，其中讀取訪問已受到其他授權模組的限制
   * 過度需要巢狀CUG可能會反白顯示內容設計中的問題
   * 對CUG的過度需求（例如，在每個頁面上）可能表示需要自訂授權模型，這可能更符合應用程式和手邊內容的特定安全性需求。

* 將CUG策略支援的路徑限制在儲存庫中的幾個樹中，以便獲得最佳效能。 例如，僅允許以AEM 6.3以來的預設值形式出貨的/content節點下方的CUG。
* CUG策略的設計目的是授予對一小組承擔者的讀取訪問權限。 大量原則的需要可能會突出內容或應用程式設計中的問題，應該重新考慮。

### 驗證：定義驗證要求 {#authentication-defining-the-auth-requirement}

CUG功能的驗證相關部分允許標籤需要驗證的樹並可選地指定專用登錄頁。 根據先前版本，新實現允許在內容儲存庫中標籤需要驗證的樹，並有條件地允許與負責最終實施該要求並重定向到登 `Sling org.apache.sling.api.auth.Authenticator`錄資源的負責者同步。

這些要求是透過提供註冊屬性的OSGi服務向驗證者 `sling.auth.requirements` 註冊。 然後，這些屬性會用來動態擴充驗證需求。 如需詳細資訊，請參閱 [Sling檔案](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用專用混合類型定義認證要求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

出於安全原因，新實作會以名為的專用混音類型取代剩餘JCR屬性的使用 `granite:AuthenticationRequired`，該類型為登入路徑定義單一可選屬性類型STRING `granite:loginPath`。 只有與此混音類型相關的內容變更，才能更新Apache Sling Authenticator註冊的需求。 在持續進行任何暫時修改時，會追蹤這些修改，因此需 `javax.jcr.Session.save()` 要呼叫生效。

這同樣適用於屬 `granite:loginPath` 性。 只有當它由驗證要求相關混音類型定義時，才會受到尊重。 在非結構化JCR節點上添加具有此名稱的剩餘屬性將不顯示所需的效果，而負責更新OSGi註冊的處理程式將忽略該屬性。

>[!NOTE]
>
>設定登錄路徑屬性是可選的，僅當需要驗證的樹無法返回預設值或繼承的登錄頁時才需要。 請參閱 [下方的登入路徑評估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 。

#### 使用Sling Authenticator註冊驗證要求和登入路徑 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由於此類型的驗證需求預計會限制在某些執行模式和內容儲存庫中的樹的一小部分，因此追蹤需求混合類型和登入路徑屬性是有條件的，並且會系結至定義支援路徑的對應設定（請參閱下方的設定選項）。 因此，只有這些受支援路徑範圍內的變更才會觸發OSGi註冊的更新，而其他地方的mixin類型和屬性都將被忽略。

預設的AEM設定現在允許在作者執行模式中設定mixin，以利用此設定，但只會在複製至發佈例項時生效。 請參 [閱本頁](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) ，以取得Sling如何強制執行驗證要求的詳細資訊。

在已配置 `granite:AuthenticationRequired` 的受支援路徑中添加混合類型將導致更新負責處理程式的OSGi註冊，該註冊包含一個包含屬性的新的附加條 `sling.auth.requirements` 目。 如果給定的驗證要求指定了可選屬 `granite:loginPath` 性，則該值會以「-」前置詞向驗證方另外註冊，以便排除在驗證要求之外。

#### 認證需求的評估與繼承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling驗證需求預期會透過頁面或節點階層繼承。 對於繼承和驗證要求（如順序和優先順序）的評估的詳細資訊，本文將視為實施細節，不予記錄。

#### 登錄路徑評估 {#evaluation-of-login-path}

驗證時，登入路徑的評估並重新導向至對應資源，目前是Adobe Granite Login Selector Authentication Handler( `com.day.cq.auth.impl.LoginSelectorHandler`)的實作詳細資料，此處是預設設定有AEM的Apache Sling AuthenticationHandler。

呼叫此處 `AuthenticationHandler.requestCredentials` 理常式時，會嘗試判斷將使用者重新導向的對應登入頁面。 這包括下列步驟：

* 區分過期密碼和需要定期登入以做為重新導向的原因；
* 若是定期登入，測試是否可依下列順序取得登入路徑：

   * 從LoginPathProvider中建置 `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * 從舊有、已過時的CUG實作，
   * 從「登入頁面對應」中，以 `LoginSelectorHandler`「
   * 最後，依使用所定義的「預設登入頁面」 `LoginSelectorHandler`。

* 一旦透過上述呼叫取得有效的登入路徑，使用者的要求就會重新導向至該頁面。

本檔案的目標是評估內部介面所公開的登入路 `LoginPathProvider` 徑。 自AEM 6.3起出貨的實作如下：

* 登入路徑的註冊取決於是否區分過期的密碼，以及是否需要定期登入以做為重新導向的原因
* 若是定期登入，測試是否可依下列順序取得登入路徑：

   * 從 `LoginPathProvider``com.adobe.granite.auth.requirement.impl.RequirementService`新的，
   * 從舊有、已過時的CUG實作，
   * 從「登入頁面對應」中， `LoginSelectorHandler`
   * 最後回退至使用定義的預設登入頁面 `LoginSelectorHandler`。

* 一旦透過上述呼叫取得有效的登入路徑，使用者的要求就會重新導向至該頁面。

Granite `LoginPathProvider` 中新的驗證需求支援所實作的登入路徑會依屬性定義 `granite:loginPath` ，而屬性又依上述混合類型定義。 保存登錄路徑的資源路徑與屬性值本身的映射保存在記憶體中，並將被評估以為層次中的其他節點找到合適的登錄路徑。

>[!NOTE]
>
>僅對與配置的支援路徑中的資源相關聯的請求執行評估。 對於任何其他請求，將評估確定登錄路徑的替代方法。

#### Best Practices {#best-practices-1}

在定義驗證要求時，應考慮以下最佳做法：

* 避免巢狀驗證需求：在樹的開頭放置單個驗證要求標籤應該足夠，並繼承到目標節點定義的整個子樹。 該樹狀結構中的其他驗證需求應視為多餘，並可能在評估Apache Sling中的驗證需求時導致效能問題。 通過將授權和認證相關的CUG區分開，可以通過CUG或其他類型的策略限制讀訪問，同時強制對整個樹進行認證。
* 模型儲存庫內容，以便驗證要求適用於整個樹，而無需再次排除嵌套子樹。
* 要避免指定，並隨後註冊冗餘登錄路徑：

   * 依賴繼承並避免定義嵌套登錄路徑，
   * 不要將可選登錄路徑設定為與預設值或繼承值相對應的值，
   * 應用程式開發人員應識別應在與關聯的全域登入路徑組態（預設和對應）中設定哪些登入路徑 `LoginSelectorHandler`。

## 儲存庫中的表示法 {#representation-in-the-repository}

### 儲存庫中的CUG策略表示 {#cug-policy-representation-in-the-repository}

Oak檔案涵蓋新CUG原則在儲存庫內容中的反映方式。 如需詳細資訊，請 [參閱本頁](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 儲存庫中的驗證要求 {#authentication-requirement-in-the-repository}

對單獨驗證要求的需求反映在儲存庫內容中，該儲存庫內容具有位於目標節點上的專用混合節點類型。 混合類型定義了一個可選屬性，用於為目標節點定義的樹指定專用登錄頁。

與登錄路徑關聯的頁面可以位於該樹內或外。 它將被排除在驗證要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份驗證要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR訪問控制管理API管理用於限制CUG讀訪問的新型訪問控制策略，並遵循 [JCR 2.0規範中描述的機制](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)。

#### 設定新的CUG策略 {#set-a-new-cug-policy}

在以前沒有設定CUG的節點上應用新CUG策略的代碼。 請注意， `getApplicablePolicies` 僅會傳回之前未設定的新政策。 最後，政策需要回覆，而且需要持續改變。

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

編輯現有CUG策略時需要執行以下步驟。 請注意，修改後的策略需要回寫，而且需要使用保留更改 `javax.jcr.Session.save()`。

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

JCR訪問控制管理定義了檢索在給定路徑上生效的策略的最佳方法。 由於CUG策略的評估是有條件的，並且取決於要啟用的相應配置，呼叫是驗證給定CUG策略是否在給定安裝中生效的一種方便方法。 `getEffectivePolicies`

>[!NOTE]
>
>請注意與後續程 `getEffectivePolicies` 式碼範例之間的差異，這些範例會逐漸上移階層，以找出特定路徑是否已屬於現有CUG的一部分。

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

尋找在指定路徑上定義的所有巢狀CUG，而不論其是否生效。 如需詳細資訊，請參閱「 [設定選項](/help/sites-administering/closed-user-groups.md#configuration-options) 」一節。

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

#### 按Pincipal管理CUG策略 {#managing-cug-policies-by-pincipal}

允許按承擔者編 `JackrabbitAccessControlManager` 輯訪問控制策略的由定義的擴展不會與CUG訪問控制管理一起實現，因為定義中，CUG策略始終影響所有承擔者：列在其中的 `PrincipalSetPolicy` 承擔者將被授予讀取訪問權限，而所有其他承擔者將無法讀取目標節點定義的樹中的內容。

對應的方法始終返回空策略陣列，但不會拋出異常。

### 管理驗證要求 {#managing-the-authentication-requirement}

通過改變目標節點的有效節點類型來實現新認證需求的建立、修改或移除。 然後，可使用一般JCR API來編寫選用的登入路徑屬性。

>[!NOTE]
>
>如果已設定目標且目標包含在受支援路徑所定義的樹狀結構中，則上述對指定目標節點所做的修改只會反映在 `RequirementHandler` Apache Sling Authenticator上（請參閱「設定選項」一節）。
>
>如需詳細資訊，請參 [閱「指定Mixin節點類型]」(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3指定Mixin節點類型)和「 []新增節點和設定屬性」(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4新增節點和設定屬性)

#### 新增驗證需求 {#adding-a-new-auth-requirement}

建立新驗證要求的步驟如下。 請注意，如果已針對包含目標節點的樹狀結構設定需求， `RequirementHandler` 則此需求只會註冊至Apache Sling Authenticator。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登入路徑新增驗證需求 {#add-a-new-auth-requirement-with-login-path}

建立新驗證要求的步驟，包括登入路徑。 請注意，如果已針對包含目標節點的樹狀結構設定登入路徑的需求和排除， `RequirementHandler` 則僅會向Apache Sling Authenticator註冊。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改現有登錄路徑 {#modify-an-existing-login-path}

變更現有登入路徑的步驟詳述如下。 如果已為包含目標節點的樹狀結構設定修改， `RequirementHandler` 則只會向Apache Sling Authenticator註冊。 先前的登入路徑值將從註冊中移除。 此修改不會影響與目標節點關聯的驗證要求。

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

移除現有登入路徑的步驟。 如果已針對包含目標節點的樹狀結構設定登入路徑項目， `RequirementHandler` 則登入路徑項目只會從Apache Sling Authenticator中取消註冊。 與目標節點關聯的驗證要求不受影響。

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

或者，您可以使用下列方法來達到相同的目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 移除驗證要求 {#remove-an-auth-requirement}

移除現有驗證要求的步驟。 如果已針對包含目標節點的樹狀結構設定此需求， `RequirementHandler` 則只會從Apache Sling Authenticator中取消註冊。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 檢索有效的驗證要求 {#retrieve-effective-auth-requirements}

沒有專用的公用API可讀取所有已註冊Apache Sling Authenticator的有效驗證需求。 不過，此清單會在系統主控台的「驗證 `https://<serveraddress>:<serverport>/system/console/slingauth` 要求設定」**區段下公開**。

下圖顯示AEM發佈例項與示範內容的驗證需求。 社群頁面的反白顯示路徑說明本檔案中所述實施新增的需求如何反映在Apache Sling Authenticator中。

>[!NOTE]
>
>在此示例中，未設定可選登錄路徑屬性。 因此，沒有向驗證者註冊第二項。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 檢索有效登錄路徑 {#retrieve-the-effective-login-path}

目前沒有公用API可擷取在匿名存取需要驗證的資源時生效的登入路徑。 如需如何擷取登入路徑的實作詳細資訊，請參閱登入路徑評估一節。

但請注意，除了使用此功能定義的登入路徑外，還有其他方式可指定重新導向至登入，在設計內容模型和指定AEM安裝的驗證需求時，應考量這些方法。

#### 檢索繼承的驗證要求 {#retrieve-the-inherited-auth-requirement}

與登入路徑一樣，沒有公用API可擷取內容中定義的繼承驗證需求。 下列範例說明如何列出已使用指定階層定義的所有驗證需求，而不論這些需求是否生效。 如需詳細資訊，請參 [閱設定選項](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建議使用繼承機制來滿足驗證要求和登入路徑，並避免建立巢狀驗證要求。
>
>如需詳細資訊，請 [參閱驗證要求的評估與繼承](#evaluation-and-inheritance-of-the-authentication-requirement)、 [登入路徑的評估](#evaluation-of-login-path) 與最 [佳實務](#best-practices)。

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

下表列出CUG原則的有效組合，以及AEM例項中的驗證要求，此AEM例項透過設定同時啟用這兩個模組。

| **需要驗證** | **登入路徑** | **受限讀取存取** | **預期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 只有在有效權限評估授予訪問權限時，給定用戶才能查看用CUG策略標籤的子樹。 未驗證的使用者將重新導向至指定的登入頁面。 |
| 是 | 否 | 是 | 只有在有效權限評估授予訪問權限時，給定用戶才能查看用CUG策略標籤的子樹。 未驗證的使用者將重新導向至繼承的預設登入頁面。 |
| 是 | 是 | 否 | 未驗證的使用者將重新導向至指定的登入頁面。 是否允許它查看使用驗證要求標籤的樹取決於該子樹中包含的單個項目的有效權限。 沒有專用的CUG限制讀訪問。 |
| 是 | 否 | 否 | 未驗證的使用者將重新導向至繼承的預設登入頁面。 是否允許它查看使用驗證要求標籤的樹取決於該子樹中包含的單個項目的有效權限。 沒有專用的CUG限制讀訪問。 |
| 否 | 否 | 是 | 如果有效權限評估授予訪問權限，則給定的已驗證或未驗證用戶只能查看以CUG策略標籤的子樹。 未驗證的使用者會受到同等對待，不會重新導向至登入。 |

>[!NOTE]
>
>上方未列出「驗證要求」=「否」和「登入路徑」=「是」的組合，因為「登入路徑」是與驗證要求相關聯的選用屬性。 指定具有該名稱的JCR屬性而不添加定義的mixin類型將無效，並將被相應的處理程式忽略。

## OSGi元件和配置 {#osgi-components-and-configuration}

本節概述OSGi元件以及新CUG實施中引入的各個配置選項。

另請參閱CUG對應檔案，以取得舊實作與新實作之間設定選項的完整對應。

### 授權：設定與設定 {#authorization-setup-and-configuration}

新的授權相關部件包含在 **Oak CUG Authorization** bundle( `org.apache.jackrabbit.oak-authorization-cug`)中，此套件是AEM預設安裝的一部分。 該包定義了一個單獨的授權模型，該授權模型旨在作為管理讀訪問的一種附加方法進行部署。

#### 設定CUG授權 {#setting-up-cug-authorization}

相關Apache文檔中詳細說明了設定CUG [授權](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)。 依預設，AEM在所有執行模式中都部署了CUG授權。 該逐步指令也可用於在那些需要不同授權設定的安裝中禁用CUG授權。

#### 設定反向連結篩選 {#configuring-the-referrer-filter}

您也需要設定 [Sling Referrer Filter](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) ，其中包含所有可能用來存取AEM的主機名稱；例如，透過CDN、Load Balancer和其他任何方式。

如果未設定反向連結篩選，則當使用者嘗試登入CUG網站時，會看到類似下列的錯誤：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi元件的特性 {#characteristics-of-osgi-components}

已引入下列兩個OSGi元件，以定義驗證需求並指定專用的登入路徑：

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
   <td>專用於設定和評估CUG權限的授權設定。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另請參閱下 <a href="#configuration-options">方的設定</a> 選項。</p> </td>
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
   <td>允許從CUG評估中排除具有配置名稱的承擔者。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另請參閱下方的「設定選項」一節。</p> </td>
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

#### Configuration Options {#configuration-options}

主要配置選項包括：

* `cugSupportedPaths`:指定可能包含CUG的子樹。 未設定預設值
* `cugEnabled`:配置選項，以啟用對當前CUG策略的權限評估。

與CUG-authorization模組相關的可用配置選項列於 [Apache Oak Documentation中，並詳細說明](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)。

#### 從CUG評估中排除承擔者 {#excluding-principals-from-cug-evaluation}

對個人原則不進行CUG評價。 新的CUG授權以名為CugExclude的專用介面來涵蓋此點。 Apache Jackrabbit Oak 1.4提供預設實作，排除固定的承擔者集合，以及可設定個別承擔者名稱的擴充實作。 後者是在AEM發佈例項中設定。

自AEM 6.3以來的預設值可防止下列承擔者受到CUG原則的影響：

* 管理承擔者（管理員使用者、管理員群組）
* 服務用戶承擔者
* 儲存庫內部系統主機

如需詳細資訊，請參閱下方「自AEM 6.3 [以來的預設設定」一節中的](#default-configuration-since-aem) 表格。

「管理員」群組的排除可在 **Apache Jackrabbit Oak CUG排除清單的設定區段中，在系統主控台中變更或擴充**。

或者，可以提供和部署CugExclude介面的自定義實現，以在特殊需要時調整排除的承擔者集。 如需詳細資訊和 [範例實作](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) ，請參閱CUG可插拔性檔案。

### 驗證：設定與設定 {#authentication-setup-and-configuration}

新的驗證相關部分包含在 **Adobe Granite Authentication Handler** bundle( `com.adobe.granite.auth.authhandler` 5.6.48版)中。 此套件是AEM預設安裝的一部分。

若要針對已過時的CUG支援設定驗證需求取代，某些OSGi元件必須存在並在指定的AEM安裝中生效。 如需詳細資訊，請 **參閱下方的OSGi元件** 特性。

>[!NOTE]
>
>由於RequirementHandler具有強制性設定選項，因此只有在透過指定一組支援的路徑啟用功能時，驗證相關部分才會生效。 在標準AEM安裝中，功能會在作者執行模式中停用，並在發佈執行模式中啟用/content。

**OSGi元件的特性**

已引入下列2個OSGi元件，以定義驗證需求並指定專用的登入路徑：

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
   <td>用於驗證要求的專用OSGi服務，該服務會向觀察器註冊影響驗證要求的內容更改（通過混合類型）和登錄路徑 <code>granite:AuthenticationRequirement</code><code>LoginSelectorHandler</code>。 </td>
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

| 標籤 | Adobe Granite驗證需求與登入路徑處理常式 |
|---|---|
| 說明 | `RequirementHandler` 會更新Apache Sling驗證需求的實作，以及相關登入路徑的對應排除。 |
| 組態屬性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | 不適用 |

#### Configuration Options {#configuration-options-1}

CUG重寫的驗證相關部分僅隨附與Adobe Granite驗證要求和登入路徑處理常式相關聯的單一設定選項：

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
   <td>此處理常式將遵循驗證要求的路徑。 如果要將混合類型添加到節點而不強制執行 <code>granite:AuthenticationRequirement</code> （例如，在作者實例上），請取消設定此配置。 如果缺失，則禁用此功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3以來的預設設定 {#default-configuration-since-aem}

AEM的新安裝預設會將新的實施用於CUG功能的授權和驗證相關部分。 舊版實作「Adobe Granite Closed User Group(CUG)Support」已過時，依預設會在所有AEM安裝中停用。 新實作將改為啟用如下：

### 作者例項 {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **說明** |
|---|---|
| 支援的路徑 `/content` | 已啟用CUGpolicys的訪問控制管理。 |
| 啟用CUG評估的FALSE | 權限評估已停用。 CUG政策沒有作用。 |
| 等級 | 200 | 請參閱Oak檔案。 |

>[!NOTE]
>
>預設編寫例 **項上未顯示Apache Jackrabbit Oak CUG Exclude List****和Adobe Granite Authentication Requirement和Login Path Handler** 。

### 發佈例項 {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **說明** |
|---|---|
| 支援的路徑 `/content` | CUG策略的訪問控制管理在配置的路徑下啟用。 |
| 啟用CUG評估TRUE | 在已設定路徑下方啟用權限評估。 CUG政策生效 `Session.save()`。 |
| 等級 | 200 | 請參閱Oak檔案。 |

| **&quot;Apache Jackrabbit Oak CUG排除清單&quot;** | **說明** |
|---|---|
| 承擔者名稱管理員 | 排除管理員承擔者，使其不參與CUG評估。 |

| **「Adobe Granite Authentication Requirement and Login Path Handler」** | **說明** |
|---|---|
| 支援的路徑 `/content` | 通過混合類型在儲存庫中定義的驗證要求 `granite:AuthenticationRequired` 將在下面生 `/content` 效 `Session.save()`。 Sling Authenticator會更新。 將混合類型添加到支援路徑之外會被忽略。 |

## 禁用CUG授權和驗證要求 {#disabling-cug-authorization-and-authentication-requirement}

如果給定安裝不使用CUG或使用不同的方法進行驗證和授權，則可以完全禁用新實施。

### 禁用CUG授權 {#disable-cug-authorization}

請參閱 [CUG可插拔性檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) ，以取得如何從複合授權設定移除CUG授權模型的詳細資訊。

### 禁用驗證要求 {#disable-the-authentication-requirement}

為了停用對模組提供之驗證要求的支援， `granite.auth.authhandler` 請移除與 **Adobe Granite驗證要求和登入路徑處理常式相關的組態**。

>[!NOTE]
>
>但是，請注意，刪除配置不會取消註冊mixin類型，該類型仍適用於節點，但不會產生影響。

## 與其他模組的交互 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

為了反映CUG授權模型使用的新型訪問控制策略，擴展了Apache Jackrabbit定義的API。 自從2.11.0版本的模 `jackrabbit-api` 塊定義了名為的新介面 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`，該介面從中擴展 `javax.jcr.security.AccessControlPolicy`。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的導入機制已經調整，以處理類型的訪問控制策略 `PrincipalSetPolicy`。

### Apache Sling Content Distribution {#apache-sling-content-distribution}

請參閱上述 [Apache Jackrabbit FileVault部分](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 。

### Adobe Granite複製 {#adobe-granite-replication}

複製模組已稍作調整，以便能夠在不同AEM實例之間複製CUG策略：

* `DurboImportConfiguration.isImportAcl()` 僅影響訪問控制策略的實施 `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 將僅遵守此配置，以便使用真正的ACL
* 其他策略(如 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` 由CUG授權模型建立的實例)將始終被複製，並且將忽略 `DurboImportConfiguration.isImportAcl`配置選項()。

複製CUG策略有一個限制。 如果在不刪除相應的混音節點類型的情況下刪除了給定的CUG策 `rep:CugMixin,` 略，則複製時將不反映刪除。 已解決此問題：在刪除策略時始終刪除混音。 不過，如果手動添加混合類型，則可能會顯示該限制。

### Adobe Granite驗證處理常式 {#adobe-granite-authentication-handler}

套件隨附的驗 **證處理常式Adobe Granite HTTP Header Authentication Handler** , `com.adobe.granite.auth.authhandler` 包含對相同模組所定義 `CugSupport` 之介面的參考。 它用於在某些情況下計算「領域」，返回到使用處理程式配置的領域。

這已經調整為可選引用，以 `CugSupport` 確保當特定設定決定重新啟用已過時的實作時，最大回溯相容性。 使用實作的安裝將不再取得從CUG實作擷取的領域，但一律會顯示以 **Adobe Granite HTTP標題驗證處理常式定義的領域**。

>[!NOTE]
>
>依預設， **Adobe Granite HTTP Header Authentication Handler** ( `auth.http.nologin`Adobe Granite HTTP Header Authentication Handler)僅在發佈執行模式中設定，並啟用「停用登入頁面」()選項。

### AEM LiveCopy {#aem-livecopy}

將CUG與LiveCopy一起配置在儲存庫中通過添加一個額外節點和一個額外屬性來表示，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

這兩個元素都在下面建立 `cq:Page`。 在當前設計中，MSM僅處理位於()節點下的節 `cq:PageContent` 點和`jcr:content`屬性。

因此，CUG群組無法從Blueprint回滾至即時副本。 設定即時副本時，請據此規劃。

## 新CUG實作的變更 {#changes-with-the-new-cug-implementation}

本節的目的是概述對CUG功能所做的更改以及新舊實施的比較。 它列出了影響CUG支援配置方式的更改，並說明了如何和由誰在儲存庫內容中管理CUG。

### CUG設定和配置的差異 {#differences-in-cug-setup-and-configuration}

已過時的OSGi元件 **Adobe Granite Closed User Group(CUG)Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已由新元件取代，以便能夠分別處理前CUG功能的授權和驗證相關部分。

## 管理儲存庫內容中CUG的差異 {#differences-in-managing-cugs-in-the-repository-content}

以下各節從實施和安全性角度說明新舊實施之間的差異。 雖然新的實作旨在提供相同的功能，但在使用新CUG時，有一些細微的變更需要知道。

### 授權方面的差異 {#differences-with-regards-to-authorization}

從授權角度來看，主要差異概列於下列清單：

**CUG專用的存取控制內容**

在舊實施中，預設授權模型用於在發佈時操縱訪問控制清單策略，由CUG授權的設定替換任何現有ACE。 這是由寫入規則、剩餘的JCR屬性（在發佈時解譯）所觸發。

在新實施中，預設授權模型的訪問控制設定不受建立、修改或刪除的任何CUG的影響。 而是將名為的新策略類 `PrincipalSetPolicy` 型作為附加訪問控制內容應用於目標節點。 此附加策略將作為目標節點的子節點進行定位，並作為預設策略節點的同級節點（如果存在）。

**在訪問控制管理中編輯CUG策略**

從剩餘的JCR屬性移動到專用訪問控制策略會影響建立或修改CUG功能授權部分所需的權限。 由於這被視為對訪問控制內容的修改，因此它需 `jcr:readAccessControl` 要 `jcr:modifyAccessControl` 和權限才能寫入儲存庫。 因此，只有有權修改頁面存取控制內容的內容作者才能設定或修改此內容。 這與舊版實作不同，舊版實作中寫入一般JCR屬性的能力已足夠，導致權限竊取。

**由策略定義的目標節點**

CUG策略預期會在JCR節點上建立，該節點定義要受限制讀訪問的子樹。 這可能是AEM頁面，以防CUG影響整個樹狀結構。

請注意，將CUG原則僅放在位於指定頁面下方的jcr:content節點上，只會限制對指定頁面內容s.str的存取，但不會對任何同級或子頁面產生作用。 這可能是一個有效的使用案例，而且可以使用允許應用細粒度訪問內容的儲存庫編輯器來實現。 不過，它會與之前的實作比較，其中將cq:cugEnabled屬性置於jcr:content節點上會在內部重新對應至頁面節點。 不再執行此映射。

**使用CUG策略的權限評估**

從舊版CUG支援移轉至其他授權模型，會變更有效讀取權限的評估方式。 如 [Jackrabbit檔案所述](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)，如果Oak資料庫中設定的所有模型的權限評估授與讀取存取權，則允許檢視的指定承擔者 `CUGcontent` ，將僅獲得讀取存取權。

換言之，為評估有效權限，將同時考慮 `CUGPolicy` 和預設訪問控制項，並且只有在兩種策略都授予對CUG內容的讀訪問權時才授予對CUG內容的讀訪問權。 在預設的AEM發佈安裝中，每個人都可取得完整 `/content` 樹狀結構的讀取存取權，CUG原則的效果將與舊實作相同。

**隨選評估**

CUG授權模型允許個別開啟存取控制管理與權限評估：

* 如果模組具有一個或多個可建立CUG的支援路徑，則啟用訪問控制管理
* 僅當另外勾選「啟用 **CUG評估」選項時** ，才啟用權限評估。

在CUG原則的新AEM預設設定評估中，它只會以&#39;publish&#39;執行模式啟用。 請參閱自AEM 6.3以 [來的預設設定詳細資訊](#default-configuration-since-aem) ，以取得詳細資訊。 這可以通過將給定路徑的有效策略與儲存在內容中的策略進行比較來驗證。 只有在啟用CUG的權限評估時，才會顯示有效的原則。

如上所述，CUG存取控制原則現在一律儲存在內容中，但只有在Apache Jackrabbit Oak **CUG Configuration的系統主控台中開啟** CUG Evaluation Enabled **，才會執行這些原則產生的有效權限評估。** 依預設，它僅啟用「發佈」執行模式。

### 與驗證的差異 {#differences-with-regards-to-authentication}

以下說明與驗證有關的差異。

#### 用於驗證要求的專用混合類型 {#dedicated-mixin-type-for-authentication-requirement}

在前一個實現中，CUG的授權和認證都由單個JCR屬性( `cq:cugEnabled`)觸發。 就驗證而言，這會產生與Apache Sling Authenticator實作一起儲存的更新驗證需求清單。 通過新的實施，通過用專用混頻類型( `granite:AuthenticationRequired`)標籤目標節點來獲得相同的結果。

#### 用於排除登錄路徑的屬性 {#property-for-excluding-login-path}

mixin類型定義了一個名為的可選屬性， `granite:loginPath`它基本上與屬性相 `cq:cugLoginPage` 對應。 與先前的實施相比，只有在其聲明節點類型為上述混音時，才會考慮登入路徑屬性。 新增具有該名稱的屬性而不設定mixin類型將無效，且不會向驗證者報告登入路徑的新要求或排除。

#### 驗證要求的權限 {#privilege-for-authentication-requirement}

添加或刪除混合類型需要授 `jcr:nodeTypeManagement` 予權限。 在先前的實作中，權 `jcr:modifyProperties` 限用於編輯剩餘屬性。

就目前而言， `granite:loginPath` 添加、修改或移除屬性時需要相同的權限。

#### 由Mixin類型定義的目標節點 {#target-node-defined-by-mixin-type}

驗證要求應在JCR節點上建立，該節點定義要受強制登錄約束的子樹。 這可能是AEM頁面，以防CUG預期會影響整個樹狀結構，而新實作的UI會因此在頁面節點上新增驗證需求混合類型。

將CUG原則僅放在位於指定頁面下方的jcr:content節點，只會限制內容的存取，但不會影響頁面節點本身或任何子頁面。

這可能是一個有效的方案，而且對於允許將混合放在任意節點的儲存庫編輯器是可能的。 但是，此行為與前一個實作不同，其中在jcr:content節點上放置cq:cugEnabled或cq:cugLoginPage屬性會在內部重新對應至頁面節點。 不再執行此映射。

#### 已配置支援的路徑 {#configured-supported-paths}

mixin類 `granite:AuthenticationRequired` 型和granite:loginPath屬性只會在 **Adobe Granite Authentication Requirement和Login Path Handler所顯示的一組「受支援路徑」設定選項所定義的範圍內使用******。 如果未指定路徑，則完全禁用驗證要求功能。 在此例中，混合類型或屬性在添加或設定為給定JCR節點時生效。

### JCR內容、OSGi服務和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下文檔提供了舊實施和新實施之間OSGi服務、配置和儲存庫內容的完整映射。

AEM 6.3以來的CUG對應

[取得檔案](assets/cug-mapping.pdf)

## 升級CUG {#upgrade-cug}

### 使用已過時的CUG的現有安裝 {#existing-installations-using-the-deprecated-cug}

舊版CUG支援實作已過時，將在未來版本中移除。 從AEM 6.3之前的版本升級時，建議移至新的實作。

對於升級的AEM安裝，請務必確保只啟用一個CUG實作。 新的和舊的、已過時的CUG支援的組合不會進行測試，並可能導致不希望的行為：

* Sling驗證器中與驗證要求的衝突
* 當與舊CUG關聯的ACL設定與新CUG策略衝突時，拒絕讀訪問。

### 移轉現有的CUG內容 {#migrating-existing-cug-content}

Adobe提供移轉至新CUG實作的工具。 若要使用它，請執行下列步驟：

1. 前往 `https://<serveraddress>:<serverport>/system/console/cug-migration` 存取工具。
1. 輸入要檢查的CUG的根路徑，然後按「 **Perform dry run** （執行乾式運行）」按鈕。 這會掃描在選取位置符合轉換資格的CUG。
1. 複查結果後，按「執 **行遷移** 」按鈕遷移到新實施。

>[!NOTE]
>
>如果您遇到問題，則可以在 **DEBUG** level `com.day.cq.auth.impl.cug` on上設定特定記錄器，以取得移轉工具的輸出。 如需如 [何執行此動作的詳細資訊](/help/sites-deploying/configure-logging.md) ，請參閱記錄。

