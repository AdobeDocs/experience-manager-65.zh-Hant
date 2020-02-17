---
title: 更新發行工具定義
seo-title: 更新發行工具定義
description: 本文詳細說明各種AEM版本，包括完整版本、功能套件和服務套件。
seo-description: 本文詳細說明各種AEM版本，包括完整版本、功能套件和服務套件。
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# AEM Update發行工具定義{#update-release-vehicle-definitions}

本檔案包含Adobe Experience Manager(AEM)各種版本的詳細資訊，包括Adobe提供給其客戶的完整版本、功能套件和服務套件。

>[!Note]
>
>如需AEM更新版本的發行排程，請參閱 [AEM更新版本藍圖](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## 完整版 {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>排程發行</li>
     <li>支援特定版本的升級途徑，這些途徑在版本注意事項中定義</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>主要版本的版本號碼會依公式X+1.Y.Z而增加。 </li>
     <li>次要版本的版本號碼會根據公式X.Y+1.Z而增加</li>
    </ul> <p>其中X是主要版本號，Y是次要版本號，Z是補丁程式號。</p> </td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>
    <ul>
     <li>新功能</li>
     <li>改進</li>
     <li>錯誤修正</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>
    <ul>
     <li>檔案入口網站提供發行說明</li>
     <li>說明檔案入口網站提供功能、改進和錯誤修正的檔案</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>每年</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>以獨立版產品安裝程式形式提供</li>
     <li>可從授權網站和受管理服務授權網站取得</li>
     <li>可能需要內容儲存庫遷移</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>由QA完全驗證</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>排程發行</li>
     <li>目前，無法回滾</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>修補程式版本號是單位數字</li>
     <li>安裝後，將根據公式X.Y.Z.SPx增加已安裝的發行版本號修補程式數</li>
     <li>其中X是主要版本號，Y是次要版本號，Z是補丁程式號。 x是服務包號。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>
    <ul>
     <li>新功能</li>
     <li>改進</li>
     <li>錯誤修正</li>
     <li>Common Interest功能套件（如果有）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>
    <ul>
     <li>說明檔案入口網站上的發行說明</li>
     <li>說明檔案入口網站功能、改進和錯誤修正的檔案</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>每季</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>以套件形式傳送</li>
     <li>在包共用中提供</li>
     <li>需要現有的功能安裝</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>
    <ul>
     <li>已驗證所有修正QA</li>
     <li>使用自動執行功能，讓整個套件的健全運作</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 累積修補程式套件 {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>釋放修正的單一傳送模型</li>
     <li>包含個別元件之內容封裝的匯整器內容封裝</li>
     <li>CFP是Hotfix的轉換功能，但並未提供任何改進。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>其中X是主要版本號，Y是次要版本號，Z是補丁程式號。 x是累積的Service Pack編號。</p> </td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td><p>CFP是包含所有元件在指定日期之前修正的累積修補程式套件。 例如，如果客戶套用CFP3，則CFP3 = CFP1 + CFP2。</p> </td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>說明檔案入口網站上的發行說明</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Quaterly</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>以套件形式傳送</li>
     <li>在包共用中提供</li>
     <li>取決於最新發佈的Service Pack</li>
     <li>CFP是自行決定的。 客戶無需擔心尋找／解決相依性。 CFP應安裝在最新發行的Service Pack。</li>
     <li>CFP可以安裝為單一套件，以改善客戶體驗。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>QA已在整合層級和回歸測試中驗證</td>
  </tr>
 </tbody>
</table>

## Oak Cumulative Fix Pack {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>類似標準CFP，但僅包含Oak相關修正</li>
     <li>COFP是自相關的（無相依性）。 客戶無需擔心尋找／解決相依性。 [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>oak &lt;version&gt;</td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>COFP是包含特定1.x版本所有Oak元件的累積修補程式套件。 例如，如果客戶套用COHF 1.x.3，則COHF 1.x.3。 = COHF 1.x.1 + COHF 1.x.2。</td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td><p>視需要</p> </td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>COFP安裝程式已簡化，以改善客戶體驗。 （客戶只需為所有元件安裝單一套件即可）。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td><p>QA已驗證</p> </td>
  </tr>
 </tbody>
</table>

## 修補程式 {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td><p>包含為解決產品缺陷而建立的一個或多個檔案的軟體包，該產品缺陷嚴重降低了基本服務或顯著影響了業務運營。 </p> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;Release Version&gt;-hotfix-&lt;Hotfix ID&gt;-&lt;Hotfix版本&gt;</td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>包含特定問題的修正</td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>公開Hotfix的發行說明僅能根據客戶透過AEM支援入口網站的要求提供。</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>視需要</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>以套件形式傳送</li>
     <li>在包共用中提供</li>
     <li>取決於最新發佈的Service Pack</li>
     <li>除非已指定，否則大部分的Hotfix都是獨立的。 可以按任何順序安裝。 可通過「從屬關係」元素的「包共用詳細資訊」頁籤進行驗證。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>
    <ul>
     <li>經客戶服務驗證</li>
     <li>AEM Hotfix無法享有與服務套件或產品發行相同等級的品質保證。 因此，應首先在測試環境上驗證它們，作為質量部署流程的一部分。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 覆蓋 {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>overlay-&lt;票證ID&gt;</td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>JS或JSP檔案的錯誤修正</td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>無</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>視需要</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>由AEM客戶服務以套件形式提供</li>
     <li>Service pack或完整版不一定包含在內</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>經客戶服務驗證</td>
  </tr>
 </tbody>
</table>

## 功能套件 {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>功能包是附加功能，並通過Service Pack提供。 如果AEM版本已發行其最後一個Service Pack,Adobe將來不會針對它提供任何功能套件。</li>
     <li>FP包含產品增強功能，已排定在後續產品發行時推出，但會根據Adobe產品管理部門的決定提前提供。</li>
     <li>功能一律會與下一個主要版本合併，然後備份至客戶所需的AEM版本</li>
     <li>Common Interest和GA功能包合併到下一個Service Pack中</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;發行版本&gt;-featurepack-&lt;featurepack ID&gt;-&lt;featurepack版本&gt;</td>
  </tr>
  <tr>
   <td><strong>包含項目</strong></td>
   <td>
    <ul>
     <li>新功能</li>
     <li>改進</li>
     <li>錯誤修正（增量產品更新）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文件</strong></td>
   <td>說明檔案可在helpx.adobe.com上取得。</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>視產品區域而定</td>
  </tr>
  <tr>
   <td><strong>可用性和安裝</strong></td>
   <td>
    <ul>
     <li>通過Service pack提供</li>
     <li>可在Package Share上使用。 客戶透過Package Share接受Adobe的條款與條件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>測試等級</strong></td>
   <td>「一般可用性」功能包經過QA驗證</td>
  </tr>
 </tbody>
</table>

* [1]:OAK修正不會以個別Hotfix的形式提供。 不過，這些修補程式會包含在後續的Cumulative Oak Hotfix中。 如有必要，可以在最新COFP之上提供診斷版本。 前提是客戶擁有最新的COFP運行。 診斷構建版本僅提供與Hot Fix相同的級別品質保證。 因此，它們無法提供與累積修補程式套件、服務套件或產品發行相同等級的品質保證。 最終修正方案將隨下一個CFP提供。

