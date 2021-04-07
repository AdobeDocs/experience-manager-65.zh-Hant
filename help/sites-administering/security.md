---
title: 使用者管理與安全性
seo-title: 使用者管理與安全性
description: 瞭解中的「用戶管理和安全性」AEM。
seo-description: 瞭解中的「用戶管理和安全性」AEM。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: 安全性
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '5488'
ht-degree: 1%

---

# 使用者管理與安全性{#user-administration-and-security}

本章介紹如何配置和維護用戶授權，並介紹身份驗證和授權如何運作的理論AEM。

## {#users-and-groups-in-aem}中AEM的使用者和群組

本節將更詳細地介紹各種實體和相關概念，以幫助您配置易於維護的用戶管理概念。

### 使用者 {#users}

使用者將使用其AEM帳戶登入。 每個使用者帳戶都是唯一的，並包含基本帳戶詳細資訊以及指派的權限。

使用者通常是群組的成員，可簡化這些權限和／或權限的分配。

### 群組 {#groups}

群組是使用者和／或其他群組的集合；這些都稱為群組成員。

其主要目的是透過減少要更新的實體數目來簡化維護程式，因為對群組所做的變更會套用至群組的所有成員。 群組通常反映：

* 應用程式中的角色；例如，允許瀏覽內容的人，或允許提供內容的人。
* 您自己的組織；當內容樹狀結構中的貢獻者被限制在不同分支時，您可能想要擴充角色，以區分不同部門的貢獻者。

因此，群組往往保持穩定，而使用者來來回的頻率則更高。

透過規劃和簡潔的結構，群組的使用可以反映您的結構，提供清楚的概述和有效的更新機制。

### 內建使用者和群組{#built-in-users-and-groups}

AEMWCM會安裝許多使用者和群組。 在安裝後首次存取Security Console時，就會看到這些。

下表列出每個項目，並列出：

* 簡短描述
* 任何關於必要變更的建議

*請變更所有預設密碼* （如果您未在特定情況下刪除帳戶本身）。

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
   <td><p>具有完全訪問權限的系統管理帳戶。</p> <p>此帳戶用於WCM和AEMCRX之間的連接。</p> <p>如果意外刪除了此帳戶，系統將在資料庫重新啟動時（在預設設定中）重新建立該帳戶。</p> <p>管理員帳戶是平台的一項AEM要求。 因此，此帳戶無法刪除。</p> </td>
   <td><p>Adobe強烈建議將此使用者帳戶的密碼從預設值變更。</p> <p>優選地，在安裝時，儘管可以在安裝後完成。</p> <p>注意：此帳戶不要與CQ Servlet引擎的管理員帳戶混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>使用者</td>
   <td><p>保留對實例的未驗證訪問的預設權限。 根據預設，這會保留最低存取權限。</p> <p>如果您意外刪除此帳戶，系統會在啟動時重新建立此帳戶。 它無法永久刪除，但可以禁用。</p> </td>
   <td>請避免刪除或停用此帳戶，因為這會對作者例項的運作造成負面影響。 如果有安全性要求您必須刪除它，請務必先正確測試它對系統的影響。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>預設密碼：作者</p> </td>
   <td>使用者</td>
   <td><p>允許寫入/content的作者帳戶。 涵蓋投稿人和衝浪者特權。</p> <p>可以作為網站管理員使用，因為它可以訪問整個/content樹。</p> <p>這不是內建使用者，而是其他geometrixx展示使用者</p> </td>
   <td><p>Adobe建議完全刪除帳戶，或從預設值變更密碼。</p> <p>優選地，在安裝時，儘管可以在安裝後完成。</p> </td>
  </tr>
  <tr>
   <td>管理員</td>
   <td>群組</td>
   <td><p>授予其所有成員管理員權限的組。 只允許管理員編輯此群組。</p> <p>擁有完整存取權。</p> </td>
   <td>如果您在節點上設定「拒絕每個人」，則管理員只有在該群組再次啟用時才能擁有存取權。</td>
  </tr>
  <tr>
   <td>內容作者</td>
   <td>群組</td>
   <td><p>負責內容編輯的群組。 需要讀取、修改、建立和刪除權限。</p> </td>
   <td>只要您新增讀取、修改、建立和刪除權限，就可以使用專案特定存取權限建立您自己的內容作者群組。</td>
  </tr>
  <tr>
   <td>contributor</td>
   <td>群組</td>
   <td><p>可讓使用者編寫內容的基本權限（僅限功能）。</p> <p>不為/content樹分配任何權限——這些權限必須專門分配給各個組或用戶。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>群組</td>
   <td>典型AEM Assets用戶的現成可用參考組。 此群組成員具有適當的權限，可啟用資產和系列的上傳／共用。</td>
   <td> </td>
  </tr>
  <tr>
   <td>every</td>
   <td>群組</td>
   <td><p>每個使用AEM者都是群組的成員，即使您在所有工具中可能看不到群組或成員關係。</p> <p>此群組可視為預設權限，因為它可用來套用每個人的權限，甚至是將來建立的使用者。</p> </td>
   <td><p>請勿修改或刪除此群組。</p> <p>修改此帳戶會產生額外的安全性影響。</p> </td>
  </tr>
  <tr>
   <td>tag-administrators</td>
   <td>群組</td>
   <td>允許編輯標籤的群組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>user-administrators</td>
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
   <td>workflow-users</td>
   <td>群組</td>
   <td><p>參與工作流程的使用者必須是群組工作流程使用者的成員。 這可讓他或她完全存取：/etc/workflow/instances，讓他／她可以更新工作流程例項。</p> <p>此群組已包含在標準安裝中，但您必須手動將使用者新增至群組。</p> </td>
  </tr>
 </tbody>
</table>

## &lt;a0/AEM>中的權限{#permissions-in-aem}

使AEM用ACL來確定用戶或組可以採取哪些操作以及可以在何處執行這些操作。

### 權限和ACL {#permissions-and-acls}

權限定義允許誰對資源執行哪些操作。 權限是[訪問控制](#access-control-lists-and-how-they-are-evaluated)評估的結果。

您可以選擇或清除個別[操作](security.md#actions)的複選框，以更改授予／拒絕給定用戶的權AEM限。 複選標籤表示允許執行動作。 無複選標籤表示動作被拒絕。

複選標籤位於網格中的位置還指示用戶在哪些位置(即AEM哪些路徑)擁有哪些權限。

### 動作 {#actions}

可以在頁（資源）上執行操作。 對於階層中的每個頁面，您可以指定允許使用者對該頁面執行的動作。 [授](#permissions-and-acls) 權您允許或拒絕動作。

<table>
 <tbody>
  <tr>
   <td><strong>動作 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>讀取</td>
   <td>使用者可讀取頁面和任何子頁面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>修改頁面上和任何子頁面上的現有內容。</li>
     <li>在頁面上或任何子頁面上建立新段落。</li>
    </ul> <p>在JCR級別，用戶可以通過修改資源的屬性、鎖定、版本修訂和nt-modifications來修改資源，並且他們對定義jcr:content子節點的節點具有完全的寫權限，例如cq:Page、nt:file、cq:Asset。</p> </td>
  </tr>
  <tr>
   <td>建立</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>建立新頁面或子頁面。</li>
    </ul> <p>如果拒絕<strong>modify</strong>，則會明確排除jcr:content下方的子樹，因為建立jcr:content及其子節點被視為頁面修改。 這僅適用於定義jcr:content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>從頁面或任何子頁面刪除現有段落。</li>
     <li>刪除頁面或子頁面。</li>
    </ul> <p>如果拒絕<strong>modify</strong>，則會明確排除jcr:content下方的任何子樹，以移除jcr:content，其子節點會被視為頁面修改。 這僅適用於定義jcr:content子節點的節點。</p> </td>
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
   <td>使用者可將內容複製至其他環境（例如發佈環境）。 此權限也適用於任何子頁面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>自AEM動為[Collections](/help/assets/manage-collections.md)中的角色分配（擁有者、編輯者、檢視器）產生使用者群組。 不過，手動為此類組添加ACL會在中引入安全漏洞AEM。 Adobe建議您避免手動添加ACL。

### 訪問控制清單及其評估方式{#access-control-lists-and-how-they-are-evaluated}

WCMAEM使用訪問控制清單(ACL)來組織要應用到各頁的權限。

「存取控制清單」是由個別權限所組成，用來決定實際套用這些權限的順序。 該清單根據所考慮的頁面的層次形成。 然後，會自底向上掃描此清單，直到找到套用至頁面的第一個適當權限為止。

>[!NOTE]
>
>示例中包含一些ACL。 建議您檢閱並判斷哪些應用程式適合您的應用程式。 要查看包含的ACL，請轉至**CRXDE **，並為以下節點選擇&#x200B;**訪問控制**&#x200B;頁籤：
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`:允許每個人讀取。
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`:允許每個人讀取。
>`/home/users/geometrixx-outdoors`:允許每個人讀取`*/profile*`和
>`*/social/relationships/following/*`。
>
>您的自訂應用程式可設定其他關係的存取權，例如`*/social/relationships/friend/*`或`*/social/relationships/pending-following/*`。
>
>當您建立特定於社區的ACL時，加入這些社區的成員可能會獲得額外的權限。 例如，當使用者在`/content/geometrixx-outdoors/en/community/hiking`或`/content/geometrixx-outdoors/en/community/winter-sports`加入社群時，可能會發生這種情況。

### 權限狀態{#permission-states}

>[!NOTE]
>
>針對CQ 5.3使用者：
>
>與舊版CQ相比，如果使用者只需修改頁面，則不應再授與&#x200B;**create**&#x200B;和&#x200B;**delete**。 請改為僅在您希望使用者能夠在現有頁面上建立、修改或刪除元件時，才授與&#x200B;**modify**&#x200B;動作。
>
>基於向後相容性的原因，動作測試沒有考慮定義&#x200B;**jcr:content**&#x200B;的節點的特殊處理。

| **動作** | **說明** |
|---|---|
| 允許（複選標籤） | AEMWCM可讓使用者在此頁面或任何子頁面上執行動作。 |
| 拒絕（無複選標籤） | AEMWCM不允許使用者在此頁面或任何子頁面上執行動作。 |

權限也會套用至任何子頁面。

如果權限未繼承自父節點，但至少有一個本地條目，則會將下列符號附加到該複選框。 本地條目是在CRX 2.2介面中建立的條目（通配符ACL當前只能在CRX中建立）。

對於指定路徑上的操作：

<table>
 <tbody>
  <tr>
   <td>*（星號）</td>
   <td>至少有一個本地條目（有效或無效）。 這些通配符ACL在CRX中定義。</td>
  </tr>
  <tr>
   <td>! （驚嘆號）</td>
   <td>至少有一個條目目前沒有作用。</td>
  </tr>
 </tbody>
</table>

將滑鼠指標暫留在星號或驚嘆號上時，工具提示會提供有關已宣告項目的詳細資訊。 工具提示會分割為兩個部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>列出有效條目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列出在樹中其他位置可能具有效果的非有效條目（由具有相應ACE的特殊屬性表示，該屬性限制條目的範圍）。 或者，這是一個條目，其效果已被在給定路徑或祖先節點上定義的另一個條目撤銷。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果未定義頁面的權限，則會拒絕所有動作。

以下是有關管理訪問控制清單的建議：

* 請勿直接將權限指派給使用者。 僅將它們指派給群組。

   這將簡化維護作業，因為群組數目比使用者人數少得多，而且波動性也較小。

* 如果您希望群組／使用者只能修改頁面，請勿授與他們建立或拒絕權限。 僅授予他們修改和讀取權限。
* 謹慎使用「拒絕」。 請盡量僅使用「允許」。

   如果權限的套用順序與預期順序不同，則使用deny可能會造成非預期的效果。 如果用戶是多個組的成員，來自一個組的拒絕語句可以取消來自另一個組的允許語句，反之亦然。 發生此情況時，很難保留概述，並且很容易導致無法預見的結果，而「允許」分配不會造成此類衝突。

   Adobe建議您使用「允許」而非「拒絕」，請參閱[最佳實踐](#best-practices)。

在修改任一權限之前，請務必瞭解其運作方式及相互關聯。 請參見CRX文檔以說明AEMWCM [如何評估訪問權限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)以及有關設定訪問控制清單的示例。

### 權限 {#permissions}

權限可讓使用者和群組存取頁AEM面上的AEM功能。

通過展開／折疊節點，可以按路徑瀏覽權限，並且可以跟蹤到根節點的權限繼承。

您可以選擇或清除適當的核取方塊，以允許或拒絕權限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看詳細權限資訊{#viewing-detailed-permission-information}

除了格線檢視外，還AEM提供特定路徑上所選使用者／群組權限的詳細檢視。 詳細資訊視圖提供了其他資訊。

除了檢視資訊外，您也可以將目前的使用者或群組納入或排除在群組之外。 請參閱[新增權限時新增使用者或群組](#adding-users-or-groups-while-adding-permissions)。 此處所做的變更會立即反映在詳細檢視的上半部。

要訪問「詳細資訊」視圖，請在&#x200B;**權限**&#x200B;頁籤中，按一下任何選定組／用戶和路徑的&#x200B;**詳細資訊**。

![權限詳細資訊](assets/permissiondetails.png)

詳細資訊分為兩部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>重複樹網格中顯示的資訊。 對於每個動作，都會顯示動作是否允許或拒絕：</p>
    <ul>
     <li>no icon = no declared entry</li>
     <li>（勾選）=宣告的動作（允許）</li>
     <li>(-)=聲明的操作（拒絕）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td><p>顯示執行下列作業的使用者和群組格線：</p>
    <ul>
     <li>聲明給定路徑的條目AND</li>
     <li>指定的可授權OR是群組嗎</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模擬其他用戶{#impersonating-another-user}

使用[Impersonate功能](/help/sites-authoring/user-properties.md#user-settings)，使用者可以代表其他使用者工作。

這表示使用者帳戶可以指定其他帳戶，以便與其帳戶一起運作。 換言之，如果允許user-B模擬使用者-A，則user-B可使用user-A的完整帳戶詳細資訊採取動作。

這可讓模擬帳戶完成工作，就像使用其模擬的帳戶；例如，在缺勤期間或在短期內共用過多負荷。

>[!NOTE]
>
>為了模擬為非管理員使用者所使用，模擬者（在上述情況下為user-B）必須擁有`/home/users`路徑中的READ權限。
>
>有關如何實現此目的的詳細資訊，請參見AEM](/help/sites-administering/security.md#permissions-in-aem)中的[權限。

>[!CAUTION]
>
>如果某個帳戶冒充另一個帳戶，就很難看到。 當冒充開始和結束時，在審計日誌中建立一個條目，但其他日誌檔案（如訪問日誌）不保存有關事件上發生冒充的事實的資訊。 因此，如果user-B模擬使用者- A所有事件看起來都像是使用者- A個人執行的。

>[!CAUTION]
>
>在模擬使用者時可以執行鎖定頁面。 不過，以此方式鎖定的頁面，只能以模擬的使用者或具有管理員權限的使用者身分解除鎖定。
>
>無法模擬鎖定頁面的使用者來解除鎖定頁面。

### 最佳作法 {#best-practices}

以下說明使用權限和權限時的最佳實務：

| 規則 | 原因 |
|--- |--- |
| *使用群組* | 避免依使用者指派存取權限。 原因有幾：<ul><li>您的使用者比群組多，因此群組可簡化結構。</li><li>群組可協助提供所有帳戶的概觀。</li> <li>對於群組，繼承更簡單。</li><li>使用者來來去。 群體是長期的。</li></ul> |
| *積極* | 請務必使用「允許」陳述式來指定群組的權利（盡可能）。 避免使用Deny語句。 群組依順序評估，而順序的定義可能與使用者不同。 換句話說：您可能對語句的實施和評估順序幾乎沒有控制權。 如果您只使用「允許」陳述式，則訂單無關緊要。 |
| *保持簡單* | 在配置新安裝時投入一些時間和思考，將獲得很好的回報。 套用清楚的結構可簡化持續的維護與管理，確保您目前的同事和／或未來的繼任者都能輕鬆瞭解正在實施的內容。 |
| *測試* | 使用測試安裝來練習並確保您瞭解不同使用者和群組之間的關係。 |
| *預設使用者／群組* | 安裝後請立即更新預設使用者和群組，協助避免任何安全性問題。 |

## 管理用戶和組{#managing-users-and-groups}

用戶包括使用系統的用戶和向系統發出請求的外國系統。

群組是一組使用者。

這兩者都可使用安全控制台中的用戶管理功能進行配置。

### 使用Security Console {#accessing-user-administration-with-the-security-console}訪問用戶管理

您可使用安全性主控台存取所有使用者、群組和相關權限。 本節中介紹的所有過程都在此窗口中執行。

若要存AEM取WCM安全性，請執行下列其中一項作業：

* 在「歡迎」螢幕或中的各個位置AEM中，按一下安全表徵圖：

![](do-not-localize/wcmtoolbar.png)

* 直接導覽至`https://<server>:<port>/useradmin`。 請確定您以管理員AEM的身分登入。

將顯示以下窗口：

![cqsecuritypage](assets/cqsecuritypage.png)

左樹列出系統中當前的所有用戶和組。 您可以選取要顯示的欄、排序欄的內容，甚至將欄標題拖曳至新位置，以變更欄的顯示順序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

這些頁籤可訪問各種配置：

<!-- ??? in table below. -->

| 索引標籤 | 說明 |
|--- |--- |
| 篩選方塊 | 用於篩選列出的用戶和／或組的機制。 請參閱[篩選使用者和群組](#filtering-users-and-groups)。 |
| 隱藏使用者 | 切換開關，將隱藏列出的所有使用者，僅保留群組。 請參閱[隱藏使用者和群組](#hiding-users-and-groups)。 |
| 隱藏群組 | 切換開關，可隱藏所有列出的群組，僅保留使用者。 請參閱[隱藏使用者和群組](#hiding-users-and-groups)。 |
| 編輯 | 可讓您建立和刪除以及啟用和停用使用者或群組的功能表。 請參閱[建立用戶和組](#creating-users-and-groups)和[刪除用戶和組](#deleting-users-and-groups)。 |
| 屬性 | 列出有關可包含電子郵件資訊、說明和名稱資訊之使用者或群組的資訊。 也允許您更改用戶的密碼。 請參閱[建立用戶和組](#creating-users-and-groups)、[修改用戶和組屬性](#modifying-user-and-group-properties)和[更改用戶密碼](#changing-a-user-password)。 |
| 群組 | 列出選定用戶或組所屬的所有組。 您可以將選取的使用者或群組指派給其他群組，或從群組中移除。 請參閱[群組](#adding-users-or-groups-to-a-group)。 |
| 成員 | 僅適用於群組。 列出特定群組的成員。 請參閱[成員](#members-adding-users-or-groups-to-a-group)。 |
| 權限 | 您可以為使用者或群組分配權限。 可讓您控制下列項目：<ul><li>與特定頁面／節點相關的權限。 請參閱[設定權限](#setting-permissions)。 </li><li>與建立和刪除頁面及階層修改相關的權限。???可讓您[分配權限](#settingprivileges)，例如階層修改，讓您建立和刪除頁面，</li><li>根據路徑與[複製權限](#setting-replication-privileges)（通常從作者到發佈）相關的權限。</li></ul> |
| Impersonator | 讓其他使用者模擬帳戶。 當您需要使用者代表其他使用者時，就很有用。 請參閱[模擬使用者](#impersonating-another-user)。 |
| 偏好設定 | 設定組或用戶](#setting-user-and-group-preferences)的[首選項。 例如，語言偏好設定。 |

### 篩選使用者和群組{#filtering-users-and-groups}

您可以輸入篩選運算式來篩選清單，此運算式會隱藏所有不符合運算式的使用者和群組。 您也可以使用[隱藏使用者和隱藏群組](#hiding-users-and-groups)按鈕來隱藏使用者和群組。

若要篩選使用者或群組：

1. 在左樹清單中，在提供的空格中輸入篩選運算式。 例如，輸入&#x200B;**admin**&#x200B;會顯示包含此字串的所有使用者和群組。
1. 按一下放大鏡以篩選清單。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 當您要移除所有篩選器時，按一下&#x200B;**x**。

### 隱藏用戶和組{#hiding-users-and-groups}

隱藏使用者或群組是篩選系統中所有使用者和群組清單的另一種方式。 有兩種切換機制。 按一下「隱藏使用者」可隱藏所有使用者，然後按一下「隱藏群組」可隱藏所有群組（您無法同時隱藏使用者和群組）。 若要使用篩選運算式來篩選清單，請參閱[篩選使用者和群組](#filtering-users-and-groups)。

要隱藏用戶和組：

1. 在&#x200B;**Security**&#x200B;主控台中，按一下「隱藏使用者&#x200B;**」或「隱藏群組**」。 ****&#x200B;選取的按鈕會反白顯示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 若要重新顯示使用者或群組，請再次按一下對應的按鈕。

### 建立用戶和組{#creating-users-and-groups}

要建立新用戶或組：

1. 在&#x200B;**Security**&#x200B;控制台樹清單中，按一下&#x200B;**Edit**，然後按一下&#x200B;**Create User**&#x200B;或&#x200B;**Create Group**。

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根據您要建立使用者或群組，輸入所需的詳細資訊。

   * 如果選擇&#x200B;**建立用戶，則**&#x200B;輸入登錄ID、名字和姓氏、電子郵件地址和密碼。 預設情AEM況下，根據姓氏的第一個字母建立路徑，但可以選擇其他路徑。

   ![createuserdial](assets/createuserdialog.png)

   * 如果選擇&#x200B;**建立組**，則輸入組ID和可選說明。

   ![creategroupdial](assets/creategroupdialog.png)

1. 按一下&#x200B;**建立**。您建立的用戶或組將顯示在樹清單中。

### 刪除用戶和組{#deleting-users-and-groups}

要刪除用戶或組：

1. 在&#x200B;**Security**&#x200B;主控台中，選取您要刪除的使用者或群組。 如果要刪除多個項目，請按住Shift鍵並按一下或按住Control鍵並按一下以選擇這些項目。
1. 按一下「編輯」，然後選取「刪除」。 **** AEMWCM會詢問您是否要刪除使用者或群組。
1. 按一下&#x200B;**OK**&#x200B;確認或取消取消操作。

### 修改用戶和組屬性{#modifying-user-and-group-properties}

要修改用戶和組屬性：

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要修改的用戶或組名。

1. 按一下「**屬性**」頁籤，進行所需更改，然後按一下「保存&#x200B;**」。**

   ![cqsecurityuserprop](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>用戶的路徑顯示在用戶屬性的底部。 無法修改。

### 更改用戶密碼{#changing-a-user-password}

請按下列步驟修改用戶的口令。

>[!NOTE]
>
>您無法使用安全控制台來變更管理員密碼。 若要變更管理員帳戶的密碼，請使用Granite Operations提供的[Users console](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。
>
>如果您在JEE上使用AEM Forms，請勿使用下列指示變更密碼，而是使用JEE管理控制台(/adminui)上的AEM Forms來變更密碼。

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要更改密碼的用戶名。
1. 按一下&#x200B;**屬性**&#x200B;頁籤（如果尚未激活）。
1. 按一下&#x200B;**設定密碼**。 「Set Password（設定密碼）」視窗隨即開啟，您可在其中變更密碼。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 輸入新密碼兩次；由於它們未顯示在明文中，因此這是供確認的——如果它們不匹配，系統將顯示錯誤。
1. 按一下&#x200B;**設定**&#x200B;以激活帳戶的新密碼。

### 將用戶或組添加到組{#adding-users-or-groups-to-a-group}

提AEM供三種將使用者或群組新增至現有群組的不同方式：

* 在群組中時，您可以新增成員（使用者或群組）。
* 在成員中時，可以向組添加成員。
* 當您使用「權限」時，可以將成員添加到組。

### 組——向組{#groups-adding-users-or-groups-to-a-group}添加用戶或組

**Groups**&#x200B;標籤顯示當前帳戶所屬的組。 您可以使用它將所選帳戶新增至群組：

1. 連按兩下您要指派給群組的帳戶（使用者或群組）名稱。
1. 按一下&#x200B;**組**&#x200B;頁籤。 您會看到帳戶已屬於的群組清單。
1. 在樹清單中，按一下要添加到帳戶的組的名稱，並將其拖動到&#x200B;**組**&#x200B;窗格。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Control鍵並按一下這些名稱並拖動它們。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 成員——將用戶或組添加到組{#members-adding-users-or-groups-to-a-group}

**成員**&#x200B;頁籤僅適用於組，並顯示哪些用戶和組屬於當前組。 您可以用它來新增帳戶至群組：

1. 按兩下要添加成員的組的名稱。
1. 按一下&#x200B;**成員**&#x200B;頁籤。 您會看到已屬於此群組的成員清單。
1. 在樹清單中，按一下要添加到組的成員的名稱，並將其拖動到&#x200B;**成員**&#x200B;窗格。 （如果要添加多個用戶，請按住Shift鍵並按一下或按住Control鍵並按一下這些名稱並拖動它們。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 在添加權限{#adding-users-or-groups-while-adding-permissions}時添加用戶或組

要在特定路徑中向組添加成員，請執行以下操作：

1. 連按兩下您要新增使用者之群組或使用者的名稱。

1. 按一下&#x200B;**權限**&#x200B;頁籤。

1. 導覽至您要新增權限的路徑，然後按一下&#x200B;**詳細資訊**。 詳細資訊視窗的下半部分提供有關誰擁有該頁面權限的資訊。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 在&#x200B;**Member**&#x200B;列中，為要具有該路徑權限的成員選擇複選框。 清除要移除權限的成員的複選框。 在您所做變更的儲存格中，會出現紅色三角形。
1. 按一下&#x200B;**確定**&#x200B;保存更改。

### 從組{#removing-users-or-groups-from-groups}中刪除用戶或組

提AEM供三種從群組中移除使用者或群組的不同方式：

* 在群組設定檔中時，您可以移除成員（使用者或群組）。
* 在成員配置檔案中時，可以從組中刪除成員。
* 當您使用「權限」時，可以從群組中移除成員。

### 組——從組{#groups-removing-users-or-groups-from-groups}中刪除用戶或組

要從組中刪除用戶或組帳戶：

1. 連按兩下您要從群組移除的群組或使用者帳戶名稱。
1. 按一下&#x200B;**組**&#x200B;頁籤。 您可以看到所選帳戶所屬的群組。
1. 在&#x200B;**群組**&#x200B;窗格中，按一下您要從群組移除的使用者或群組名稱，然後按一下&#x200B;**移除**。 （如果要刪除多個帳戶，請按住Shift鍵並按一下或按住Control鍵並按一下這些名稱，然後按一下&#x200B;**刪除**。）

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 成員——從組{#members-removing-users-or-groups-from-groups}中刪除用戶或組

要從組中刪除帳戶，請執行以下操作：

1. 按兩下要從中刪除成員的組的名稱。
1. 按一下&#x200B;**成員**&#x200B;頁籤。 您會看到已屬於此群組的成員清單。
1. 在&#x200B;**成員**&#x200B;窗格中，按一下要從組中刪除的成員的名稱，然後按一下&#x200B;**刪除**。 （如果要刪除多個用戶，請按住Shift鍵並按一下或按住Control鍵並按一下這些名稱，然後按一下&#x200B;**Remove**。）

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 在添加權限{#removing-users-or-groups-while-adding-permissions}時刪除用戶或組

要在特定路徑上從組中刪除成員：

1. 連按兩下您要移除使用者之群組或使用者的名稱。

1. 按一下&#x200B;**權限**&#x200B;頁籤。

1. 導覽至您要移除權限的路徑，然後按一下&#x200B;**Details**。 詳細資訊視窗的下半部分提供有關誰擁有該頁面權限的資訊。

   ![chlimage_1-115](assets/chlimage_1-114.png)

1. 在&#x200B;**Member**&#x200B;列中，為要具有該路徑權限的成員選擇複選框。 清除要移除權限的成員的複選框。 在您所做變更的儲存格中，會出現紅色三角形。
1. 按一下&#x200B;**確定**&#x200B;保存更改。

### 用戶同步{#user-synchronization}

當部署為[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，所有發佈節點之間需要同步用戶和組。

要瞭解用戶同步以及如何啟用它，請參閱[用戶同步](/help/sites-administering/sync.md)。

## 管理權限{#managing-permissions}

>[!NOTE]
>
>Adobe已推出新的以Touch UI為基礎的權限管理主要檢視。 有關如何使用它的詳細資訊，請參閱[本頁](/help/sites-administering/touch-ui-principal-view.md)。

本節介紹如何設定權限，包括複製權限。

### 設定權限{#setting-permissions}

權限可讓使用者在特定路徑上對資源執行特定動作。 它也包含建立或刪除頁面的功能。

要添加、修改或刪除權限：

1. 在&#x200B;**Security**&#x200B;控制台中，按兩下要為或[搜索節點](#searching-for-nodes)設定權限的用戶或組的名稱。

1. 按一下&#x200B;**權限**&#x200B;頁籤。

   ![cquser權限](assets/cquserpermissions.png)

1. 在樹形網格中，選擇一個複選框以允許選定用戶或組執行操作，或清除一個複選框以拒絕選定用戶或組執行操作。 有關詳細資訊，請按一下&#x200B;**Details**。

1. 完成後，按一下&#x200B;**保存**。

### 設定複製權限{#setting-replication-privileges}

複製權限是發佈內容的權限，可為組和用戶設定。

>[!NOTE]
>
>* 應用到組的任何複製權限都應用於該組中的所有用戶。
>* 用戶的複製權限將取代組的複製權限。
>* 「允許複製」權限的優先順序高於「拒絕」複製權限。 如需詳細資訊，請參閱AEM](#permissions-in-aem)中的[權限。

>



要設定複製權限，請執行以下操作：

1. 從清單中選擇用戶或組，按兩下以開啟，然後按一下&#x200B;**權限**。
1. 在網格中，導航到希望用戶具有複製權限或[搜索節點的路徑。](#searching-for-nodes)

1. 在所選路徑的&#x200B;**Replicate**&#x200B;列中，選擇一個複選框以添加該用戶或組的複製權限，或清除該複選框以刪除複製權限。 在您AEM所做的變更尚未儲存的任何地方，都會顯示紅色三角形。

   ![cquserreplicate權限](assets/cquserreplicatepermissions.png)

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 搜索節點{#searching-for-nodes}

新增或移除權限時，您可以瀏覽或搜尋節點。

路徑搜尋有兩種不同類型：

* 路徑搜索——如果搜索字串以&quot;/&quot;開頭，則搜索將搜索給定路徑的直接子節點：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜尋方塊中，您可以執行下列動作：

| 動作 | 它的功能 |
|--- |--- |
| 向右鍵 | 在搜索結果中選擇子節點 |
| 向下鍵 | 再次啟動搜索。 |
| 輸入（返回）鍵 | 選擇子節點並將其載入到樹狀網格中 |

* 全文搜索——如果搜索字串不以&quot;/&quot;開頭，則對路徑&quot;/content&quot;下的所有節點執行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要對路徑或全文執行搜索，請執行以下操作：

1. 在安全控制台中，選擇用戶或組，然後按一下&#x200B;**權限**&#x200B;頁籤。

1. 在「搜尋」方塊中，輸入要搜尋的詞語。

### 模擬用戶{#impersonating-users}

您可以指定一或多個允許模擬目前使用者的使用者。 這表示他們可以將帳戶設定切換為目前使用者的帳戶設定，並代表此使用者行事。

使用此函式時請小心謹慎，因為它可能允許使用者執行其使用者無法執行的動作。 在模擬使用者時，會通知使用者他們並未以自己的身分登入。

您可能想要使用此功能時，會出現多種情況，包括：

* 如果您不在辦公室，您可以讓其他人在您不在的時候冒充您。 使用此功能，您可以確保某人擁有您的存取權限，而您不需要修改使用者設定檔或提供密碼。
* 您可將其用於除錯用途。 例如，若要查看網站如何尋找具有限制存取權限的使用者。 此外，如果使用者抱怨技術問題，您可以模擬該使用者來診斷和修正問題。

要模擬現有用戶，請執行以下操作：

1. 在樹清單中，選擇要為其他用戶指派模擬的人員的名稱。 按兩下以開啟。
1. 按一下&#x200B;**Impersonators**&#x200B;頁籤。
1. 按一下您要能夠模擬所選使用者的使用者。 將使用者（將模擬的使用者）從清單拖曳至「模擬」窗格。 名稱會出現在清單中。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 按一下「**儲存**」。

### 設定用戶和組首選項{#setting-user-and-group-preferences}

要設定用戶和組首選項，包括語言、窗口管理和工具欄首選項：

1. 在左側樹中選擇要更改其首選項的用戶或組。 要選擇多個用戶或組，請按住Ctrl鍵並按一下或按住Shift鍵並按一下您的選項。
1. 按一下&#x200B;**首選項**&#x200B;頁籤。

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 根據需要對組或用戶首選項進行更改，並在完成後按一下「保存」。****

### 將用戶或管理員設定為具有管理其他用戶{#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}的權限

若要設定使用者或管理員擁有刪除／啟用／停用其他使用者的權限：

1. 將您要授予管理其他使用者權限的使用者新增至管理員群組，並儲存您所做的變更。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用戶的&#x200B;**權限**&#x200B;頁籤中，導航到&quot;/&quot;，在複製列中，選擇複選框以允許在&quot;/&quot;進行複製，然後按一下&#x200B;**保存**。

   ![cqsecurityreplicate權限](assets/cqsecurityreplicatepermissions.png)

   選取的使用者現在可以停用、啟用、刪除和建立使用者。

### 擴展項目級別{#extending-privileges-on-a-project-level}的權限

如果您打算實作應用程式特定權限，下列資訊將說明您實作自訂權限時需要瞭解的資訊，以及如何在整個CQ中實施自訂權限：

階層修改權限由jcr-privileges的組合所涵蓋。 複製權限名為&#x200B;**crx:replicate**，該權限與jcr儲存庫上的其他權限一起儲存／評估。 但是，它並未在jcr層級上執行。

自訂權限的定義和註冊正式屬於[Jackrabbit API](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html)自2.4版起（另請參閱[JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)）。 JCR訪問控制管理包括進一步的使用，如由[JSR 283](https://jcp.org/en/jsr/detail?id=283)（第16節）定義。 此外，Jackrabbit API還定義了數個擴充功能。

權限註冊機制反映在&#x200B;**Repository Configuration**&#x200B;下的UI中。

新（自定義）權限的註冊本身受到必須在儲存庫級別(在JCR中：將&#39;null&#39;傳入ac mgt api中作為&#39;absPath&#39;參數，如需詳細資訊，請參閱jsr 333)。 預設情況下，**admin**&#x200B;和所有管理員成員都具有該權限。

>[!NOTE]
>
>雖然實作會負責驗證和評估自訂權限，但除非它們是內建權限的匯總，否則無法強制執行這些權限。
