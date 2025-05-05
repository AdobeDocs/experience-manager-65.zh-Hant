---
title: 使用CRXDE Lite開發
description: CRXDE Lite已內嵌至Adobe Experience Manager (AEM)中，可讓您在瀏覽器中執行標準開發工作
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 1%

---

# 使用CRXDE Lite開發{#developing-with-crxde-lite}

本節說明如何使用CRXDE Lite開發您的Adobe Experience Manager (AEM)應用程式。

請參閱概述檔案，深入瞭解可用的不同開發環境。

CRXDE Lite內嵌於AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄時建立專案、建立和編輯檔案(如.jsp和.java)、資料夾、範本、元件、對話方塊、節點、屬性和組合。
當您無法直接存取AEM伺服器時，建議使用CRXDE Lite。 或者，當您透過擴充或修改現成可用的元件和Java™套件組合來開發應用程式時，或當您不需要專用的偵錯工具時，程式碼完成和語法醒目提示。

>[!NOTE]
>
>從AEM 6.5.5.0開始，已無法再匿名存取CRXDE Lite。
>系統會將使用者重新導向至登入畫面。


>[!NOTE]
>
>Adobe建議您在專案開發期間使用[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md)和[AEM HTL Brackets擴充功能](/help/sites-developing/aem-brackets.md)。

## CRXDE Lite快速入門 {#getting-started-with-crxde-lite}

若要開始使用CRXDE Lite，請依照下列步驟進行：

1. 安裝AEM。
1. 在您的瀏覽器中，輸入`https://<host>:<port>/crx/de`。 預設為`https://localhost:4502/crx/de`。
1. 輸入您的&#x200B;**使用者名稱**&#x200B;和&#x200B;**密碼**。 預設為`admin`和`admin`。

1. 按一下&#x200B;**「確定」**。

CRXDE Lite使用者介面在您的瀏覽器中看起來如下所示：

![chlimage_1-18](assets/crx-interface.jpg)

您現在可以使用CRXDE Lite來開發您的應用程式。

## 使用者介面概觀 {#overview-of-the-user-interface}

CRXDE Lite提供下列功能：

<table>
 <tbody>
  <tr>
   <td>頂端切換器列</td>
   <td>快速在CRXDE Lite、封裝管理器和封裝共用之間切換。</td>
  </tr>
  <tr>
   <td>節點路徑Widget</td>
   <td><p>顯示所選節點的路徑。</p> <p>您也可以使用它來跳至節點，方法是手動輸入路徑，或從其他位置貼上路徑，然後按下Enter。</p> <p>此外，它也能支援尋找具有特定節點名稱的節點。 輸入要尋找的節點名稱，然後等待（或按一下右側的搜尋符號）。 例如，您可以嘗試在Widget中輸入字串<em>oak</em>，檢視其運作方式。 如果將指定的節點載入總管窗格，則會顯示清單，您可以選取路徑並點選Enter以導覽至該路徑。 它僅適用於瀏覽器中載入到CRXDE使用者端應用程式的節點。 如果要搜尋整個存放庫，請使用工具，然後使用查詢。</p> </td>
  </tr>
  <tr>
   <td>瀏覽器窗格</td>
   <td><p>顯示儲存區域中所有節點的樹狀結構。</p> <p>按一下節點，以便在<strong>屬性</strong>索引標籤中顯示其屬性。 按一下節點後，您可以在工具列中選取動作。 再按一下節點以重新命名。</p> <p>樹狀結構導覽篩選（雙目圖示）：可讓您篩選儲存區域中，其名稱包含輸入文字的節點。 它僅適用於已在本機載入的節點。<br /> </p> </td>
  </tr>
  <tr>
   <td>編輯窗格</td>
   <td><p><strong>首頁</strong>標籤：可讓您搜尋內容和/或檔案，並存取開發人員資源（檔案、開發人員部落格、知識庫）和支援(Adobe首頁和支援中心)。<br /> </p> <p>連按兩下<strong>總管</strong>窗格中的檔案，以便顯示其內容。 例如，.jsp或.java檔案。 然後，您可以修改它並儲存變更。</p> <p>在<strong>編輯</strong>窗格中編輯檔案後，工具列上有下列工具： <br /> </p> - <strong>在樹狀結構中顯示： </strong>在存放庫樹狀結構中顯示檔案。<br /> - <strong>搜尋/取代……</strong>：執行搜尋或取代。<br /> <br />連按兩下<strong>編輯</strong>窗格的狀態行會開啟<strong>移至行</strong>對話方塊，讓您能夠輸入要移至的特定行號。<br /> </td>
  </tr>
  <tr>
   <td>屬性標籤<br /> </td>
   <td>顯示您已選取之節點的特性。 您可以新增屬性或刪除現有屬性。<br /> </td>
  </tr>
  <tr>
   <td>存取控制標籤</td>
   <td><p>根據路徑、存放庫層級或主體顯示許可權。</p> <p>這些許可權會劃分為</p> <p>- <strong>適用的存取控制原則</strong>：可套用至選取範圍的原則。</p> <p>- <strong>本機存取控制原則</strong>：原則已套用至選取範圍。</p> <p>- <strong>有效的存取控制原則</strong>：套用至選取範圍的原則、可能設定在本機或從父節點繼承。</p> <p>注意。 若要能夠檢視存取控制資訊，登入CRXDE Lite的使用者必須擁有ACL專案的讀取許可權。 匿名使用者預設無法看到此資訊 — 例如，以管理員身分登入以檢視資訊。</p> </td>
  </tr>
  <tr>
   <td>「復寫」標籤</td>
   <td><p>顯示節點的復寫狀態。 您可以復寫及復寫刪除節點。</p> </td>
  </tr>
  <tr>
   <td>主控台索引標籤<br /> </td>
   <td><p><strong>伺服器記錄檔</strong>：</p> <p>顯示日誌訊息。 您可以設定記錄層級、清除主控台、釘選選取的捲動位置，以及啟用或停用訊息顯示。<br /> </p> <p><strong>版本控制</strong>：</p> <p>顯示版本控制訊息。<br /> </p> </td>
  </tr>
  <tr>
   <td>建置資訊索引標籤<br /> </td>
   <td>在建置組合時顯示資訊。<br /> </td>
  </tr>
  <tr>
   <td>重新整理<br /> </td>
   <td>重新整理選取專案。 來自其他使用者的變更會在您檢視的存放庫中更新。 您所做的變更不受影響。<br /> </td>
  </tr>
  <tr>
   <td>儲存全部</td>
   <td><p><strong>儲存全部</strong>：<br /> </p> <p>儲存您所做的所有變更。 在您按一下「儲存」之前，變更是暫時性的，當您退出主控台時便會遺失。</p> <p><strong>回覆</strong>：</p> <p>捨棄您自上次儲存動作後對所選節點所做的所有變更，然後重新載入所選節點的存放庫狀態。</p> <p><strong>全部回覆</strong>：</p> <p>捨棄您自上次儲存動作以來，在整個存放庫中所做的所有變更，然後重新載入存放庫的狀態。</p> </td>
  </tr>
  <tr>
   <td>建立……<br /> </td>
   <td><p>在選取的節點下建立下列專案的下拉式功能表： <br /> </p> <p>- <strong>節點</strong>：具有任意節點型別的節點<br /> </p> <p>- <strong>檔案</strong>： nt：file節點及其nt：resource子節點</p> <p>- <strong>資料夾</strong>： nt：folder節點</p> <p>- <strong>範本</strong>： AEM範本</p> <p>- <strong>元件</strong>： AEM元件</p> <p>- <strong>對話方塊</strong>： AEM對話方塊</p> </td>
  </tr>
  <tr>
   <td>刪除<br /> </td>
   <td>刪除選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>複製</td>
   <td>複製選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>貼上<br /> </td>
   <td>將複製的節點貼到選取的節點下。<br /> </td>
  </tr>
  <tr>
   <td>移動……<br /> </td>
   <td>將選取的節點移至透過對話方塊設定的節點。</td>
  </tr>
  <tr>
   <td>重新命名……<br /> </td>
   <td>重新命名選取的節點。<br /> </td>
  </tr>
  <tr>
   <td>Mixin ...<br /> </td>
   <td>可讓您將mixin型別新增至節點型別。 mixin型別主要用於新增進階功能，例如版本設定、存取控制、參照和鎖定節點。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>包含下列工具的下拉式功能表：</p> <p>- <strong>伺服器設定……</strong>：存取Felix主控台。</p> <p>- <strong>查詢……</strong>：查詢存放庫。</p> <p>- <strong>許可權……</strong>：開啟許可權管理，您可以在其中檢視及新增許可權。</p> <p>- <strong>測試存取控制……</strong>：您可以在此測試特定路徑和/或主體的許可權。</p> <p>- <strong>匯出節點型別</strong>：將系統中的節點型別匯出為cnd標籤法。</p> <p>- <strong>匯入節點型別……</strong>：使用cnd標籤法匯入節點型別。</p> <p>- <strong>安裝SiteCatalyst偵錯工具……</strong>：如何安裝Analytics偵錯工具的說明。</p> </td>
  </tr>
  <tr>
   <td>登入Widget<br /> </td>
   <td><p>顯示登入的使用者及其登入的工作區，例如admin@crx.default。</p> <p>按一下以登入或以特定使用者身分重新登入。 如果您未指定要登入的工作區，則會登入預設工作區crx.default。</p> <p>如果您想要以匿名使用者身分瀏覽存放庫，請使用<strong>匿名</strong>作為登入名稱，並使用任何密碼（例如空格或點）。<br /> </p> <p>如果您的授權不再有效（例如，已過期），登入Widget會顯示"<strong>未獲授權 — 登入……</strong>"。 按一下以重新登入。</p> </td>
  </tr>
 </tbody>
</table>

## 建立資料夾 {#creating-a-folder}

若要建立具有CRXDE Lite的資料夾：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在[導覽]窗格中，用滑鼠右鍵按一下您要建立資料夾的資料夾，選取&#x200B;**建立……**，然後選取&#x200B;**建立資料夾……**。

1. 輸入資料夾&#x200B;**名稱**&#x200B;並按一下&#x200B;**確定**。

1. 按一下[儲存全部]&#x200B;**&#x200B;**&#x200B;儲存伺服器上的變更。

## 建立範本 {#creating-a-template}

若要使用CRXDE Lite建立範本：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，用滑鼠右鍵按一下您要建立範本的資料夾，選取&#x200B;**建立……**，然後選取&#x200B;**建立範本……**。

1. 輸入範本的&#x200B;**標籤**、**標題**、**描述**、**資源型別**&#x200B;和&#x200B;**排名**。 按一下「**下一步**」。

1. 此步驟為選用：設定&#x200B;**允許的路徑**。 按一下&#x200B;**下一步**

1. 此步驟是選擇性的：設定&#x200B;**允許的父項**。 按一下「**下一步**」。

1. 此步驟是選用的：設定&#x200B;**允許的子項**。 按一下&#x200B;**「確定」**。

1. 按一下[儲存全部]&#x200B;**&#x200B;**&#x200B;儲存伺服器上的變更。

它會建立：

* 具有範本屬性的型別`cq:Template`節點

* 具有頁面內容屬性的型別`cq:PageContent`的子節點

您可以將屬性新增至範本：請參閱[建立屬性](#creating-a-property)區段。

## 建立元件 {#creating-a-component}

此處說明的功能只有在已安裝CQ5時才能使用，亦即節點型別`cq:Component`可在存放庫中使用。

若要建立具有CRXDE Lite的元件：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在[導覽]窗格中，用滑鼠右鍵按一下您要建立元件的資料夾，選取&#x200B;**建立……**，然後選取&#x200B;**建立元件……**。

1. 輸入元件的&#x200B;**標籤**、**標題**、**描述**、**超級資源型別**&#x200B;和&#x200B;**群組**。 按一下「**下一步**」。

1. 此步驟是選擇性的：設定元件屬性&#x200B;**Is Container、** **No Decoration**、**儲存格名稱**&#x200B;和&#x200B;**對話方塊路徑**。 按一下「**下一步**」。

1. 此步驟是選擇性的：設定元件屬性&#x200B;**允許的父項**。 按一下「**下一步**」。

1. 此步驟是選擇性的：設定元件屬性&#x200B;**允許的子項**。 按一下&#x200B;**「確定」**。

1. 按一下[儲存全部]&#x200B;**&#x200B;**&#x200B;儲存伺服器上的變更。

它會建立：

* 型別為`cq:Component`的節點
* 元件屬性
* 元件.jsp指令碼

## 建立對話方塊 {#creating-a-dialog}

若要使用CRXDE Lite建立對話方塊：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，用滑鼠右鍵按一下您要建立對話方塊的元件，選取&#x200B;**建立……**，然後選取&#x200B;**建立對話方塊……**。

1. 輸入&#x200B;**標籤**&#x200B;和&#x200B;**標題**。 按一下&#x200B;**「確定」**。

1. 按一下&#x200B;**儲存全部** l以儲存伺服器上的變更。

它會建立具有下列結構的對話方塊：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您現在可以修改屬性或建立節點，讓對話方塊符合您的需求。

您也可以使用對話方塊編輯器來編輯對話方塊。 在CRXDE Lite中的對話方塊節點上按兩下會開啟編輯器。 如需詳細資訊，請參閱[對話方塊編輯器](/help/sites-developing/dialog-editor.md)。

## 建立節點 {#creating-a-node}

若要建立具有CRXDE Lite的節點：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，用滑鼠右鍵按一下您要建立節點的節點，選取&#x200B;**建立……**，然後選取&#x200B;**建立節點……**。
1. 輸入&#x200B;**名稱**&#x200B;和&#x200B;**型別**。 按一下&#x200B;**「確定」**。
1. 按一下[儲存全部]&#x200B;**&#x200B;**&#x200B;儲存伺服器上的變更。

您現在可以透過修改屬性或建立節點來調整節點以符合您的需求。

>[!NOTE]
>
>大部分的編輯操作（包括「建立節點」）會保留記憶體中的所有變更，並只會在儲存時將它們儲存在存放庫中（透過「儲存全部」按鈕）。 不過，某些作業（例如移動）會自動持續存在。
>
>有關父節點的節點型別是否允許新建立的節點的驗證，也會在儲存變更時先由JCR存放庫執行。 如果您在儲存節點時收到錯誤訊息，請檢查內容結構是否有效（例如，您無法建立`nt:unstructured`節點作為`nt:folder`節點的子節點）。

## 建立屬性 {#creating-a-property}

若要使用CRXDE Lite建立屬性：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在「導覽」窗格中，選取您要新增屬性的節點。
1. 在底部窗格的&#x200B;**屬性**&#x200B;索引標籤中，輸入&#x200B;**名稱**、**型別**&#x200B;和&#x200B;**值**。 按一下&#x200B;**新增**。

1. 按一下[儲存全部]&#x200B;**&#x200B;**&#x200B;儲存伺服器上的變更。

## 建立指令碼 {#creating-a-script}

若要建立指令碼：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在導覽窗格中，用滑鼠右鍵按一下您要建立指令碼的元件，選取&#x200B;**建立……**，然後選取&#x200B;**建立檔案……**。

1. 輸入包含副檔名的檔案&#x200B;**名稱**。 按一下&#x200B;**「確定」**。

1. 新檔案會在「編輯」窗格中開啟為標籤。
1. 編輯檔案。
1. 按一下[全部儲存]&#x200B;**儲存變更。**

## 匯出和匯入節點型別 {#exporting-and-importing-node-types}

透過CRXDE Lite，您可以在[CND （壓縮名稱空間和節點型別定義）表示法](https://jackrabbit.apache.org/jcr/node-type-notation.html)中匯入和/或匯出節點型別定義。

若要匯出節點型別定義，請執行下列動作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選取您需要的節點。
1. 選取&#x200B;**工具**&#x200B;然後&#x200B;**匯出節點型別**。

1. 定義會以指令碼方式顯示在瀏覽器中。 視需要儲存資訊。

若要匯入節點型別定義，請執行下列動作：

1. 在瀏覽器中開啟CRXDE Lite。
1. 選取&#x200B;**工具**&#x200B;然後&#x200B;**匯入節點型別……**。

1. 在文字方塊中輸入定義的CND標籤法。
1. 如果要更新現有的定義，請核取&#x200B;**允許更新**。
1. 按一下&#x200B;**匯入**。

## 記錄 {#logging}

透過CRXDE Lite，您可以顯示位於檔案系統`<crx-install-dir>/crx-quickstart/server/logs`上的檔案`error.log`，並使用適當的記錄層級加以篩選。 請依照下列步驟進行：

1. 在瀏覽器中開啟CRXDE Lite。
1. 在視窗底部的&#x200B;**主控台**&#x200B;標籤中，在右側的下拉式功能表中，選取&#x200B;**伺服器記錄檔**。

1. 按一下&#x200B;**停止**&#x200B;圖示以顯示訊息。

您可以：

* 按一下&#x200B;**記錄組態**&#x200B;圖示，調整Felix主控台中的記錄引數。
* 按一下&#x200B;**筆刷**&#x200B;圖示以清除訊息。
* 按一下&#x200B;**釘選**&#x200B;圖示，在選取專案釘選訊息。
* 按一下&#x200B;**停止**&#x200B;圖示，啟用或停用訊息顯示。

## 存取控制 {#access-control}

>[!NOTE]
>
>如需詳細資訊，請參閱[使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md)。
