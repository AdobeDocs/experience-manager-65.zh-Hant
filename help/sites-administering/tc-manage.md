---
title: 管理翻譯專案
description: 瞭解如何在Adobe Experience Manager中管理翻譯專案。
exl-id: 968bba02-98fe-4eaf-9937-ce5cfdf5b413
solution: Experience Manager, Experience Manager Sites
feature: Language Copy
role: Admin
source-git-commit: 26ac50aa27501fe6a80b38a474e9811338c4fb56
workflow-type: tm+mt
source-wordcount: '3519'
ht-degree: 3%

---

# 管理翻譯專案{#managing-translation-projects}

在準備要翻譯的內容後，您需要透過建立遺漏的語言副本來完成語言結構，並建立翻譯專案。

翻譯專案使您能夠管理 AEM 內容的翻譯。翻譯專案是AEM [專案](/help/sites-authoring/projects.md)的型別，其中包含要翻譯成其他語言的資源。 這些資源是從語言主版建立的[語言副本](/help/sites-administering/tc-prep.md)的頁面和資產。

將資源新增至翻譯專案時，系統會為其建立翻譯工作。 工作會提供相關命令和狀態資訊，您可用來管理在資源上執行的人工翻譯和機器翻譯工作流程。

>[!NOTE]
>
>翻譯專案可包含多個翻譯工作。

翻譯專案是長期執行的專案，由語言和翻譯方法/提供者定義，以符合全球化的組織治理。 作業應於初始翻譯期間或手動啟動一次，並在整個內容和翻譯更新活動中維持有效。

翻譯專案和工作是使用翻譯準備工作流程建立的。 這些工作流程有三個選項，適用於初始翻譯（建立和翻譯）和更新（更新翻譯）：

1. [建立新專案](#creating-translation-projects-using-the-references-panel)
1. [新增至現有專案](#adding-pages-to-a-translation-project)
1. [僅限內容結構](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>選項3與翻譯工作/專案無關。 它可讓您將語言主版中的內容和結構變更複製到（未翻譯的）語言副本。 即使沒有翻譯，您也可以使用此項讓您的語言主版保持同步。

## 執行初始翻譯並更新現有翻譯 {#performing-initial-translations-and-updating-existing-translations}

AEM會偵測是否正在為內容的初始翻譯建立翻譯專案，或更新已翻譯的語言副本。 當您為頁面建立翻譯專案並指示您要翻譯的語言副本時，AEM會偵測來源頁面是否已存在於目標語言副本中：

* **語言副本不包含頁面：** AEM將此情況視為初始翻譯。 頁面會立即複製到語言副本，並包含在專案中。 將翻譯頁面匯入AEM時，AEM會直接將其複製到語言副本。
* **語言副本已包含頁面：** AEM將此情況視為更新的翻譯。 系統隨即會建立啟動項，並將頁面副本新增至啟動項，並包含在專案中。 啟動可讓您在將更新的翻譯送交語言副本之前，先檢閱這些翻譯：

   * 將翻譯頁面匯入AEM時，會覆寫啟動中的頁面。
   * 只有在提升啟動項時，翻譯的頁面才會覆寫語言副本。

例如，/content/geometrixx/fr語言根是為/content/geometrixx/en主語言的法文翻譯所建立。 法文副本中沒有任何其他頁面。

* 系統會針對/content/geometrixx/en/products頁面及所有子頁面，以法語副本為目標，建立翻譯專案。 因為語言副本不包含/content/geometrixx/fr/products頁面，AEM會立即將/content/geometrixx/en/products頁面和所有子頁面複製到法文副本。 這些副本也包含在翻譯專案中。
* 系統會針對/content/geometrixx/en頁面及所有子頁面，以法語副本為目標，建立翻譯專案。 由於語言副本包含與/content/geometrixx/en頁面對應的頁面（語言根），因此AEM會複製/content/geometrixx/en頁面和所有子頁面，並將其新增至啟動。 這些副本也包含在翻譯專案中。

## 使用「參考」面板建立翻譯專案 {#creating-translation-projects-using-the-references-panel}

建立翻譯專案，讓您能夠執行和管理翻譯語言母版資源的工作流程。 當您建立專案時，您會以要翻譯的語言主版指定頁面，以及要為其執行翻譯的語言副本：

* 與所選頁面關聯的翻譯整合框架的雲端設定會決定翻譯專案的許多屬性，例如要使用的翻譯工作流程。
* 系統會為每個選取的語言副本建立專案。
* 所選頁面和相關資產的副本隨即建立，並新增至每個專案。 這些副本稍後會傳送給翻譯提供者進行翻譯。

您可以指定也選取所選頁面的子頁面。 在這種情況下，子頁面的副本也會新增到每個專案中，以便進行翻譯。 當任何子頁面與不同的翻譯整合框架設定相關聯時，AEM會建立其他專案。

您也可以[手動建立翻譯專案](#creating-a-translation-project-using-the-projects-console)。

>[!NOTE]
>
>若要建立專案，您的帳戶必須是`project-administrators`群組的成員。

**初始翻譯與更新翻譯**

「參照」面板會指出您是要更新現有的語言副本，還是要建立語言副本的第一個版本。 當所選頁面存在語言副本時，會出現「更新語言副本」索引標籤，以提供對專案相關命令的存取。

![chlimage_1-239](assets/chlimage_1-239.png)

翻譯之後，您可以[先檢閱翻譯](#reviewing-and-promoting-updated-content)，然後再用它覆寫語言副本。 當所選頁面不存在語言副本時，建立和翻譯索引標籤會出現，以提供對專案相關命令的存取。

![chlimage_1-240](assets/chlimage_1-240.png)

### 建立新語言副本的翻譯專案 {#create-translation-projects-for-a-new-language-copy}

1. 使用網站主控台來選取您要新增至翻譯專案的頁面。

   例如，若要翻譯Geometrixx示範網站的英文頁面，請選取「Geometrixx示範網站>英文」。

1. 在工具列上，按一下「參照」。

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. 選取「語言副本」，然後選取您要翻譯來源頁面的語言副本。
1. 按一下「建立並翻譯」 ，然後設定翻譯工作：

   * 使用「語言」下拉式清單，選取您要翻譯的語言副本。 視需要選取其他語言。 出現在清單中的語言與您建立的[語言根對應](/help/sites-administering/tc-prep.md#creating-a-language-root)。
   * 若要翻譯您選取的頁面和所有子頁面，請選取「選取所有子頁面」。 若只要翻譯您所選取的頁面，請清除選項。
   * 針對「專案」，選取「建立新翻譯專案」。
   * 輸入專案名稱。

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. 按一下「建立」。

### 建立現有語言副本的翻譯專案 {#create-translation-projects-for-an-existing-language-copy}

1. 使用網站主控台來選取您要新增至翻譯專案的頁面。

   例如，若要翻譯Geometrixx示範網站的英文頁面，請選取「Geometrixx示範網站>英文」。

1. 在工具列上，按一下「參照」。

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. 選取「語言副本」，然後選取您要翻譯來源頁面的語言副本。
1. 按一下「更新語言副本」 ，然後設定翻譯工作：

   * 若要翻譯您選取的頁面和所有子頁面，請選取「選取所有子頁面」。 若只要翻譯您所選取的頁面，請清除選項。
   * 針對「專案」，選取「建立新翻譯專案」。
   * 輸入專案名稱。

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. 按一下「開始」。

## 新增頁面至翻譯專案 {#adding-pages-to-a-translation-project}

建立翻譯專案後，您可以使用「資源」窗格將頁面新增至專案。 當您將來自不同分支的頁面納入同一個專案時，新增頁面會很有用。

當您將頁面新增到翻譯專案時，這些頁面會包含在新的翻譯工作中。 您也可以[將頁面新增至現有工作](#adding-pages-assets-to-a-translation-job)。

如同建立專案一樣，新增頁面時，頁面副本會在必要時新增至啟動項，以避免覆寫現有語言副本。 （請參閱[建立現有語言副本的翻譯專案](#performing-initial-translations-and-updating-existing-translations)。）

1. 使用Sites Console來選取您要新增至翻譯專案的頁面。

   例如，若要翻譯Geometrixx示範網站的英文頁面，請選取「Geometrixx示範網站>英文」。

1. 在工具列上，按一下「參照」。

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. 選取「語言副本」，然後選取您要翻譯來源頁面的語言副本。

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. 按一下「更新語言副本」 ，然後設定屬性：

   * 若要翻譯您選取的頁面和所有子頁面，請選取「選取所有子頁面」。 若只要翻譯您所選取的頁面，請清除選項。
   * 針對專案，選取「新增至現有翻譯專案」。
   * 選取專案。

   >[!NOTE]
   >
   >「翻譯專案」中設定的目標語言應與「參考」面板中顯示的語言副本路徑相符。

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. 按一下「開始」。

## 新增頁面/Assets至翻譯工作 {#adding-pages-assets-to-a-translation-job}

您可以將頁面、資產、標籤或i18n字典新增至翻譯專案的翻譯工作。 若要新增頁面或資產：

1. 在翻譯專案的「翻譯工作」方塊底部，按一下省略符號。

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. 按一下「新增」和「頁面/Assets」 。

   ![chlimage_1-247](assets/chlimage_1-247.png)

1. 選取您要新增之分支的最上層專案，然後按一下核取記號圖示。 您可以選取多個專案。

   ![chlimage_1-248](assets/chlimage_1-248.png)

1. 或者，您可以選取搜尋圖示，輕鬆尋找要新增至翻譯工作的頁面或資產。

   ![chlimage_1-249](assets/chlimage_1-249.png)

您的頁面和/或資產會新增至您的翻譯工作。

## 新增i18n字典至翻譯工作 {#adding-i-n-dictionaries-to-a-translation-job}

您可以將頁面、資產、標籤或i18n字典新增至翻譯專案的翻譯工作。 新增i18n字典：

1. 在翻譯專案的「翻譯工作」方塊底部，按一下省略符號。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 按一下「新增」和「I18N字典」。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 選取要新增的&#x200B;**根目錄**&#x200B;和字典（如有必要），然後選取&#x200B;**新增**。

   ![i18N字典](assets/tc-manage-i18n-dictionary.png)

1. 如有要求，請選取更新的性質：

   ![翻譯](assets/tc-manage-translate.png)

您的字典現在正在翻譯工作中。

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>如需i18n字典的詳細資訊，請閱讀[使用翻譯工具管理字典](/help/sites-developing/i18n-translator.md)。

## 新增標籤至翻譯工作 {#adding-tags-to-a-translation-job}

您可以將頁面、資產、標籤或i18n字典新增至翻譯專案的翻譯工作。 若要新增標籤：

1. 在翻譯專案的「翻譯工作」方塊底部，按一下省略符號。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 按一下「新增」，然後按一下「標籤」。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選取您要新增的標籤，然後按一下核取記號圖示。 您可以選取多個專案。

   ![chlimage_1-256](assets/chlimage_1-256.png)

您的標籤現在已新增至翻譯工作中。

![chlimage_1-257](assets/chlimage_1-257.png)

## 檢視翻譯專案詳細資料 {#seeing-translation-project-details}

「翻譯摘要」表徵圖包含為翻譯專案設定的屬性。 除了一般[專案資訊](/help/sites-authoring/projects.md#project-info)之外，「翻譯」索引標籤還包含翻譯特定的屬性：

* Source語言：正在翻譯的頁面語言。
* 目標語言：頁面將翻譯成何種語言。
* 翻譯方法：翻譯工作流程。 支援人工翻譯或機器翻譯。
* 翻譯提供者：執行翻譯的翻譯服務提供者。
* 內容類別： （機器翻譯）用於翻譯的內容類別。
* 雲端設定：專案所用翻譯服務聯結器的雲端設定。

使用頁面的「資源」窗格建立專案時，系統會根據來源頁面的屬性自動設定這些屬性。

![chlimage_1-258](assets/chlimage_1-258.png)

## 監控翻譯工作的狀態 {#monitoring-the-status-of-a-translation-job}

翻譯專案的翻譯工作表徵圖提供翻譯工作的狀態，以及工作中的頁面和資產數量。

![chlimage_1-259](assets/chlimage_1-259.png)

下表說明工作或工作中的專案可以具有的每種狀態：

| 狀態 | 說明 |
|---|---|
| 草稿 | 翻譯工作尚未開始。 翻譯工作在建立時處於草稿狀態。 |
| 已提交 | 當翻譯工作中的檔案成功傳送至翻譯服務時，檔案會具有此狀態。 發出Request Scope指令或Start指令後，可能會出現此狀態。 |
| 已要求範圍 | 對於人工翻譯工作流程，作業中的檔案已提交給翻譯供應商來設定範圍。 發出「要求範圍」指令後，此狀態會出現。 |
| 範圍已完成 | 供應商已設定翻譯工作的範圍。 |
| 已送交供翻譯 | 專案所有者已接受範圍。 此狀態表示翻譯廠商應開始翻譯工作中的檔案。 |
| 翻譯進行中 | 針對工作，工作中的一或多個檔案的翻譯尚未完成。 針對工作中的專案，該專案正在轉譯。 |
| 已翻譯 | 對於工作，工作中的所有檔案的翻譯已完成。 若為工作中的專案，則會轉譯該專案。 |
| 準備好審查 | 作業中的專案已翻譯，且檔案已匯入至AEM。 |
| 完成 | 專案所有者已指出翻譯合約已完成。 |
| 取消 | 指出翻譯供應商應停止處理翻譯工作。 |
| 錯誤更新 | 在AEM和翻譯服務之間傳輸檔案時發生錯誤。 |
| 未知狀態 | 發生未知的錯誤。 |

若要檢視作業中每個檔案的狀態，請按一下圖磚底部的省略符號。

## 設定翻譯工作的到期日 {#setting-the-due-date-of-translation-jobs}

指定翻譯廠商必須傳回已翻譯檔案的日期。 您可以設定專案或特定工作的到期日：

* **專案：**&#x200B;專案中的翻譯工作會繼承到期日。
* **工作：**&#x200B;您為工作設定的到期日會覆寫為專案設定的到期日。

只有在您使用的翻譯廠商支援此功能時，才能正確設定到期日。

下列程式會設定專案的到期日。

1. 按一下「翻譯摘要」方塊底部的省略符號。

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. 在基本索引標籤上，使用到期日期屬性的日期選擇器來選取到期日期。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. 按一下「完成」。

下列程式會設定翻譯工作的到期日。

1. 在「翻譯工作」圖磚上，按一下命令功能表，然後按一下「到期日」。

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. 在對話方塊中，按一下行事曆圖示，然後選取日期與時間作為到期日，再按一下「儲存」。

   ![chlimage_1-263](assets/chlimage_1-263.png)

## 設定翻譯工作的範圍 {#scoping-a-translation-job}

設定翻譯工作的範圍，從翻譯服務供應商取得翻譯成本的預估值。 設定工作範圍時，來源檔案會提交給翻譯廠商，後者會將文字與其儲存的翻譯集區（翻譯記憶庫）進行比較。 通常，範圍是需要翻譯的字數。

若要取得範圍設定結果的詳細資訊，請聯絡您的翻譯廠商。

>[!NOTE]
>
>範圍設定為選用。 您可以在不設定範圍的情況下開始翻譯工作。

當您設定翻譯工作的範圍時，工作的狀態為`Scope Requested`。 當翻譯廠商傳回範圍時，狀態會變更為`Scope Completed`。 範圍設定完成後，您可以使用「顯示範圍」指令來檢閱範圍設定結果。

只有在您使用的翻譯供應商支援此功能時，範圍設定才會正確運作。

1. 在「專案」主控台中，開啟您的翻譯專案。
1. 在「翻譯工作」圖磚上，按一下命令功能表，然後按一下「請求範圍」。

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. 當工作狀態變更為SCOPE_COMPLETED時，在「翻譯工作」拼貼上按一下命令功能表，然後按一下「顯示範圍」。

## 開始翻譯工作 {#starting-a-translation-job}

開始翻譯工作，將來源頁面翻譯成目標語言。 根據「翻譯摘要」拼貼的屬性值執行翻譯。

開始翻譯工作後，「翻譯工作」表徵圖會顯示「翻譯進行中」狀態。

![chlimage_1-265](assets/chlimage_1-265.png)

1. 在「專案」主控台中，開啟翻譯專案。
1. 在「翻譯工作」圖磚上，按一下命令功能表，然後按一下「開始」。

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. 在確認開始翻譯的「動作」對話方塊中，按一下「關閉」。

## 取消翻譯工作 {#canceling-a-translation-job}

取消翻譯工作以停止翻譯程式並阻止翻譯供應商執行任何進一步的翻譯。 當工作狀態為`Committed For Translation`或`Translation In Progress`時，您可以取消工作。

1. 在「專案」主控台中，開啟翻譯專案。
1. 在「翻譯工作」圖磚上，按一下命令功能表，然後按一下「取消」。
1. 在確認取消轉譯的「動作」對話方塊中，按一下「確定」。

## 接受/拒絕工作流程 {#accept-reject-workflow}

當內容在翻譯後返回並處於準備好審查狀態時，您可以進入翻譯工作並接受/拒絕內容。

![chlimage_1-267](assets/chlimage_1-267.png)

如果您選取「拒絕翻譯」，則可選擇新增註解。

![chlimage_1-268](assets/chlimage_1-268.png)

若拒絕內容，系統會將其傳回翻譯廠商，以便他檢視意見。

## 檢閱和提升更新的內容 {#reviewing-and-promoting-updated-content}

為現有語言副本翻譯內容時，請檢閱翻譯並在必要時進行變更，然後提升翻譯以將其移至語言副本。 您可以在翻譯作業顯示「準備好審查」狀態時審查已翻譯檔案。

![chlimage_1-269](assets/chlimage_1-269.png)

1. 在語言主版中選取頁面，按一下「參照」，然後按一下「語言副本」。
1. 按一下要檢閱的語言副本。

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. 按一下啟動以顯示與啟動相關的命令。

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. 若要開啟頁面的啟動復本以檢閱和編輯內容，請按一下「開啟頁面」 。
1. 檢閱內容並進行必要的變更後，若要提升啟動副本，請按一下「提升」 。
1. 在「提升啟動」頁面上，指定要提升的頁面，然後按一下「提升」 。

## 比較語言副本 {#comparing-language-copies}

若要將語言副本與語言主要版本進行比較：

1. 在&#x200B;**網站**&#x200B;主控台中，導覽至您要比較的語言副本。
1. 開啟&#x200B;**[參考](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板。
1. 在&#x200B;**復本**&#x200B;標題下，選取&#x200B;**語言復本。**
1. 選取您的特定語言副本，然後您可以按一下**與主版比較**或**與上一個比較**（如果適用）。

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. 兩個頁面（啟動項和來源）將並排開啟。

   如需有關使用此功能的完整資訊，請參閱[頁面差異](/help/sites-authoring/page-diff.md)。

## 完成並封存翻譯工作 {#completing-and-archiving-translation-jobs}

在檢閱來自供應商的已翻譯檔案後，完成翻譯工作。 對於人工翻譯工作流程，完成翻譯會向供應商指出已履行翻譯合約，且他們應將翻譯儲存至其翻譯記憶庫。

完成工作後，工作會變成「完成」狀態。

![chlimage_1-272](assets/chlimage_1-272.png)

在翻譯工作完成後將其封存，您就不再需要檢視工作狀態詳細資訊。 當您封存工作時，翻譯工作表徵圖會從專案中移除。

## 建立語言副本的結構 {#creating-the-structure-of-a-language-copy}

填入您的語言副本，使其包含您正在翻譯之主要語言的內容。 您必須先[建立語言副本的語言根](/help/sites-administering/tc-prep.md#creating-a-language-root)，才能填入語言副本。

1. 使用Sites Console來選取您用來作為來源的主要語言的語言根。 例如，若要翻譯Geometrixx示範網站的英文頁面，請選取「內容>Geometrixx示範網站>英文」。
1. 在工具列上，按一下「參照」。

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. 選取「語言副本」，然後選取您要填入的語言副本。

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. 按一下「更新語言副本」以顯示翻譯工具並設定屬性：

   * 選取「選取所有子頁面」選項。
   * 針對「專案」，選取「僅建立結構」。

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. 按一下「開始」。

## 移動或重新命名Source頁面 {#move-source}

如果已經翻譯的來源頁面需要[重新命名或移動](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)，請在移動後根據新的頁面名稱/位置重新翻譯頁面，以建立語言副本。 根據先前名稱/位置的舊語言副本仍然存在。 為避免此問題，您可以在移動後使用更新語言複製功能：

1. 移動有語言副本的頁面。
1. 選取語言副本根目錄。
1. 開啟&#x200B;**參考**&#x200B;面板。
1. 選取&#x200B;**語言副本**。
1. 選取您要更新的目標語言。
1. 選取&#x200B;**更新語言副本**。

   ![正在更新語言副本](assets/translation-move-to.png)

1. 按一下&#x200B;**更新**。 將建立[啟動](/help/sites-authoring/launches-promoting.md)。
1. 導覽至所需的語言根並加以選取。
1. 使用&#x200B;**參考**&#x200B;面板，選取&#x200B;**啟動**。

   ![promote-launch-translation](assets/promote-launch-translation.png)

1. 按一下已建立的啟動項，然後按一下&#x200B;**提升啟動項**。

現在，來源頁面已移動，且相關的語言副本也已移動。

## 使用專案控制檯建立翻譯專案 {#creating-a-translation-project-using-the-projects-console}

如果您偏好使用專案主控台，可以手動建立翻譯專案。

>[!NOTE]
>
>若要建立專案，您的帳戶必須是`projects-administrators`群組的成員。

當您手動建立翻譯專案時，除了[基本屬性](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project)之外，還必須提供下列翻譯相關屬性的值：

* **名稱：**&#x200B;專案名稱。
* **Source語言：**&#x200B;來源內容的語言。
* **目標語言：**&#x200B;內容將翻譯成何種語言。
* **翻譯方法：**&#x200B;選取「人工翻譯」以指示要手動執行翻譯。

1. 在「專案」控制檯的工具列上，按一下「建立」。
1. 選取翻譯專案範本，然後按「下一步」。
1. 輸入基本屬性的值。
1. 按一下進階，並提供翻譯相關屬性的值。
1. 按一下「建立」。 在確認方塊中，按一下完成以返回專案主控台，或按一下開啟專案以開啟並開始管理專案。

## 匯出翻譯工作 {#exporting-a-translation-job}

例如，您可以下載翻譯工作的內容，透過聯結器傳送給未與AEM整合的翻譯提供者，或檢閱內容。

1. 從「翻譯工作」方塊的下拉式功能表中，按一下「匯出」。
1. 在「匯出」對話方塊中，按一下「下載匯出的檔案」，並視需要使用Web瀏覽器對話方塊來儲存檔案。
1. 在「匯出」對話方塊中，按一下「關閉」。

## 匯入翻譯工作 {#importing-a-translation-job}

例如，當您的翻譯提供者將翻譯內容傳送給您時，您可將翻譯內容匯入至AEM，因為它們未透過聯結器與AEM整合。

1. 從「翻譯工作」方塊的下拉式功能表中，按一下「匯入」。
1. 使用網頁瀏覽器的對話方塊來選取要匯入的檔案。
1. 在「匯入」對話方塊中，按一下「關閉」。
