---
title: 使用CRXDE Lite開發
seo-title: Developing with CRXDE Lite
description: CRXDE Lite內嵌於AEM中，可讓您在瀏覽器中執行標準開發工作
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 2%

---

# 使用CRXDE Lite開發{#developing-with-crxde-lite}

本節說明如何使用CRXDE Lite開發您的AEM應用程式。

如需可用不同開發環境的詳細資訊，請參閱概述檔案。

CRXDE Lite內嵌於AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄時建立項目、建立和編輯檔案(如.jsp和.java)、資料夾、模板、元件、對話框、節點、屬性和包。
當您沒有AEM伺服器的直接存取權、透過擴充或修改現成元件和Java套件組合來開發應用程式時，或您不需要專用的除錯工具、程式碼完成和語法醒目提示時，建議使用CRXDE Lite。

>[!NOTE]
>
>從AEM 6.5.5.0開始，已無法再匿名存取CRXDE Lite。
>系統會將使用者重新導向至登入畫面。


>[!NOTE]
>
>建議使用 [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) 和 [AEM HTL Brackets擴充功能](/help/sites-developing/aem-brackets.md) 在項目開發期間。

## 開始使用CRXDE Lite {#getting-started-with-crxde-lite}

若要開始使用CRXDE Lite，請繼續如下：

1. 安裝AEM。
1. 在瀏覽器中，輸入 `https://<host>:<port>/crx/de`. 預設為 `https://localhost:4502/crx/de`.
1. 輸入 **用戶名** 和 **密碼**. 預設為 `admin` 和 `admin`.

1. 按一下&#x200B;**「確定」**。

CRXDE Lite使用者介面在瀏覽器中的外觀如下：

![chlimage_1-18](assets/crx-interface.jpg)

您現在可以使用CRXDE Lite來開發您的應用程式。

## 使用者介面概觀 {#overview-of-the-user-interface}

CRXDE Lite提供下列功能：

<table>
 <tbody>
  <tr>
   <td>頂級切換器列</td>
   <td>可讓您快速切換CRXDE Lite、封裝管理器和封裝共用。</td>
  </tr>
  <tr>
   <td>節點路徑構件</td>
   <td><p>顯示當前所選節點的路徑。</p> <p>您也可以使用它跳到節點，方法是手動輸入路徑，或從其他位置貼上路徑，然後按Enter。</p> <p>它還支援查找具有特定節點名稱的節點。 輸入要查找的節點名稱，然後等待（或按一下右側的搜索符號）。 您可以嘗試輸入，例如字串 <em>oak</em> 進入介面工具集，了解運作方式。 如果給定的節點或節點被載入到瀏覽器窗格中，則會顯示該清單，您可以選擇路徑，然後按Enter鍵導航到該路徑。 請注意，它僅適用於瀏覽器中目前載入至CRXDE用戶端應用程式的節點。 如果要搜索整個儲存庫，請使用「工具」，然後使用「查詢」。</p> </td>
  </tr>
  <tr>
   <td>瀏覽器窗格</td>
   <td><p>顯示儲存庫中所有節點的樹。</p> <p>按一下節點以在 <strong>屬性</strong> 標籤。 按一下節點後，您可以在工具列中選取動作。 再按一下該節點以重新命名。</p> <p>樹狀導航過濾器（雙目表徵圖）:可讓您篩選儲存庫中名稱包含輸入文字的節點。 它僅適用於已在本機載入的節點。<br /> </p> </td>
  </tr>
  <tr>
   <td>編輯窗格</td>
   <td><p><strong>首頁</strong> 標籤：可讓您搜尋內容和/或檔案，並存取開發人員資源（檔案、開發人員部落格、知識庫）和支援(Adobe首頁和支援中心)。<br /> </p> <p>按兩下 <strong>瀏覽器</strong> 窗格來顯示其內容；例如.jsp或.java檔案。 然後，您可以修改它並儲存變更。</p> <p>在 <strong>編輯</strong> ，工具欄上將提供以下工具：<br /> </p> - <strong>在樹中顯示： </strong>在儲存庫樹中顯示檔案。<br /> - <strong>搜索/替換……</strong>:搜尋或取代。<br /> <br /> 按兩下 <strong>編輯</strong> 窗格開啟 <strong>轉到行</strong> 對話框，以便輸入要轉到的特定行號。<br /> </td>
  </tr>
  <tr>
   <td>「屬性」頁簽<br /> </td>
   <td>顯示所選節點的屬性。 您可以新增屬性或刪除現有屬性。<br /> </td>
  </tr>
  <tr>
   <td>「訪問控制」頁簽</td>
   <td><p>根據當前路徑、儲存庫級別或主體顯示權限。</p> <p>權限會劃分為</p> <p>- <strong>適用的訪問控制策略</strong>:可應用於當前選擇的策略。</p> <p>- <strong>本地訪問控制策略</strong>:當前策略在本地應用於當前選擇。</p> <p>- <strong>有效的訪問控制策略</strong>:當前策略應用於當前選擇，可以在本地設定，也可以從父節點繼承。</p> <p>注意. 要能夠查看訪問控制資訊，登錄到CRXDE Lite的用戶必須具有讀取ACL項的權限。 匿名用戶預設看不到此資訊 — 請以（例如，管理員）身份登錄以查看該資訊。</p> </td>
  </tr>
  <tr>
   <td>復寫索引標籤</td>
   <td><p>顯示當前節點的複製狀態。 您可以複製和複製刪除當前節點。</p> </td>
  </tr>
  <tr>
   <td>主控台標籤<br /> </td>
   <td><p><strong>伺服器日誌</strong>:</p> <p>顯示日誌消息。 您可以設定記錄層級、清除主控台、釘選選取的捲動位置，以及啟用/停用訊息顯示。<br /> </p> <p><strong>版本控制</strong>:</p> <p>顯示版本控制消息。<br /> </p> </td>
  </tr>
  <tr>
   <td>建置資訊標籤<br /> </td>
   <td>顯示建立套件組合時的資訊。<br /> </td>
  </tr>
  <tr>
   <td>重新整理<br /> </td>
   <td>刷新當前選擇。 系統會在您檢視存放庫時更新其他使用者的變更。 您所做的變更不受影響。<br /> </td>
  </tr>
  <tr>
   <td>儲存全部</td>
   <td><p><strong>儲存全部</strong>:<br /> </p> <p>保存您所做的所有更改。 在您按一下「儲存」之前，變更為暫時狀態，當您退出主控台時將會遺失。</p> <p><strong>回復</strong>:</p> <p>放棄自上次保存操作以來在選定節點上所做的所有更改，然後重新載入選定節點的儲存庫的當前狀態。</p> <p><strong>全部回復</strong>:</p> <p>放棄自上次保存操作後在整個儲存庫中所做的所有更改，然後重新載入儲存庫的當前狀態。</p> </td>
  </tr>
  <tr>
   <td>建立 ...<br /> </td>
   <td><p>下拉式功能表，在選取的節點下建立下列項目：<br /> </p> <p>- <strong>節點</strong>:具有任意節點類型的節點<br /> </p> <p>- <strong>檔案</strong>:nt:file節點及其nt:resource子節點</p> <p>- <strong>資料夾</strong>:nt:folder節點</p> <p>- <strong>範本</strong>:AEM範本</p> <p>- <strong>元件</strong>:AEM元件</p> <p>- <strong>對話方塊</strong>:AEM對話方塊</p> </td>
  </tr>
  <tr>
   <td>刪除<br /> </td>
   <td>刪除選定節點。<br /> </td>
  </tr>
  <tr>
   <td>複製</td>
   <td>複製所選節點。<br /> </td>
  </tr>
  <tr>
   <td>貼上<br /> </td>
   <td>將複製的節點貼入所選節點下。<br /> </td>
  </tr>
  <tr>
   <td>移動 ...<br /> </td>
   <td>將所選節點移動到通過對話框設定的節點。</td>
  </tr>
  <tr>
   <td>重新命名 ...<br /> </td>
   <td>更名所選節點。<br /> </td>
  </tr>
  <tr>
   <td>Mixin ...<br /> </td>
   <td>可讓您將混合類型新增至節點類型。 混合類型主要用於添加高級功能，如版本設定、訪問控制、引用和鎖定到節點。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉式功能表搭配下列工具：</p> <p>- <strong>伺服器配置……</strong>:來存取Felix Console。</p> <p>- <strong>查詢……</strong>:來查詢儲存庫。</p> <p>- <strong>權限……</strong>:要開啟權限管理，可在其中查看和添加權限。</p> <p>- <strong>測試訪問控制……</strong>:可以測試特定路徑和/或主體權限的位置。</p> <p>- <strong>導出節點類型</strong>:要將系統中的節點類型導出為cnd標籤法。</p> <p>- <strong>導入節點類型……</strong>:要使用cnd標籤法導入節點類型，請執行以下操作：</p> <p>- <strong>安裝SiteCatalyst調試器……</strong>:Analytics偵錯工具安裝說明。</p> </td>
  </tr>
  <tr>
   <td>登入介面工具集<br /> </td>
   <td><p>顯示目前登入的使用者及其登入的工作區，例如admin@crx.default。</p> <p>按一下它以登入或重新登入為特定使用者。 如果您未指定要登入的工作區，則會登入預設工作區crx.default。</p> <p>如果要以匿名用戶身份瀏覽儲存庫，請使用 <strong>匿名</strong> 作為登入名稱，以及任何密碼（例如空格或點）。<br /> </p> <p>如果您的授權不再有效（例如已過期），則登入Widget會顯示「<strong>未授權 — 登錄……</strong>」。 按一下它以重新登入。</p> </td>
  </tr>
 </tbody>
</table>

## 建立資料夾 {#creating-a-folder}

要建立具有CRXDE Lite的資料夾：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導航窗格中，按一下右鍵要在其下建立新資料夾的資料夾，選擇 **建立……**，然後 **建立資料夾……**.

1. 輸入資料夾 **名稱** 按一下 **確定**.

1. 按一下 **全部儲存** 以在伺服器上儲存變更。

## 建立範本 {#creating-a-template}

若要建立具有CRXDE Lite的範本：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導航窗格中，按一下右鍵要建立模板的資料夾，選擇 **建立……**，然後 **建立模板……**.

1. 輸入 **標籤**, **標題**, **說明**, **資源類型** 和 **排名** 範本。 按一下&#x200B;**下一步**。

1. 此步驟為選用：設定 **允許的路徑**. 按一下 **下一個**

1. 此步驟為選用：設定 **允許的父項**. 按一下&#x200B;**下一步**。

1. 此步驟為選用：設定 **允許的子項**. 按一下&#x200B;**「確定」**。

1. 按一下 **全部儲存** 以在伺服器上儲存變更。

它會建立：

* 類型的節點 `cq:Template` 具有模板屬性

* 類型的子節點 `cq:PageContent` 具有頁面內容屬性

您可以將屬性新增至範本：請參閱 [建立屬性](#creating-a-property) 區段。

## 建立元件 {#creating-a-component}

只有安裝CQ5（亦即節點類型）時，此處所述的功能才可使用 `cq:Component` 可在存放庫中使用。

要建立具有CRXDE Lite的元件：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導航窗格中，按一下右鍵要建立元件的資料夾，然後選擇 **建立……**，然後 **建立元件……**.

1. 輸入 **標籤**, **標題**, **說明**, **超級資源類型** 和 **群組** 的下界。 按一下&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **是容器，** **無裝飾**, **儲存格名稱** 和 **對話方塊路徑**. 按一下&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **允許的父項**. 按一下&#x200B;**下一步**。

1. 此步驟為選用：設定元件屬性 **允許的子項**. 按一下&#x200B;**「確定」**。

1. 按一下 **全部儲存** 以在伺服器上儲存變更。

它會建立：

* 類型的節點 `cq:Component`
* 元件屬性
* 元件.jsp指令碼

## 建立對話方塊 {#creating-a-dialog}

要建立具有CRXDE Lite的對話框：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，按一下右鍵要建立對話框的元件，然後選擇 **建立……**，然後 **建立對話框……**.

1. 輸入 **標籤** 和 **標題**. 按一下&#x200B;**「確定」**。

1. 按一下 **保存全部** l將更改保存在伺服器上。

它會建立具有下列結構的對話方塊：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您現在可以修改屬性或建立新節點，以適應您的需求。

也可以使用對話框編輯器編輯對話框。 按兩下CRXDE Lite中的對話方塊節點會顯示編輯器。 有關對話框編輯器的更多資訊 [此處](/help/sites-developing/dialog-editor.md).

## 建立節點 {#creating-a-node}

要建立具有CRXDE Lite的節點：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，按一下右鍵要建立新節點的節點，然後選擇 **建立……**，然後 **建立節點……**.
1. 輸入 **名稱** 和 **類型**. 按一下&#x200B;**「確定」**。
1. 按一下 **全部儲存** 以在伺服器上儲存變更。

您現在可以修改屬性或建立新節點，以適應您的需求。

>[!NOTE]
>
>大多數編輯操作（包括「建立節點」）都保留記憶體中的所有更改，並且僅在保存時（通過「全部保存」按鈕）將其儲存到儲存庫中。 不過，某些操作（例如移動）會自動持續存在。
>
>在保存更改時，JCR儲存庫也首先執行有關新建立的節點是否允許父節點的節點類型的驗證。 如果您在儲存節點時收到錯誤訊息，請檢查內容結構是否有效(例如，您無法建立 `nt:unstructured` 節點作為的子節點 `nt:folder` 節點)。

## 建立屬性 {#creating-a-property}

若要建立具有CRXDE Lite的屬性：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，選擇要添加新屬性的節點。
1. 在 **屬性** 頁簽，輸入 **名稱**, **類型** 和 **值**. 按一下&#x200B;**「新增」**。

1. 按一下 **全部儲存** 以在伺服器上儲存變更。

## 建立指令碼 {#creating-a-script}

要建立新指令碼：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，按一下右鍵要建立指令碼的元件，然後選擇 **建立……**，然後 **建立檔案……**.

1. 輸入檔案 **名稱** 包括其擴充功能。 按一下&#x200B;**「確定」**。

1. 新檔案在「編輯」窗格中以頁簽形式開啟。
1. 編輯檔案。
1. 按一下 **全部儲存** 以儲存變更。

## 導出和導入節點類型 {#exporting-and-importing-node-types}

有了CRXDE Lite，您可以在 [CND（緊密命名空間和節點類型定義）記號](https://jackrabbit.apache.org/jcr/node-type-notation.html).

要導出節點類型定義，請執行以下操作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選取您所需的節點。
1. 選擇 **工具** then **導出節點類型**.

1. 定義（以符號表示）會顯示在您的瀏覽器中。 視需要儲存資訊。

要導入節點類型定義，請執行以下操作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選擇 **工具** then **導入節點類型……**.

1. 在文本框中輸入定義的CND注釋。
1. 檢查 **允許更新** 如果要更新現有定義。
1. 按一下 **匯入**.

## 記錄 {#logging}

透過CRXDE Lite，您可以顯示檔案 `error.log` 位於 `<crx-install-dir>/crx-quickstart/server/logs` 並以適當的記錄層級篩選。 按如下步驟進行：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在 **主控台** 標籤，在右側的下拉式功能表中，選取 **伺服器記錄檔**.

1. 按一下 **停止** 圖示來顯示訊息。

您可以：

* 按一下 **記錄設定** 表徵圖。
* 按一下 **筆刷** 表徵圖。
* 按一下 **針** 表徵圖。
* 按一下 **停止** 表徵圖。

## 存取控制 {#access-control}

>[!NOTE]
>
>請參閱 [使用者、群組和存取權限管理](/help/sites-administering/user-group-ac-admin.md) 以取得更多資訊。
