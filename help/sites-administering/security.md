---
title: 使用者管理與安全性
seo-title: 使用者管理與安全性
description: 了解AEM中的使用者管理與安全性。
seo-description: 了解AEM中的使用者管理與安全性。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: 安全性
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '5488'
ht-degree: 1%

---

# 用戶管理和安全性{#user-administration-and-security}

本章介紹如何配置和維護用戶授權，並介紹身份驗證和授權在AEM中如何工作的理論。

## AEM {#users-and-groups-in-aem}中的使用者和群組

本節將更詳細地介紹各種實體和相關概念，以幫助您配置易於維護的用戶管理概念。

### 使用者 {#users}

使用者將使用其帳戶登入AEM。 每個使用者帳戶都是唯一的，並包含基本帳戶詳細資訊以及指派的權限。

使用者通常是群組的成員，可簡化這些權限和/或權限的分配。

### 群組 {#groups}

群組是使用者和/或其他群組的集合；這些都稱為組的成員。

其主要用途是透過減少要更新的實體數量來簡化維護程式，因為對群組所做的變更會套用至群組的所有成員。 群組通常會反映：

* 應用程式內的角色；例如有權衝浪內容的人，或有權貢獻內容的人。
* 您自己的組織；您可能想要擴充角色，以區分內容樹狀結構中不同分支的貢獻者，以及不同部門的貢獻者。

因此，群組傾向於保持穩定，而使用者來來來得更頻繁。

透過規劃和簡潔的結構，群組的使用可反映您的結構，為您提供清楚的概覽和有效的更新機制。

### 內置用戶和組{#built-in-users-and-groups}

AEM WCM會安裝許多使用者和群組。 安裝後第一次存取安全控制台時，就會看到這些。

下表列出每個項目，並搭配：

* 簡短描述
* 關於必要變更的任何建議

*請變更所有預設密碼* （如果您未在某些情況下刪除帳戶本身）。

<table>
 <tbody>
  <tr>
   <td>使用者 ID</td>
   <td>類型</td>
   <td>說明</td>
   <td>建議</td>
  </tr>
  <tr>
   <td><p>管理員</p> <p>預設密碼：管理員</p> </td>
   <td>使用者</td>
   <td><p>具有完全訪問權限的系統管理帳戶。</p> <p>此帳戶用於AEM WCM和CRX之間的連線。</p> <p>如果您不小心刪除了此帳戶，系統會在重新啟動存放庫時（在預設設定中）重新建立此帳戶。</p> <p>管理帳戶是AEM平台的需求。 因此，無法刪除此帳戶。</p> </td>
   <td><p>Adobe強烈建議將此使用者帳戶的密碼從預設值變更為。</p> <p>最好在安裝時，儘管可以在安裝後完成。</p> <p>注意：此帳戶不應與CQ Servlet引擎的管理帳戶混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>使用者</td>
   <td><p>保留未驗證執行個體存取的預設權限。 預設情況下，這包含最低的存取權限。</p> <p>如果您不小心刪除了此帳戶，則在啟動時會重新建立該帳戶。 無法永久刪除，但可以禁用。</p> </td>
   <td>請避免刪除或停用此帳戶，因為這會對製作執行個體的運作造成負面影響。 如果存在要求您刪除的安全要求，請務必先正確測試它對您的系統的影響。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>預設密碼：作者</p> </td>
   <td>使用者</td>
   <td><p>允許寫入/content的作者帳戶。 包含貢獻者和瀏覽者的權限。</p> <p>可作為網站管理員使用，因為它可以訪問整個/content樹。</p> <p>這不是內建使用者，而是其他geometrixx示範使用者</p> </td>
   <td><p>Adobe建議完全刪除帳戶，或從預設值變更密碼。</p> <p>最好在安裝時，儘管可以在安裝後完成。</p> </td>
  </tr>
  <tr>
   <td>管理員</td>
   <td>群組</td>
   <td><p>授予其所有成員管理員權限的組。 僅允許管理員編輯此組。</p> <p>具有完全訪問權限。</p> </td>
   <td>如果您在節點上設定了「拒絕所有人」，則只有在該組再次啟用時，管理員才具有訪問權限。</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>群組</td>
   <td><p>負責內容編輯的群組。 需要讀取、修改、建立和刪除權限。</p> </td>
   <td>只要您新增讀取、修改、建立和刪除權限，即可使用專案特定存取權限建立您自己的內容製作群組。</td>
  </tr>
  <tr>
   <td>貢獻者</td>
   <td>群組</td>
   <td><p>允許用戶寫入內容的基本權限（僅在功能中）。</p> <p>不會為/content樹分配任何權限 — 必須為各個組或用戶專門分配這些權限。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>群組</td>
   <td>典型AEM Assets使用者的現成可用參考群組。 此群組的成員具有適當權限，可啟用資產和集合的上傳/共用。</td>
   <td> </td>
  </tr>
  <tr>
   <td>every</td>
   <td>群組</td>
   <td><p>AEM中的每位使用者都是群組的成員，即使您在所有工具中可能看不到群組或成員關係。</p> <p>可將此群組視為預設權限，因為它可用來套用每個人的權限，甚至是將來建立的使用者。</p> </td>
   <td><p>請勿修改或刪除此群組。</p> <p>修改此帳戶會產生其他安全影響。</p> </td>
  </tr>
  <tr>
   <td>標籤管理員</td>
   <td>群組</td>
   <td>允許編輯標籤的群組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>使用者管理員</td>
   <td>群組</td>
   <td>授權使用者管理，即建立使用者和群組的權利。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流程編輯器</td>
   <td>群組</td>
   <td>允許建立和修改工作流模型的組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流 — 使用者</td>
   <td>群組</td>
   <td><p>參與工作流的用戶必須是組工作流用戶的成員。 這可讓他或她完全存取：/etc/workflow/instances，以便他/她可以更新工作流實例。</p> <p>該組包含在標準安裝中，但您必須手動將用戶添加到組。</p> </td>
  </tr>
 </tbody>
</table>

## AEM {#permissions-in-aem}中的權限

AEM會使用ACL來判斷使用者或群組可採取哪些動作，以及可在何處執行這些動作。

### 權限和ACL {#permissions-and-acls}

權限會定義允許誰對資源執行哪些動作。 權限是[訪問控制](#access-control-lists-and-how-they-are-evaluated)評估的結果。

您可以選取或清除個別AEM [actions](security.md#actions)的核取方塊，以變更授予/拒絕給定使用者的權限。 勾號表示允許執行動作。 無複選標籤表示操作被拒絕。

勾選記號在格線中的位置也代表使用者在AEM內的哪些位置（即哪些路徑）中擁有哪些權限。

### 動作 {#actions}

可在頁面（資源）上執行動作。 對於階層中的每個頁面，您可以指定允許使用者對該頁面採取的動作。 [](#permissions-and-acls) 允許或拒絕動作的權限。

<table>
 <tbody>
  <tr>
   <td><strong>動作 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>讀取</td>
   <td>允許使用者讀取頁面和任何子頁面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>修改頁面上和任何子頁面上的現有內容。</li>
     <li>在頁面上或任何子頁面上建立新段落。</li>
    </ul> <p>在JCR級別，用戶可以通過修改資源的屬性、鎖定、版本設定、nt-modification來修改資源，並且他們對定義jcr:content子節點的節點（例如cq:Page、nt:file、cq:Asset）具有完全寫權限。</p> </td>
  </tr>
  <tr>
   <td>建立</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>建立新頁面或子頁面。</li>
    </ul> <p>如果拒絕<strong>modify</strong>，則會明確排除jcr:content下的子樹，因為建立jcr:content及其子節點被視為頁面修改。 這僅適用於定義jcr:content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>從頁面或任何子頁面中刪除現有段落。</li>
     <li>刪除頁面或子頁面。</li>
    </ul> <p>如果拒絕<strong>modify</strong> ，則會明確排除jcr:content下的任何子樹，作為刪除jcr:content，其子節點將被視為頁面修改。 這僅適用於定義jcr:content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>讀取 ACL</td>
   <td>用戶可以讀取頁面或子頁面的訪問控制清單。</td>
  </tr>
  <tr>
   <td>編輯 ACL</td>
   <td>用戶可以修改頁面或任何子頁面的訪問控制清單。</td>
  </tr>
  <tr>
   <td>複寫</td>
   <td>使用者可將內容複製至其他環境（例如，發佈環境）。 此權限也會套用至任何子頁面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM會自動為[Collections](/help/assets/manage-collections.md)中的角色指派（擁有者、編輯者、檢視者）產生使用者群組。 不過，手動新增這類群組的ACL可能會在AEM中造成安全漏洞。 Adobe建議您避免手動新增ACL。

### 訪問控制清單及其評估方式{#access-control-lists-and-how-they-are-evaluated}

AEM WCM使用存取控制清單(ACL)來組織套用至各種頁面的權限。

「存取控制清單」是由個別權限組成，用於決定實際套用這些權限的順序。 清單根據所考慮頁面的階層來形成。 接著會從下到上掃描此清單，直到找到要套用至頁面的第一個適當權限為止。

>[!NOTE]
>
>示例中包含了ACL。 建議您檢閱並決定適合您應用程式的項目。 要查看包含的ACL，請轉至**CRXDE **，並為以下節點選擇&#x200B;**Access Control**&#x200B;頁簽：
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`:允許每個人讀取訪問權限。
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`:允許每個人讀取訪問權限。
>`/home/users/geometrixx-outdoors`:允許每個人讀取`*/profile*`和
>`*/social/relationships/following/*`。
>
>您的自定義應用程式可以設定其他關係（如`*/social/relationships/friend/*`或`*/social/relationships/pending-following/*`）的訪問權限。
>
>建立特定於社區的ACL時，加入這些社區的成員可能會獲得附加權限。 例如，當使用者在`/content/geometrixx-outdoors/en/community/hiking`或`/content/geometrixx-outdoors/en/community/winter-sports`處加入社群時，即會發生此情況。

### 權限狀態{#permission-states}

>[!NOTE]
>
>若為CQ 5.3使用者：
>
>與先前的CQ版本不同，如果使用者只需修改頁面，則不應再授與&#x200B;**create**&#x200B;和&#x200B;**delete**。 相反地，僅當希望用戶能夠在現有頁面上建立、修改或刪除元件時，才授予&#x200B;**modify**&#x200B;操作。
>
>基於向後相容性原因，動作測試沒有考慮定義&#x200B;**jcr:content**&#x200B;的節點的特殊處理。

| **動作** | **說明** |
|---|---|
| 允許（複選標籤） | AEM WCM可讓使用者在此頁面或任何子頁面上執行動作。 |
| 拒絕（無複選標籤） | AEM WCM不允許使用者在此頁面或任何子頁面上執行動作。 |

權限也會套用至任何子頁面。

如果權限不是從父節點繼承的，但至少有一個本地條目，則以下符號將附加到複選框。 本機項目是在CRX 2.2介面中建立的項目（目前只能在CRX中建立萬用字元ACL）。

若是指定路徑的動作：

<table>
 <tbody>
  <tr>
   <td>*（星號）</td>
   <td>至少有一個本地條目（有效或無效）。 這些萬用字元ACL在CRX中定義。</td>
  </tr>
  <tr>
   <td>! （感嘆號）</td>
   <td>至少有一個條目當前無效。</td>
  </tr>
 </tbody>
</table>

將滑鼠指標暫留在星號或驚嘆號上時，工具提示會提供關於宣告項目的詳細資訊。 工具提示分為兩個部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>列出有效條目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列出可能在樹中其他位置有效果的無效條目（如具有限制條目範圍的相應ACE的特殊屬性所示）。 或者，這是一個條目，其效果已被在給定路徑或祖先節點處定義的另一個條目撤銷。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果未為頁面定義權限，則所有動作都會遭到拒絕。

以下是管理存取控制清單的建議：

* 請勿直接將權限指派給使用者。 僅將其指派給群組。

   這將簡化維護，因為組數比用戶數少得多，而且波動性也小。

* 如果您希望群組/使用者只能修改頁面，請勿授予他們建立或拒絕權限。 僅授予他們修改和讀取權限。
* 請謹慎使用「拒絕」。 盡可能僅使用「允許」。

   如果權限的套用順序與預期順序不同，則使用拒絕可能會造成非預期的影響。 如果用戶是多個組的成員，來自一個組的拒絕語句可以取消來自另一個組的允許語句，反之亦然。 發生此情況時很難保留概覽，並且很容易導致無法預料的結果，但「允許」分配不會造成此類衝突。

   Adobe建議您使用「允許」而非「拒絕」，請參閱[最佳實務](#best-practices)。

在修改任一權限之前，請務必了解這些權限的運作方式和相互關聯。 請參閱CRX檔案，以說明AEM WCM [如何評估存取權限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)以及設定存取控制清單的範例。

### 權限 {#permissions}

權限可讓使用者和群組存取AEM頁面上的AEM功能。

您可以展開/收合節點，依路徑瀏覽權限，並且可以追蹤到根節點的權限繼承。

您可以選取或清除適當的核取方塊，以允許或拒絕權限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看詳細權限資訊{#viewing-detailed-permission-information}

除了格線檢視之外，AEM還提供指定路徑上所選使用者/群組的詳細權限檢視。 詳細資訊檢視提供其他資訊。

除了檢視資訊外，您也可以從群組中包含或排除目前的使用者或群組。 請參閱「新增權限時新增使用者或群組」](#adding-users-or-groups-while-adding-permissions)。 [此處所做的變更會立即反映在詳細檢視的上部。

若要存取「詳細資料」檢視，請在&#x200B;**Permissions**&#x200B;標籤中，按一下任何所選群組/使用者和路徑的&#x200B;**Details**。

![權限詳細資訊](assets/permissiondetails.png)

詳細資訊分為兩部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>重複在樹網格中看到的資訊。 對於每個動作，圖示會顯示是否允許或拒絕動作：</p>
    <ul>
     <li>無表徵圖=無聲明條目</li>
     <li>(tick)=宣告動作（允許）</li>
     <li>(-)=聲明操作（拒絕）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td><p>顯示執行下列操作的用戶和組的網格：</p>
    <ul>
     <li>聲明給定路徑的條目AND</li>
     <li>指定的可授權OR是群組</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模擬其他用戶{#impersonating-another-user}

透過[模擬功能](/help/sites-authoring/user-properties.md#user-settings)，使用者可以代表其他使用者工作。

這表示使用者帳戶可以指定其他可搭配其帳戶運作的帳戶。 換句話說，如果允許使用者B模擬使用者A，則使用者B可使用使用者A的完整帳戶詳細資訊來執行動作。

這可讓模擬者帳戶完成工作，就像使用其模擬的帳戶一樣；例如，在缺勤期間或在短期內共用過多負荷。

>[!NOTE]
>
>為了模擬對非管理員使用者有效，模擬器（在上述案例中為user-B）必須在`/home/users`路徑中擁有讀取權限。
>
>如需如何達成此目標的詳細資訊，請參閱AEM](/help/sites-administering/security.md#permissions-in-aem)中的[權限。

>[!CAUTION]
>
>如果某個帳戶模擬另一個帳戶，就很難看到。 模擬開始和結束時，在審核日誌中建立一個條目，但其他日誌檔案（如訪問日誌）不包含有關事件上發生了模擬的事實的資訊。 因此，如果使用者B模擬使用者A，則所有事件看起來都像是由使用者A個人執行。

>[!CAUTION]
>
>模擬使用者時，可執行鎖定頁面的作業。 不過，以此方式鎖定的頁面只能以模擬的使用者或具有管理員權限的使用者身分解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。

### 最佳作法 {#best-practices}

以下說明使用權限時的最佳實務：

| 規則 | 原因 |
|--- |--- |
| *使用群組* | 避免按用戶分配訪問權限。 原因有幾：<ul><li>您的使用者比群組多，因此群組可簡化結構。</li><li>群組可協助您提供所有帳戶的概觀。</li> <li>對於群組，繼承較簡單。</li><li>用戶來來去。 群體是長期的。</li></ul> |
| *積極* | 一律使用「允許」陳述式來指定群組的權利（盡可能）。 避免使用Deny語句。 系統會依序評估群組，且順序的定義可能會因使用者而異。 換句話說：您可能對語句的實施和評估順序幾乎沒有控制權。 如果您只使用Allow陳述式，則順序並不重要。 |
| *保持簡單* | 在配置新安裝時花一些時間和時間進行思考將得到很好的回報。 應用清晰的結構將簡化持續的維護和管理，確保您的當前同事和/或未來的繼任者都能輕鬆了解正在實施的內容。 |
| *測試* | 使用測試安裝來實踐並確保您了解各種使用者和群組之間的關係。 |
| *預設使用者/群組* | 安裝後請一律立即更新預設使用者和群組，以避免發生任何安全問題。 |

## 管理用戶和組{#managing-users-and-groups}

用戶包括使用系統的用戶和向系統提出請求的外國系統。

群組是一組使用者。

兩者皆可使用安全控制台中的「使用者管理」功能來設定。

### 使用安全控制台{#accessing-user-administration-with-the-security-console}訪問用戶管理

您可以使用安全控制台訪問所有用戶、組和關聯權限。 本節中描述的所有過程都將在此窗口中執行。

若要存取AEM WCM安全性，請執行下列其中一項操作：

* 在歡迎畫面或AEM中的各種位置中，按一下安全性圖示：

![](do-not-localize/wcmtoolbar.png)

* 直接導覽至`https://<server>:<port>/useradmin`。 請務必以管理員身分登入AEM。

隨即顯示下列視窗：

![cqsecuritypage](assets/cqsecuritypage.png)

左側樹列出系統中當前的所有用戶和組。 您可以選取要顯示的欄、排序欄的內容，甚至將欄標題拖曳到新位置，以變更欄的顯示順序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

這些頁簽提供對各種配置的訪問：

<!-- ??? in table below. -->

| 索引標籤 | 說明 |
|--- |--- |
| 篩選方塊 | 篩選所列使用者和/或群組的機制。 請參閱[篩選使用者和群組](#filtering-users-and-groups)。 |
| 隱藏使用者 | 切換開關，將隱藏列出的所有用戶，僅保留組。 請參閱[隱藏使用者和群組](#hiding-users-and-groups)。 |
| 隱藏群組 | 切換開關，將隱藏所列的所有組，僅保留用戶。 請參閱[隱藏使用者和群組](#hiding-users-and-groups)。 |
| 編輯 | 功能表可讓您建立和刪除，以及啟用和停用使用者或群組。 請參閱[建立使用者和群組](#creating-users-and-groups)和[刪除使用者和群組](#deleting-users-and-groups)。 |
| 屬性 | 列出關於用戶或組的資訊，這些資訊可以包括電子郵件資訊、說明和名稱資訊。 也可讓您變更使用者的密碼。 請參閱[建立用戶和組](#creating-users-and-groups)、[修改用戶和組屬性](#modifying-user-and-group-properties)和[更改用戶密碼](#changing-a-user-password)。 |
| 群組 | 列出選定用戶或組所屬的所有組。 您可以將選取的使用者或群組指派給其他群組，或從群組中移除。 請參閱[群組](#adding-users-or-groups-to-a-group)。 |
| 成員 | 僅適用於群組。 列出特定組的成員。 請參閱[成員](#members-adding-users-or-groups-to-a-group)。 |
| 權限 | 您可以為使用者或群組分配權限。 可讓您控制下列項目：<ul><li>與特定頁面/節點相關的權限。 請參閱[設定權限](#setting-permissions)。 </li><li>與建立和刪除頁面及階層修改相關的權限。???可讓您[分配權限](#settingprivileges)，例如階層修改，以便建立和刪除頁面，</li><li>根據路徑與[復寫權限](#setting-replication-privileges)（通常從作者發佈到發佈）相關的權限。</li></ul> |
| Impersonator | 讓其他使用者模擬帳戶。 當您需要使用者代表其他使用者行事時，此功能相當實用。 請參閱[模擬使用者](#impersonating-another-user)。 |
| 偏好設定 | 設定組或用戶](#setting-user-and-group-preferences)的[首選項。 例如，語言偏好設定。 |

### 篩選用戶和組{#filtering-users-and-groups}

您可以輸入篩選運算式來篩選清單，這會隱藏不符合運算式的所有使用者和群組。 您也可以使用[隱藏用戶和隱藏組](#hiding-users-and-groups)按鈕來隱藏用戶和組。

若要篩選使用者或群組：

1. 在左樹狀清單中，在提供的空格中輸入篩選運算式。 例如，輸入&#x200B;**admin**&#x200B;會顯示包含此字串的所有使用者和群組。
1. 按一下放大鏡以篩選清單。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 若要移除所有篩選器，請按一下&#x200B;**x**。

### 隱藏用戶和組{#hiding-users-and-groups}

隱藏用戶或組是篩選系統中所有用戶和組的清單的另一種方法。 有兩個切換機構。 按一下「隱藏使用者」會隱藏所有使用者，按一下「隱藏群組」會隱藏所有使用者的檢視（您無法同時隱藏使用者和群組）。 若要使用篩選運算式來篩選清單，請參閱「篩選使用者和群組」[。](#filtering-users-and-groups)

要隱藏用戶和組，請執行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，按一下「隱藏用戶」**或「隱藏組」**。 ****&#x200B;所選按鈕將突出顯示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 若要讓使用者或群組重新出現，請再次按一下對應的按鈕。

### 建立用戶和組{#creating-users-and-groups}

要建立新用戶或組：

1. 在&#x200B;**Security**&#x200B;控制台樹清單中，按一下&#x200B;**Edit**，然後按一下&#x200B;**Create User**&#x200B;或&#x200B;**Create Group**。

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根據您要建立使用者或群組，輸入所需的詳細資訊。

   * 如果選擇「**建立用戶」，則輸入登錄ID、名字和姓氏、電子郵件地址和密碼。**&#x200B;依預設，AEM會根據姓氏的第一個字母建立路徑，但您可以選取其他路徑。

   ![createuserdialog](assets/createuserdialog.png)

   * 如果選擇「**建立組**」，請輸入組ID和可選說明。

   ![creategroupdialog](assets/creategroupdialog.png)

1. 按一下&#x200B;**建立**。您建立的用戶或組將顯示在樹清單中。

### 刪除用戶和組{#deleting-users-and-groups}

要刪除用戶或組：

1. 在&#x200B;**Security**&#x200B;控制台中，選擇要刪除的用戶或組。 如果要刪除多個項目，請按住Shift鍵並按一下或按住Ctrl鍵並按一下以選取這些項目。
1. 按一下「**編輯」，**，然後選擇「刪除」。 AEM WCM會詢問您是否要刪除該使用者或群組。
1. 按一下&#x200B;**OK**&#x200B;以確認或取消以取消操作。

### 修改用戶和組屬性{#modifying-user-and-group-properties}

要修改用戶和組屬性，請執行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要修改的用戶或組名稱。

1. 按一下&#x200B;**屬性**&#x200B;頁簽，進行所需的更改，然後按一下&#x200B;**保存**。

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>使用者的路徑會顯示在使用者屬性底部。 無法修改。

### 更改用戶密碼{#changing-a-user-password}

使用以下過程修改用戶的密碼。

>[!NOTE]
>
>您無法使用安全控制台來更改管理員密碼。 若要變更管理員帳戶的密碼，請使用Granite Operations提供的[Users主控台](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。
>
>如果您在JEE上使用AEM Forms，請勿使用下列指示來變更密碼，而是使用JEE Admin Console(/adminui)來變更密碼。

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要更改密碼的用戶名。
1. 按一下&#x200B;**屬性**&#x200B;標籤（如果尚未啟用）。
1. 按一下「**設定密碼**」。 「設定密碼」(Set Password)窗口將開啟，您可以在其中更改密碼。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 輸入新密碼兩次；由於它們未顯示在明文中，因此這是為了確認 — 如果它們不匹配，系統會顯示錯誤。
1. 按一下&#x200B;**設定**&#x200B;以啟用帳戶的新密碼。

### 將用戶或組添加到組{#adding-users-or-groups-to-a-group}

AEM提供三種將使用者或群組新增至現有群組的方法：

* 在組中時，可以添加成員（用戶或組）。
* 在成員中時，可向組添加成員。
* 使用權限時，可以向組添加成員。

### 組 — 將用戶或組添加到組{#groups-adding-users-or-groups-to-a-group}

**群組**&#x200B;標籤會顯示目前帳戶所屬的群組。 您可以使用它將選取的帳戶新增至群組：

1. 連按兩下您要指派給群組的帳戶名稱（使用者或群組）。
1. 按一下&#x200B;**群組**&#x200B;標籤。 您會看到帳戶已屬於的群組清單。
1. 在樹清單中，按一下要添加到帳戶的組的名稱，並將其拖動到&#x200B;**組**&#x200B;窗格。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱並拖動它們。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 成員 — 將用戶或組添加到組{#members-adding-users-or-groups-to-a-group}

**成員**&#x200B;頁簽僅適用於組，並顯示哪些用戶和組屬於當前組。 您可以使用它來新增帳戶至群組：

1. 按兩下要添加成員的組的名稱。
1. 按一下&#x200B;**Members**&#x200B;頁簽。 您會看到已屬於此組的成員清單。
1. 在樹清單中，按一下要添加到組的成員的名稱，並將其拖動到&#x200B;**成員**&#x200B;窗格。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱並拖動它們。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 新增權限{#adding-users-or-groups-while-adding-permissions}時新增使用者或群組

若要在特定路徑的將成員新增至群組：

1. 按兩下要添加用戶的組或用戶的名稱。

1. 按一下&#x200B;**Permissions**&#x200B;標籤。

1. 導覽至您要新增權限的路徑，然後按一下&#x200B;**Details**。 詳細資訊視窗的下半部分提供關於誰擁有該頁面權限的資訊。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 在&#x200B;**成員**&#x200B;列中，為要具有該路徑權限的成員選擇複選框。 清除要為刪除權限的成員的複選框。 在您對進行變更的儲存格中，會顯示紅色三角形。
1. 按一下&#x200B;**OK**&#x200B;以儲存變更。

### 從組{#removing-users-or-groups-from-groups}中刪除用戶或組

AEM提供三種從群組中移除使用者或群組的方法：

* 在組配置檔案中時，可以刪除成員（用戶或組）。
* 在成員配置檔案中時，可以從組中刪除成員。
* 使用權限時，可以從組中刪除成員。

### 組 — 從組{#groups-removing-users-or-groups-from-groups}中刪除用戶或組

要從組中刪除用戶或組帳戶：

1. 按兩下要從組中刪除的組或用戶帳戶的名稱。
1. 按一下&#x200B;**群組**&#x200B;標籤。 您會看到所選帳戶所屬的群組。
1. 在&#x200B;**組**&#x200B;窗格中，按一下要從組中刪除的用戶或組的名稱，然後按一下&#x200B;**刪除**。 （如果要刪除多個帳戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱，然後按一下&#x200B;**Remove**。）

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 成員 — 從組{#members-removing-users-or-groups-from-groups}中刪除用戶或組

要從組中刪除帳戶，請執行以下操作：

1. 按兩下要從中刪除成員的組的名稱。
1. 按一下&#x200B;**Members**&#x200B;頁簽。 您會看到已屬於此組的成員清單。
1. 在&#x200B;**成員**&#x200B;窗格中，按一下要從組中刪除的成員的名稱，然後按一下&#x200B;**刪除**。 （如果要刪除多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱，然後按一下&#x200B;**Remove**。）

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 新增權限{#removing-users-or-groups-while-adding-permissions}時移除使用者或群組

要在特定路徑從組中刪除成員：

1. 按兩下要從中刪除用戶的組或用戶的名稱。

1. 按一下&#x200B;**Permissions**&#x200B;標籤。

1. 導覽至您要移除權限的路徑，然後按一下&#x200B;**Details**。 詳細資訊視窗的下半部分提供關於誰擁有該頁面權限的資訊。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 在&#x200B;**成員**&#x200B;列中，為要具有該路徑權限的成員選擇複選框。 清除要為刪除權限的成員的複選框。 在您對進行變更的儲存格中，會顯示紅色三角形。
1. 按一下&#x200B;**OK**&#x200B;以儲存變更。

### 用戶同步{#user-synchronization}

當部署為[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，需要在所有發佈節點之間同步用戶和組。

要了解用戶同步以及如何啟用它，請參閱[用戶同步](/help/sites-administering/sync.md)。

## 管理權限{#managing-permissions}

>[!NOTE]
>
>Adobe推出新的觸控式UI型權限管理主體檢視。 有關如何使用它的詳細資訊，請參見[此頁](/help/sites-administering/touch-ui-principal-view.md)。

本節說明如何設定權限，包括復寫權限。

### 設定權限{#setting-permissions}

權限可讓使用者對特定路徑上的資源執行特定動作。 也包含建立或刪除頁面的功能。

要添加、修改或刪除權限，請執行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要為或[搜索節點](#searching-for-nodes)設定權限的用戶或組的名稱。

1. 按一下&#x200B;**Permissions**&#x200B;標籤。

   ![cquserpermissions](assets/cquserpermissions.png)

1. 在樹網格中，選擇一個複選框，以允許所選用戶或組執行操作，或清除一個複選框以拒絕所選用戶或組執行操作。 有關詳細資訊，請按一下&#x200B;**Details**。

1. 完成後，按一下&#x200B;**Save**。

### 設定複製權限{#setting-replication-privileges}

復寫權限是發佈內容的權利，可為群組和使用者設定。

>[!NOTE]
>
>* 套用至群組的任何復寫權限皆適用於該群組中的所有使用者。
>* 用戶的複製權限取代組的複製權限。
>* 允許複製權限的優先順序高於拒絕複製權限。 如需詳細資訊，請參閱AEM](#permissions-in-aem)中的[權限。

>



要設定複製權限，請執行以下操作：

1. 從清單中選擇用戶或組，按兩下以開啟，然後按一下&#x200B;**Permissions**。
1. 在網格中，導航到希望用戶具有複製權限或[搜索節點的路徑。](#searching-for-nodes)

1. 在所選路徑的&#x200B;**複製**&#x200B;列中，選擇一個複選框以添加該用戶或組的複製權限，或清除該複選框以刪除複製權限。 AEM會在您所做變更尚未儲存的任何位置顯示紅色三角形。

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 搜索節點{#searching-for-nodes}

新增或移除權限時，您可以瀏覽或搜尋節點。

路徑搜尋有兩種不同類型：

* 路徑搜尋 — 如果搜尋字串的開頭為「/」，則搜尋會搜尋指定路徑的直接子節點：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜尋方塊中，您可以執行下列動作：

| 動作 | 它的作用 |
|--- |--- |
| 向右鍵 | 在搜索結果中選擇子節點 |
| 向下鍵 | 再次開始搜索。 |
| 輸入（返回）鍵 | 選取子節點並將其載入樹狀格中 |

* 全文搜索 — 如果搜索字串的開頭不是&quot;/&quot;，則對路徑&quot;/content&quot;下的所有節點執行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要對路徑或全文執行搜索：

1. 在安全控制台中，選擇用戶或組，然後按一下&#x200B;**權限**&#x200B;頁簽。

1. 在「搜索」框中，輸入要搜索的詞。

### 模擬用戶{#impersonating-users}

您可以指定一或多個允許模擬目前使用者的使用者。 這表示他們可以將其帳戶設定切換為目前使用者的帳戶設定，並代表此使用者行事。

使用此函式時請小心，因為它可能允許使用者執行其自己使用者無法執行的動作。 模擬使用者時，系統會通知使用者自己未登入。

您可能會想要使用此功能的各種案例，包括：

* 如果您不在辦公室，可以讓其他人在您不在的時候模擬您。 使用此功能，您可以確保某人擁有您的訪問權限，而且您不需要修改用戶配置檔案或洩露您的密碼。
* 您可將其用於除錯用途。 例如，若要查看網站如何尋找具有限制存取權限的使用者。 此外，如果用戶抱怨技術問題，您可以模擬該用戶以診斷和修復問題。

要模擬現有用戶：

1. 在樹清單中，選擇要為其分配其他用戶進行模擬的人員的名稱。 按兩下以開啟。
1. 按一下&#x200B;**模擬器**&#x200B;標籤。
1. 按一下您要能夠模擬所選使用者的使用者。 將使用者（將模擬的使用者）從清單拖曳至「模擬」窗格。 名稱會出現在清單中。

   ![chlimage_1-114](assets/chlimage_1-115.png)

1. 按一下「**儲存**」。

### 設定用戶和組首選項{#setting-user-and-group-preferences}

要設定用戶和組首選項，包括語言、窗口管理和工具欄首選項：

1. 在左側樹中選擇要更改其首選項的用戶或組。 若要選取多個使用者或群組，請按住Ctrl鍵並按一下或按住Shift鍵並按一下您的選取項目。
1. 按一下&#x200B;**Preferences**&#x200B;標籤。

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 根據需要對組或用戶首選項進行更改，並在完成後按一下&#x200B;**Save**。

### 設定用戶或管理員有權管理其他用戶{#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

若要設定使用者或管理員擁有刪除/啟用/停用其他使用者的權限：

1. 將要授予管理其他用戶權限的用戶添加到管理員組並保存更改。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用戶的&#x200B;**權限**&#x200B;頁簽中，導航到「/」，在「複製」列中，選擇允許在「/」進行複製的複選框，然後按一下&#x200B;**保存**。

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   選取的使用者現在能停用、啟用、刪除及建立使用者。

### 擴展項目級別{#extending-privileges-on-a-project-level}的權限

如果您打算實作應用程式特定權限，下列資訊將說明實作自訂權限所需了解的事項，以及如何在CQ中強制執行該權限：

層次結構修改權限由jcr權限的組合覆蓋。 複製權限的名稱為&#x200B;**crx:replicate**，該權限與jcr儲存庫上的其他權限一起儲存/評估。 但是，它沒有在jcr層級執行。

自訂權限的定義和註冊正式屬於2.4版起的[Jackrabbit API](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html)的一部分（另請參閱[JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)）。 JCR訪問控制管理涵蓋進一步的使用，如由[JSR 283](https://jcp.org/en/jsr/detail?id=283)（第16節）定義。 此外，Jackrabbit API定義一些擴充功能。

權限註冊機制反映在UI的&#x200B;**Repository Configuration**&#x200B;下。

新（自訂）權限的註冊本身受必須在儲存庫級別(在JCR中：在ac mgt api中將&#39;null&#39;傳遞為&#39;absPath&#39;參數，如需詳細資訊，請參閱jsr 333)。 預設情況下，**admin**&#x200B;和管理員的所有成員都具有該權限。

>[!NOTE]
>
>雖然實作會負責驗證和評估自訂權限，但除非這些權限是內建權限的匯總，否則無法強制執行。
