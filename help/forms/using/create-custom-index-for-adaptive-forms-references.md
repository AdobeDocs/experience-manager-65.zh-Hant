---
title: 建立最適化表單參考的自訂索引
description: 瞭解如何在AEM Forms中為最適化表單參考查詢建立標籤Lucene索引，以避免在發佈體驗片段時周遊查詢。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# 建立最適化表單參考的自訂索引 {#create-custom-index-for-adaptive-forms-references}

建立標籤Lucene索引以避免在Adobe Experience Manager (AEM) Forms解析最適化表單參考時周遊查詢。 如果沒有適當的索引，發佈包含最適化表單參考的體驗片段可能會在記錄檔中產生`Traversal query (query without index)`警告。

在AEM Forms 6.5.24.0和更新版本中，參考查詢使用`aemformsAFReferences`索引標籤。 這些發行版本包含查詢變更，但您必須使用該標籤建立自訂索引。 本文說明如何定義及部署索引。

若為AEM Forms 6.5 LTS，請參閱[在AEM Forms 6.5 LTS中為最適化表單參考建立自訂索引](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references)。

## 先決條件 {#prerequisites}

在開始之前，請確定您已：

* AEM Forms 6.5.24.0或更新版本，已安裝對應的Forms附加元件。
* 存取權以在作者執行個體上的`/oak:index`下建立索引。
* 如果您透過內容套件部署索引，或存取開發替代方案的CRXDE Lite，則為具有`ui.apps`模組的AEM專案。

在將索引部署到生產環境之前，請先在開發或中繼環境中測試索引。 [在大型存放庫上建立索引可能需要一些時間](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes)。

## 定義自訂索引 {#define-the-custom-index}

在`/oak:index/customAFReferenceLuceneIndex-1`處建立索引。 您可以選擇不同的索引節點名稱，但保留`aemformsAFReferences`標籤不變，以便Forms參考查詢可以選取索引。

使用下列定義。 它在`/content`下的`nt:unstructured`節點上索引`sling:resourceType`。

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

不要新增`analyzed=true`。 參考查詢使用屬性限制而非全文`contains`條件，因此不需要設定。

## 使用內容封裝部署索引 {#deploy-the-index-with-a-content-package}

使用內容套件進行生產部署。

1. 在您的AEM專案的`ui.apps`模組中，建立`ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`。
1. 在該目錄中建立`.content.xml`，其定義如下：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. 在`ui.apps/src/main/content/META-INF/vault/filter.xml`中的現有`workspaceFilter`元素中新增下列篩選器。 保留專案的其他篩選器不變。

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. 使用現有的建置設定建置專案，並在製作執行個體上安裝產生的內容套件。 如需封裝上載和安裝指示，請參閱[封裝管理員](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)。
1. 確認`/oak:index/customAFReferenceLuceneIndex-1`存在。 在檢查查詢計畫之前，允許完成非同步索引。

如果您選擇不同的索引名稱，請在目錄、篩選器和存放庫路徑中一致地使用該名稱。

## 使用CRXDE Lite建立索引 {#create-the-index-with-crxde-lite}

在開發環境中使用此替代方案，而非內容封裝方法。

建立索引節點時，請使用下列屬性：

| 屬性 | 類型 | 值 |
| --- | --- | --- |
| `selectionPolicy` | 字串 | `tag` |
| `compatVersion` | 長 | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | 字串 | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | 布林值 | `true` |
| `reindex` | 布林值 | `false` |

`String[]`表示多值String屬性，即使它只包含一個值。

1. 開啟 `http://localhost:4502/crx/de/index.jsp`。 將主機和連線埠取代為您的製作執行個體的主機和連線埠。
1. 導覽至 `/oak:index`。 以滑鼠右鍵按一下節點，然後選取[!UICONTROL 建立] > [!UICONTROL 建立節點]。
1. 使用型別`oak:QueryIndexDefinition`建立`customAFReferenceLuceneIndex-1`。
1. 將上表的屬性新增至索引節點。
1. 在索引節點下，建立下列子節點階層。 將每個子節點的型別設定為`nt:unstructured`：

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. 在`resourceType`上，新增值為`sling:resourceType`的`name` （字串）和值為`true`的`propertyIndex` （布林值）。
1. 選取[!UICONTROL 全部儲存]並允許非同步索引完成。

## 驗證查詢是否使用索引 {#verify-that-the-query-uses-the-index}

檢查查詢計畫，確認參考查詢會選取您的自訂索引。

1. 確認非同步索引已完成。 使用[索引管理員](/help/sites-administering/operations-dashboard.md#the-index-manager)來檢查索引狀態。
1. 開啟[!UICONTROL 工具] > [!UICONTROL 作業] > [!UICONTROL 診斷] > [!UICONTROL 查詢效能]並選取[!UICONTROL 說明查詢]。 選取XPath查詢語言並輸入：

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. 選取[!UICONTROL 說明]。 確認計畫使用`lucene:customAFReferenceLuceneIndex-1`和`/oak:index/customAFReferenceLuceneIndex-1`或您選擇的索引名稱來查詢的分支，而不是周遊計畫。 如需詳細資訊，請參閱[說明查詢](/help/sites-administering/operations-dashboard.md#explain-query)。
1. 重複產生警告的體驗片段發佈操作。 檢查`error.log`是否有來自`com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`的新周遊警告。

如果計畫未選取自訂索引，請對照上述範例檢查標籤、`indexRules`階層及`sling:resourceType`屬性定義。 如需進一步的診斷，請參閱[疑難排解Oak索引](/help/sites-deploying/troubleshooting-oak-indexes.md)。

## 相關任務 {#related-tasks}

如需查詢效能和索引設定的詳細資訊，請參閱：

* [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)
* [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [疑難排解緩慢查詢](/help/sites-developing/troubleshooting-slow-queries.md)
