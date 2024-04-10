---
title: 許可權管理的主體檢視
description: 瞭解新的觸控式UI介面有助於進行許可權管理。
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# 許可權管理的主體檢視{#principal-view-for-permissions-management}

## 概觀 {#overview}

AEM 6.5推出使用者和群組的許可權管理。 主要功能與傳統UI相同，但更加方便使用者且更有效率。

## 使用方式 {#how-to-use}

### 存取UI {#accessing-the-ui}

新的UI型許可權管理可透過「安全性」下的「許可權」卡進行存取，如下所示：

![許可權管理UI](assets/screen_shot_2019-03-17at63333pm.png)

新檢視可讓您更輕鬆地檢視所有已明確授予許可權的路徑中指定主體的整套許可權和限制。 如此一來，您就不需要前往

CRXDE可管理進階許可權和限制。 它已在相同檢視中合併。 該檢視預設為「所有人」群組。

![「所有人」群組的檢視](assets/unu-1.png)

有一個篩選器可讓使用者選擇要檢視的主參與者型別 **使用者**， **群組**，或 **全部**&#x200B;並搜尋任何主體&#x200B;**.**

![搜尋主參與者型別](assets/image2019-3-20_23-52-51.png)

### 檢視主體的許可權 {#viewing-permissions-for-a-principal}

左側的框架可讓使用者向下捲動以尋找任何主參與者，或根據選取的篩選器搜尋「群組」或「使用者」，如下所示：

![檢視主體的許可權](assets/doi-1.png)

按一下名稱即可在右側顯示指派的許可權。 許可權窗格會顯示特定路徑上的存取控制專案清單以及設定的限制。

![檢視ACL清單](assets/trei-1.png)

### 為主體加入新的存取控制專案 {#adding-new-access-control-entry-for-a-principal}

可以透過新增存取控制專案來新增新許可權。 只要按一下「新增ACE」按鈕即可。

![為主體新增新的ACL](assets/patru.png)

這會顯示以下視窗，下一步是選擇必須設定許可權的路徑。

![設定許可權路徑](assets/cinci-1.png)

您可在此選取一個路徑，從中設定許可權 **dam-users**：

![dam-users的設定範例](assets/sase-1.png)

選取路徑後，工作流程會返回此畫面，使用者可在其中從可用名稱空間(例如 `jcr`， `rep` 或 `crx`)，如下所示。

您可以使用文字欄位進行搜尋，然後從清單中選取，以新增許可權。

>[!NOTE]
>
>如需許可權和說明的完整清單，請參閱 [此頁面](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![指定路徑的搜尋許可權。](assets/image2019-3-21_0-5-47.png) ![新增「dam-users」專案，如垂直欄中所選路徑所示。](assets/image2019-3-21_0-6-53.png)

選取許可權清單後，使用者即可選擇許可權型別：拒絕或允許，如下所示。

![選取許可權](assets/screen_shot_2019-03-17at63938pm.png) ![選取許可權](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制 {#using-restrictions}

除了指定路徑的許可權清單和許可權型別之外，此畫面還可讓您新增精細存取控制的限制，如下所示：

![新增限制](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>如需每個限制含義的詳細資訊，請參閱 [Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

選擇限制型別、輸入值並按一下 **+** 圖示。

![新增限制型別](assets/sapte-1.png) ![新增限制型別](assets/opt-1.png)

新的ACE會反映在「存取控制清單」中，如下所示。 請注意 `jcr:write` 是包含下列專案的彙總許可權 `jcr:removeNode` 以上所新增，但並未於下方顯示為 `jcr:write`.

### 編輯ACE {#editing-aces}

選取主參與者並選擇您要編輯的ACE，即可編輯存取控制專案。

例如，您可以在此處編輯以下專案 **dam-users** 按一下右側的鉛筆圖示：

![新增限制](assets/image2019-3-21_0-35-39.png)

編輯畫面中會顯示預先選取的已設定ACE，按一下它們旁邊的交叉圖示即可刪除這些ACE，或者可以為指定路徑新增許可權，如下所示。

![編輯專案](assets/noua-1.png)

此處 `addChildNodes` 已新增許可權 **dam-users** 於指定路徑。

![新增許可權](assets/image2019-3-21_0-45-35.png)

按一下「 」以儲存變更 **儲存** 按鈕，而變更會反映在的新許可權中 **dam-users** 如下所示：

![儲存變更](assets/zece-1.png)

### 刪除ACE {#deleting-aces}

可以刪除存取控制專案，以移除指定給特定路徑上主要人的所有許可權。 ACE旁的X圖示可用來刪除它，如下所示：

![刪除ACE](assets/image2019-3-21_0-53-19.png) ![刪除ACE](assets/unspe.png)

### 傳統UI許可權組合 {#classic-ui-privilege-combinations}

新許可權UI會明確使用基本許可權集，而非無法真正反映已授與之確切基礎許可權的預定義組合。

這會導致混淆，無法確定確切的設定內容。 下表列出從傳統UI到組成許可權的實際許可權組合之間的對應：

<table>
 <tbody>
  <tr>
   <th>傳統UI許可權組合</th>
   <th>許可權UI許可權</th>
  </tr>
  <tr>
   <td>讀取</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>建立</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>讀取 ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>編輯 ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>複寫</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
