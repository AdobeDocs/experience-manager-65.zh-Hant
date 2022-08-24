---
title: 中的已關閉用戶AEM組
seo-title: Closed User Groups in AEM
description: 瞭解中的關閉用戶組AEM。
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
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6872'
ht-degree: 0%

---

# 中的已關閉用戶AEM組{#closed-user-groups-in-aem}

## 簡介 {#introduction}

自AEM6.3以來，新的封閉用戶組實施旨在解決現有實施中存在的效能、可擴充性和安全問題。

>[!NOTE]
>
>為了簡單起見，本文檔中將使用CUG縮寫。

新實施的目標是在需要時覆蓋現有功能，同時解決舊版本的問題和設計限制。 結果為具有以下特點的CUG新設計：

* 明確區分可單獨或組合使用的驗證和授權元素；
* 專用授權模型，在配置的CUG樹上反映受限讀訪問，而不干擾其他訪問控制設定和權限要求；
* 將編寫實例時通常需要的受限讀訪問的訪問控制設定與發佈時通常需要的權限評估分開；
* 編輯受限讀取權限，而不提升權限；
* 專用節點類型擴展來標籤認證要求；
* 與身份驗證要求關聯的可選登錄路徑。

### 新的自定義用戶組實現 {#the-new-custom-user-group-implementation}

CUG（在上下文中稱為）由AEM以下步驟組成：

* 限制對需要保護的樹的讀訪問，並僅允許讀取與給定CUG實例一起列出或完全從CUG評估中排除的承擔者。 這稱為 **授權** 的子菜單。
* 在給定樹上強制驗證，並可選地為該樹指定一個專用登錄頁，該頁隨後被排除。 這稱為 **認證** 的子菜單。

新的實現被設計為在驗證和授權元素之間划出一條線。 從6.AEM3開始，可以在不顯式添加身份驗證要求的情況下限制讀訪問。 例如，如果給定實例完全需要驗證，或者給定樹已駐留在需要驗證的子樹中。

同樣，在不改變有效權限設定的情況下，可以用驗證要求來標籤給定樹。 組合及結果列於 [將CUG策略與身份驗證要求相結合](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 的子菜單。

## 概觀 {#overview}

### 授權：限制讀取訪問 {#authorization-restricting-read-access}

CUG的關鍵功能是限制內容儲存庫中給定樹上除所選承擔者之外的所有人的讀取訪問。 新實現不是在即時操作預設訪問控制內容，而是採用不同的方法定義表示CUG的專用訪問控制策略類型。

#### CUG的訪問控制策略 {#access-control-policy-for-cug}

此新類型的策略具有以下特徵：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定義）類型的訪問控制策略；
* PrincipalSetPolicy授予可修改的承擔者集的權限；
* 授予的權限和策略的範圍是實施詳細資訊。

用於表示CUG的PrincipalSetPolicy的實現還定義了：

* CUG策略僅授予對常規JCR項的讀訪問權限（例如，排除訪問控制內容）;
* 該範圍由保存CUG策略的接入控制節點定義；
* CUG策略可以嵌套，嵌套的CUG啟動新CUG而不繼承「parent」 CUG的主集；
* 如果啟用了評估，則策略的效果將繼承到整個子樹，直到下一個嵌套的CUG。

這些CUG策略通過名為oak-authorization-cugAEM的單獨授權模組部署到實例。 該模組具有自己的訪問控制管理和權限評估功能。 換句話說，預設設定提供AEM了Oak內容儲存庫配置，該配置結合了多個授權機制。 有關詳細資訊，請參見 [Apache Oak文檔上的此頁](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

在此複合設定中，新CUG不會替換附加到目標節點的現有訪問控制內容，而是設計為補充，稍後也可以刪除，而不影響原始訪問控制，預設情況下AEM，在中是訪問控制清單。

與前一種實施方式相反，新的CUG策略總是被識別和視為訪問控制內容。 這意味著它們是使用JCR訪問控制管理API建立和編輯的。 有關詳細資訊，請參閱 [管理CUG策略](#managing-cug-policies) 的子菜單。

#### CUG策略的權限評估 {#permission-evaluation-of-cug-policies}

除了CUG的專用訪問控制管理之外，新授權模型允許有條件地啟用對其策略的許可評估。 這允許在轉移環境中設定CUG策略，並且只允許在複製到生產環境後評估有效權限。

CUG策略的權限評估以及與預設或任何附加授權模型的交互遵循為Apache Jackrabbit Oak中的多個授權機制設計的模式：如果且僅當所有模型都授予訪問權限時，才授予給定權限集。 請參閱 [此頁](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) 的子菜單。

以下特徵適用於與用於處理和評估CUG策略的授權模型相關的權限評估：

* 它只處理常規節點和屬性的讀取權限，而不處理讀取訪問控制內容
* 它不處理被保護的JCR內容（訪問控制、節點類型資訊、版本控制、鎖定或用戶管理等）的修改所需的寫權限或任何類型的權限；這些權限不受CUG策略的影響，並且不會由關聯的授權模型評估。 是否授予這些權限取決於在安全設定中配置的其他模型。

單個CUG策略對權限評估的影響可概括如下：

* 除了包含策略中列出的排除的承擔者或承擔者的主題外，所有人都拒絕讀取權限；
* 該策略對保存策略及其屬性的接入控制節點生效；
* 此效果在層次結構下被繼承，即由訪問控制節點定義的項目樹；
* 但是，它不影響接入控制節點的同級和祖先；
* 給定CUG的繼承在嵌套CUG處停止。

#### 最佳作法 {#best-practices}

在通過CUG定義受限讀訪問時，應考慮以下最佳做法：

* 有意識地決定您對CUG的需求是限制讀訪問還是驗證要求。 如果是後者，或者需要兩者兼備，請參考「最佳做法」一節，瞭解有關「驗證」要求的詳細資訊
* 為需要保護的資料或內容建立威脅模型，以識別威脅邊界並清楚地瞭解資料的敏感性以及與授權訪問相關的角色
* 為儲存庫內容和CUG建模時應牢記與一般授權相關的方面和最佳做法：

   * 請記住，僅當給定的CUG和安裝授權中部署的其他模組的評估允許給定主題讀取給定的儲存庫項目時，才授予讀取權限
   * 避免在讀取訪問已被其他授權模組限制的情況下建立冗餘CUG
   * 對嵌套CUG的過度需求可能會突出內容設計中的問題
   * 對CUG的過度需求（例如，在每一頁上）可能表明需要定制授權模型，這可能更適合於滿足應用程式和現有內容的特定安全需求。

* 將CUG策略支援的路徑限制在儲存庫中的幾個樹上，以便實現優化的效能。 例如，自6.3以來，僅允許將/content節點下的CUG作為預設值AEM提供。
* CUG策略旨在授予對一小組主體的讀取訪問權限。 需要大量負責人可能會突出內容或應用設計中的問題，應重新考慮。

### 身份驗證：定義身份驗證要求 {#authentication-defining-the-auth-requirement}

CUG功能的驗證相關部分允許標籤需要驗證的樹並可選地指定專用登錄頁。 根據先前版本，新實現允許在內容儲存庫中標籤需要驗證的樹並有條件地啟用與 `Sling org.apache.sling.api.auth.Authenticator`負責最終強制執行要求並重定向到登錄資源。

這些要求通過提供OSGi服務向驗證器註冊 `sling.auth.requirements` 註冊屬性。 然後，這些屬性用於動態擴展驗證要求。 有關詳細資訊，請參考 [Sling文檔](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用專用混合類型定義驗證要求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

出於安全原因，新的實現將剩餘JCR屬性的使用替換為稱為的專用混合類型 `granite:AuthenticationRequired`，它為登錄路徑定義STRING類型的單個可選屬性 `granite:loginPath`。 只有與此混合類型相關的內容更改才能更新向Apache Sling Authenticator註冊的要求。 在保存任何臨時修改時跟蹤這些修改，因此需要 `javax.jcr.Session.save()` 要求生效。

同樣適用於 `granite:loginPath` 屬性。 只有由身份驗證要求相關的混合類型定義，才會尊重它。 在非結構化JCR節點添加具有此名稱的剩餘屬性將不顯示所需效果，而負責更新OSGi註冊的處理程式將忽略該屬性。

>[!NOTE]
>
>設定登錄路徑屬性是可選的，並且僅當需要身份驗證的樹不能回退到預設值或繼承的登錄頁時才需要。 查看 [登錄路徑評估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 下。

#### 向Sling Authenticator註冊身份驗證要求和登錄路徑 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由於此類身份驗證要求預計將限於某些運行模式和內容儲存庫中的一小部分樹，因此跟蹤要求混合類型和登錄路徑屬性是有條件的，並綁定到定義受支援路徑的相應配置（請參見下面的配置選項）。 因此，只有這些受支援路徑範圍內的更改才會觸發OSGi註冊的更新，在其他位置，將忽略混合類型和屬性。

預設設AEM置現在通過允許以作者運行模式設定混合來利用此配置，但僅在複製到發佈實例時生效。 請參閱 [此頁](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) 詳細瞭解Sling如何強制執行身份驗證要求。

添加 `granite:AuthenticationRequired` 配置的支援路徑中的混合類型將導致更新負責處理程式的OSGi註冊，該註冊包含一個新的附加條目 `sling.auth.requirements` 屬性。 如果給定的身份驗證要求指定了可選 `granite:loginPath` 屬性中，該值將用「 — 」前置詞額外註冊到驗證器，以便從驗證要求中排除。

#### 認證需求的評估與繼承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling身份驗證要求應通過頁面或節點層次結構繼承。 繼承和驗證要求評估的詳細資訊（如順序和優先順序）被視為實施詳細資訊，本文不會記錄在案。

#### 登錄路徑評估 {#evaluation-of-login-path}

在驗證時評估登錄路徑並重定向到相應資源是當前Adobe花崗岩登錄選擇器驗證處理程式( `com.day.cq.auth.impl.LoginSelectorHandler`)，預設配置為Apache Sling AuthenticationHandlerAEM。

呼叫 `AuthenticationHandler.requestCredentials` 此處理程式嘗試確定將將用戶重定向到的映射登錄頁。 這包括以下步驟：

* 區分過期密碼和需要定期登錄作為重定向原因；
* 如果是常規登錄，則按以下順序獲取登錄路徑時test:

   * 從LoginPathProvider中 `com.adobe.granite.auth.requirement.impl.RequirementService`。
   * 從舊的、過時的CUG實現，
   * 從「登錄頁映射」中， `LoginSelectorHandler`。
   * 最後，回退到預設登錄頁，如 `LoginSelectorHandler`。

* 一旦通過上述呼叫獲得了有效的登錄路徑，用戶的請求將重定向到該頁。

本文檔的目標是評估由內部 `LoginPathProvider` 。 自6.3起發AEM運的實施如下：

* 登錄路徑的註冊取決於對過期密碼的區分，以及是否需要定期登錄作為重定向的原因
* 在常規登錄時，按以下順序獲取登錄路徑時會test:

   * 從 `LoginPathProvider` 由新 `com.adobe.granite.auth.requirement.impl.RequirementService`。
   * 從舊的、過時的CUG實現，
   * 從登錄頁映射中 `LoginSelectorHandler`。
   * 最後回退到使用 `LoginSelectorHandler`。

* 一旦通過上述呼叫獲得了有效的登錄路徑，用戶的請求將重定向到該頁。

的 `LoginPathProvider` 由Granite中的新身份驗證要求支援實現，顯示由 `granite:loginPath` 屬性，這些屬性又由上述混合類型定義。 保存登錄路徑的資源路徑和屬性值本身的映射被保存在記憶體中，並將被評估以為層次中的其他節點找到合適的登錄路徑。

>[!NOTE]
>
>僅對與配置的支援路徑中的資源相關聯的請求執行評估。 對於任何其他請求，將評估確定登錄路徑的替代方法。

#### 最佳作法 {#best-practices-1}

在定義身份驗證要求時應考慮以下最佳做法：

* 避免嵌套身份驗證要求：在樹的開頭放置一個身份驗證要求標籤應該足夠，並且會繼承到目標節點定義的整個子樹。 該樹中的其他身份驗證要求應視為冗餘，在評估Apache Sling中的身份驗證要求時，可能會導致效能問題。 通過將授權和認證相關的CUG區域分離，可以通過CUG或其他類型的策略來限制讀取訪問，同時強制對整個樹進行認證。
* 模型儲存庫內容，這樣驗證要求就適用於整個樹，而無需再次從要求中排除嵌套子樹。
* 要避免指定並隨後註冊冗餘登錄路徑，請執行以下操作：

   * 依靠繼承，避免定義嵌套登錄路徑，
   * 不要將可選登錄路徑設定為與預設值或繼承值對應的值，
   * 應用程式開發人員應確定在與全局登錄路徑關聯的全局登錄路徑配置（預設路徑和映射）中應配置哪些登錄路徑 `LoginSelectorHandler`。

## 儲存庫中的表示法 {#representation-in-the-repository}

### 儲存庫中的CUG策略表示 {#cug-policy-representation-in-the-repository}

Oak文檔介紹了新CUG策略在儲存庫內容中的反映方式。 有關詳細資訊，請查閱 [此頁](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 儲存庫中的身份驗證要求 {#authentication-requirement-in-the-repository}

對單獨認證要求的需要在儲存庫內容中反映，在目標節點處放置專用混合節點類型。 混合類型定義一個可選屬性，用於為目標節點定義的樹指定專用登錄頁。

與登錄路徑關聯的頁面可以位於該樹的內部或外部。 它將被排除在身份驗證要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份驗證要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR訪問控制管理API管理用於限制CUG讀訪問的新類型的訪問控制策略，並遵循與 [JCR 2.0規範](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)。

#### 設定新的CUG策略 {#set-a-new-cug-policy}

在以前未設定CUG的節點應用新CUG策略的代碼。 請注意 `getApplicablePolicies` 將僅返回以前未設定的新策略。 最後，需要回寫策略，並且需要持續更改。

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

#### 編輯現有CUG策略 {#edit-an-existing-cug-policy}

編輯現有CUG策略需要執行以下步驟。 請注意，修改後的策略需要回寫，並且需要使用 `javax.jcr.Session.save()`。

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

JCR訪問控制管理定義一種最佳方法來檢索在給定路徑上生效的策略。 由於CUG策略的評估是有條件的，並且取決於要啟用的相應配置，因此調用 `getEffectivePolicies` 是驗證給定CUG策略是否在給定安裝中生效的一種簡便方法。

>[!NOTE]
>
>請注意 `getEffectivePolicies` 以及隨後的代碼示例，該代碼示例在層次結構中查找給定路徑是否已是現有CUG的一部分。

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

查找在給定路徑上定義的所有嵌套CUG，而不管它們是否有效。 有關詳細資訊，請參閱 [配置選項](/help/sites-administering/closed-user-groups.md#configuration-options) 的子菜單。

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

由定義的擴展 `JackrabbitAccessControlManager` 允許按承擔者編輯訪問控制策略的訪問控制策略未通過CUG訪問控制管理實現，因為根據定義，CUG策略始終影響所有承擔者：那些 `PrincipalSetPolicy` 將被授予讀訪問權限，同時將阻止所有其他主體讀取目標節點定義的樹中的內容。

相應的方法始終返回空策略陣列，但不會引發異常。

### 管理身份驗證要求 {#managing-the-authentication-requirement}

通過改變目標節點的有效節點類型來實現新認證要求的建立、修改或移除。 然後，可以使用常規JCR API編寫可選登錄路徑屬性。

>[!NOTE]
>
>對上述給定目標節點的修改將僅反映在Apache Sling Authenticator上，如果 `RequirementHandler` 已配置，並且目標包含在受支援路徑定義的樹中（請參見「配置選項」一節）。
>
>有關詳細資訊，請參見 [分配混合節點類型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配混合節點類型)和 [添加節點和設定屬性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加節點和設定屬性)

#### 添加新的身份驗證要求 {#adding-a-new-auth-requirement}

下面詳細介紹了建立新身份驗證要求的步驟。 請注意，只有在 `RequirementHandler` 已為包含目標節點的樹配置。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 添加具有登錄路徑的新身份驗證要求 {#add-a-new-auth-requirement-with-login-path}

建立包括登錄路徑的新身份驗證要求的步驟。 請注意，只有在以下情況下，登錄路徑的要求和排除才會註冊到Apache Sling Authenticator `RequirementHandler` 已為包含目標節點的樹配置。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改現有登錄路徑 {#modify-an-existing-login-path}

下面詳細說明了更改現有登錄路徑的步驟。 只有在以下情況下，才會向Apache Sling Authenticator註冊修改 `RequirementHandler` 已為包含目標節點的樹配置。 將從註冊中刪除以前的登錄路徑值。 與此目標節點關聯的身份驗證要求不受此修改的影響。

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

#### 刪除現有登錄路徑 {#remove-an-existing-login-path}

刪除現有登錄路徑的步驟。 只有在以下情況下，才會從Apache Sling Authenticator註銷登錄路徑項： `RequirementHandler` 已為包含目標節點的樹配置。 與目標節點關聯的身份驗證要求不受影響。

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

或者，您可以使用以下方法實現相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 刪除身份驗證要求 {#remove-an-auth-requirement}

刪除現有身份驗證要求的步驟。 只有在以下情況下，才會從Apache Sling Authenticator註銷該要求： `RequirementHandler` 已為包含目標節點的樹配置。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 檢索有效的身份驗證要求 {#retrieve-effective-auth-requirements}

沒有專用的公共API來讀取向Apache Sling Authenticator註冊的所有有效身份驗證要求。 但是，該清單會在以下位置的系統控制台中顯示 `https://<serveraddress>:<serverport>/system/console/slingauth` 下&#x200B;**身份驗證要求配置**&#x200B;的子菜單。

下圖顯示了包含演示內容的發AEM布實例的驗證要求。 社區頁面的突出顯示路徑說明了本文檔中描述的實現所添加的要求如何反映在Apache Sling Authenticator中。

>[!NOTE]
>
>在此示例中，未設定可選登錄路徑屬性。 因此，沒有向驗證器註冊第二個條目。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 檢索有效登錄路徑 {#retrieve-the-effective-login-path}

當前沒有公共API可檢索在匿名訪問需要身份驗證的資源時生效的登錄路徑。 有關如何檢索登錄路徑的實現詳細資訊，請參閱「登錄路徑評估」一節。

但請注意，除了使用此功能定義的登錄路徑之外，還有其他方法來指定指向登錄的重定向，在設計內容模型和給定安裝的驗證要求時，應考慮這AEM些方法。

#### 檢索繼承的身份驗證要求 {#retrieve-the-inherited-auth-requirement}

與登錄路徑一樣，沒有公共API來檢索內容中定義的繼承的身份驗證要求。 以下示例說明如何列出已使用給定層次定義的所有驗證要求，而不管這些要求是否有效。 有關詳細資訊，請參見 [配置選項](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建議在驗證要求和登錄路徑上都使用繼承機制，並避免建立嵌套的驗證要求。
>
>有關詳細資訊，請參閱 [認證需求的評估與繼承](#evaluation-and-inheritance-of-the-authentication-requirement)。 [登錄路徑評估](#evaluation-of-login-path) 和 [最佳做法](#best-practices)。

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

### 將CUG策略與身份驗證要求相結合 {#combining-cug-policies-and-the-authentication-requirement}

下表列出了CUG策略的有效組合和實例中的驗證要求，AEM該實例通過配置啟用了兩個模組。

| **需要身份驗證** | **登錄路徑** | **受限讀取訪問** | **預期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效權限評估授予訪問權限，則給定用戶將只能查看使用CUG策略標籤的子樹。 未經過身份驗證的用戶將被重定向到指定的登錄頁。 |
| 是 | 否 | 是 | 如果有效權限評估授予訪問權限，則給定用戶將只能查看使用CUG策略標籤的子樹。 未經過身份驗證的用戶將被重定向到繼承的預設登錄頁。 |
| 是 | 是 | 否 | 未經過身份驗證的用戶將被重定向到指定的登錄頁。 是否允許查看標籤有身份驗證要求的樹取決於該子樹中包含的單個項目的有效權限。 沒有專用CUG限制讀取訪問。 |
| 是 | 否 | 否 | 未經過身份驗證的用戶將被重定向到繼承的預設登錄頁。 是否允許查看標籤有身份驗證要求的樹取決於該子樹中包含的單個項目的有效權限。 沒有專用CUG限制讀取訪問。 |
| 否 | 否 | 是 | 如果有效的權限評估授予訪問權限，則給定的已驗證或未驗證的用戶只能查看使用CUG策略標籤的子樹。 未經身份驗證的用戶將得到同等對待，不會重定向到登錄。 |

>[!NOTE]
>
>上面未列出「驗證要求」=「否」和「登錄路徑」=「是」的組合，因為「登錄路徑」是與驗證要求關聯的可選屬性。 指定具有該名稱的JCR屬性而不添加定義混合類型將無效，並且將被相應的處理程式忽略。

## OSGi元件和配置 {#osgi-components-and-configuration}

本節概述了新CUG實施中引入的OSGi元件和各個配置選項。

另請參見CUG映射文檔，以瞭解舊實施和新實施之間配置選項的全面映射。

### 授權：設定和配置 {#authorization-setup-and-configuration}

新的授權相關部件包含在 **Oak CUG授權** 捆綁包( `org.apache.jackrabbit.oak-authorization-cug`)，這是預設安裝的AEM一部分。 該捆綁包定義了一個單獨的授權模型，該模型旨在作為管理讀取訪問的附加方法進行部署。

#### 設定CUG授權 {#setting-up-cug-authorization}

有關設定CUG授權的詳細說明，請參見 [相關Apache文檔](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)。 預設情況下，AEM已在所有運行模式中部署CUG授權。 該逐步指令也可用於在那些需要不同授權設定的安裝中禁用CUG授權。

#### 配置引用過濾器 {#configuring-the-referrer-filter}

您還需要配置 [吊具引用過濾器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) 所有可用於訪問的主機名AEM;例如，通過CDN、Load Balancer和任何其他方法。

如果未配置引用過濾器，則當用戶嘗試登錄CUG站點時，將出現與以下類似的錯誤：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi組分的特性 {#characteristics-of-osgi-components}

已引入以下兩個OSGi元件來定義身份驗證要求並指定專用登錄路徑：

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>Apache Jackrabbit Oak CUG配置</td>
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
    </ul> <p>另請參見 <a href="#configuration-options">配置選項</a> 下。</p> </td>
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
    </ul> <p>另請參閱下面的「配置選項」一節。</p> </td>
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

關鍵配置選項包括：

* `cugSupportedPaths`:指定可能包含CUG的子樹。 未設定預設值
* `cugEnabled`:配置選項，以啟用對當前CUG策略的權限評估。

有關CUG授權模組的可用配置選項，請在 [Apache Oak文檔](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)。

#### 從CUG評估中排除承擔者 {#excluding-principals-from-cug-evaluation}

從前的實施中，已採取免除個別負責人的CUG評價。 新的CUG授權使用名為CugExclude的專用介面來覆蓋此權限。 Apache Jackrabbit Oak 1.4附帶預設實現，該實現不包括一組固定的承擔者，以及允許配置單個承擔者名稱的擴展實現。 後者在發佈實例AEM中配置。

自6.3以AEM來的預設值可防止CUG策略影響以下承擔者：

* 管理主體（管理員用戶、管理員組）
* 服務用戶主體
* 儲存庫內部系統主體

有關詳細資訊，請參閱 [自6.AEM3以來的預設配置](#default-configuration-since-aem) 的下界。

在配置部分的系統控制台中，可以更改或擴展「administrators」組的排除 **Apache Jackrabbit Oak CUG排除清單**。

或者，可以提供和部署CugExclude介面的定製實現，以在特殊需要時調整排除的承擔者集。 請參閱 [CUG可插入性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 的子菜單。

### 身份驗證：設定和配置 {#authentication-setup-and-configuration}

新的身份驗證相關部件包含在 **Adobe花崗岩驗證處理程式** 捆綁包( `com.adobe.granite.auth.authhandler` 版本5.6.48)。 此捆綁包是預設安AEM裝的一部分。

為了設定不建議使用的CUG支援的驗證要求替換，某些OSGi元件必須存在並在給定安裝中處於活動狀態AEM。 有關詳細資訊，請參閱 **OSGi組分的特性** 下。

>[!NOTE]
>
>由於RequirementHandler具有強制配置選項，因此只有通過指定一組受支援的路徑啟用了該功能時，驗證相關部件才會處於活動狀態。 在標準安AEM裝中，在作者運行模式下禁用該功能，在發佈運行模式下為/content啟用該功能。

**OSGi組分的特性**

已引入以下2個OSGi元件來定義身份驗證要求並指定專用登錄路徑：

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
   <td>用於驗證要求的專用OSGi服務，該服務註冊觀察器以瞭解影響驗證要求的內容更改(通過 <code>granite:AuthenticationRequirement</code> 混合類型)和登錄路徑 <code>LoginSelectorHandler</code>。 </td>
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

| 標籤 | Adobe花崗岩認證要求和登錄路徑處理程式 |
|---|---|
| 說明 | `RequirementHandler` 更新Apache Sling驗證要求以及相關登錄路徑的相應排除的實現。 |
| 組態屬性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | 不適用 |

#### 配置選項 {#configuration-options-1}

CUG重寫的驗證相關部分僅附帶與Adobe花崗岩驗證要求和登錄路徑處理程式相關聯的單個配置選項：

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
   <td>設定&lt;string&gt;</td>
   <td>-</td>
   <td>此處理程式將遵循驗證要求的路徑。 如果要添加 <code>granite:AuthenticationRequirement</code> 混合類型到節點，而不強制執行它們（例如，在作者實例上）。 如果缺失，則禁用該功能。 </td>
  </tr>
 </tbody>
</table>

## 自6.AEM3以來的預設配置 {#default-configuration-since-aem}

預設情AEM況下，新安裝將使用新實現來授權和驗證CUG功能的相關部分。 舊實現「Adobe花崗岩封閉用戶組(CUG)支援」已棄用，預設情況下將在所有安裝中禁AEM用。 將按如下方式啟用新實施：

### 作者實例 {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **解釋** |
|---|---|
| 支援的路徑 `/content` | 已啟用CUGpolicies的訪問控制管理。 |
| 啟用CUG評估為FALSE | 權限評估已禁用。 CUG策略無效。 |
| 等級 | 200 | 請參閱Oak文檔。 |

>[!NOTE]
>
>沒有配置 **Apache Jackrabbit Oak CUG排除清單** 和 **Adobe花崗岩認證要求和登錄路徑處理程式** 在預設創作實例上存在。

### 發佈實例 {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **解釋** |
|---|---|
| 支援的路徑 `/content` | CUG策略的訪問控制管理在配置的路徑下啟用。 |
| 啟用CUG評估為TRUE | 在配置的路徑下啟用權限評估。 CUG策略在 `Session.save()`。 |
| 等級 | 200 | 請參閱Oak文檔。 |

| **&quot;Apache Jackrabbit Oak CUG排除清單&quot;** | **解釋** |
|---|---|
| 承擔者名稱管理員 | 從CUG評估中排除管理員主體。 |

| **&quot;Adobe花崗岩驗證要求和登錄路徑處理程式&quot;** | **解釋** |
|---|---|
| 支援的路徑  `/content` | 通過 `granite:AuthenticationRequired` 混合類型在下面生效 `/content` 於 `Session.save()`。 Sling Authenticator已更新。 將忽略在支援的路徑之外添加混合類型。 |

## 禁用CUG授權和身份驗證要求 {#disabling-cug-authorization-and-authentication-requirement}

如果給定的安裝不使用CUG或使用不同的方法進行驗證和授權，則可以完全禁用新實施。

### 禁用CUG授權 {#disable-cug-authorization}

咨詢 [CUG可插入性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 文檔，瞭解有關如何從複合授權設定中刪除CUG授權模型的詳細資訊。

### 禁用身份驗證要求 {#disable-the-authentication-requirement}

為了禁用對由提供的驗證要求的支援 `granite.auth.authhandler` 該模組足以刪除與 **Adobe花崗岩認證要求和登錄路徑處理程式**。

>[!NOTE]
>
>但請注意，刪除配置不會取消註冊混合類型，該類型仍適用於節點，但不會產生任何影響。

## 與其他模組的交互 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

為了反映CUG授權模型使用的新型訪問控制策略，擴展了Apache Jackrabbit定義的API。 自2.11.0版 `jackrabbit-api` 模組定義稱為 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`，從 `javax.jcr.security.AccessControlPolicy`。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的導入機制已調整為處理類型的訪問控制策略 `PrincipalSetPolicy`。

### Apache Sling內容分發 {#apache-sling-content-distribution}

請參閱上面 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 的子菜單。

### Adobe花崗岩複製 {#adobe-granite-replication}

複製模組已稍作調整，以便能夠在不同實例之間複製CUG策AEM略：

* `DurboImportConfiguration.isImportAcl()` 只影響訪問控制策略的實施 `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 將僅對真實ACL執行此配置
* 其他策略，如 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` 由CUG授權模型建立的實例將始終被複製，並且配置選項 `DurboImportConfiguration.isImportAcl`()將被忽略。

複製CUG策略有一個限制。 如果刪除了給定的CUG策略而未刪除相應的混合節點類型 `rep:CugMixin,` 複製時不會反映刪除。 通過始終在刪除策略時刪除混合來解決此問題。 如果手動添加混合類型，則可能會顯示限制。

### Adobe花崗岩驗證處理程式 {#adobe-granite-authentication-handler}

驗證處理程式 **Adobe花崗岩HTTP標頭身份驗證處理程式** 隨附 `com.adobe.granite.auth.authhandler` 束包含對 `CugSupport` 由同一模組定義的介面。 它用於在特定情況下計算「領域」，並返回到使用處理程式配置的領域。

此值已調整，以參考 `CugSupport` （可選）以確保在給定安裝程式決定重新啟用不建議使用的實施時最大向後相容性。 使用該實現的安裝將不再從CUG實現中提取領域，但將始終顯示定義的領域 **Adobe花崗岩HTTP標頭身份驗證處理程式**。

>[!NOTE]
>
>預設情況下， **Adobe花崗岩HTTP標頭身份驗證處理程式** 僅在發佈運行模式下使用「禁用登錄頁」( `auth.http.nologin`)選項。

### 實AEM時 {#aem-livecopy}

將CUG與LiveCopy結合配置在儲存庫中時，會添加一個額外的節點和一個額外的屬性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

這兩個元素都在 `cq:Page`。 在當前設計中，MSM僅處理位於 `cq:PageContent` (`jcr:content`)節點。

因此，無法將CUG組推出到「藍圖中的即時副本」。 配置Live Copy時，請圍繞此進行規劃。

## 隨新CUG實施而發生的變化 {#changes-with-the-new-cug-implementation}

本節旨在概述對CUG功能所做的更改，以及舊實現和新實現的比較。 它列出了影響CUG支援配置方式的更改，並描述了如何和由誰在儲存庫內容中管理CUG。

### CUG設定和配置的差異 {#differences-in-cug-setup-and-configuration}

已棄用的OSGi元件 **Adobe花崗岩封閉用戶組(CUG)支援** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已被新元件替換，以便能夠分別處理以前CUG功能的授權和驗證相關部分。

## 儲存庫內容中管理CUG的差異 {#differences-in-managing-cugs-in-the-repository-content}

以下各節從實施和安全形度描述了新舊實施之間的差異。 雖然新實施旨在提供相同的功能，但在使用新CUG時，有一些細微的變化是需要瞭解的。

### 與授權的差異 {#differences-with-regards-to-authorization}

從授權角度來看，主要差異概述如下：

**CUG的專用訪問控制內容**

在舊實現中，預設授權模型用於操縱發佈時的訪問控制清單策略，由CUG授權的設定替換任何現有ACE。 這是由寫入常規的、剩餘的JCR屬性觸發的，這些屬性在發佈時進行瞭解釋。

在新實現中，預設授權模型的訪問控制設定不受任何正在建立、修改或刪除的CUG的影響。 而是名為 `PrincipalSetPolicy` 作為附加訪問控制內容應用於目標節點。 此附加策略將作為目標節點的子級進行定位，並且如果存在，則將作為預設策略節點的同級。

**在訪問控制管理中編輯CUG策略**

此從剩餘JCR屬性移動到專用訪問控制策略會影響建立或修改CUG功能授權部分所需的權限。 由於這被視為對訪問控制內容的修改，因此需要 `jcr:readAccessControl` 和 `jcr:modifyAccessControl` 權限，以便寫入儲存庫。 因此，只有有權修改頁面訪問控制內容的內容作者才能設定或修改此內容。 這與舊實現形成對比，舊實現中編寫常規JCR屬性的能力已足夠，導致權限提升。

**策略定義的目標節點**

CUG策略應在JCR節點建立，該節點定義要受限制讀取訪問的子樹。 如果CUG應影響整AEM個樹，則此頁很可能為頁。

請注意，將CUG策略僅放置在給定頁面下方的jcr:content節點，將僅限制對給定頁面內容s.str的訪問，但不會對任何同級或子頁面生效。 這可能是一個有效的使用案例，並且可以使用允許應用細粒度訪問內容的儲存庫編輯器來實現。 但是，它與以前的實現進行了比較，前者將cq:cugEnabled屬性放置在jcr:content節點上是在內部重新映射到頁面節點的。 不再執行此映射。

**使用CUG策略的權限評估**

從舊的CUG支援轉移到附加授權模型，改變評估有效讀取權限的方式。 如 [Jackrabbit文檔](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)，允許查看給定的主體 `CUGcontent` 只有在Oak儲存庫中配置的所有模型的權限評估授予讀訪問權限時，才授予讀訪問權限。

換句話說，為了評估有效權限， `CUGPolicy` 並且，將考慮預設訪問控制項，並且僅當CUG內容被兩種策略授予時才授予其讀訪問權限。 在預設發AEM布安裝中，讀取對完成的 `/content` 樹是給每個人的，CUG策略的效果與舊實施的效果相同。

**按需評估**

CUG授權模型允許單獨啟用訪問控制管理和權限評估：

* 如果模組具有一個或多個可建立CUG的支援路徑，則啟用訪問控制管理
* 僅當選項時才啟用權限評估 **已啟用CUG評估** 的上界。

在CUG策AEM略的新預設設定評估中，它僅使用「publish」運行模式啟用。 請參閱 [自AEM6.3以來的預設配置](#default-configuration-since-aem) 的子菜單。 這可以通過將給定路徑的有效策略與儲存在內容中的策略進行比較來驗證。 只有在啟用CUG的權限評估時才顯示有效策略。

如上所述，CUG訪問控制策略現在始終儲存在內容中，但只有在強制執行對由這些策略產生的有效權限的評估時 **已啟用CUG評估** 在Apache Jackrabbit Oak的系統控制台中開啟 **CUG配置。** 預設情況下，僅使用「publish」運行模式啟用它。

### 與身份驗證的區別 {#differences-with-regards-to-authentication}

下面介紹了與身份驗證有關的差異。

#### 用於認證要求的專用混合類型 {#dedicated-mixin-type-for-authentication-requirement}

在前一個實現中，CUG的授權和認證都由一個JCR屬性觸發( `cq:cugEnabled`)。 就身份驗證而言，這會生成與Apache Sling Authenticator實現一起儲存的身份驗證要求的更新清單。 通過新的實現，通過用專用混合類型標籤目標節點( `granite:AuthenticationRequired`)。

#### 排除登錄路徑的屬性 {#property-for-excluding-login-path}

混合類型定義一個名為的可選屬性 `granite:loginPath`，這基本上與 `cq:cugLoginPage` 屬性。 與先前的實現不同，只有當其聲明節點類型是上述混合時，才會尊重登錄路徑屬性。 添加具有該名稱的屬性而不設定混合類型將無效，並且不會向驗證器報告對登錄路徑的新要求或排除。

#### 身份驗證要求的權限 {#privilege-for-authentication-requirement}

添加或刪除混合類型需要 `jcr:nodeTypeManagement` 授予權限。 在上一實施中， `jcr:modifyProperties` 權限用於編輯剩餘屬性。

至 `granite:loginPath` 涉及添加、修改或刪除屬性所需的相同權限。

#### 由混合類型定義的目標節點 {#target-node-defined-by-mixin-type}

在JCR節點上應建立驗證要求，該節點定義要強制登錄的子樹。 如果CUG預期會影響整個樹，AEM則這可能是一個頁面，而新實現的UI將因此在頁面節點上添加身份驗證要求混合類型。

將CUG策略僅放置在給定頁面下方的jcr:content節點，將僅限制對內容的訪問，但不會影響頁面節點本身或任何子頁面。

這可能是一個有效的方案，並且對於允許將混合放在任何節點的儲存庫編輯器是可能的。 但是，該行為與以前的實現形成了對比，在前者中，將cq:cugEnabled或cq:cugLoginPage屬性放置在jcr:content節點上，最終被內部重新映射到頁面節點。 不再執行此映射。

#### 已配置支援的路徑 {#configured-supported-paths}

都 `granite:AuthenticationRequired` mixin類型和granite:loginPath屬性只在由組定義的範圍內受到尊重 **支援的路徑** 配置選項 **Adobe花崗岩認證要求和登錄路徑處理程式**。 如果未指定路徑，則完全禁用身份驗證要求功能。 在這種情況下，在添加或設定給定JCR節點時，混合類型或屬性將生效。

### JCR內容、OSGi服務和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

下面的文檔提供了舊實施和新實施之間OSGi服務、配置和儲存庫內容的全面映射。

自6.3AEM以來的CUG映射

[取得檔案](assets/cug-mapping.pdf)

## 升級CUG {#upgrade-cug}

### 使用已棄用的CUG的現有安裝 {#existing-installations-using-the-deprecated-cug}

舊的CUG支援實現已棄用，將在將來的版本中刪除。 建議在從6.3版以前的版本升級時，移AEM動到新實施。

對於升AEM級安裝，必須確保只啟用一個CUG實施。 新的和舊的、不建議使用的CUG支援的組合未經測試，並且可能導致不希望的行為：

* Sling Authenticator中與身份驗證要求的衝突
* 當與舊CUG關聯的ACL設定與新CUG策略衝突時，拒絕讀取訪問。

### 遷移現有CUG內容 {#migrating-existing-cug-content}

Adobe為遷移到新的CUG實施提供了工具。 要使用它，請執行以下步驟：

1. 轉到 `https://<serveraddress>:<serverport>/system/console/cug-migration` 的雙曲餘切值。
1. 輸入要檢查CUG的根路徑，然後按 **執行乾式運行** 按鈕 這將掃描所選位置中符合轉換條件的CUG。
1. 查看結果後，按 **執行遷移** 按鈕以遷移到新實施。

>[!NOTE]
>
>如果遇到問題，可以在 **調試** 級別 `com.day.cq.auth.impl.cug` 獲取遷移工具的輸出。 請參閱 [記錄](/help/sites-deploying/configure-logging.md) 的子菜單。
