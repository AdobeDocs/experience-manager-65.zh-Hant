---
title: 停止支援 SPA 編輯器
description: 雖然SPA Editor仍受Adobe支援，但瞭解其淘汰對您的專案有何影響，以及您對未來專案有哪些選項。
feature: Developing
role: Admin, Leader, User, Developer
exl-id: ea6e46ee-4a90-4236-8d93-292a4dda4dc0
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 16%

---


# 停止支援 SPA 編輯器 {#spa-editor-deprecation}

雖然SPA Editor仍受Adobe支援，但瞭解其淘汰對您的專案有何影響，以及您對未來專案有哪些選項。

## 摘要 {#summary}

Adobe已透過[AEM 6.5，](/help/release-notes/release-notes.md#spa-editor)的6.5.23版取代SPA Editor，這表示其SDK將不再進行進一步的增強功能或更新。 Adobe鼓勵您針對任何新的Headless專案使用[通用編輯器](/help/sites-developing/universal-editor/introduction.md)，以利用AEM的最新創新。

## 淘汰的詳細資訊 {#details}

棄用SPA編輯器&#x200B;**並不意味著立即移除**，而且如果您有現有的實作，**只要符合您的需求，您就可以繼續使用。**&#x200B;但是，請注意其過時的下列影響。

* Adobe未來將只會解決P1和P2問題和安全漏洞。
* 其SDK不再進行任何開發、增強功能或更新。

取代表示下列SDK現在處於功能凍結狀態。

* [AEM專案原型](https://github.com/adobe/aem-project-archetype/)
* [AEM SPA專案核心](https://github.com/adobe/aem-spa-project-core)
* [AEM SPA頁面模型管理員](https://github.com/adobe/aem-spa-page-model-manager)
* [AEM SPA元件對應](https://github.com/adobe/aem-spa-component-mapping)
* [AEM SPA React 可編輯的元件](https://github.com/adobe/aem-react-editable-components)
   * [AEM React核心元件](https://github.com/adobe/aem-react-core-wcm-components)
   * [AEM React核心元件庫](https://github.com/adobe/aem-react-core-wcm-components-base)
   * [AEM React Core Components SPA](https://github.com/adobe/aem-react-core-wcm-components-spa)
   * [AEM React核心元件範例](https://github.com/adobe/aem-react-core-wcm-components-examples)
* [AEM SPA Angular可編輯元件](https://github.com/adobe/aem-angular-editable-components)
   * [AEM Angular核心元件](https://github.com/adobe/aem-angular-core-wcm-components)
   * [AEM Angular核心元件庫](https://github.com/adobe/aem-angular-core-wcm-components-base)
   * [AEM Angular核心元件SPA](https://github.com/adobe/aem-angular-core-wcm-components-spa)
   * [AEM Angular核心元件範例](https://github.com/adobe/aem-angular-core-wcm-components-examples)
* [AEM SPA Vue可編輯元件](https://github.com/mavicellc/aem-vue-editable-components)

## SPA編輯器的替代方案 {#alternatives}

最適合取代SPA Editor的作法取決於您的專案需求。

* **[通用編輯器](/help/sites-developing/universal-editor/introduction.md)**&#x200B;是直接取代SPA編輯器的最佳選擇。
   * Universal Editor也是視覺化編輯器，專為分離式實施而設計，結合了Adobe從SPA Editor的所有體驗。
   * Universal Editor也已[針對AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)發行，因此除了雲端服務之外，還支援AMS和內部部署使用案例。
* **[偏好表單式編輯器的使用者可選擇內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)**。
   * 將內容結構化為內容片段而非頁面時，內容片段編輯器最適合使用。

使用內容片段來建構內容不排除使用通用編輯器作為視覺化編輯器，兩個編輯器可搭配使用。

## 移轉至通用編輯器 {#migrate-ue}

Universal Editor具備許多優點，因此移轉至此編輯器可成為新專案的絕佳解決方案。

* **Visual Editing：**&#x200B;如同SPA Editor，作者可以在預覽中直接編輯內容，並立即看到其變更如何影響訪客體驗。
* **符合未來需求：** AEM 的路徑圖優先發展作為視覺化編輯器的通用編輯器。採用通用編輯器可以確保獲得最新的創新和增強功能。
* **更簡單的整合：**&#x200B;使用通用編輯器不需要 AEM 特定的 SDK，減少過度依賴技術堆疊的情形。
* **自備應用程式：**&#x200B;通用編輯器支援任何網頁框架或架構，不需要複雜的重構過程即可採用。
* **可擴充性：**&#x200B;因為擁有強大的[擴充框架，](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/extending)包括與生成式 AI、Workfront 等的整合，使通用編輯器更具優勢。

沒有從SPA編輯器直接移轉至通用編輯器的路徑。 這是因為兩種技術存在根本差異。

* 通用編輯器並未重新引進範本編輯器、樣式系統或回應式網格等功能。
   * 在Edge Delivery Services或Headless專案中，現在可使用精簡前端CSS和JS更有效地處理這些使用案例。
* 由於通用編輯器是editor-as-a-service，實作人員無法將CSS或JS插入元件對話方塊中。
   * 故不能從頁面編輯器自動轉換元件對話框。
   * 此情況會影響對話框的很多地方，例如自訂小工具、欄位驗證、顯示/隱藏規則，以及範本型自訂功能。

考慮到這些技術差異，Adobe建議您：

* 維持現有的SPA Editor網站不變，因為支援作業會繼續進行。
* 對所有新開發專案採用通用編輯器，包括新網站、區段或頁面。

請記住，即使在Universal Editor中並沒有直接實作某些SPA Editor功能，但是有新方法可使用Universal Editor的新靈活性來解決相同問題。

## 比較SPA編輯器和通用編輯器 {#spa-vs-ue}

如下列圖表所示，通用編輯器為Web應用程式的實作者提供更大的自由度。

![比較Universal Editor和SPA Editor架構](assets/spa-editor-vs-ue.png)

|  | SPA 編輯器 | 通用編輯器 |
|---|---|---|
| **佈景主題** | 應用程式必須使用AEM的格線CSS實作版面。 | 應用程式可使用任何現代CSS技術進行版面。 |
| **演算** | 應用程式必須遵循SPA編輯器的路由結構。 | 應用程式可自由實作，不需遵循任何規則或模式。 |
| **SDK** | 實作必須緊密整合SDK。 | 在作者層級，應用程式僅載入`corlib.js`並透過HTML註解指示通用編輯器。 |
| **架構** | 應用程式必須使用受支援的React或Angular版本。 | 應用程式可使用任何架構或架構。 |
| **主控** | 應用程式必須在AEM網域上託管。 | 應用程式可完全分離並隨處託管。 |
| **API** | 應用程式必須從`model.json` API擷取內容。 | 應用程式可以使用任何API，包括自訂的API。 |
| **持續性** | SPA編輯器僅支援用於視覺化編輯的頁面內容。 | 通用編輯器原生支援對頁面和內容片段進行視覺化編輯。 |
|  |  | 可延伸通用編輯器，以使用相同的視覺功能來編輯外部內容。 |
|  | 開發人員必須在AEM中部署Sling模型和`cq:Dialog`。 | 開發人員幾乎不需要任何AEM體驗，也不需要編寫任何Java。 |
