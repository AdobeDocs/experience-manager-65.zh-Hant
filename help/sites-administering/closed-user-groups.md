---
title: AEM 中的封閉使用者群組
description: 了解封閉式使用者群組，以及這些群組為AEM的擴充性和安全性帶來的優勢。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '6654'
ht-degree: 0%

---

# AEM 中的封閉使用者群組{#closed-user-groups-in-aem}

## 簡介 {#introduction}

自AEM 6.3開始，已推出新的封閉使用者群組實作，旨在解決現有實作帶來的效能、擴充性和安全性問題。

>[!NOTE]
>
>為了簡單起見，本檔案全程使用CUG縮寫。

新實作的目標是在必要時涵蓋現有功能，同時解決舊版本的問題和設計限制。 結果會產生具有下列特性的新CUG設計：

* 身份驗證和授權元素的明確分離，可單獨或組合使用；
* 專屬授權模型，可反映已設定之CUG樹狀結構的受限讀取存取權，而不會干擾其他存取控制設定和許可權需求；
* 將編寫執行個體所需的受限讀取存取權的存取控制設定，與僅發佈時所需的許可權評估分開；
* 編輯受限制的讀取存取權而不提升許可權；
* 專用的節點型別延伸以標示驗證需求；
* 與驗證需求相關聯的選擇性登入路徑。

### 新的自訂使用者群組實作 {#the-new-custom-user-group-implementation}

在AEM中稱為CUG，其包含下列步驟：

* 限制必須保護的樹狀結構上的讀取存取權，並只允許讀取在特定CUG執行個體中列出或完全從CUG評估中排除的主參與者。 這稱為&#x200B;**授權**&#x200B;專案。
* 強制驗證指定的樹狀結構，並選擇性地指定該樹狀結構的專用登入頁面，然後排除該頁面。 這稱為&#x200B;**驗證**&#x200B;專案。

新實作的設計目的是在驗證和授權元素之間畫出一條線。 自AEM 6.3起，您可以限制讀取存取權，而不明確新增驗證需求。 例如，如果指定的執行處理完全需要驗證，或指定的樹狀結構已位於需要驗證的子樹狀結構中。

同樣地，指定樹狀結構可標示驗證需求，而不需變更有效的許可權設定。 組合和結果列在[組合CUG原則與驗證需求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)區段中。

## 概觀 {#overview}

### 授權：限制讀取存取權 {#authorization-restricting-read-access}

CUG的主要功能是限制內容存放庫中指定樹狀結構的讀取存取權，僅限選取的主參與者以外的所有人。 新實作不會即時操控預設存取控制內容，而是會透過定義代表CUG的專屬存取控制原則型別採取不同方法。

#### CUG的存取控制政策 {#access-control-policy-for-cug}

這種新型別的原則具有以下特性：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy型別的存取控制原則（由Apache Jackrabbit API定義）；
* PrincipalSetPolicy授予許可權給可修改的主體集；
* 授與的許可權和原則的範圍是實作詳細資訊。

用於表示CUG的PrincipalSetPolicy實作還定義了：

* CUG政策僅授予一般JCR專案的讀取存取權（例如，排除存取控制內容）；
* 範圍由存取CUG原則的控制節點定義；
* CUG原則可以是巢狀的，巢狀的CUG會啟動新的CUG，而不會繼承「父」CUG的主體集；
* 如果已啟用評估，則原則的效果會繼承至整個子樹狀結構，直到下一個巢狀CUG。

這些CUG原則會透過名為oak-authorization-cug的個別授權模組部署至AEM執行個體。 此模組隨附自己的存取控制管理和許可權評估。 換言之，預設的AEM設定會提供Oak內容存放庫設定，該設定結合了多種授權機制。 如需詳細資訊，請參閱Apache Oak檔案上的[此頁面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

在這個複合設定中，新的CUG不會取代附加到目標節點的現有存取控制內容。 相反地，這是一種補充資料，稍後也可以移除，而不會影響原始存取控制，預設情況下，AEM中的會是一個存取控制清單。

相較於前者，新的CUG政策一律會被辨識及視為存取控制內容。 這表示它們是使用JCR存取控制管理API建立和編輯的。 如需詳細資訊，請參閱[管理CUG原則](#managing-cug-policies)區段。

#### CUG原則的許可權評估 {#permission-evaluation-of-cug-policies}

除了CUG的專用存取控制管理外，新的授權模型可讓您有條件地啟用其原則的許可權評估。 這可讓您在中繼環境中設定CUG原則，並且只允許在複製到生產環境後評估有效許可權。

CUG原則的許可權評估以及與預設或任何其他授權模型的互動，遵循為Apache Jackrabbit Oak中的多個授權機制設計的模式。 也就是說，若且唯若所有模型都授予存取權時，才授予一組特定許可權。 如需詳細資訊，請參閱[Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

下列特性適用於與授權模型相關的許可權評估，這些授權模型設計用來處理和評估CUG原則：

* 它只會處理一般節點和屬性的讀取許可權，不會讀取存取控制內容
* 它不處理寫入許可權或修改受保護JCR內容所需的任何型別的許可權（存取控制、節點型別資訊、版本設定、鎖定或使用者管理等等）。 這些許可權不受CUG原則影響，也不會由關聯的授權模型評估。 這些許可權是否授予，取決於安全性設定中所設定的其他模型。

單一CUG原則對許可權評估的影響可概括如下：

* 除了包含原則中所列排除的主體或主體之外的所有人，其讀取存取權都會遭到拒絕；
* 此原則會在儲存原則及其屬性的存取控制節點上生效；
* 該效果也會沿階層向下繼承，即由存取控制節點定義的專案樹狀結構；
* 但是，它不會影響存取控制節點的同層級或祖項；
* 指定CUG的繼承會在巢狀CUG停止。

#### 最佳做法 {#best-practices}

下列最佳實務應說明如何定義透過CUG的限制讀取存取權：

* 針對您對CUG的需求是否與限制讀取存取權或驗證需求相關，做出清醒的決定。 如果是後者，或同時需要兩者，請參閱最佳實務區段，以取得驗證需求的詳細資訊
* 為必須保護的資料或內容建立威脅模型，以識別威脅範圍，並清楚瞭解資料的敏感度以及與授權存取相關的角色
* 為存放庫內容和CUG建模，以掌握一般授權相關層面和最佳實務：

   * 請記住，只有在特定CUG以及設定授權中部署的其他模組評估允許特定主題讀取特定存放庫專案時，才會授予讀取許可權
   * 避免建立讀取存取權已受其他授權模組限制的備援CUG
   * 對巢狀CUG的過度需求可能會突顯內容設計中的問題
   * 對CUG的需求過度（例如，在每個頁面上）可能表示需要自訂授權模式，可能更適合應用程式和手頭內容的特定安全性需求。

* 將CUG原則支援的路徑限制在存放庫中的幾個樹狀結構，以便獲得最佳效能。 例如，自AEM 6.3起，僅允許將/content節點底下的CUG作為預設值出貨。
* CUG原則的設計目的，是要授予一小部分主體的讀取存取權。 大量主體的需求可能會突顯內容或應用程式設計中的問題，因此應重新考慮。

### 驗證：定義驗證需求 {#authentication-defining-the-auth-requirement}

CUG功能的認證相關部分可讓您標籤需要認證的樹狀結構，並選擇性地指定專用登入頁面。 根據舊版，新的實作可讓您在內容存放庫中標籤需要驗證的樹狀結構。 它也會有條件地啟用與`Sling org.apache.sling.api.auth.Authenticator`的同步處理，負責最終強制要求並重新導向至登入資源。

這些需求是由提供`sling.auth.requirements`註冊屬性的OSGi服務向驗證者註冊。 這些屬性接著可用來動態擴充驗證需求。 如需詳細資訊，請參閱[Sling檔案](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用專用的Mixin型別定義驗證需求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

基於安全理由，新實作會以名稱為`granite:AuthenticationRequired`的專用mixin型別取代剩餘JCR屬性的使用，該型別為登入路徑`granite:loginPath`定義型別為STRING的單一選擇性屬性。 只有與此mixin型別相關的內容變更，才會導致在Apache Sling Authenticator中註冊的要求更新。 在保留任何暫時性修改時會追蹤修改，因此需要`javax.jcr.Session.save()`呼叫才能生效。

同樣適用於`granite:loginPath`屬性。 只有當它是由驗證需求相關的mixin型別定義時，才會被遵守。 在非結構化JCR節點中新增具有此名稱的剩餘屬性不會顯示所需的效果，並且負責更新OSGi註冊的處理常式會忽略該屬性。

>[!NOTE]
>
>設定登入路徑屬性是選擇性的，而且只有在需要驗證的樹狀結構無法回覆為預設或以其他方式繼承的登入頁面時才需要。 請參閱下方的[登入路徑評估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling驗證者註冊驗證需求和登入路徑 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由於此型別的驗證需求應限製為某些執行模式，以及內容存放庫中的一小部分樹狀結構，因此追蹤需求mixin型別和登入路徑屬性是有條件的。 而且，它繫結到定義受支援路徑的對應配置（請參閱下面的配置選項）。 因此，只有這些支援路徑範圍內的變更才會觸發OSGi註冊的更新，其他地方mixin型別和屬性都會被忽略。

預設的AEM設定現在可允許以製作執行模式設定mixin，但只有在複製到發佈執行個體時才會生效，藉以使用此設定。 請參閱[Sling驗證 — 架構](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)檔案，以瞭解Sling如何強制執行驗證要求的詳細資訊。

在設定的支援路徑中新增`granite:AuthenticationRequired` mixin型別，會導致負責處理常式的OSGi註冊被更新，包含具有`sling.auth.requirements`屬性的新增、其他專案。 如果指定的驗證需求指定了選用的`granite:loginPath`屬性，則值也會向驗證器註冊，且具有&#39;-&#39;前置詞，以排除驗證需求。

#### 驗證需求的評估與繼承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling驗證需求會透過頁面或節點階層繼承。 繼承和評估驗證需求（例如順序和優先順序）的詳細資訊會被視為實施詳細資訊，而不會記錄在本文中。

#### 登入路徑評估 {#evaluation-of-login-path}

評估登入路徑並在驗證時重新導向至對應資源，是Adobe Granite登入選擇器驗證處理常式( `com.day.cq.auth.impl.LoginSelectorHandler`)的實作詳細資料，這是預設透過AEM設定的Apache Sling AuthenticationHandler。

在呼叫`AuthenticationHandler.requestCredentials`時，此處理常式會嘗試判斷將使用者重新導向到的對應登入頁面。 此工作流程包含下列步驟：

* 區分過期密碼和需要定期登入作為重新導向的原因；
* 如果是定期登入，會測試是否可依下列順序取得登入路徑：

   * 從由新`com.adobe.granite.auth.requirement.impl.RequirementService`實作的LoginPathProvider，
   * 舊有已棄用的CUG實作，
   * 從登入頁面對應（如`LoginSelectorHandler`所定義），
   * 最後，依與`LoginSelectorHandler`的定義回覆至預設登入頁面。

* 透過上述呼叫取得有效的登入路徑時，使用者的請求會重新導向至該頁面。

本檔案的目標是評估內部`LoginPathProvider`介面所公開的登入路徑。 自AEM 6.3之後發行的實作行為如下：

* 登入路徑的註冊取決於區分過期密碼和需要定期登入作為重新導向的原因
* 若為一般登入，會測試登入路徑是否可依下列順序取得：

   * 從`LoginPathProvider` （由新的`com.adobe.granite.auth.requirement.impl.RequirementService`實作），
   * 舊有已棄用的CUG實作，
   * 從以`LoginSelectorHandler`定義的登入頁面對應，
   * 最後回復到以`LoginSelectorHandler`定義的預設登入頁面。

* 透過上述呼叫取得有效的登入路徑時，使用者的請求會重新導向至該頁面。

由Granite中新的驗證需求支援實作的`LoginPathProvider`會公開由`granite:loginPath`屬性定義的登入路徑，這些屬性又由如上所述的mixin型別定義。 儲存登入路徑的資源路徑與屬性值本身的對應會保留在記憶體中，並會評估為階層中的其他節點尋找合適的登入路徑。

>[!NOTE]
>
>評估只會針對與位於已設定支援路徑中的資源相關聯的請求執行。 對於任何其他請求，將會評估判斷登入路徑的替代方法。

#### 最佳做法 {#best-practices-1}

定義驗證需求時，應考量下列最佳實務：

* 避免巢狀驗證需求：在樹狀結構開頭放置單一驗證需求標籤，應該就足夠了，並且可以繼承至目標節點定義的整個子樹狀結構。 在評估Apache Sling中的驗證需求時，應該將該樹狀結構中的其他驗證需求視為備援，可能會導致效能問題。 透過將授權和驗證相關的CUG區域分離，可以限制CUG或其他型別原則的讀取存取權，同時強制整個樹狀結構的驗證。
* 為存放庫內容建模，使得驗證需求適用於整個樹狀結構，而無需再次從需求中排除巢狀子樹狀結構。
* 若要避免指定，然後註冊多餘的登入路徑，請執行下列動作：

   * 依賴繼承並避免定義巢狀登入路徑
   * 請勿將選擇性登入路徑設為對應至預設值或繼承值的值，
   * 應用程式開發人員應識別在與`LoginSelectorHandler`關聯的全域登入路徑設定（預設和對應）中應設定哪些登入路徑。

## 在存放庫中的表示方式 {#representation-in-the-repository}

### 存放庫中的CUG原則表示 {#cug-policy-representation-in-the-repository}

Oak檔案說明新的CUG政策在存放庫內容中的反映方式。 如需詳細資訊，請參閱有關使用CUG管理存取許可權的[Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存放庫中的驗證需求 {#authentication-requirement-in-the-repository}

將專用mixin節點型別放置在目標節點的存放庫內容中，會反映需要單獨的驗證要求。 mixin型別會定義選擇性屬性，以指定目標節點所定義之樹狀結構的專用登入頁面。

與登入路徑相關聯的頁面可能位於該樹狀結構內部或外部。 它被排除在驗證需求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG原則和驗證需求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG政策 {#managing-cug-policies}

使用JCR存取控制管理API來管理限制CUG讀取存取的新型別的存取控制原則，並遵循[JCR 2.0規格](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)所述的機制。

#### 設定新的CUG政策 {#set-a-new-cug-policy}

此程式碼可在之前未設定CUG的節點套用新的CUG原則。 請注意，`getApplicablePolicies`只會傳回之前未設定的新原則。 最後，必須回寫原則並保留變更。

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 編輯現有的CUG原則 {#edit-an-existing-cug-policy}

編輯現有CUG原則需要下列步驟。 必須回寫修改的原則，而且必須使用`javax.jcr.Session.save()`保留變更。

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

### 擷取有效的CUG原則 {#retrieve-effective-cug-policies}

JCR存取控制管理會定義最大努力方法，以擷取在指定路徑生效的原則。 因為評估CUG原則是有條件的，而且取決於要啟用的對應組態，所以呼叫`getEffectivePolicies`是驗證指定的CUG原則是否在指定的安裝中生效的便利方式。

>[!NOTE]
>
>`getEffectivePolicies`和後續程式碼範例之間的差異，這些程式碼範例會向上檢視階層以尋找給定路徑是否已是現有CUG的一部分。

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

#### 擷取繼承的CUG原則 {#retrieve-inherited-cug-policies}

尋找已在指定路徑定義的所有巢狀CUG，無論其是否生效。 如需詳細資訊，請參閱[組態選項](/help/sites-administering/closed-user-groups.md#configuration-options)區段。

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

#### 依主體管理CUG原則 {#managing-cug-policies-by-pincipal}

`JackrabbitAccessControlManager`所定義的擴充功能可讓您編輯主要專案的存取控制原則，但並未以CUG存取控制管理實作，因為根據定義，CUG原則一律會影響所有主要專案：列示於`PrincipalSetPolicy`的專案會被授與讀取存取權，而所有其他主要專案則會被禁止讀取目標節點所定義的樹狀結構中的內容。

對應方法一律會傳回空的原則陣列，但不會擲回例外狀況。

### 管理驗證需求 {#managing-the-authentication-requirement}

新驗證需求的建立、修改或移除是透過變更目標節點的有效節點型別來實現的。 然後，您可使用一般JCR API來寫入選用的登入路徑屬性。

>[!NOTE]
>
>如果已經設定`RequirementHandler`，而且目標包含在由支援的路徑所定義的樹狀結構中（請參閱設定選項區段），則上述對指定目標節點的修改只會反映在Apache Sling驗證程式上。
>
>如需詳細資訊，請參閱[指派Mixin節點型別]&#x200B;(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3指派Mixin節點型別)和[新增節點及設定屬性]&#x200B;(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4新增節點及設定屬性)

#### 新增驗證需求 {#adding-a-new-auth-requirement}

建立驗證需求的步驟詳述如下。 只有在已針對包含目標節點的樹狀結構設定`RequirementHandler`時，才會向Apache Sling驗證器登入需求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登入路徑新增驗證需求 {#add-a-new-auth-requirement-with-login-path}

建立包含登入路徑的驗證要求的步驟。 登入路徑的需要和排除只有在包含目標節點的樹狀結構已設定`RequirementHandler`時，才會向Apache Sling驗證器註冊。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改現有登入路徑 {#modify-an-existing-login-path}

變更現有登入路徑的步驟詳述如下。 只有為包含目標節點的樹狀結構設定了`RequirementHandler`時，修改才會向Apache Sling驗證器註冊。 先前的登入路徑值會從註冊中移除。 此修改不會影響與目標節點相關聯的驗證需求。

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

#### 移除現有的登入路徑 {#remove-an-existing-login-path}

移除現有登入路徑的步驟。 只有在已針對包含目標節點的樹狀結構設定`RequirementHandler`時，登入路徑專案才會從Apache Sling驗證程式取消註冊。 與目標節點相關聯的驗證需求不受影響。

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

或者，您也可以使用下列方法來達到相同目的：

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

移除現有驗證需求的步驟。 只有在已針對包含目標節點的樹狀結構設定`RequirementHandler`時，才會從Apache Sling驗證程式取消登入要求。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 擷取有效的驗證需求 {#retrieve-effective-auth-requirements}

沒有專用的公用API可讀取在Apache Sling Authenticator註冊的所有有效驗證需求。 但是，清單在`https://<serveraddress>:<serverport>/system/console/slingauth`的系統主控台中於&quot;**驗證需求組態**&quot;區段下公開。

下圖顯示具有示範內容的AEM發佈執行個體的驗證需求。 社群頁面醒目提示的路徑說明本檔案中說明的實作新增的需求如何反映在Apache Sling驗證器中。

>[!NOTE]
>
>在此範例中，未設定選用的登入路徑屬性。 因此，沒有向驗證者註冊第二個專案。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 擷取有效登入路徑 {#retrieve-the-effective-login-path}

目前沒有公用API可擷取匿名存取需要驗證的資源時生效的登入路徑。 如需如何擷取登入路徑的實作詳細資訊，請參閱登入路徑評估區段。

但請注意，除了此功能定義的登入路徑之外，還有其他方法可指定重新導向至登入，在設計內容模型和特定AEM安裝的驗證需求時，應將這些方法列入考量。

#### 擷取繼承的驗證需求 {#retrieve-the-inherited-auth-requirement}

就像登入路徑一樣，沒有公用API可擷取內容中定義的繼承驗證需求。 下列範例說明如何列出已使用指定階層定義的所有驗證需求，無論其是否生效。 如需詳細資訊，請參閱[組態選項](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>對於驗證需求和登入路徑，建議依賴繼承機制，並避免建立巢狀驗證需求。
>
>如需詳細資訊，請參閱[驗證需求的評估與繼承](#evaluation-and-inheritance-of-the-authentication-requirement)、[登入路徑的評估](#evaluation-of-login-path)以及[最佳實務](#best-practices)。

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

### 結合CUG政策與驗證需求 {#combining-cug-policies-and-the-authentication-requirement}

下表列出AEM執行個體中，透過設定同時啟用兩個模組的CUG原則及驗證需求的有效組合。

| **需要驗證** | **登入路徑** | **限制的讀取存取權** | **預期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效的許可權評估授予存取權，特定使用者將只能檢視以CUG原則標籤的子樹狀結構。 未經驗證的使用者會重新導向至指定的登入頁面。 |
| 是 | 否 | 是 | 如果有效的許可權評估授予存取權，特定使用者將只能檢視以CUG原則標籤的子樹狀結構。 未經驗證的使用者會重新導向至繼承的預設登入頁面。 |
| 是 | 是 | 否 | 未經驗證的使用者會重新導向至指定的登入頁面。 是否允許檢視以驗證需求標示的樹狀結構，取決於該子樹狀結構中個別專案的有效許可權。 沒有專用的CUG限制讀取存取權。 |
| 是 | 否 | 否 | 未經驗證的使用者會重新導向至繼承的預設登入頁面。 是否允許檢視標示驗證需求的樹狀結構，取決於該子樹狀結構中個別專案的有效許可權。 沒有專用的CUG限制讀取存取權。 |
| 否 | 否 | 是 | 如果有效的許可權評估授權存取，則指定的已驗證或未驗證使用者只能檢視以CUG原則標籤的子樹狀結構。 未驗證的使用者會得到同等對待，且不會重新導向以登入。 |

>[!NOTE]
>
>「驗證需求」=「否」和「登入路徑」=「是」的組合未列出，因為「登入路徑」是與驗證需求相關聯的選擇性屬性。 指定具有該名稱的JCR屬性而不新增定義mixin型別沒有效果，且會被對應的處理常式忽略。

## OSGi元件和設定 {#osgi-components-and-configuration}

本節提供OSGi元件的概觀，以及新CUG實施匯入的個別設定選項。

另請參閱CUG對應檔案，取得新舊實施之間的設定選項完整對應。

### 授權：設定和設定 {#authorization-setup-and-configuration}

新的授權相關零件包含在&#x200B;**Oak CUG Authorization**&#x200B;套件( `org.apache.jackrabbit.oak-authorization-cug`)中，這是AEM預設安裝的一部分。 該套件定義了一個獨立的授權模型，旨在部署為管理讀取存取權的額外方法。

#### 設定CUG授權 {#setting-up-cug-authorization}

在[相關Apache檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)中詳細說明設定CUG授權。 依預設，AEM在所有執行模式中都會部署CUG授權。 在需要不同授權設定的安裝中，也可以使用逐步指示來停用CUG授權。

#### 設定反向連結篩選 {#configuring-the-referrer-filter}

您也必須將[Sling反向連結篩選器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)設定為可用於存取AEM的所有主機名稱；例如，透過CDN、負載平衡器及任何其他專案。

如果未設定反向連結篩選器，則當使用者嘗試登入CUG網站時，會看到類似下列的錯誤：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi元件的特性 {#characteristics-of-osgi-components}

下列兩個OSGi元件已匯入以定義驗證需求並指定專用登入路徑：

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
   <td>專門用於設定和評估CUG許可權的授權設定。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另請參閱下方的<a href="#configuration-options">組態選項</a>。</p> </td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>參照</td>
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
   <td>可讓您從CUG評估中排除具有已設定名稱的主參與者。</td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另請參閱下方的組態選項一節。</p> </td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>參照</td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

#### 設定選項 {#configuration-options}

主要組態選項包括：

* `cugSupportedPaths`：指定可能包含CUG的子樹狀結構。 未設定預設值
* `cugEnabled`：組態選項，可啟用目前CUG原則的許可權評估。

與CUG-authorization模組相關的可用設定選項已列出，並在[Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)中詳細說明。

#### 從CUG評估排除主體 {#excluding-principals-from-cug-evaluation}

先前實作已採用免除個別主參與者進行CUG評估。 新的CUG授權透過名為CugExclude的專用介面來涵蓋此功能。 Apache Jackrabbit Oak 1.4隨附預設實施，其中排除一組固定的主體名稱和可讓您設定個別主體名稱的擴展實施。 後者在AEM發佈執行個體中設定。

根據AEM 6.3的預設值，下列主體不會受到CUG政策的影響：

* 管理主體（管理員使用者、管理員群組）
* 服務使用者主體
* 存放庫內部系統主體

如需詳細資訊，請參閱下方[自AEM 6.3](#default-configuration-since-aem)以來的預設設定一節中的表格。

可以在&#x200B;**Apache Jackrabbit Oak CUG排除清單**&#x200B;之設定區段中的系統主控台中，變更或擴充「管理員」群組的排除。

或者，可以提供並部署CugExclude介面的自訂實作，以在有特殊需求時調整排除的主體集。 如需詳細資訊和實作範例，請參閱[CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)的相關檔案。

### 驗證：設定與組態 {#authentication-setup-and-configuration}

新的驗證相關部分包含在&#x200B;**Adobe Granite驗證處理常式**&#x200B;套件（ `com.adobe.granite.auth.authhandler`版本5.6.48）中。 此套件組合是AEM預設安裝的一部分。

若要設定取代已棄用CUG支援的驗證需求，部分OSGi元件必須在指定的AEM安裝中存在並作用中。 如需詳細資訊，請參閱下方的&#x200B;**OSGi元件的特性**。

>[!NOTE]
>
>由於RequirementHandler的強制組態選項，驗證相關零件只有在透過指定一組支援的路徑來啟用該功能時，才會生效。 在標準AEM安裝中，此功能會在製作執行模式中停用，並在發佈執行模式中啟用/content 。

**OSGi元件的特性**

下列兩個OSGi元件已匯入以定義驗證需求並指定專用登入路徑：

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
   <td>針對影響驗證需求（透過<code>granite:AuthenticationRequirement</code> mixin型別）的內容變更註冊觀察者的驗證需求專用OSGi服務，以及透過的登入路徑會公開給<code>LoginSelectorHandler</code>。 </td>
  </tr>
  <tr>
   <td>組態屬性</td>
   <td>-</td>
  </tr>
  <tr>
   <td>設定原則</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>參照</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 標籤 | Adobe Granite驗證需求和登入路徑處理常式 |
|---|---|
| 說明 | 更新Apache Sling驗證需求和相關聯登入路徑之對應排除的`RequirementHandler`實作。 |
| 組態屬性 | `supportedPaths` |
| 設定原則 | `ConfigurationPolicy.REQUIRE` |
| 參照 | 不適用 |

#### 設定選項 {#configuration-options-1}

CUG重寫的驗證相關部分只隨附與Adobe Granite驗證需求和登入路徑處理常式關聯的單一設定選項：

**「驗證需求和登入路徑處理常式」**

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
   <td>此處理常式遵循驗證要求的路徑。 如果您想要將<code>granite:AuthenticationRequirement</code> mixin型別新增至節點，而不需要強制執行這些節點（例如在作者執行個體上），請將此設定保留為未設定。 如果遺失，則功能會停用。 </td>
  </tr>
 </tbody>
</table>

## AEM 6.3之後的預設設定 {#default-configuration-since-aem}

AEM的新安裝預設會將新的實施用於CUG功能的授權和驗證相關部分。 舊版實作「Adobe Granite封閉使用者群組(CUG)支援」已淘汰，並預設會在所有AEM安裝中停用。 新的實作將改為啟用，如下所示：

### 作者執行個體 {#author-instances}

| **「Apache Jackrabbit Oak CUG設定」** | **說明** |
|---|---|
| 支援的路徑`/content` | CUGpolicies的存取控制管理已啟用。 |
| CUG評估啟用FALSE | 已停用許可權評估。 CUG政策無效。 |
| 排名\|200 | 請參閱Oak檔案。 |

>[!NOTE]
>
>預設的編寫執行個體上沒有&#x200B;**Apache Jackrabbit Oak CUG排除清單**&#x200B;和&#x200B;**Adobe Granite驗證需求和登入路徑處理常式**&#x200B;的設定。

### 發佈執行個體 {#publish-instances}

| **「Apache Jackrabbit Oak CUG設定」** | **說明** |
|---|---|
| 支援的路徑`/content` | 在設定的路徑下方啟用CUG原則的存取控制管理。 |
| CUG評估啟用TRUE | 已針對設定的路徑啟用許可權評估。 CUG原則會在`Session.save()`生效。 |
| 排名\|200 | 請參閱Oak檔案。 |

| **「Apache Jackrabbit Oak CUG排除清單」** | **說明** |
|---|---|
| 主體名稱管理員 | 排除CUG評估中的管理員主體。 |

| **&quot;Adobe Granite驗證需求和登入路徑處理常式&quot;** | **說明** |
|---|---|
| 支援的路徑`/content` | 由`granite:AuthenticationRequired` mixin型別在存放庫中定義的驗證需求於`/content`在`Session.save()`以下生效。 Sling驗證器已更新。 在支援的路徑之外新增mixin型別會被忽略。 |

## 停用CUG授權與驗證需求 {#disabling-cug-authorization-and-authentication-requirement}

如果指定的安裝未使用CUG或使用不同的驗證和授權方式，則新實作可能會完全停用。

### 停用CUG授權 {#disable-cug-authorization}

如需有關如何從複合授權設定中移除CUG授權模型的詳細資訊，請參閱[CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)檔案。

### 停用驗證需求 {#disable-the-authentication-requirement}

若要停用`granite.auth.authhandler`模組所提供的驗證需求支援，只要移除與&#x200B;**Adobe Granite驗證需求和登入路徑處理常式**&#x200B;相關聯的組態就足夠了。

>[!NOTE]
>
>但是請注意，移除設定將不會取消註冊mixin型別，這仍然適用於節點而不會生效。

## 與其他模組的互動 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

為了反映CUG授權模型使用的新型別的存取控制政策，Apache Jackrabbit定義的API已擴充。 因為`jackrabbit-api`模組的2.11.0版定義了一個名為`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新介面，從`javax.jcr.security.AccessControlPolicy`延伸。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

已調整Apache Jackrabbit FileVault的匯入機制，以處理型別`PrincipalSetPolicy`的存取控制原則。

### Apache Sling內容發佈 {#apache-sling-content-distribution}

請參閱上述[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)區段。

### Adobe Granite復寫 {#adobe-granite-replication}

復寫模組已稍微調整，以便能夠在不同的AEM執行個體之間復寫CUG原則：

* `DurboImportConfiguration.isImportAcl()`會逐字解譯，只會影響實作`javax.jcr.security.AccessControlList`的存取控制原則

* `DurboImportTransformer`只會對真正的ACL遵守此設定
* CUG授權模型所建立的其他原則（例如`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`執行個體）一律會被復寫，且組態選項`DurboImportConfiguration.isImportAcl`()將被忽略。

複製CUG政策有一個限制。 如果未移除對應的mixin節點型別`rep:CugMixin,`就移除指定的CUG原則，則復寫時將不會反映移除。 原則移除後，一律移除mixin即可解決此問題。 不過，如果手動新增mixin型別，則可能會顯示此限制。

### Adobe Granite驗證處理常式 {#adobe-granite-authentication-handler}

**套件組合隨附的驗證處理常式** Adobe Granite HTTP Header Authentication Handler`com.adobe.granite.auth.authhandler`包含相同模組所定義`CugSupport`介面的參考。 在特定情況下，它可用來計算「範圍」，並歸入使用處理常式設定的範圍。

此設定已經過調整，以使`CugSupport`的參考成為選用，以便在指定設定決定重新啟用已棄用的實作時，確保最大的回溯相容性。 使用實作的安裝將不會再從CUG實作中擷取領域，但將一律顯示使用&#x200B;**Adobe Granite HTTP標頭驗證處理常式**&#x200B;定義的領域。

>[!NOTE]
>
>根據預設，**Adobe Granite HTTP Header驗證處理常式**&#x200B;僅設定於發佈執行模式，並啟用「停用登入頁面」( `auth.http.nologin`)選項。

### AEM LiveCopy {#aem-livecopy}

使用LiveCopy設定CUG時，在存放庫中會以新增一個額外節點和一個額外屬性的方式表示，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

這兩個元素都是在`cq:Page`下建立。 使用目前的設計，MSM只會處理`cq:PageContent` (`jcr:content`)節點下的節點和屬性。

因此，CUG群組無法從Blueprint轉出至即時副本。 設定即時副本時，請對此進行規劃。

## 新CUG實作的變更 {#changes-with-the-new-cug-implementation}

本節旨在提供對CUG功能所做變更的概述，以及舊實作與新實作的比較。 其中列出影響CUG支援設定方式的變更，並說明CUG在存放庫內容中的管理方式及管理者。

### CUG設定和設定的差異 {#differences-in-cug-setup-and-configuration}

已棄用的OSGi元件&#x200B;**Adobe Granite Closed User Group (CUG)支援** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已由新元件取代，以便能夠分別處理以前CUG功能的授權和驗證相關部分。

## 管理存放庫內容中CUG的差異 {#differences-in-managing-cugs-in-the-repository-content}

以下各節從實作和安全性角度說明舊實作與新實作之間的差異。 雖然新實施旨在提供相同的功能，但在使用新CUG時需瞭解一些重要的細微變更。

### 與授權相關的差異 {#differences-with-regards-to-authorization}

授權視角的主要差異概述於以下清單：

CUG的&#x200B;**專用存取控制內容**

在舊版實作中，預設授權模型用於操控發佈上的存取控制清單原則，以CUG強制執行的設定取代任何現有的ACE。 觸發此問題的原因是寫入了在發佈時解譯的規則剩餘JCR屬性。

在新實作中，預設授權模型的存取控制設定不受任何建立、修改或移除的CUG影響。 而是將名為`PrincipalSetPolicy`的新原則型別套用為目標節點的額外存取控制內容。 此額外原則位於目標節點的子節點中，如果存在，則為預設原則節點的同層級。

**在存取控制管理中編輯CUG原則**

這種從剩餘JCR屬性到專用存取控制政策的移動會影響建立或修改CUG功能的授權部分所需的許可權。 由於這被視為存取控制內容的修改，因此需要將`jcr:readAccessControl`和`jcr:modifyAccessControl`許可權寫入存放庫。 因此，只有有權修改頁面存取控制內容的內容作者才能設定或修改此內容。 這與舊版實作形成對比，舊版實作中寫入一般JCR屬性的能力已足夠，導致許可權提升。

**由原則**&#x200B;定義的目標節點

在JCR節點建立CUG原則，定義要接受受限讀取存取的子樹狀結構。 這可能是個AEM頁面，以防CUG可能影響整個樹狀結構。

將CUG原則僅放置在位於指定頁面下方的jcr:content節點上，只會限制對指定頁面內容s.str的存取，而不會對任何同級頁面或子頁面生效。 這可能是有效的使用案例，並且可以使用存放庫編輯器來完成，該編輯器可讓您套用精細存取內容。 不過，它與先前實作不同，在先前實作中，將cq:cugEnabled屬性放置在jcr:content節點上，已在內部重新對應到頁面節點。 不再執行此對應。

使用CUG原則進行&#x200B;**許可權評估**

從舊的CUG支援移至其他授權模型，會變更有效讀取許可權的評估方式。 如[Jackrabbit檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)所述，只有在Oak存放庫中設定的所有模型許可權評估授與讀取存取權時，允許檢視`CUGcontent`的指定主體才會被授與讀取存取權。

換句話說，為了評估有效許可權，`CUGPolicy`和預設存取控制專案都會被考慮，而且只有在這兩種原則都授與的情況下，才會授與CUG內容的讀取存取權。 在預設AEM發佈安裝中，其中向所有人授予完整`/content`樹狀結構的讀取存取權，CUG政策的效果與舊實作相同。

**隨選評估**

CUG授權模型可讓您個別開啟存取控制管理和許可權評估：

* 如果模組有一或多個可建立CUG的支援路徑，則會啟用存取控制管理
* 只有同時核取選項&#x200B;**CUG Evaluation Enabled**&#x200B;時，才會啟用許可權評估。

在新的AEM預設設定CUG原則評估中，它僅在「發佈」執行模式中啟用。 如需詳細資訊，請參閱AEM 6.3[之後的](#default-configuration-since-aem)預設設定。 這可透過比較給定路徑的有效原則與內容中儲存的原則來驗證。 只有啟用CUG的許可權評估時，才會顯示有效原則。

如上所述，CUG存取控制原則現在一律會儲存在內容中，但是只有在Apache Jackrabbit Oak **CUG組態的系統主控台中開啟**&#x200B;啟用CUG評估&#x200B;**時，才會強制執行這些原則所產生的有效許可權評估。**&#x200B;依預設，它僅以&#39;publish&#39;執行模式啟用。

### 與驗證相關的差異 {#differences-with-regards-to-authentication}

關於驗證的差異如下所述。

#### 驗證需求的專用Mixin型別 {#dedicated-mixin-type-for-authentication-requirement}

在之前的實作中，CUG的授權和驗證層面都是由單一JCR屬性( `cq:cugEnabled`)觸發。 就驗證而言，這會產生與Apache Sling Authenticator實作儲存的驗證需求更新清單。 使用新的實作時，以專用的mixin型別( `granite:AuthenticationRequired`)標籤目標節點可獲得相同的結果。

#### 排除登入路徑的屬性 {#property-for-excluding-login-path}

mixin型別定義了一個稱為`granite:loginPath`的選擇性屬性，基本上與`cq:cugLoginPage`屬性對應。 相較於先前的實作，只有當其宣告節點型別是上述的mixin時，才會考量登入路徑屬性。 在不設定mixin型別的情況下新增具有該名稱的屬性不會產生任何效果，並且不會向驗證者報告針對登入路徑的新要求或排除。

#### 驗證要求的許可權 {#privilege-for-authentication-requirement}

新增或移除mixin型別需要授予`jcr:nodeTypeManagement`許可權。 在上一個實作中，`jcr:modifyProperties`許可權是用來編輯剩餘屬性。

就`granite:loginPath`而言，新增、修改或移除屬性需要相同的許可權。

#### 由Mixin型別定義的目標節點 {#target-node-defined-by-mixin-type}

在JCR節點建立驗證需求，定義要強制登入的子樹狀結構。 這可能是個AEM頁面，以防CUG可能影響整個樹狀結構，以及新實作的UI，因此會在頁面節點上新增驗證需求mixin型別。

僅將CUG原則置於指定頁面下方的jcr:content節點只會限制內容的存取權。 但是，它不會影響頁面節點本身或任何子頁面。

這可能是有效的案例，並且可在存放庫編輯器中讓您將mixin放置在任何節點上。 不過，此行為與之前的實作不同，也就是將cq:cugEnabled或cq:cugLoginPage屬性放置在jcr:content節點上，最終在內部重新對應到頁面節點。 不再執行此對應。

#### 已設定的支援路徑 {#configured-supported-paths}

`granite:AuthenticationRequired` mixin型別和Granite:loginPath屬性都只能在&#x200B;**Adobe Granite驗證需求和登入路徑處理常式**&#x200B;的&#x200B;**支援路徑**&#x200B;組態選項集所定義的範圍內接受。 如果未指定路徑，則會完全停用驗證需求功能。 在這種情況下，將mixin型別或屬性新增或設定到給定JCR節點時會生效。

### JCR內容、OSGi服務和設定的對應 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下檔案提供舊實作與新實作之間的OSGi服務、設定和存放庫內容的完整對應。

AEM 6.3之後的CUG對應

[取得檔案](assets/cug-mapping.pdf)

## 升級CUG {#upgrade-cug}

### 使用已棄用CUG的現有安裝 {#existing-installations-using-the-deprecated-cug}

舊的CUG支援實作已淘汰，並將在未來版本中移除。 從AEM 6.3之前的版本升級時，建議改用新的實作。

對於升級的AEM安裝，請務必確保僅啟用一個CUG實作。 新的和舊的、已棄用的CUG支援組合未經測試，並可能會導致不良行為：

* Sling驗證器中有關驗證需求的衝突
* 當與舊CUG相關聯的ACL設定與新CUG原則衝突時，拒絕讀取存取權。

### 移轉現有的CUG內容 {#migrating-existing-cug-content}

Adobe提供了移轉至新CUG實作的工具。 若要使用，請執行下列步驟：

1. 移至`https://<serveraddress>:<serverport>/system/console/cug-migration`以存取工具。
1. 輸入您要檢查CUG的根路徑，然後按&#x200B;**執行試執行**&#x200B;按鈕。 這會在選取的位置中掃描符合轉換條件的CUG。
1. 檢閱結果後，請按&#x200B;**執行移轉**&#x200B;按鈕以移轉到新的實作。

>[!NOTE]
>
>如果您遇到問題，可以在&#x200B;**上的** DEBUG`com.day.cq.auth.impl.cug`層級設定特定記錄器，以取得移轉工具的輸出。 請參閱[記錄](/help/sites-deploying/configure-logging.md)以瞭解如何執行此動作的詳細資訊。
