---
title: C2PA中繼資料[!DNL Experience Manager Assets]
description: 瞭解[!DNL Experience Manager Assets]如何在上傳資產上偵測C2PA中繼資料、在使用者介面中標示這些資料，以及簽署其為Gen AI資產產生的轉譯。
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: f47205896ed512deadb4d31acbfe0fafa18515e7
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 6%
---

# [!DNL Experience Manager Assets]中的C2PA中繼資料 {#c2pa-metadata}

各大品牌均比從前更加關注內容透明度、AI 揭露，以及防止資產被篡改等情況。 Adobe 的 Content Authenticity Initiative (CAI) 可建置符合[內容來源與真實性聯盟](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) (C2PA) 技術標準的工具。 C2PA中繼資料是一種新型的中繼資料，可協助檢視者瞭解內容的譜系並確保品牌資產的完整性。 其中可能包含廣泛的溯源資料，提供關於數位資產歷史記錄的洞察。

這些資訊包括：

* **簽發者或簽署者：**&#x200B;發行資產數位簽章之實體或公司的相關資訊。
* **問題日期：**&#x200B;將C2PA中繼資料套用至資產的日期。
* **處理：**&#x200B;編輯或修改資產的任何記錄。
* **裝置詳細資料：**&#x200B;用於建立或編輯資產之應用程式或裝置的相關資訊。
* **使用的AI工具：**&#x200B;如果使用generative AI編輯或建立資產，則會包含使用的模型名稱。
* **其他相關資訊：**&#x200B;提供更多資產歷史記錄相關內容的其他資料。

如需有關資產記錄的詳細資訊，請參閱[驗證](https://contentcredentials.org/verify)。

當您上傳或更新資產時，[!DNL Adobe Experience Manager Assets]會偵測C2PA中繼資料、在[!DNL Assets]使用者介面中標示這些資產，並將Gen AI揭露完整保留在[!DNL Experience Manager]產生的轉譯上。 每當[!DNL Experience Manager]建立或修改Gen AI資產的轉譯時（例如縮圖、Web轉譯、加水印的復本或視訊轉碼），[!DNL Experience Manager]都會以參照原始資產作為其父級的新C2PA中繼資料簽署該轉譯。 您下載、發佈或共用的轉譯會保留其出處。

## 先決條件 {#Prerequisites}

C2PA中繼資料支援需要[!DNL Adobe Experience Manager] 6.5 Service Pack。 在Service Pack 6.5.25.0上，安裝[AEM 6.5 SP25 - C2PA GenAI法規遵循Hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-ASSETS-75868-SP25-1.0.zip)。

## 支援的格式和平台 {#supported-formats}

### 格式 {#formats}

[!DNL Experience Manager]會以[C2PA規格](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)支援內嵌資訊清單的格式簽署轉譯。

| 類型 | 格式 | MIME 類型 |
|---|---|---|
| 影像 | JPEG、PNG、GIF、TIFF、DNG、WebP、JPEG XL、AVIF、HEIC/HEIF、SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| 影片 | MP4、MOV、AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| 音訊 | MP3、M4A、WAV、FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager]也可辨識常見別名，例如`image/jpg`、`image/pjpeg`、`image/x-png`和`video/mov`。 [!DNL Experience Manager]會檢查每個上傳的資產是否有資訊清單，無論檔案格式為何。 PSD或EPS等其他格式的轉譯均未經簽署。

### 平台 {#platforms}

C2PA中繼資料支援仰賴`cq-dam-core`套件組合內隨附的原生C2PA元件，每個支援的平台各有一個組建。 服務啟動時，[!DNL Experience Manager]會將您平台（`adobe_c2patool`或Windows上的`adobe_c2patool.exe`）的組建擷取到套件組合的私人資料夾，檢查SHA-256總和檢查碼，並以個別程式執行。 您不需要安裝任何專案或變更`PATH`。

| 作業系統 | 架構 |
|---|---|
| Linux （glibc 2.28或更新版本，包括Red Hat Enterprise Linux 8） | `x86_64`, `aarch64` |
| macOS | `x86_64`， `aarch64` (Apple silicon) |
| Windows | `x86_64` |

這在[!DNL Adobe Managed Services]和內部部署上的運作方式相同。 請確定[!DNL Experience Manager]處理序可以啟動此可執行檔。 如果您使用`noexec`掛載、防毒或端點安全性軟體，請允許`adobe_c2patool`從`crx-quickstart`資料夾執行。 否則，無法啟動C2PA中繼資料支援。

## C2PA中繼資料的運作方式 {#how-c2pa-metadata-works}

C2PA中繼資料支援分為兩個部分：偵測何時上傳或更新資產，以及每當[!DNL Experience Manager]產生或修改轉譯時重新簽署。

### 工作流程設定 {#workflow}

[偵測C2PA中繼資料](#detect)中顯示的&#x200B;**[!UICONTROL 偵測C2PA認證]**&#x200B;步驟是預設&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程模型的一部分。 如果您使用該模型的自訂副本，請自行新增步驟：

1. 在[!DNL Experience Manager]介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**，並在![編輯圖示](assets/edit.svg) **[!UICONTROL 編輯]**&#x200B;模式中開啟您的模型。
1. 在&#x200B;**[!UICONTROL 中繼資料處理器]**&#x200B;之後，在任何步驟產生轉譯之前，新增&#x200B;**[!UICONTROL 偵測C2PA認證]**&#x200B;步驟。
1. 選取&#x200B;**[!UICONTROL 同步]**&#x200B;以儲存模型。

只有在資產上已執行偵測時，轉譯步驟才會簽署其輸出。 如果在偵測之後執行，則其轉譯會保持未簽署，直到工作流程再次執行為止。

### 偵測C2PA中繼資料 {#detect}

**[!UICONTROL DAM更新資產]**&#x200B;工作流程包含在&#x200B;**[!UICONTROL 中繼資料處理器]**&#x200B;步驟之後執行的&#x200B;**[!UICONTROL 偵測C2PA認證]**&#x200B;步驟，如下圖所示。 它會讀取資產的原始二進位檔，並將結果記錄在資產的中繼資料節點`jcr:content/metadata`中。

![工作流程](assets/workflow.png)

下表列出C2PA中繼資料工作流程中的主要中繼資料屬性。

| 屬性 | 類型 | 說明 |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | `true`，如果原始二進位檔案具有內嵌C2PA資訊清單。 永遠都是寫好的。 |
| `dam:isAiGenerated` | `boolean` | `true`，如果資訊清單將資產放在Gen AI標籤的範圍內。 只有在資訊清單存在時才寫入。 |
| `dam:c2paValidationState` | `string` | 它描述資訊清單的驗證狀態： `TRUSTED`、`VALID`、`INVALID`或`UNKNOWN`。 只有在資訊清單存在時才寫入。 |

當資訊清單出現時，[!DNL Experience Manager]也會將其儲存為`c2pa-manifest.json`轉譯(`application/json`)。

如果您以沒有資訊清單的二進位檔取代原始資產，下一個工作流程執行會將`dam:hasC2PAManifest`設定為`false`並移除`dam:isAiGenerated`、`dam:c2paValidationState`和`c2pa-manifest.json`轉譯。

>[!NOTE]
>
>偵測失敗不會封鎖資產擷取。 如果讀取資訊清單逾時或失敗，[!DNL Experience Manager]會記錄錯誤、保留中繼資料不變，並繼續工作流程的其餘部分。

### 在[!DNL Assets]使用者介面中檢視C2PA中繼資料 {#view-c2pa-metadata}

攜帶C2PA中繼資料的Assets會在[!DNL Assets]使用者介面中顯示&#x200B;**cr** （C2PA中繼資料）徽章。 導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**，然後在的左下角尋找徽章：

* **[!UICONTROL 卡片檢視]**&#x200B;中的資產縮圖。
* **[!UICONTROL 欄檢視]**&#x200B;中的資產縮圖。 選取要顯示其縮圖的資產。
* 資產詳細資訊頁面的預覽區域。

下圖中顯示的&#x200B;**cr**&#x200B;徽章指出資產是否包含C2PA中繼資料。 它不會顯示資訊清單本身。 若要檢視完整的資訊清單，請下載該資產，並在[驗證](https://contentcredentials.org/verify)中將其開啟。

![cr徽章](assets/cr.png)

[!DNL Experience Manager]會將偵測到的資訊清單儲存為資產上的`c2pa-manifest.json`轉譯。 此轉譯為內部轉譯。 它不會出現在資產詳細資料頁面的&#x200B;**[!UICONTROL 轉譯]**&#x200B;面板或轉譯選擇器中。

### 簽署轉譯 {#sign-renditions}

轉譯是新的二進位，因此內嵌在原始資產中的資訊清單不會涵蓋它。 為了讓Gen AI公開完整無缺，[!DNL Experience Manager]會將每個合格的轉譯簽章為產生該轉譯之程式的最後一步。 新的C2PA中繼資料：

* 參考原始資產作為其&#x200B;**父項**&#x200B;成分。
* 紀錄如何從原始資產衍生轉譯，作為C2PA動作`c2pa.resized`、`c2pa.transcoded`或`c2pa.edited`之一。
* 將`Adobe Experience Manager`命名為軟體代理。

[!DNL Experience Manager]只有在下列所有專案皆為`true`時才簽署轉譯：

* 來源資產的`dam:isAiGenerated`已設定為`true`。 載有資訊清單但未透過AI產生的Assets仍會顯示&#x200B;**cr**&#x200B;徽章，但[!DNL Experience Manager]不會重新簽署其轉譯。
* 來源資訊清單是可讀取的，其驗證狀態不是`INVALID`。 [!DNL Experience Manager]絕對不會將新簽章鏈結到驗證失敗的資訊清單上，例如在資產被竄改之後。
* 轉譯格式支援內嵌C2PA資訊清單。 如需詳細資訊，請參閱[支援的格式](#supported-formats)。 [!DNL Experience Manager]會略過不支援的格式，而不會發生錯誤。

[偵測C2PA中繼資料](#detect)中顯示&#x200B;**[!UICONTROL DAM更新資產工作流程已完成]**&#x200B;工作流程的下列步驟對其輸出簽署。

| 工作流程步驟 | 已簽署的轉譯 | 已記錄C2PA動作 |
|---|---|---|
| **[!UICONTROL 處理縮圖]** | 縮圖轉譯和啟用Web的影像。 | 格式變更時`c2pa.resized`和`c2pa.transcoded`。 |
| **[!UICONTROL EPS縮圖（由ImageMagick支援）]** | 主要輸出、衍生縮圖和Web轉譯。 | `c2pa.resized`、`c2pa.transcoded`或`c2pa.edited` |
| **[!UICONTROL FFmpeg縮圖]** | 視訊海報影格和縮圖。 | `c2pa.resized` 和 `c2pa.transcoded` |
| **[!UICONTROL FFmpeg轉碼]** | 視訊編碼。 | `c2pa.transcoded` |
| **[!UICONTROL 點陣化PDF/AI影像預覽轉譯]** | 預覽轉譯。 (`cqdam.preview.png`) | `c2pa.transcoded` |

當您在&#x200B;**[!UICONTROL DAM更新資產工作流程已完成]**&#x200B;工作流程、其他工作流程或自訂工作流程模型中使用下列工作流程時，這些工作流程也會對其輸出簽名。 在[偵測C2PA中繼資料](#detect)中所顯示的工作流程步驟的&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;清單中選取它們。

| 工作流程程式 | 已簽署的轉譯 | 已記錄C2PA動作 |
|---|---|---|
| **[!UICONTROL 建立縮圖]** | 縮圖轉譯。 | 格式變更時`c2pa.resized`和`c2pa.transcoded`。 |
| **[!UICONTROL 建立啟用Web的影像]** | 網頁轉譯。 | 格式變更時`c2pa.resized`和`c2pa.transcoded`。 |
| **[!UICONTROL 命令列]**，例如，[!DNL ImageMagick] | 主要輸出、衍生縮圖和Web轉譯。 | `c2pa.resized`、`c2pa.transcoded`或`c2pa.edited` |
| **[!UICONTROL 影像浮水印程式]** | 浮水印轉譯，或浮水印就緒時的原始轉譯。 如需詳細資訊，請參閱[為您的資產加上浮水印](/help/assets/watermarking.md)。 | `c2pa.edited` |
| **[!UICONTROL 建立視訊指令碼]** | 分鏡指令碼關鍵影格。 | `c2pa.transcoded` |
| **[!UICONTROL XMP回寫]** | 回寫中繼資料後的原始轉譯。 如需詳細資訊，請參閱[XMP轉譯回寫](/help/assets/xmp-writeback.md)。 | `c2pa.edited` |

### 在XMP回寫期間保護原始二進位 {#xmp-writeback}

XMP回寫會重寫原始二進位，這會破壞其內嵌資訊清單。 對於將`dam:hasC2PAManifest`設為`true`的資產，[!DNL Experience Manager]會變更&#x200B;**[!UICONTROL DAM中繼資料回寫]**&#x200B;工作流程的&#x200B;**[!UICONTROL XMP回寫程式]**&#x200B;步驟的行為，如下所示：

* **Gen AI資產** （`dam:isAiGenerated`為`true`）： [!DNL Experience Manager]會寫入XMP，然後重新簽署原始二進位檔，並將預先寫入的二進位檔當作父項。 這會同時儲存回寫和新簽名。 如果重新簽署失敗，它會捨棄兩者，且無法執行此步驟。
* **攜帶資訊清單的其他資產**： [!DNL Experience Manager]會略過XMP回寫並記錄原因。 原始二進位檔及其資訊清單保持不變。

### 簽署模式 {#signing-mode}

[!DNL Experience Manager]在本機簽署轉譯（在生產轉譯的執行個體上），並使用其自行產生的短暫自我簽署憑證。 簽署不需要網路存取，也不需要憑證或私密金鑰設定。

>[!NOTE]
>
>您無法設定自己的簽署憑證。 [驗證](https://contentcredentials.org/verify)之類的驗證器會顯示轉譯的Gen AI公開以及與原始檔案的連結，但不會將您的組織識別為簽署者。

## 設定C2PA中繼資料 {#configure}

預設會啟用C2PA中繼資料支援。 您不需要安裝或設定任何專案。

### OSGi設定 {#osgi-configuration}

若要變更預設設定，請在`https://[aem_server]:[port]/system/console/configMgr`的Configuration Manager中設定&#x200B;**[!UICONTROL Day CQ DAM C2PA服務]** (PID `com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl`)，如下圖所示，或將OSGi設定新增至您的專案。 如需詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

![OSGi設定](assets/OSGi.png)

下表列出專案的OSGi設定中的屬性。

| 屬性 | Configuration Manager的名稱 | 預設 | 說明 |
|---|---|---|---|
| `enabled` | **[!UICONTROL 已啟用]** | `true` | 開啟或關閉C2PA中繼資料支援。 關閉時，[!DNL Experience Manager]不會偵測資訊清單，也不會簽署轉譯。 |
| `timeoutMillis` | **[!UICONTROL CLI逾時（毫秒）]** | `30000` | 指定[!DNL Experience Manager]在檔案上等待單一讀取或簽署作業，然後將其視為逾時的最長時間（毫秒）。 針對大型視訊或高解析度影像檔案提升此值。 |

例如，在`/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`新增OSGi設定。

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### 關閉C2PA中繼資料支援 {#disable}

在[OSGi設定](#osgi-configuration)中顯示的&#x200B;**[!UICONTROL Day CQ DAM C2PA服務]**&#x200B;設定中，停用&#x200B;**[!UICONTROL 已啟用]**&#x200B;選項，然後儲存變更。 變更立即生效，無需重新啟動：

* 顯示在[偵測C2PA中繼資料](#detect)中的&#x200B;**[!UICONTROL 偵測C2PA認證]**&#x200B;步驟變成無法運作。
* 工作流程步驟無需簽署即可建立轉譯。
* Assets先前已處理並保留其`dam:hasC2PAManifest`屬性，且仍會顯示&#x200B;**cr**&#x200B;徽章。

>[!CAUTION]
>
>停用&#x200B;**[!UICONTROL 已啟用]**&#x200B;選項後，Gen AI資產的轉譯不會附帶C2PA中繼資料。 如果您要遵守Gen AI公開法規，請啟用&#x200B;**[!UICONTROL 已啟用]**&#x200B;選項。

## 自訂處理管道 {#customize}

若要在&#x200B;**[!UICONTROL DAM Update Asset]**&#x200B;中新增、移除或重新排序步驟，並且仍保持Gen AI公開不變，請遵循下列規則：

* **請先執行偵測。** 在每個建立或修改轉譯的步驟前保留&#x200B;**[!UICONTROL 偵測C2PA認證]**。
* **最後簽署。** 簽署後對二進位檔的任何變更都會使其簽章失效。 請勿在簽署轉譯的步驟之後，執行修改轉譯的步驟。
* **使用簽署的步驟。** [簽署轉譯](#sign-renditions)中列出的內建步驟會簽署其輸出。 除非明確新增簽署，否則您透過&#x200B;**[!UICONTROL 命令列]**&#x200B;程式以外的任何程式執行的自訂步驟和協力廠商工具不會簽署其輸出。 如需詳細資訊，請參閱[使用媒體處理常式和工作流程處理資產](/help/assets/media-handlers.md)。
* **請勿就地修改原始專案**，除非步驟重新簽署，如&#x200B;**[!UICONTROL XMP回寫]**&#x200B;和&#x200B;**[!UICONTROL 影像浮水印程式]**&#x200B;所做的那樣。

### 從自訂工作流程步驟簽署轉譯 {#custom-step}

產生轉譯的自訂工作流程步驟可透過`com.day.cq.dam.api.c2pa.C2PASigner` OSGi服務加以簽署。 它會套用與內建步驟相同的適用性規則，但將結果回報為`C2PASigningOutcome`。

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

只有在您的步驟完成撰寫轉譯後，才呼叫`signIfEligible`。 OSGi服務提供下表所列的方法。

| 方法 | 使用它可以 |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | 簽署新的轉譯，並將來源資產作為其父項。 |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | 簽署衍生自相同資產的多個轉譯。 此方法會讀取一次來源資訊清單。 |
| `captureResignState(Asset)` | 在步驟就地修改原始資產之前，先拍攝原始資產的影像。 如果資產不合格，此方法會傳回`null`。 |
| `resign(Asset, Rendition, List<C2PAAction>)` | 就地變更後，重新簽署原始資產，將影像作為其父項。 |
| `discardResignState(Rendition)` | 放置您拍攝但不使用的影像，例如，因為您的變更失敗。 |

下表提及`C2PASigningOutcome`的值。

| 結果 | 說明 |
|---|---|
| `SIGNED` | [!DNL Experience Manager]已簽署轉譯。 |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | 來源資產不會標籤為AI產生的資產。 |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | 轉譯格式不支援內嵌C2PA資訊清單。 |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager]在來源資產上找不到資訊清單。 |
| `SKIPPED_MANIFEST_NOT_VALID` | 來源資訊清單驗證失敗。 |
| `SKIPPED_SERVICE_UNAVAILABLE` | C2PA中繼資料支援已關閉或無法使用。 |
| `FAILED` | 讀取來源資訊清單或簽署轉譯失敗。 |

若要在產生昂貴轉譯之前檢查資格，請呼叫`C2PASupportedFormats.isEligible(...)`。

## 疑難排解 {#troubleshooting}

進行疑難排解時，請在&#x200B;**[!UICONTROL Apache Sling記錄記錄器設定]**&#x200B;中將下列記錄器設定為`DEBUG`。

* `com.day.cq.dam.core.impl.c2pa`：擷取原生C2PA元件、資訊清單讀取和簽署。
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess`：偵測。

| 症狀 | 可能的原因 | 解決方法 |
|---|---|---|
| 沒有資產顯示&#x200B;**cr**&#x200B;徽章。 | C2PA中繼資料支援已關閉，或您的工作流程模型不包含偵測步驟。 | 檢查是否已在&#x200B;**[!UICONTROL Day CQ DAM C2PA服務]**&#x200B;設定中啟用&#x200B;**[!UICONTROL 已啟用]**，而且您的&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型包含&#x200B;**[!UICONTROL 偵測C2PA認證]**。 |
| 您知道有資訊清單但不顯示徽章的資產。 | 該資產是在功能可用之前上傳的。 | 再次在資產上執行&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程，例如，從&#x200B;**[!UICONTROL 時間表]** > **[!UICONTROL 開始工作流程]**。 |
| 服務無法啟動。 錯誤記錄檔報告`adobe_c2patool`無法擷取或標籤為可執行檔。 | 作業系統或架構沒有二進位檔案，或是檔案系統封鎖可執行檔。 | 使用支援的平台。 允許[!DNL Experience Manager]處理序從其`crx-quickstart`資料夾執行可執行檔。 |
| 錯誤記錄檔報告`GLIBC_2.xx not found`。 | Linux主機執行2.28以前的glibc版本。 | 升級主機作業系統。 |
| 偵測或簽署逾時。 | 大型檔案需要的時間超過預設的30秒逾時。 | 提升&#x200B;**[!UICONTROL CLI逾時（毫秒）]**。 |
| Gen AI資產的轉譯未經簽署。 | 不支援此格式、資訊清單為`INVALID`，或在轉譯步驟之後執行偵測。 | 檢查`dam:c2paValidationState`和轉譯格式。 將&#x200B;**[!UICONTROL 偵測C2PA認證]**&#x200B;移到轉譯步驟之前。 |
| XMP回寫不會更新資產。 | 該資產攜帶資訊清單，但未透過AI產生，因此[!DNL Experience Manager]會維持其原始資訊清單不變。 | 這是預期行為。 如需詳細資訊，請參閱[在XMP回寫期間保護原始檔案](#xmp-writeback)。 |

## 限制 {#limitations}

* [!DNL Assets]使用者介面只會顯示C2PA中繼資料是否存在。 資訊清單詳細資料沒有面板。
* [!DNL Experience Manager]只為透過AI產生的資產重新簽署轉譯。 含有資訊清單的其他資產轉譯專案是在沒有C2PA中繼資料的情況下建立的。
* [!DNL Experience Manager]簽章使用自我簽署的無期憑證。 不支援自訂或組織特定的簽署憑證。


>[!MORELIKETHIS]
>
>*  [!DNL Experience Manager as a Cloud Service]&#x200B;[&#128279;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)的Assets檢視中的C2PA中繼資料
>*  [!DNL Experience Manager Assets Essentials]&#x200B;[&#128279;](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/content-credentials)中的C2PA中繼資料
>*  [!DNL Dynamic Media]&#x200B;[&#128279;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)中的C2PA中繼資料
>* [XMP回寫至轉譯](/help/assets/xmp-writeback.md)
>* [為您的資產加上浮水印](/help/assets/watermarking.md)
>* [Content Authenticity Initiative](https://contentauthenticity.org/)
>* [驗證](https://contentcredentials.org/verify)
