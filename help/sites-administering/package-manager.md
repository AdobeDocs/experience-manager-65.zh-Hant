---
title: 封裝管理員
description: 通過包管理器了AEM解包管理的基本知識。
feature: Administering
role: Admin
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: b48b7631c501cea7e4ef1133a452fb6984e4547f
workflow-type: tm+mt
source-wordcount: '3573'
ht-degree: 2%

---


# 封裝管理員 {#working-with-packages}

程式包可以導入和導出儲存庫內容。 您可以使用軟體包來安裝新內容、安裝新功能、在實例之間傳輸內容以及備份儲存庫內容。

使用包管理器，可以在實例和本AEM地檔案系統之間傳輸包以用於開發目的。

## 什麼是包？ {#what-are-packages}

軟體包是一個zip檔案，它以檔案系統序列化形式保存儲存庫內容，稱為儲存庫序列化，提供了檔案和資料夾的易於使用和易於編輯的表示形式。 包中包含的內容是使用篩選器定義的。

包還包含保管庫元資訊，包括篩選器定義和導入配置資訊。 不用於包提取的附加內容屬性可以包括在包中，如說明、可視影像或表徵圖。 這些附加內容屬性僅用於內容包使用者和資訊目的。

>[!NOTE]
>
>包表示生成包時內容的當前版本。 它們不包括儲存庫中保留的任何AEM以前版本的內容。

## 封裝管理員 {#package-manager}

包管理器管理安裝中AEM的包。 等你 [分配了必要的權限](#permissions-needed-for-using-the-package-manager) 您可以使用包管理器執行各種操作，包括配置、構建、下載和安裝包。

### 所需權限 {#required-permissions}

要建立、修改、上載和安裝軟體包，用戶必須對以下節點擁有相應的權限：

* 完全權限（刪除時除外） `/etc/packages`
* 包含包內容的節點

>[!CAUTION]
>
>授予包權限可能會導致敏感資訊洩露和資料丟失。
>
>為限制這些風險，強烈建議僅授予專用子樹的特定組權限。

### 訪問包管理器 {#accessing}

可以通過以下三種方式訪問包管理器：

1. 從主AEM菜單 — > **工具** -> **部署** -> **包**
1. 從 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 使用頂部切換器欄
1. 通過訪問 `http://<host>:<port>/crx/packmgr/`

### 包管理器UI {#ui}

包管理器分為四個主要功能區：

* **左導航面板**  — 此面板允許您篩選和排序包清單。
* **包清單**  — 這是實例上按左側導航面板中的選擇篩選和排序的包清單。
* **活動日誌**  — 此面板最初被最小化，並展開以詳細瞭解包管理器的活動，例如在生成或安裝包時。 「活動日誌」頁籤中有其它按鈕，用於：
   * **清除日誌**
   * **顯示/隱藏**
* **工具欄**  — 工具欄包含「左導航面板」和「包」清單的刷新按鈕，以及用於搜索、建立和上載包的按鈕。

![包管理器UI](assets/package-manager-ui.png)

按一下左側導航面板中的選項可立即過濾包清單。

按一下包名稱會展開「包清單」中的條目，以顯示有關包的詳細資訊。

![擴展的包詳細資訊](assets/package-expand.png)

當擴展包詳細資訊時，可通過工具欄按鈕對包執行的操作數目。

* [編輯](#edit-package)
* [建置](#building-a-package)
* [重新安裝](#reinstalling-packages)
* [下載](#downloading-packages-to-your-file-system)
* [共用](#share)

在以下位置可執行進一步操作 **更多** 按鈕

* [刪除](#deleting-packages)
* [適用範圍](#package-coverage)
* [內容](#viewing-package-contents-and-testing-installation)
* [折行](#rewrapping-a-package)
* [其他版本](#other-versions)
* [解除安裝](#uninstalling-packages)
* [測試安裝](#viewing-package-contents-and-testing-installation)
* [驗證](#validating-packages)
* [複寫](#replicating-packages)

### 包狀態 {#package-status}

包清單中的每個條目都有一個狀態指示器，讓您一目瞭然地瞭解包的狀態。 懸停在狀態上時，會顯示帶有狀態詳細資訊的工具提示。

![包狀態](assets/package-status.png)

如果包已更改或從未構建，則狀態將顯示為一個連結，以便快速執行重建或安裝包的操作。

## 包設定 {#package-settings}

軟體包實際上是一組篩選器和基於這些篩選器的儲存庫資料。 使用包管理器UI，可以按一下包，然後 **編輯** 按鈕查看包的詳細資訊，包括以下設定。

* [一般設定](#general-settings)
* [包篩選器](#package-filters)
* [包依賴項](#package-dependencies)
* [進階設定](#advanced-settings)
* [包螢幕截圖](#package-screenshots)

### 一般設定 {#general-settings}

您可以編輯各種包設定來定義資訊，如包說明、依賴項和提供程式詳細資訊。

的 **包設定** 對話框可通過 **編輯** 按鈕 [建立](#creating-a-new-package) 或 [編輯](#viewing-and-editing-package-information) 包。 進行任何更改後，按一下 **保存**。

![編輯包對話框，常規設定](assets/general-settings.png)

| 欄位 | 說明 |
|---|---|
| 名稱 | 包的名稱 |
| 群組 | 對於組織包，可以鍵入新組的名稱或選擇現有組 |
| 版本 | 用於版本的文本 |
| 說明 | 允許格式化的HTML標籤的包的簡要描述 |
| 縮圖 | 隨包清單一起顯示的表徵圖 |

#### 包縮略圖 {#thumbnails}

縮略圖提供了包含內容的快速參考視覺表示。 然後，這將顯示在包清單中，有助於輕鬆識別包或包類。

以下是公約用於正式包裝的實例：

正式修補程式

![正式熱修復縮略圖](assets/official-hotfix.png)

正AEM式安裝擴展

![正式AEM安裝或擴展縮略圖](assets/official-installation.png)

正式服務包

![正式AEMService Pack表徵圖](assets/official-service-pack.png)

為包使用唯一表徵圖。 不要重用Adobe使用的表徵圖。

### 包篩選器 {#package-filters}

篩選器標識要包括在包中的儲存庫節點。 A **篩選器定義** 指定以下資訊：

* 的 **根路徑** 包含的內容
* **規則** 包括或排除根路徑下的特定節點

使用 **+** 按鈕 使用 **-** 按鈕

規則根據其順序應用，因此使用 **上** 和 **向下** 箭頭按鈕。

篩選器可以包含零個或多個規則。 如果未定義規則，則包將包含根路徑下的所有內容。

可以為包定義一個或多個篩選器定義。 使用多個篩選器來包括來自多個根路徑的內容。

![「篩選器」頁籤](assets/edit-filter.png)

建立篩選器時，可以定義路徑或使用規則運算式指定要包括或排除的所有節點。

| 規則類型 | 說明 |
|---|---|
| include | 包括一個目錄將包括該目錄以及該目錄中的所有檔案和資料夾（即整個子樹），但 **不會** 在指定的根路徑下包含其他檔案或資料夾。 |
| 排除 | 排除目錄將排除該目錄以及該目錄中的所有檔案和資料夾（即整個子樹）。 |

包篩選器最常在首次定義時 [建立包。](#creating-a-new-package) 但是，也可以稍後編輯這些內容，之後應重建包，以根據新的篩選器定義更新其內容。

>[!TIP]
>
>一個包可以包含多個篩選器定義，以便來自不同位置的節點可以容易地組合成一個包。

### 相依性 {#dependencies}

![「依賴項」頁籤](assets/dependencies.png)

| 欄位 | 說明 | 範例/詳細資料 |
|---|---|---|
| 測試方式 | 此軟體包的目標產品名稱和版本或與之相容。 | `6.5` |
| 已修正的問題 | 一個文本欄位，用於列出此包修復的Bug的詳細資訊，每行一個Bug | - |
| 取決於 | 列出安裝時所需的其他軟體包，以便當前軟體包按預期運行 | `groupId:name:version` |
| 取代 | 此包替換的已過時包的清單 | `groupId:name:version` |

### 進階設定 {#advanced-settings}

![「高級設定」頁籤](assets/advanced-settings.png)

| 欄位 | 說明 | 範例/詳細資料 |
|---|---|---|
| 名稱 | 包的提供程式的名稱 | `WKND Media Group` |
| URL | 提供程式的URL | `https://wknd.site` |
| 連結 | 到提供程式頁的包特定連結 | `https://wknd.site/package/` |
| 需要 | 定義安裝軟體包時是否存在任何限制 | **管理**  — 只能以管理員權限安裝軟體包&#x200B;<br>**重新啟動**  — 安AEM裝包後必須重新啟動 |
| AC 處理 | 指定在導入包時如何處理包中定義的訪問控制資訊 | **忽略**  — 保留儲存庫中的ACL <br>**覆蓋**  — 覆蓋儲存庫中的ACL <br>**合併**  — 合併兩組ACL <br>**合併保留**  — 通過添加內容中不存在的主體的訪問控制項，將內容中的訪問控制與隨包提供的訪問控制合併&#x200B;<br>**清除**  — 清除ACL |

### 包螢幕截圖 {#package-screenshots}

您可以將多個螢幕截圖附加到包中，以提供內容顯示方式的可視表示。

![螢幕截圖頁籤](assets/screenshots.png)

## 包操作 {#package-actions}

可以對包執行許多操作。

### 建立包 {#creating-a-new-package}

1. [訪問包管理器。](#accessing)

1. 按一下 **建立包**。

   >[!TIP]
   >
   >如果實例包很多，則可能存在資料夾結構。 在這種情況下，在建立新包之前更容易導航到所需的目標資料夾。

1. 在 **新建包** 對話框，輸入以下欄位：

   ![新建包對話框](assets/new-package-dialog.png)

   * **包名稱**  — 選擇描述性名稱，以幫助您（和其他人）輕鬆識別包的內容。

   * **版本**  — 這是一個文本欄位，用於指示版本。 這將附加到包名稱中，以形成zip檔案的名稱。

   * **組**  — 這是目標組（或資料夾）名稱。 組可幫助您組織包。 如果組不存在，則為其建立資料夾。 如果將組名留空，它將在主包清單中建立包。

1. 按一下 **確定** 的子菜單。

1. AEM在包清單頂部列出新包。

   ![新包](assets/new-package.png)

1. 按一下 **編輯** 定義 [包內容。](#package-contents) 按一下 **保存** 編輯完設定後。

1. 你現在可以 [生成](#building-a-package) 你的包裹。

建立包後立即生成包並非強制性。 未構建的包不包含任何內容，並且僅包含包的篩選器資料和其他元資料。

### 生成包 {#building-a-package}

通常在您同時生成包 [建立包](#creating-a-new-package)，但稍後可以返回生成或重建包。 如果儲存庫中的內容已更改或包篩選器已更改，則此功能非常有用。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **生成**。 一個對話框要求確認您確實要生成包，因為任何現有包內容都將被覆蓋。

1. 按一下&#x200B;**「確定」**。生AEM成包，在活動清單中列出添加到包的所有內容。 完成時AEM，顯示已生成包的確認，並（關閉對話框時）更新包清單資訊。

### 編輯包 {#edit-package}

包上載到後AEM，可以修改其設定。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **編輯** 並更新 **[包設定](#package-settings)** 按需要。

1. 按一下 **保存** 來保存。

你可能需要 [重建包](#building-a-package) 根據您所做的更改更新其內容。

### 重新包裝包 {#rewrapping-a-package}

一旦生成了包，就可以重新包裝。 重新包裝將更改包資訊，而不更改包內容。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **編輯** 並更新 **[包設定](#package-settings)** 按需要。

1. 按一下 **保存** 來保存。

1. 按一下 **更多** -> **重繞** 對話會要求確認。

### 查看其他包版本 {#other-versions}

因為軟體包的每個版本都以任何其他軟體包的形式顯示在清單中，所以軟體包管理器可以查找所選軟體包的其他版本。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **更多** -> **其他版本** 並開啟一個對話框，其中列出了包含狀態資訊的同一軟體包的其他版本。

### 查看包內容和測試安裝 {#viewing-package-contents-and-testing-installation}

生成包後，您可以查看內容。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 要查看內容，請按一下 **更多** -> **內容**，並且包管理器在活動日誌中列出包的全部內容。

   ![包內容](assets/package-contents.png)

1. 要執行安裝的乾式運行，請按一下 **更多** -> **Test安裝** 和「包管理器」在活動日誌中報告結果，就像執行了安裝一樣。

   ![Test安裝](assets/test-install.png)

### 將包下載到檔案系統 {#downloading-packages-to-your-file-system}

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **下載** 按鈕或包詳細資訊區域中包的連結檔案名。

1. 將包AEM下載到您的電腦。

### 共用包 {#share}

包共用是用於分發內容包的集中公共服務。 包共用已被 [軟體分發](#software-distribution) 這個按鈕就不工作了。

### 從檔案系統上載包 {#uploading-packages-from-your-file-system}

1. [訪問包管理器。](#accessing)

1. 選擇要將包上載到的組資料夾。

1. 按一下 **上載包** 按鈕

1. 提供有關上載的包的必要資訊。

   ![包上載對話框](assets/package-upload-dialog.png)

   * **包**  — 使用 **瀏覽……** 按鈕，從本地檔案系統中選擇所需的包。
   * **強制上載**  — 如果已存在具有此名稱的包，則此選項將強制上載並覆蓋現有包。

1. 按一下 **確定** 並且上載所選的包並相應地更新包清單。

包內容現在存AEM在於，但要使內容可用，請確保 [安裝軟體包](#installing-packages)。

### 驗證包 {#validating-packages}

由於軟體包可以修改現有內容，因此在安裝前驗證這些更改通常非常有用。

#### 驗證選項 {#validation-options}

包管理器可以執行以下驗證：

* [OSGi軟體包導入](#osgi-package-imports)
* [覆蓋](#overlays)
* [ACL](#acls)

##### 驗證 OSGi 封裝匯入 {#osgi-package-imports}

**檢查的內容**

此驗證檢查包中所有JAR檔案（OSGi捆綁包），提取它們 `manifest.xml` （包含所述OSGi捆綁所依賴的版本控制依賴項），並驗證實例用AEM正確的版本導出所述依賴項。

**報告方式**

實例無法滿足的任何版本化依賴AEM項都列在包管理器的活動日誌中。

**錯誤狀態**

如果不滿足依賴項，則包中具有這些依賴項的OSGi捆綁將不會啟動。 這會導致應用程式部署中斷，因為依賴未啟動的OSGi捆綁包的任何應用程式都會無法正常運行。

**錯誤解決方法**

要解決由於未滿足的OSGi捆綁包而引起的錯誤，必須調整捆綁包中具有未滿足的導入的依賴關係版本。

##### 驗證覆蓋 {#overlays}

**檢查的內容**

此驗證確定所安裝的軟體包是否包含已在目標實例中覆蓋的AEM檔案。

例如，在 `/apps/sling/servlet/errorhandler/404.jsp`，包含 `/libs/sling/servlet/errorhandler/404.jsp`，以便更改現有檔案 `/libs/sling/servlet/errorhandler/404.jsp`。

**報告方式**

包管理器的活動日誌中描述了任何此類覆蓋。

**錯誤狀態**

錯誤狀態表示包正在嘗試部署已覆蓋的檔案，因此包中的更改將被覆蓋覆蓋（因此「隱藏」）覆蓋，而不會生效。

**錯誤解決方法**

要解決此問題，請在中維護覆蓋檔案的 `/apps` 必須查看對所覆蓋檔案的更改 `/libs` 並根據需要將更改合併到疊加( `/apps`)，並重新部署重疊檔案。

>[!NOTE]
>
>如果重疊內容已正確地合併到重疊檔案中，則驗證機制無法協調。 因此，即使進行了必要的更改，此驗證仍將繼續報告衝突。

##### 驗證 ACL {#acls}

**檢查的內容**

此驗證將檢查正在添加的權限、將如何處理（合併/替換），以及當前權限是否會受到影響。

**報告方式**

這些權限在包管理器的活動日誌中介紹。

**錯誤狀態**

不能提供顯式錯誤。 驗證僅指示安裝軟體包是否會添加或影響任何新ACL權限。

**錯誤解決方法**

利用驗證提供的資訊，可以在CRXDE中查看受影響的節點，並根據需要在包中調整ACL。

>[!CAUTION]
>
>作為最佳做法，建議軟體包不AEM應影響提供的ACL，因為這可能導致意外行為。

#### 執行驗證 {#performing-validation}

可以通過兩種不同的方法來驗證軟體包：

* [通過包管理器UI](#via-package-manager)
* [通過HTTPPOST請求（如與cURL）](#via-post-request)

上載包後，在安裝包之前，應始終進行驗證。

##### 通過包管理器驗證包 {#via-package-manager}

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 要驗證包，請按一下 **更多** -> **驗證**。

1. 在隨後出現的模式對話框中，使用複選框選擇驗證類型並通過按一下開始驗證 **驗證**。

1. 然後運行所選驗證，並將結果顯示在包管理器的活動日誌中。

##### 通過HTTPPOST請求進行包驗證 {#via-post-request}

POST請求採用以下形式。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

的 `type` 參數可以是任何逗號分隔的無序清單，包括：

* `osgiPackageImports`
* `overlays`
* `acls`

值 `type` 預設值 `osgiPackageImports` 如果未明確傳遞。

使用cURL時，執行類似於以下語句的語句：

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

通過POST請求驗證時，響應將作為JSON對象發回。

### 查看包覆蓋範圍 {#package-coverage}

包由其篩選器定義。 您可以讓包管理器將包的篩選器應用於現有的儲存庫內容，以顯示包的篩選器定義涵蓋的儲存庫內容。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟包詳細資訊。

1. 按一下 **更多** -> **覆蓋範圍**。

1. 服務範圍詳細資訊列在活動日誌中。

### 安裝軟體包 {#installing-packages}

上載包只將包內容添加到儲存庫，但無法訪問。 必須安裝上載的包才能使用包的內容。

>[!CAUTION]
>
>安裝軟體包可以覆蓋或刪除現有內容。 僅當您確定不刪除或覆蓋所需內容時才上載包。

在安裝包之前，包管理器會自動建立包含將被覆蓋內容的快照包。 如果卸載軟體包，將重新安裝此快照。

>[!CAUTION]
>
>* 如果要安裝數字資產，您必須：
   >  首先，停用WorkflowLauncher。
   >  使用OSGi控制台的「元件」菜單選項停用
   >  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* 接下來，安裝完成後，重新激活WorkflowLauncher。
>
>取消激活WorkflowLauncher可確保在安裝時資產導入程式框架不會（無意中）操縱資產。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟要安裝的包的包詳細資訊。

1. 按一下 **安裝** 按鈕 **安裝** 連結。

1. 對話框將請求確認並允許指定其他選項。

   * **僅提取**  — 僅解壓包，以便不建立快照，因此無法卸載
   * **保存閾值**  — 觸發自動保存之前的臨時節點數（如果遇到併發修改例外，則增加）
   * **提取子包**  — 啟用子包的自動提取
   * **訪問控制處理**  — 指定在安裝軟體包時如何處理在軟體包中定義的訪問控制資訊(選項與 [高級包設定](#advanced-settings))
   * **依賴項處理**  — 指定在安裝期間如何處理依賴項

1. 按一下 **安裝**。

1. 活動日誌詳細列出安裝進度。

安裝完成並成功後，將更新包清單，並使用 **已安裝** 在包狀態中顯示。

### 重新安裝包 {#reinstalling-packages}

重新安裝軟體包對已安裝的軟體包執行的步驟與在 [最初安裝軟體包。](#installing-packages)

### 基於檔案系統的上傳和安裝 {#file-system-based-upload-and-installation}

安裝軟體包時，您可以完全放棄包管理器。 可AEM以檢測主機本地檔案系統上特定位置的軟體包，並自動上載和安裝它們。

1. 在安AEM裝資料夾下 `crx-quicksart` jar旁邊的資料夾和 `license.properties` 的子菜單。 建立名為 `install` 在 `crx-quickstart` 導致路徑 `<aem-home>/crx-quickstart/install`。

1. 在此資料夾中，添加包。 它們將自動上傳並安裝到您的實例上。

1. 上載和安裝完成後，您可以在包管理器中查看包，就像您使用包管理器UI安裝了包一樣。

如果實例正在運行，則上載和安裝將立即開始，當您將實例添加到包中 `install` 資料夾

如果實例未運行，則將包放在 `install` 資料夾按字母順序在啟動時安裝。

### 正在卸載包 {#uninstalling-packages}

卸載軟體包會將儲存庫的內容還原為在安裝之前由軟體包管理器自動建立的快照。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，開啟要從包清單中卸載的包的包詳細資訊。

1. 按一下 **更多** -> **卸載**，從儲存庫中刪除此包的內容。

1. 對話框將請求確認並列出所做的所有更改。

1. 將刪除包並應用快照。 進程進度顯示在活動日誌中。

### 刪除包 {#deleting-packages}

刪除包只會從包管理器中刪除其詳細資訊。 如果此包已安裝，則不會刪除已安裝的內容。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱開啟要從包清單中刪除的包的包詳細資訊。

1. 包管理器要求確認要刪除包。 按一下 **確定** 確認刪除。

1. 將刪除包資訊，並在活動日誌中報告詳細資訊。

### 複製包 {#replicating-packages}

複製包的內容以將其安裝到發佈實例上。

1. [訪問包管理器。](#accessing)

1. 通過按一下包名稱，從包清單中開啟要複製的包的包詳細資訊。

1. 按一下 **更多** -> **複製**。

1. 將複製包，並在活動日誌中報告詳細資訊。

## 軟體分發 {#software-distribution}

包AEM可用於跨環境建立和共用AEM內容。

[軟體分發](https://downloads.experiencecloud.adobe.com) 是一種集中服務，旨在簡化包的搜索和下AEM載。

有關詳細資訊，請參閱 [軟體分發文檔。](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

>[!NOTE]
>
>包管理器當前未與軟體分發整合，因為它與以前的包共用服務整合。 因此，包管理器中的共用按鈕和指向包共用的其他連結不再工作。 解決方案是將軟體包下載到本地磁碟。
