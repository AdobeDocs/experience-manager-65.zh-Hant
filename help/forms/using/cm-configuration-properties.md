---
title: 對應管理配置屬性
seo-title: 對應管理配置屬性
description: 本主題說明如何使用解決方案特定的組態來修改Asset Composer。 本主題詳細說明您可以編輯的屬性，包括其說明、預設值和可接受值。
seo-description: 本主題說明如何使用解決方案特定的組態來修改Asset Composer。 本主題詳細說明您可以編輯的屬性，包括其說明、預設值和可接受值。
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 對應管理配置屬性 {#correspondence-management-configuration-properties}

若要設定這些屬性，請在瀏覽器中開啟下列URL:並選 `https://<server>:<port>/<contextPath>/system/console/configMgr` 擇「對 **應管理配置」**。

Correponsence Management具有以下配置屬性：

<table>
 <tbody>
  <tr>
   <th><p><strong>屬性</strong></p> </th>
   <th><p><strong>說明</strong></p> </th>
   <th><p><strong>預設</strong></p> </th>
   <th><p><strong>可接受的值</strong></p> </th>
  </tr>
  <tr>
   <td><p>縮排</p> </td>
   <td>模組上的縮進<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td>最小寬度數</td>
   <td>使用羅馬數字以外的編號清單時，項目符號／數字欄位應用的最小寬度</td>
   <td>8.0mm</td>
   <td>任何數字</td>
  </tr>
  <tr>
   <td><p>羅馬數字最小寬度</p> </td>
   <td><p>使用羅馬數字時，項目符號／數字欄位應用的最小寬度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td>轉譯類型</td>
   <td>「建立對應」應用程式用於渲染字母預覽的格式副本類型。 </td>
   <td>HTML轉譯</td>
   <td>HTML轉譯/PDF轉譯</td>
  </tr>
  <tr>
   <td><p>啟用CCR PDF反白顯示</p> </td>
   <td><p>在「建立對應」應用程式中啟用PDF反白顯示功能</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>目標反白顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的「目標反白顯示類型」</p> </td>
   <td><p>邊界</p> </td>
   <td><p>邊框／填充／無</p> </td>
  </tr>
  <tr>
   <td><p>目標反白顯示顏色</p> </td>
   <td><p>「建立對應」應用程式中的「目標反白顯示顏色」</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>內容反白顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的內容反白顯示類型</p> </td>
   <td><p>填滿</p> </td>
   <td><p>邊框／填充／無</p> </td>
  </tr>
  <tr>
   <td><p>內容反白顯示顏色</p> </td>
   <td><p>「建立對應」應用程式中的內容反白顯示顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>欄位反白顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的欄位突出顯示類型</p> </td>
   <td><p>填滿</p> </td>
   <td><p>邊框／填充／無</p> </td>
  </tr>
  <tr>
   <td><p>欄位反白顯示顏色</p> </td>
   <td><p>「建立對應」應用程式中的欄位突出顯示顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>應用程式超時</p> </td>
   <td><p>應用程式逾時幾秒鐘</p> </td>
   <td><p>1200</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td><p>PDF檔案參數名稱</p> </td>
   <td><p>後置處理中PDF檔案的參數名稱</p> </td>
   <td><p>inPDFoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XML資料參數名稱</p> </td>
   <td><p>後處理中XML文檔（資料）的參數名稱</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XDP檔案參數名稱</p> </td>
   <td><p>傳送至後置程式的XDP檔案的參數名稱</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>重新導向URL參數名稱</p> </td>
   <td><p>從後置程式傳送的重新導向URL的參數名稱此值可以是任何字串變數名稱</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交類型</p> </td>
   <td><p>PDF提交類型（從「建立通信」應用程式提交時產生的PDF類型）</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>互動／非互動</p> </td>
  </tr>
  <tr>
   <td><p>最佳化資料字典例項</p> </td>
   <td><p>實現資料字典實例b/w伺服器和客戶端的優化傳輸</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>自動更正不一致 </p> </td>
   <td><p>啟用後，會自動處理字母分配中可能的不一致</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>使用已配置的資料格式</p> </td>
   <td><p>控制是否使用已配置的資料編輯格式和資料顯示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料顯示格式</p> </td>
   <td><p>指定資料的地區設定特定顯示格式</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=truelocale=de_DE;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator=。;numberUseGroupSeparator=truelocale=fr_FR;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator= ;numberUseGroupSeparator=truelocale=ja_JP;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>資料編輯格式</p> </td>
   <td><p>編輯資料格式。 將資料寫入為字串或從字串剖析資料時，會使用此功能</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>在發佈時管理字母例項</p> </td>
   <td><p>啟用／停用「管理信件」功能（僅適用於Publish Server）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用審核</p> </td>
   <td><p>啟用／停用審核功能。 若為false，則會停用所有動作的稽核記錄</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用讀審計</p> </td>
   <td><p>啟用／停用資產讀取的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用建立審核</p> </td>
   <td><p>啟用／停用資產建立的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用更新審核</p> </td>
   <td><p>啟用／停用資產更新的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用還原審核</p> </td>
   <td><p>啟用／停用資產回復的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用發佈審核</p> </td>
   <td><p>啟用／停用資產發佈的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用「另存新檔」「草稿審核」</p> </td>
   <td><p>啟用／停用儲存信件草稿的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用提交審核</p> </td>
   <td><p>啟用／停用信函送出的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用電子郵件審核</p> </td>
   <td><p>啟用／停用以電子郵件寄送信件的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用打印審核</p> </td>
   <td><p>啟用／停用列印信函的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用自訂傳送稽核</p> </td>
   <td><p>啟用／停用自訂信件傳送的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>附件文檔參數名稱</p> </td>
   <td><p>發送至後置流程的附件文檔的參數名稱</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>CM用戶根</p> </td>
   <td><p>包含所有Correponsement Management用戶資產的資料夾的URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的資料夾位置</p> </td>
  </tr>
  <tr>
   <td><p>字母快取大小</p> </td>
   <td><p>指定要保存在快取中的字母數上限。</p> <p>更改此值將導致清除快取 <code>in-memory</code> 。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何數值</p> </td>
  </tr>
  <tr>
   <td><p>啟用字母快取</p> </td>
   <td><p>啟用／停用字母快取。</p> <p>更改此值將導致清除快取 <code>in-memory </code> 。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料元素順序</p> </td>
   <td><p>在建立對應介面時，依照Letter中的順序來排列資料元素順序</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>支援重新載入</p> </td>
   <td><p>啟用／停用在伺服器端轉譯的字母中重新載入支援。</p> <p>停用此功能將改善字母轉換效能。</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>臨時資料夾</td>
   <td>臨時資料夾的位置。</td>
   <td>acm.tpm資料夾</td>
   <td> </td>
  </tr>
  <tr>
   <td>遠程保存</td>
   <td>將字母例項儲存在指定的處理作者上。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>相容性選項</td>
   <td>格式configname:configvalue的相容性選項，用逗號分隔。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>調試目錄 </p> <p> </p> </td>
   <td>用於調試的檔案系統資料夾位置。 如果目錄未執行， <code>exists</code>則不會產生任何除錯轉儲。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
