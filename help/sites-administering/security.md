---
title: 用戶管理和安全
description: 瞭解中的「User Administration and Security（用戶管理和安全）AEM」。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 1%

---

# 用戶管理和安全{#user-administration-and-security}

本章介紹如何配置和維護用戶授權，並介紹身份驗證和授權工作原理AEM。

## 中的用戶和組AEM {#users-and-groups-in-aem}

本節更詳細地介紹各種實體和相關概念，以幫助您配置易於維護的用戶管理概念。

### 使用者 {#users}

用戶使用其帳AEM戶登錄。 每個用戶帳戶都是唯一的，它包含基本帳戶詳細資訊以及分配的權限。

用戶通常是組的成員，這簡化了這些權限和/或權限的分配。

### 群組 {#groups}

組是用戶或其他組的集合，或兩者。 這些集合都稱為組的成員。

它們的主要目的是通過減少要更新的實體數來簡化維護過程，因為對組所做的更改將應用於組的所有成員。 組通常反映：

* 應用程式中的角色；比如允許瀏覽內容的人，或者允許發佈內容的人。
* 你自己的組織；當參與者被限制到內容樹中的不同分支時，您可能希望擴展角色以區分不同部門的參與者。

因此，群體往往保持穩定，而用戶來來去的頻率更高。

通過規劃和乾淨的結構，組的使用可以反映您的結構，為您提供清晰的概述和有效的更新機制。

### 內置用戶和組 {#built-in-users-and-groups}

AEMWCM安裝多個用戶和組。 這些集合在安裝後首次訪問安全控制台時可見。

下表列出了每個項，並列出了：

* 簡短描述
* 任何關於必要更改的建議

*更改所有預設密碼* （如果在某些情況下不刪除帳戶本身）。

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
   <td><p>具有完全訪問權限的系統管理帳戶。</p> <p>此帳戶用於WCM和CRX之AEM間的連接。</p> <p>如果意外刪除此帳戶，則系統會在重新啟動儲存庫（在預設設定中）時重新建立該帳戶。</p> <p>管理員帳戶是平台的AEM要求。 因此，無法刪除此帳戶。</p> </td>
   <td><p>Adobe建議您更改此用戶帳戶的預設密碼。</p> <p>最好在安裝時，儘管可以在安裝後完成。</p> <p>注：不要將此帳戶與CQ Servlet引擎的管理帳戶混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>使用者</td>
   <td><p>保留對實例的未驗證訪問的預設權限。 預設情況下，此帳戶擁有最小訪問權限。</p> <p>如果意外刪除此帳戶，則在啟動時會重新建立它。 無法永久刪除它，但可以禁用它。</p> </td>
   <td>避免刪除或禁用此帳戶，因為它會對作者實例的功能產生負面影響。 如果有安全要求要求您刪除它，請確保您首先正確test它對系統的影響。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>預設密碼：作者</p> </td>
   <td>使用者</td>
   <td><p>允許寫入/content的作者帳戶。 包括參與者和衝浪者權限。</p> <p>可以用作Webmaster，因為它有權訪問整個/content樹。</p> <p>此帳戶不是內置用戶，而是另一個Geometrixx演示用戶</p> </td>
   <td><p>Adobe建議完全刪除帳戶或更改預設密碼。</p> <p>最好在安裝時，儘管可以在安裝後完成。</p> </td>
  </tr>
  <tr>
   <td>管理員</td>
   <td>群組</td>
   <td><p>為其所有成員授予管理員權限的組。 只允許管理員編輯此組。</p> <p>具有完全訪問權限。</p> </td>
   <td>即使您在節點上設定了「deny-everyone」，管理員仍然可以訪問該節點</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>群組</td>
   <td><p>負責內容編輯的組。 需要讀取、修改、建立和刪除權限。</p> </td>
   <td>只要您添加讀取、修改、建立和刪除權限，就可以使用項目特定訪問權限建立自己的內容作者組。</td>
  </tr>
  <tr>
   <td>貢獻者</td>
   <td>群組</td>
   <td><p>允許用戶寫入內容的基本權限（如中，僅限功能）。</p> <p>不向/content樹分配任何權限。 必須為單個組或用戶分配。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>大壩用戶</td>
   <td>群組</td>
   <td>典型AEM Assets用戶的現成參考組。 此組的成員具有適當的權限，可啟用資產和集合的上載/共用。</td>
   <td> </td>
  </tr>
  <tr>
   <td>人</td>
   <td>群組</td>
   <td><p>其中的每AEM個用戶都是組的成員，即使您可能未在所有工具中看到組或成員關係。</p> <p>可以將此組視為預設權限，因為它可用於為所有用戶應用權限，甚至是將來建立的用戶。</p> </td>
   <td><p>不要修改或刪除此組。</p> <p>修改此帳戶會帶來其他安全影響。</p> </td>
  </tr>
  <tr>
   <td>標籤管理員</td>
   <td>群組</td>
   <td>允許編輯標籤的組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>用戶管理員</td>
   <td>群組</td>
   <td>授權用戶管理，即建立用戶和組的權利。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流編輯器</td>
   <td>群組</td>
   <td>允許建立和修改工作流模型的組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流用戶</td>
   <td>群組</td>
   <td><p>參與工作流的用戶必須是組工作流用戶的成員。 為用戶提供對以下內容的完全訪問權限：/etc/workflow/instances，以便它們可以更新工作流實例。</p> <p>該組包含在標準安裝中，但必須手動將用戶添加到該組。</p> </td>
  </tr>
 </tbody>
</table>

## 權AEM限 {#permissions-in-aem}

使AEM用ACL確定用戶或組可以執行哪些操作以及可以在何處執行這些操作。

### 權限和ACL {#permissions-and-acls}

權限定義誰可以對資源執行哪些操作。 權限是 [訪問控制](#access-control-lists-and-how-they-are-evaluated) 評估。

您可以通過選中或清除單個用戶的複選框來更改授予/拒絕給定用戶的權AEM限 [動作](security.md#actions)。 複選標籤表示允許執行操作。 沒有複選標籤表示操作被拒絕。

複選標籤在網格中的位置還指示用戶在內的哪些位置(即AEM哪些路徑)中擁有哪些權限。

### 動作 {#actions}

可以在頁（資源）上執行操作。 對於層次結構中的每一頁，您可以指定允許用戶對該頁執行哪些操作。 [權限](#permissions-and-acls) 允許或拒絕操作。

<table>
 <tbody>
  <tr>
   <td><strong>動作 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>讀取</td>
   <td>允許用戶讀取該頁面和任何子頁面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>用戶可以：</p>
    <ul>
     <li>修改頁面上和任何子頁面上的現有內容。</li>
     <li>在頁面或任何子頁面上建立段落。</li>
    </ul> <p>在JCR級別，用戶可以通過編輯資源的屬性、鎖定、版本控制和nt-modifies來編輯資源，並且他們對定義jcr：內容子節點的節點擁有完全的寫權限。 例如cq:Page、nt:file、cq:Asset。</p> </td>
  </tr>
  <tr>
   <td>建立</td>
   <td><p>用戶可以：</p>
    <ul>
     <li>建立頁或子頁。</li>
    </ul> <p>如果 <strong>修改</strong> 被拒絕，jcr:content下的子樹將被排除，因為jcr:content及其子節點的建立被視為頁面修改。 此規則僅適用於定義jcr:content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><p>用戶可以：</p>
    <ul>
     <li>從頁面或任何子頁面中刪除現有段落。</li>
     <li>刪除頁或子頁。</li>
    </ul> <p>如果 <strong>修改</strong> 拒絕jcr:content下的任何子樹，因為刪除jcr:content而將其子節點視為頁面修改。 此規則僅適用於定義jcr:content子節點的節點。</p> </td>
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
   <td>用戶可以將內容複製到其他環境（例如，發佈環境）。 該權限也應用於任何子頁。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>自AEM動為中的角色分配（所有者、編輯器、查看器）生成用戶組 [集合](/help/assets/manage-collections.md)。 但是，手動為此類組添加ACL可能會在中引入安全漏AEM洞。 Adobe建議您避免手動添加ACL。

### 訪問控制清單及其評估方法 {#access-control-lists-and-how-they-are-evaluated}

AEMWCM使用訪問控制清單(ACL)來組織應用到各頁的權限。

訪問控制清單由各個權限組成，用於確定應用這些權限的順序。 根據所考慮的頁的層次來形成清單。 然後，將自底向上掃描此清單，直到找到第一個適用於頁面的適當權限。

>[!NOTE]
>
>示例中包含ACL。 建議您查看並確定適合您的應用程式的內容。 要查看包含的ACL，請轉到 **克爾克斯德** 的 **訪問控制** 頁籤：
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>您的自定義應用程式可以設定其他關係的訪問權限，例如：
>
>* `*/social/relationships/friend/*`
>* 或 `*/social/relationships/pending-following/*`.
>
>當您建立特定於社區的ACL時，加入這些社區的成員可能會被授予附加權限。 例如，當用戶在以下位置加入社區時： `/content/we-retail/us/en/community`

### 權限狀態 {#permission-states}

>[!NOTE]
>
>對於CQ 5.3用戶：
>
>與以前的CQ版本相比， **建立** 和 **刪除** 如果用戶只能修改頁面，則不再授予該權限。 相反，授予 **修改** 僅當希望用戶能夠在現有頁面上建立、修改或刪除元件時才執行操作。
>
>出於向後相容的原因，操作test不會對定義的節點進行特殊處理 **jcr：內容** 算進去。

| **動作** | **說明** |
|---|---|
| 允許（複選標籤） | AEMWCM允許用戶在此頁或任何子頁上執行操作。 |
| 拒絕（無複選標籤） | AEMWCM不允許用戶在此頁或任何子頁上執行該操作。 |

權限也應用於任何子頁。

如果權限未從父節點繼承，但至少有一個本地條目，則以下符號將附加到複選框中。 本地條目是在CRX 2.2介面中建立的條目（當前只能在CRX中建立通配符ACL）。

對於給定路徑上的操作：

<table>
 <tbody>
  <tr>
   <td>*（星號）</td>
   <td>至少有一個本地條目（有效或無效）。 這些通配符ACL在CRX中定義。</td>
  </tr>
  <tr>
   <td>! （感嘆號）</td>
   <td>至少有一個條目當前無效。</td>
  </tr>
 </tbody>
</table>

將滑鼠懸停在星號或感嘆號上時，工具提示將提供有關聲明條目的詳細資訊。 工具提示分為兩個部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>列出有效條目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列出可在樹中其他位置生效的無效條目（如具有相應ACE的特殊屬性所示，該屬性限制了條目的範圍）。 或者，它是一個條目，其效果被在給定路徑或祖先節點上定義的另一個條目撤銷。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果沒有為頁面定義權限，則所有操作都將被拒絕。

以下是有關管理訪問控制清單的建議：

* 不要直接將權限分配給用戶。 僅將它們分配給組。

   這樣做可簡化維護，因為組數量遠小於用戶數量，而且波動性也較小。

* 如果希望組/用戶僅能修改頁面，則不要授予它們建立或拒絕權限。 僅授予他們修改和讀取權限。
* 少使用拒絕。 盡可能只使用「允許」。

   如果權限的應用順序與預期的順序不同，則使用deny會導致意外影響。 如果用戶是多個組的成員，則來自一個組的拒絕語句可能會取消來自另一個組的允許語句或相反的方式。 發生此類情況時很難保留概覽，並且很容易導致意外結果，而「允許」分配不會導致此類衝突。

   Adobe建議您使用「允許」而不是「拒絕」查看 [最佳做法](#best-practices)。

在修改任一權限之前，請確保您瞭解它們的工作方式和相互關聯。 請參閱CRX文檔，說明WCMAEM的 [評估訪問權限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)，以及設定訪問控制清單的示例。

### 權限 {#permissions}

權限允許用戶和組訪AEM問頁面AEM功能。

通過展開/折疊節點，可以按路徑瀏覽權限，並可以跟蹤到根節點的權限繼承。

通過選擇或清除相應的複選框，可以允許或拒絕權限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看詳細權限資訊 {#viewing-detailed-permission-information}

與網格視圖一AEM起，提供給定路徑上所選用戶/組權限的詳細視圖。 詳細資訊視圖提供了其他資訊。

除了查看資訊外，您還可以將當前用戶或組包括在組中或從組中排除。 請參閱 [添加權限時添加用戶或組](#adding-users-or-groups-while-adding-permissions)。 此處所做的更改會立即反映在詳細視圖的上部。

要訪問「詳細資訊」視圖，請在 **權限** 按鈕 **詳細資訊** 的子目錄。

![權限詳細資訊](assets/permissiondetails.png)

詳細資訊分為兩部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>重複在樹網格中看到的資訊。 對於每個操作，一個表徵圖顯示是允許還是拒絕該操作：</p>
    <ul>
     <li>無表徵圖=無聲明的條目</li>
     <li>(tick)=聲明的操作（允許）</li>
     <li>(-)=聲明的操作（拒絕）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td><p>顯示執行下列操作的用戶和組的網格：</p>
    <ul>
     <li>聲明給定路徑的條目AND</li>
     <li>給定的可授權OR是組</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模擬其他用戶 {#impersonating-another-user}

使用 [模擬功能](/help/sites-authoring/user-properties.md#user-settings)，用戶可以代表其他用戶工作。

即，用戶帳戶可以指定可以使用其帳戶操作的其他帳戶。 例如，如果允許user-B模擬user-A，則user-B可以使用user-A的完整帳戶詳細資訊來操作。

此功能允許模擬者帳戶完成任務，就像他們使用的是模擬的帳戶一樣。 例如，在缺勤期間或在短期內共用過重負荷。

>[!NOTE]
>
>要模擬為非管理員用戶工作，模擬器（在上述情況下為user-B）需要在 `/home/users` 路徑。
>
>請參閱 [權AEM限](/help/sites-administering/security.md#permissions-in-aem)。

>[!CAUTION]
>
>如果一個帳戶冒充另一個帳戶，則很難看到。 當模擬開始和結束時，在審核日誌中建立一個條目，但其他日誌檔案（如訪問日誌）不包含事件上發生模擬的資訊。 因此，如果user-B模擬user-A，則所有事件看起來都像user-A執行了它們。

>[!CAUTION]
>
>在模擬用戶時可以執行鎖定頁面。 但是，只有這樣鎖定的頁面才能作為模擬的用戶或具有管理員權限的用戶解鎖。
>
>無法通過模擬鎖定頁面的用戶來解鎖頁面。

### 最佳做法 {#best-practices}

下面介紹了使用權限和權限時的最佳做法：

| 規則 | 原因 |
|--- |--- |
| *使用組* | 避免按用戶分配訪問權限。 這種建議有幾個原因：<ul><li>用戶比組多得多，因此組簡化了結構。</li><li>組幫助提供所有帳戶的概覽。</li> <li>對於組，繼承更簡單。</li><li>用戶來去。 群體是長期的。</li></ul> |
| *積極* | 始終使用Allow語句指定組的權限（盡可能）。 避免使用Deny語句。 按順序計算組，並且每個用戶可以不同地定義順序。 換句話說：您可能對語句的實施和評估順序幾乎沒有控制權。 如果僅使用Allow語句，則順序不重要。 |
| *保持簡單* | 在配置新安裝時花一些時間和時間思考是值得的。 應用清晰的結構可簡化日常維護和管理，確保您的當前同事和未來繼任者都能夠輕鬆瞭解實施的內容。 |
| *測試* | 使用test安裝來練習並確保您瞭解各種用戶和組之間的關係。 |
| *預設用戶/組* | 安裝後始終立即更新預設用戶和組，以幫助防止任何安全問題。 |

## 管理用戶和組 {#managing-users-and-groups}

用戶包括使用該系統的用戶和向系統發出請求的外國系統。

組是一組用戶。

都可以使用安全控制台中的用戶管理功能進行配置。

### 使用安全控制台訪問用戶管理 {#accessing-user-administration-with-the-security-console}

您可以使用安全控制台訪問所有用戶、組和關聯權限。 本節中描述的所有過程都在此窗口中執行。

要訪AEM問WCM安全性，請執行以下操作之一：

* 在「歡迎」螢幕或中的各個位置AEM中，按一下安全表徵圖：

![](do-not-localize/wcmtoolbar.png)

* 直接導航到 `https://<server>:<port>/useradmin`。 確保以管理員身AEM份登錄。

將顯示以下窗口：

![cqsecurity頁](assets/cqsecuritypage.png)

左樹列出系統中當前的所有用戶和組。 您可以選擇要顯示的列，對列的內容進行排序，甚至可以通過將列標題拖動到新位置來更改列的顯示順序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

這些頁籤提供對各種配置的訪問：

<!-- ??? in table below. -->

| 定位字元 | 說明 |
|--- |--- |
| 濾鏡盒 | 用於篩選列出的用戶或組或兩者的機制。 請參閱 [篩選用戶和組](#filtering-users-and-groups)。 |
| 隱藏使用者 | 一個切換開關，它隱藏列出的所有用戶，僅保留組。 請參閱 [隱藏用戶和組](#hiding-users-and-groups)。 |
| 隱藏群組 | 一個切換開關，它隱藏所有列出的組，僅保留用戶。 請參閱 [隱藏用戶和組](#hiding-users-and-groups)。 |
| 編輯 | 允許您建立和刪除以及激活和停用用戶或組的菜單。 請參閱 [建立用戶和組](#creating-users-and-groups) 和 [刪除用戶和組](#deleting-users-and-groups)。 |
| 屬性 | 列出有關用戶或組的資訊，這些資訊可包括電子郵件資訊、說明和名稱資訊。 還允許您更改用戶的密碼。 請參閱 [建立用戶和組](#creating-users-and-groups)。 [修改用戶和組屬性](#modifying-user-and-group-properties) 和 [更改用戶密碼](#changing-a-user-password)。 |
| 群組 | 列出選定用戶或組所屬的所有組。 可以將所選用戶或組指派給其他組或從組中刪除它們。 請參閱 [組](#adding-users-or-groups-to-a-group)。 |
| 成員 | 僅適用於組。 列出特定組的成員。 請參閱 [成員](#members-adding-users-or-groups-to-a-group)。 |
| 權限 | 您可以將權限分配給用戶或組。 用於控制以下內容：<ul><li>與特定頁面/節點相關的權限。 請參閱 [設定權限](#setting-permissions)。 </li><li>與建立和刪除頁面以及層次結構修改相關的權限。??讓 [分配權限](#settingprivileges)，如層次結構修改，用於建立和刪除頁面，</li><li>與 [複製權限](#setting-replication-privileges) （通常從作者到發佈）。</li></ul> |
| Impersonator | 允許其他用戶模擬該帳戶。 當需要用戶代表其他用戶操作時非常有用。 請參閱 [模擬用戶](#impersonating-another-user)。 |
| 偏好設定 | 集 [組或用戶的首選項](#setting-user-and-group-preferences)。 例如，語言首選項。 |

### 篩選用戶和組 {#filtering-users-and-groups}

您可以通過輸入篩選器表達式來篩選清單，該表達式將隱藏與表達式不匹配的所有用戶和組。 您還可以使用 [隱藏用戶和隱藏組](#hiding-users-and-groups) 按鈕。

要篩選用戶或組：

1. 在左樹清單中，在提供的空間中鍵入篩選器表達式。 例如，輸入 **管理員** 顯示包含此字串的所有用戶和組。
1. 按一下放大鏡以篩選清單。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 按一下 **x** 的子菜單。

### 隱藏用戶和組 {#hiding-users-and-groups}

隱藏用戶或組是篩選系統中所有用戶和組清單的另一種方法。 有兩個肘桿機構。 按一下「隱藏用戶」(Hide User)可隱藏所有用戶，按一下「隱藏組」(Hide Groups)可隱藏所有組（不能同時隱藏用戶和組）。 要使用篩選器表達式篩選清單，請參見 [篩選用戶和組](#filtering-users-and-groups)。

要隱藏用戶和組：

1. 在 **安全** 控制台，按一下 **隱藏用戶** 或 **隱藏組**。 選中的按鈕將突出顯示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 要使用戶或組重新出現，請再次按一下相應按鈕。

### 建立用戶和組 {#creating-users-and-groups}

要建立用戶或組：

1. 在 **安全** 控制台樹清單，按一下 **編輯** 然後 **建立用戶** 或 **建立組**。

   ![cqserityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根據您是建立用戶還是建立組，輸入所需的詳細資訊。

   * 如果選擇 **建立用戶，** 輸入登錄ID、名和姓、電子郵件地址和密碼。 預設AEM情況下，根據姓氏的首字母建立路徑，但可以選擇其他路徑。

   ![createuser對話框](assets/createuserdialog.png)

   * 如果選擇 **建立組**，輸入組ID和可選說明。

   ![建立組對話框](assets/creategroupdialog.png)

1. 按一下&#x200B;**建立**。您建立的用戶或組將顯示在樹清單中。

### 刪除用戶和組 {#deleting-users-and-groups}

要刪除用戶或組：

1. 在 **安全** 控制台，選擇要刪除的用戶或組。 如果要刪除多個項目，請按住Shift鍵並按一下或按住Ctrl鍵並按一下以選擇它們。
1. 按一下 **編輯，** 然後選擇刪除。 AEMWCM詢問您是否要刪除用戶或組。
1. 按一下 **確定** 的子菜單。

### 修改用戶和組屬性 {#modifying-user-and-group-properties}

要修改用戶和組屬性：

1. 在 **安全** 控制台，按兩下要修改的用戶或組名稱。

1. 按一下 **屬性** 頁籤，然後按一下 **保存**。

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>用戶的路徑顯示在用戶屬性的底部。 無法修改。

### 更改用戶密碼 {#changing-a-user-password}

請按下列步驟修改用戶的密碼。

>[!NOTE]
>
>您不能使用安全控制台更改管理員密碼。 要更改管理員帳戶的密碼，請使用 [用戶控制台](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) 花崗岩作業公司提供的。
>
>如果您在JEE上使用AEM Forms，請勿使用下面的說明更改密碼，而是使用JEEAdmin Console(/adminui)上的AEM Forms更改密碼。

1. 在 **安全** console ，按兩下要更改密碼的用戶名。
1. 按一下 **屬性** 頁籤（如果尚未處於活動狀態）。
1. 按一下 **設定密碼**。 此時將開啟「設定密碼」窗口，您可以在其中更改密碼。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 輸入兩次新密碼；由於它們未以明文顯示，因此此操作用於確認 — 如果它們不匹配，則系統顯示錯誤。
1. 按一下 **設定** 以激活帳戶的新密碼。

### 向組添加用戶或組 {#adding-users-or-groups-to-a-group}

提AEM供了三種將用戶或組添加到現有組的不同方法：

* 在組中時，可以添加成員（用戶或組）。
* 在成員中時，可以將成員添加到組。
* 在處理「權限」時，可以向組添加成員。

### 組 — 向組添加用戶或組 {#groups-adding-users-or-groups-to-a-group}

的 **組** 頁籤顯示當前帳戶所屬的組。 您可以使用它將所選帳戶添加到組：

1. 按兩下要分配給組的帳戶（用戶或組）的名稱。
1. 按一下 **組** 頁籤。 您會看到帳戶已屬於的組清單。
1. 在樹清單中，按一下要添加到帳戶的組的名稱，並將其拖到 **組** 的子菜單。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並拖動這些名稱。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 按一下 **保存** 的子菜單。

### 成員 — 將用戶或組添加到組 {#members-adding-users-or-groups-to-a-group}

的 **成員** 頁籤僅適用於組，並顯示屬於當前組的用戶和組。 您可以使用它向組添加帳戶：

1. 按兩下要添加成員的組的名稱。
1. 按一下 **成員** 頁籤。 您會看到已屬於此組的成員清單。
1. 在樹清單中，按一下要添加到組的成員的名稱，並將其拖到 **成員** 的子菜單。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並拖動這些名稱。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 按一下 **保存** 的子菜單。

### 添加權限時添加用戶或組 {#adding-users-or-groups-while-adding-permissions}

要將成員添加到特定路徑中的組：

1. 按兩下要添加用戶的組或用戶的名稱。

1. 按一下 **權限** 頁籤。

1. 導航到要添加權限的路徑並按一下 **詳細資訊**。 詳細資訊窗口的下半部分提供了有關誰有權訪問該頁的資訊。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 選中 **成員** 列，用於您要對該路徑具有權限的成員。 清除要刪除其權限的成員的複選框。 在您更改的單元格中顯示一個紅色三角形。
1. 按一下 **確定** 的子菜單。

### 從組中刪除用戶或組 {#removing-users-or-groups-from-groups}

提AEM供三種從組中刪除用戶或組的不同方法：

* 在組配置檔案中時，可以刪除成員（用戶或組）。
* 在成員配置檔案中時，可以從組中刪除成員。
* 在處理「權限」時，可以從組中刪除成員。

### 組 — 從組中刪除用戶或組 {#groups-removing-users-or-groups-from-groups}

要從組中刪除用戶或組帳戶：

1. 按兩下要從組中刪除的組或用戶帳戶的名稱。
1. 按一下 **組** 頁籤。 您可以看到所選帳戶所屬的組。
1. 在 **組** 窗格中，按一下要從組中刪除的用戶或組的名稱，然後按一下 **刪除**。 (如果要刪除多個帳戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱，然後按一下 **刪除**。)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 按一下 **保存** 的子菜單。

### 成員 — 從組中刪除用戶或組 {#members-removing-users-or-groups-from-groups}

要從組中刪除帳戶：

1. 按兩下要從中刪除成員的組的名稱。
1. 按一下 **成員** 頁籤。 您會看到已屬於此組的成員清單。
1. 在 **成員** 窗格中，按一下要從組中刪除的成員的名稱，然後按一下 **刪除**。 (如果要刪除多個用戶，請按住Shift鍵並按一下或按住Ctrl鍵並按一下這些名稱，然後按一下 **刪除**。)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 按一下 **保存** 的子菜單。

### 添加權限時刪除用戶或組 {#removing-users-or-groups-while-adding-permissions}

要從某個路徑的組中刪除成員：

1. 按兩下要從中刪除用戶的組或用戶的名稱。

1. 按一下 **權限** 頁籤。

1. 導航到要刪除權限的路徑並按一下 **詳細資訊**。 詳細資訊窗口的下半部分提供了有關誰有權訪問該頁的資訊。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 選中 **成員** 列，用於您要對該路徑具有權限的成員。 清除要刪除其權限的成員的複選框。 在您更改的單元格中顯示一個紅色三角形。
1. 按一下 **確定** 的子菜單。

### 用戶同步 {#user-synchronization}

當部署為 [發佈場](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，必須在所有發佈節點之間同步用戶和組。

要瞭解用戶同步以及如何啟用它，請參見 [用戶同步](/help/sites-administering/sync.md)。

## 管理權限 {#managing-permissions}

>[!NOTE]
>
>Adobe引入了新的基於Touch UI的權限管理主體視圖。 有關如何使用它的詳細資訊，請參見 [此頁](/help/sites-administering/touch-ui-principal-view.md)。

本節介紹如何設定權限，包括複製權限。

### 設定權限 {#setting-permissions}

權限允許用戶在特定路徑上對資源執行某些操作。 它還包括建立或刪除頁面的功能。

要添加、修改或刪除權限：

1. 在 **安全** 控制台，按兩下要為或設定權限的用戶或組的名稱 [搜索節點](#searching-for-nodes)。

1. 按一下 **權限** 頁籤。

   ![cquser權限](assets/cquserpermissions.png)

1. 在樹網格中，選中一個複選框以允許選定用戶或組執行操作，或清除一個複選框以拒絕選定用戶或組執行操作。 有關詳細資訊，請按一下 **詳細資訊**。

1. 完成後，按一下 **保存**。

### 設定複製權限 {#setting-replication-privileges}

複製權限是發佈內容的權限，可以為組和用戶設定。

>[!NOTE]
>
>* 應用於組的任何複製權限都適用於該組中的所有用戶。
>* 用戶的複製權限將取代組的複製權限。
>* 「允許」複製權限的優先順序高於「拒絕」複製權限。 請參閱 [權AEM限](#permissions-in-aem) 的子菜單。
>


要設定複製權限：

1. 從清單中選擇用戶或組，按兩下以開啟，然後按一下 **權限**。
1. 在網格中，導航到希望用戶具有複製權限或 [搜索節點。](#searching-for-nodes)

1. 在 **複製** 列中，選中一個複選框以添加該用戶或組的複製權限，或清除該複選框以刪除複製權限。 在AEM您所做更改但尚未保存的任何位置顯示紅色三角形。

   ![cquserreplicate權限](assets/cquserreplicatepermissions.png)

1. 按一下 **保存** 的子菜單。

### 搜索節點 {#searching-for-nodes}

添加或刪除權限時，可以瀏覽或搜索節點。

路徑搜索有兩種不同類型：

* 路徑搜索 — 如果搜索字串以「/」開頭，則它將搜索給定路徑的直接子節點：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜索框中，可以執行以下操作：

| 動作 | 作用 |
|--- |--- |
| 右箭頭鍵 | 在搜索結果中選擇子節點 |
| 向下箭頭鍵 | 再次開始搜索。 |
| 輸入（返回）鍵 | 選擇子節點並將其載入到樹網格中 |

* 全文搜索 — 如果搜索字串不以「/」開頭，則對路徑「/content」下的所有節點執行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要對路徑或全文執行搜索，請執行以下操作：

1. 在安全控制台中，選擇用戶或組，然後按一下 **權限** 頁籤。

1. 在「搜索」框中，輸入要搜索的詞。

### 模擬用戶 {#impersonating-users}

您可以指定一個或多個允許模擬當前用戶的用戶。 此功能意味著他們可以將帳戶設定切換到當前用戶的帳戶，並代表此用戶行事。

使用此函式時要小心，因為它可能允許用戶執行其用戶無法執行的操作。 模擬用戶時，系統會通知用戶他們沒有以自己的身份登錄。

您可能希望使用此功能時有多種方案，包括：

* 如果你不在辦公室，你可以讓別人在你不在的時候冒充你。 通過使用此功能，您可以確保某人具有您的訪問權限，而您不需要修改用戶配置檔案或提供您的密碼。
* 您可以將其用於調試。 例如，查看網站如何查找具有受限訪問權限的用戶。 此外，如果用戶抱怨技術問題，您可以模擬該用戶來診斷和修復問題。

模擬現有用戶：

1. 在樹清單中，選擇要為其他用戶分配模擬人的姓名。 按兩下以開啟。
1. 按一下 **模擬者** 頁籤。
1. 按一下要模擬選定用戶的用戶。 將用戶（模擬器）從清單拖到「模擬器」窗格。 該名稱將出現在清單中。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 按一下「**儲存**」。

### 設定用戶和組首選項 {#setting-user-and-group-preferences}

要設定用戶和組首選項，包括語言、窗口管理和工具欄首選項：

1. 在左側樹中選擇要更改其首選項的用戶或組。 要選擇多個用戶或組，請按住Ctrl鍵並按一下或按住Shift鍵並按一下您的選擇。
1. 按一下 **首選項** 頁籤。

   ![cqsecurity首選項](assets/cqsecuritypreferences.png)

1. 根據需要對組或用戶首選項進行更改，然後按一下 **保存** 的子菜單。

### 將用戶或管理員設定為具有管理其他用戶的權限 {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

要將用戶或管理員設定為具有刪除/激活/停用其他用戶的權限，請執行以下操作：

1. 將要授予權限以管理其他用戶的用戶添加到管理員組並保存更改。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用戶中 **權限** 頁籤，導航到「/」，然後在「複製」列中，選中允許在「/」處複製的複選框，然後按一下 **保存**。

   ![cqsecurityreplicate權限](assets/cqsecurityreplicatepermissions.png)

   所選用戶現在可以停用、激活、刪除和建立用戶。

### 擴展項目級別的權限 {#extending-privileges-on-a-project-level}

如果您計畫實施特定於應用程式的權限，則以下資訊將說明實施自定義權限時必須瞭解的內容以及如何在整個CQ中實施自定義權限：

層次結構修改權限由jcr權限的組合覆蓋。 複製權限已命名 **crx：複製** 與jcr儲存庫上的其他權限一起儲存/評估。 但是，它沒有在jcr級別上執行。

自定義權限的定義和註冊正式是 [Jackrabbit API](https://jackrabbit.apache.org/oak/docs/security/privilege.html) 截至2.4版(另請參見 [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887))。 JCR訪問控制管理(如由 [JSR 283](https://jcp.org/en/jsr/detail?id=283) （第16節）。 此外，Jackrabbit API定義了幾個擴展。

權限註冊機制在UI中反映在 **儲存庫配置**。

新（自定義）權限的註冊本身受必須在儲存庫級別授予的內置權限保護。 在JCR中：在ac mgt api中將「null」作為「absPath」參數傳遞，有關詳細資訊，請參見jsr 333。 預設情況下， **管理員** 所有管理員成員都擁有此權限。

>[!NOTE]
>
>雖然實現會負責驗證和評估自定義權限，但除非這些權限是內置權限的聚合，否則它無法強制執行。
