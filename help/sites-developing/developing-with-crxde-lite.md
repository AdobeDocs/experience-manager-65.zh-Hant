---
title: 使用CRXDE Lite進行開發
seo-title: 使用CRXDE Lite進行開發
description: CRXDE Lite已內嵌在AEM中，可讓您在瀏覽器中執行標準開發工作
seo-description: CRXDE Lite已內嵌在AEM中，可讓您在瀏覽器中執行標準開發工作
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 1%

---


# 使用CRXDE Lite進行開發{#developing-with-crxde-lite}

本節說明如何使用CRXDE Lite開發AEM應用程式。

請參閱概述檔案，以取得有關不同開發環境的詳細資訊。

CRXDE Lite已內嵌在AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄時建立專案、建立和編輯檔案（例如。jsp和。java）、檔案夾、範本、元件、對話方塊、節點、屬性和組合。
當您無法直接存取AEM伺服器、透過擴充或修改現成可用的元件和Java套件來開發應用程式時，或當您不需要專用的除錯程式、程式碼完成和語法反白顯示時，建議使用CRXDE Lite。

>[!NOTE]
>
>從AEM 6.5.5.0開始，就無法再匿名存取CRXDE Lite。
>使用者會重新導向至登入畫面。


>[!NOTE]
>
>建議在專案開發 [期間使用AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) 和 [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) 。

## CRXDE Lite快速入門 {#getting-started-with-crxde-lite}

要開始使用CRXDE Lite，請按如下步驟進行：

1. 安裝AEM。
1. 在瀏覽器中輸入 `https://<host>:<port>/crx/de`。 預設為 `https://localhost:4502/crx/de`。
1. 輸入您的 **使用者名** 稱 **和密碼**。 預設為 `admin` 和 `admin`。

1. 按一下 **確定**。

CRXDE Lite使用者介面在您的瀏覽器中的外觀如下：

![chlimage_1-18](assets/crx-interface.jpg)

您現在可以使用CRXDE Lite來開發您的應用程式。

## 使用者介面概觀 {#overview-of-the-user-interface}

CRXDE Lite提供下列功能：

<table>
 <tbody>
  <tr>
   <td>頂端切換器列</td>
   <td>可讓您快速切換CRXDE Lite、Package Manager和Package Share。</td>
  </tr>
  <tr>
   <td>節點路徑Widget</td>
   <td><p>顯示當前選定節點的路徑。</p> <p>您也可以使用它跳至節點，方法是手動輸入路徑，或從其他位置貼上路徑，然後按Enter鍵。</p> <p>它還支援查找具有特定節點名的節點。 輸入您要尋找的節點名稱，然後等待（或點擊右側的搜尋符號）。 您可以嘗試輸入，例如，將字串 <em>橡樹</em> ，輸入介面工具集，以瞭解其運作方式。 如果某個給定節點或節點已載入到瀏覽器窗格中，則會顯示清單，您可以選擇路徑並按一下Enter以導航到該路徑。 請注意，它僅適用於當前在瀏覽器中載入到CRXDE客戶端應用程式中的節點。 如果要搜索整個儲存庫，請依次使用工具和查詢。</p> </td>
  </tr>
  <tr>
   <td>瀏覽器窗格</td>
   <td><p>顯示儲存庫中所有節點的樹。</p> <p>按一下節點，在「屬性」頁籤中顯示其 <strong>屬性</strong> 。 按一下節點後，可以在工具欄中選擇操作。 再次按一下該節點以將其更名。</p> <p>樹狀導航濾鏡（雙目表徵圖）: 使您可以過濾名稱包含輸入文本的儲存庫中的節點。 它僅適用於已在本地載入的節點。<br /> </p> </td>
  </tr>
  <tr>
   <td>編輯窗格</td>
   <td><p><strong>「首頁</strong> 」頁籤： 可讓您搜尋內容和／或檔案，並存取開發人員資源（檔案、開發人員部落格、知識庫）和支援（Adobe首頁和支援中心）。<br /> </p> <p>連按兩下「檔案總管」窗格中 <strong>的檔案</strong> ，以顯示其內容； 例如，.jsp或。java檔案。 然後，您可以修改它並儲存變更。</p> <p>在「編輯」窗格中編輯檔 <strong>案後</strong> ，工具列上會提供下列工具：<br /> </p> -在 <strong>樹中顯示： </strong>顯示儲存庫樹中的檔案。<br /> -搜 <strong>尋／取代……</strong>: 進行搜尋或取代。<br /> <br /> 連按兩下「編輯」窗格的狀態行，會開啟「 <strong>跳至行</strong><strong></strong> 」對話方塊，讓您輸入要跳至的特定行號。<br /> </td>
  </tr>
  <tr>
   <td>「屬性」頁籤<br /> </td>
   <td>顯示所選節點的屬性。 您可以新增屬性或刪除現有屬性。<br /> </td>
  </tr>
  <tr>
   <td>「訪問控制」頁籤</td>
   <td><p>根據當前路徑、儲存庫級別或承擔者顯示權限。</p> <p>權限被劃分為</p> <p>-適 <strong>用的訪問控制策略</strong>: 可套用至目前選擇的原則。</p> <p>-本 <strong>地訪問控制策略</strong>: 當前策略在本地應用於當前選擇。</p> <p>-有 <strong>效的訪問控制策略</strong>: 當前為當前選擇應用的策略可以設定為本地或繼承自父節點。</p> <p>注意. 要能夠查看訪問控制資訊，登錄到CRXDE Lite的用戶必須具有讀取ACL項的權限。 匿名使用者依預設看不到此資訊——請以管理員等身分登入，以檢視資訊。</p> </td>
  </tr>
  <tr>
   <td>複製頁籤</td>
   <td><p>顯示當前節點的複製狀態。 您可以複製和複製刪除當前節點。</p> </td>
  </tr>
  <tr>
   <td>控制台頁籤<br /> </td>
   <td><p><strong>伺服器日誌</strong>:</p> <p>顯示日誌消息。 您可以設定記錄檔層級、清除控制台、釘選選取的捲動位置，並啟用／停用訊息顯示。<br /> </p> <p><strong>版本控制</strong>:</p> <p>顯示版本控制消息。<br /> </p> </td>
  </tr>
  <tr>
   <td>「構建資訊」頁籤<br /> </td>
   <td>顯示建立搭售時的資訊。<br /> </td>
  </tr>
  <tr>
   <td>重新整理<br /> </td>
   <td>刷新當前選擇。 其他用戶的更改將在儲存庫的視圖中更新。 您所做的變更不會受到影響。<br /> </td>
  </tr>
  <tr>
   <td>儲存全部</td>
   <td><p><strong>儲存全部</strong>:<br /> </p> <p>儲存您所做的所有變更。 在按一下「保存」之前，更改是臨時的，當您退出控制台時將丟失。</p> <p><strong>回復</strong>:</p> <p>放棄自上次保存操作以來您在選定節點上所做的所有更改，然後重新載入選定節點的儲存庫的當前狀態。</p> <p><strong>全部回復</strong>:</p> <p>放棄自上次保存操作後在整個儲存庫中所做的所有更改，然後重新載入儲存庫的當前狀態。</p> </td>
  </tr>
  <tr>
   <td>建立 ...<br /> </td>
   <td><p>下拉式功能表，在選取的節點下建立下列項目：<br /> </p> <p>-節 <strong>點</strong>: 具有任意節點類型的節點<br /> </p> <p>-文 <strong>件</strong>: nt：檔案節點及其nt：資源子節點</p> <p>-文 <strong>件夾</strong>: nt：資料夾節點</p> <p>-范 <strong>本</strong>: AEM範本</p> <p>-元 <strong>件</strong>: AEM元件</p> <p>-對 <strong>話框</strong>: AEM對話方塊</p> </td>
  </tr>
  <tr>
   <td>刪除<br /> </td>
   <td>刪除選定節點。<br /> </td>
  </tr>
  <tr>
   <td>複製</td>
   <td>複製選定節點。<br /> </td>
  </tr>
  <tr>
   <td>貼上<br /> </td>
   <td>將複製的節點貼上到選定節點下。<br /> </td>
  </tr>
  <tr>
   <td>移動 ...<br /> </td>
   <td>將選定節點移動到通過對話框設定的節點。</td>
  </tr>
  <tr>
   <td>重新命名 ...<br /> </td>
   <td>更名選定節點。<br /> </td>
  </tr>
  <tr>
   <td>Mixin ...<br /> </td>
   <td>允許您將混合類型添加到節點類型。 混合類型主要用於新增進階功能，例如版本控制、存取控制、參照和鎖定至節點。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉式選單，包含下列工具：</p> <p>-服 <strong>務器配置……</strong>: 去Felix Console。</p> <p>-查 <strong>詢……</strong>: 來查詢儲存庫。</p> <p>-權 <strong>限……</strong>: 以開啟權限管理，您可在其中檢視和新增權限。</p> <p>-測 <strong>試訪問控制……</strong>: 您可以在其中測試特定路徑和／或承擔者權限的位置。</p> <p>-導 <strong>出節點類型</strong>: 將系統中的節點類型導出為cnd注釋。</p> <p>-導 <strong>入節點類型……</strong>: 來導入節點類型。</p> <p>-安 <strong>裝SiteCatalyst除錯程式……</strong>: 說明如何安裝Analytics除錯程式。</p> </td>
  </tr>
  <tr>
   <td>登入介面工具集<br /> </td>
   <td><p>顯示當前登入的使用者及其登入的工作區，例如admin@crx.default。</p> <p>按一下它以登入或重新登入為特定使用者。 如果您未指定要登入的工作區，則會登入預設工作區crx.default。</p> <p>如果要以匿名用戶的身份瀏覽儲存庫，請使用 <strong>anonymous</strong> 作為登錄名和任何密碼（如空格或點）。<br /> </p> <p>如果您的授權不再有效（例如，已過期），登入介面工具集會顯示「未授<strong>權——登入……</strong>」。 按一下它以重新登入。</p> </td>
  </tr>
 </tbody>
</table>

## 建立資料夾 {#creating-a-folder}

要使用CRXDE Lite建立資料夾：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下您要建立新資料夾的資料夾，選取「建立……」 **，然****後選取「建立資料夾……」**.

1. 輸入資料夾 **名稱** ，然後按一下 **確定**。

1. 按一 **下「全部儲存** 」，將變更儲存在伺服器上。

## Creating a Template {#creating-a-template}

要使用CRXDE Lite建立模板，請：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下您要建立範本的檔案夾，選取「建立……」 **，然****後選取「建立範本……」**.

1. 輸入 **Label**、Label **、** Description **、Type Resource********** Ranking of the Label、Description、Oracle Type Ranking Of the Ranking Of the Label。 按一下&#x200B;**下一步**。

1. 此步驟為可選步驟： 設定允 **許路徑**。 Click **Next**

1. 此步驟為可選步驟： 設定「 **允許父項**」。 按一下&#x200B;**下一步**。

1. 此步驟為可選步驟： 設定「允 **許的子項**」。 按一下 **確定**。

1. 按一 **下「全部儲存** 」，將變更儲存在伺服器上。

它建立：

* 具有模板屬性的類 `cq:Template` 型節點

* 具有頁面內容屬性的 `cq:PageContent` 子節點類型

您可以將屬性新增至範本： 請參閱「 [建立屬性](#creating-a-property) 」部分。

## 建立元件 {#creating-a-component}

此處所述的功能僅在安裝了CQ5(即在儲存庫中可用的節點類 `cq:Component` 型)時可用。

要使用CRXDE Lite建立元件：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下您要建立元件的檔案夾，選取「建立……」 **，然****後選取「建立元件……」**.

1. 輸入Label ****、Title **、** Description **、** Super Type Type和Super Group Of the Label、Title、Description ******** 和Super Type Group Of the Label。 按一下&#x200B;**下一步**。

1. 此步驟為可選步驟： 設定元件屬性 **是容器、無裝飾** 、單元 **格名稱**&#x200B;和對 **話路徑******。 按一下&#x200B;**下一步**。

1. 此步驟為可選步驟： 設定元件屬性「允 **許父項」**。 按一下&#x200B;**下一步**。

1. 此步驟為可選步驟： 設定元件屬 **性Allowed Children**。 按一下 **確定**。

1. 按一 **下「全部儲存** 」，將變更儲存在伺服器上。

它建立：

* 類型節點 `cq:Component`
* 元件屬性
* 元件。jsp指令碼

## 建立對話框 {#creating-a-dialog}

要使用CRXDE Lite建立對話框：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下您要建立對話方塊的元件，選取「建立……」 **，然****後選取「建立對話方塊……」**.

1. 輸入「 **標籤** 」和「 **標題」**。 按一下 **確定**。

1. 按一 **下「**&#x200B;全部儲存」，將變更儲存在伺服器上。

它會建立具有下列結構的對話方塊：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您現在可以修改屬性或建立新節點，以依您的需求調整對話方塊。

也可以使用對話框編輯器編輯對話框。 按兩下CRXDE Lite中的對話框節點將開啟編輯器。 有關對話框編輯器的詳細資訊，請 [到此處](/help/sites-developing/dialog-editor.md)。

## 建立節點 {#creating-a-node}

要使用CRXDE Lite建立節點，請：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，按一下右鍵要建立新節點的節點，選擇「建立……」 **，然後****選擇「建立節點……」**.
1. 輸入「 **名稱** 」和「 **類型」**。 按一下 **確定**。
1. 按一 **下「全部儲存** 」，將變更儲存在伺服器上。

您現在可以修改屬性或建立新節點，以因應您的需求來調整節點。

>[!NOTE]
>
>大多數編輯操作（包括「建立節點」）都保留記憶體中的所有更改，並且僅在保存時（通過「全部保存」按鈕）將其儲存到儲存庫中。 但是，移動等某些操作會自動保留。
>
>在保存更改時，JCR儲存庫還會首先執行有關新建立的節點是否允許父節點的節點類型的驗證。 如果您在儲存節點時收到錯誤訊息，請檢查內容結構是否有效(例如，您無法將節 `nt:unstructured` 點建立為節點的子 `nt:folder` 系)。

## 建立屬性 {#creating-a-property}

要使用CRXDE Lite建立屬性：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導航」窗格中，選擇要添加新屬性的節點。
1. 在底部窗 **格的** 「屬性」頁籤中，輸入「名稱」、「類型」和「值」(Value **)**********。 按一下&#x200B;**「新增」**。

1. 按一 **下「全部儲存** 」，將變更儲存在伺服器上。

## 建立指令碼 {#creating-a-script}

要建立新指令碼：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，以滑鼠右鍵按一下您要建立指令碼的元件，選取「建立……」 **，然****後選取「建立檔案……」**.

1. 輸入「檔案 **名** 」（包括副檔名）。 按一下 **確定**。

1. 新檔案會在「編輯」窗格中以標籤的形式開啟。
1. 編輯檔案。
1. Click **Save All** to save the changes.

## 導出和導入節點類型 {#exporting-and-importing-node-types}

使用CRXDE Lite，您可以在 [CND（壓縮名稱空間和節點類型定義）注釋中導入和／或導出節點類型定義](https://jackrabbit.apache.org/jcr/node-type-notation.html)。

要導出節點類型定義，請執行以下操作：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 選擇所需的節點。
1. 依次選擇 **工具** 、導 **出節點類型**。

1. 定義（以cnd表示法）將顯示在瀏覽器中。 視需要儲存資訊。

要導入節點類型定義，請執行以下操作：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 選擇 **工具** , **然後選擇導入節點類型……**.

1. 在文本框中輸入定義的CND符號。
1. 如果 **要更新現有定義** ，請勾選「允許更新」。
1. 按一 **下匯入**。

## 記錄 {#logging}

使用CRXDE Lite，您可以顯示位於 `error.log` 檔案系統上的檔案，並 `<crx-install-dir>/crx-quickstart/server/logs` 使用適當的記錄層級加以篩選。 按如下步驟進行：

1. 在您的瀏覽器中開啟CRXDE Lite。
1. 在窗口 **底部的** 「控制台」頁籤中，在右側的下拉菜單中，選擇「伺服器日 **志」**。

1. 按一下「 **停止** 」圖示以顯示訊息。

您可以：

* 按一下「記錄設定」圖示，以調整Felix Console **中的記錄** 參數。
* 按一下「筆刷」圖示以清 **除訊息** 。
* 按一下「釘選」圖示，將訊息釘選在目 **前選取** 範圍。
* 按一下「停止」圖示，以啟用或停用訊息 **顯示** 。

## 存取控制 {#access-control}

>[!NOTE]
>
>如需詳 [細資訊，請參閱使用者、群組和存取權限](/help/sites-administering/user-group-ac-admin.md) 管理。
