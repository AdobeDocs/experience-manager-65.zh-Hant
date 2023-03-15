---
title: 通信管理配置屬性
seo-title: Correspondence Management Configuration Properties
description: 本主題說明如何使用解決方案專屬設定修改資產撰寫器。 本主題詳細說明您可編輯的屬性，以及其說明、預設值和可接受的值。
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---

# 通信管理配置屬性 {#correspondence-management-configuration-properties}

若要設定這些屬性，請在瀏覽器中開啟下列URL: `https://<server>:<port>/<contextPath>/system/console/configMgr` 選取 **通信管理配置**.

通信管理具有以下配置屬性：

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
   <td>數字最小寬度</td>
   <td>使用羅馬數字以外的編號清單時，要在項目符號/數字欄位上應用的最小寬度</td>
   <td>8.0mm</td>
   <td>任何數字</td>
  </tr>
  <tr>
   <td><p>羅馬數字最小寬度</p> </td>
   <td><p>使用羅馬數字時，要在項目符號/數字欄位上應用的最小寬度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td>轉譯類型</td>
   <td>「建立通信」應用程式用於呈現信函預覽的格式副本類型。 </td>
   <td>HTML轉譯</td>
   <td>HTML轉譯/PDF轉譯</td>
  </tr>
  <tr>
   <td><p>啟用CCRPDF突出顯示</p> </td>
   <td><p>在建立通信應用程式中啟用對PDF的突出顯示</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>目標突出顯示類型</p> </td>
   <td><p>建立通信應用程式中的目標突出顯示類型</p> </td>
   <td><p>邊框</p> </td>
   <td><p>邊框/填寫/無</p> </td>
  </tr>
  <tr>
   <td><p>目標醒目提示顏色</p> </td>
   <td><p>建立通信應用程式中的目標突出顯示顏色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>內容醒目提示類型</p> </td>
   <td><p>建立通信應用程式中的內容突出顯示類型</p> </td>
   <td><p>填充</p> </td>
   <td><p>邊框/填寫/無</p> </td>
  </tr>
  <tr>
   <td><p>內容醒目提示顏色</p> </td>
   <td><p>建立通信應用程式中的內容突出顯示顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>欄位突出顯示類型</p> </td>
   <td><p>建立通信應用程式中的欄位突出顯示類型</p> </td>
   <td><p>填充</p> </td>
   <td><p>邊框/填寫/無</p> </td>
  </tr>
  <tr>
   <td><p>欄位突出顯示顏色</p> </td>
   <td><p>建立通信應用程式中的欄位突出顯示顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>應用程式超時</p> </td>
   <td><p>應用程式超時（秒）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td><p>PDF文檔參數名</p> </td>
   <td><p>後處理中PDF文檔的參數名</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XML資料參數名稱</p> </td>
   <td><p>後處理中XML文檔（資料）的參數名</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XDP檔案參數名稱</p> </td>
   <td><p>發送至後置進程的XDP文檔的參數名</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>重新導向URL參數名稱</p> </td>
   <td><p>從後續程式傳送之重新導向URL的參數名稱此值可以是任何字串變數名稱</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交類型</p> </td>
   <td><p>PDF提交類型(從「建立通信」應用程式提交時生成的PDF類型)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>互動/非互動</p> </td>
  </tr>
  <tr>
   <td><p>最佳化資料字典例項</p> </td>
   <td><p>支援優化資料字典實例b/w伺服器和客戶端的傳輸</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>自動更正不一致 </p> </td>
   <td><p>啟用後，將自動處理信函分配中可能的不一致</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>使用配置的資料格式</p> </td>
   <td><p>控制是否使用配置的資料編輯格式和資料顯示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料顯示格式</p> </td>
   <td><p>指定資料的區域設定特定顯示格式</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=truelocale=de_DE;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator=.;numberUseGroupSeparator=truelocale=fr_FR;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator= ;numberUseGroupSeparator=truelocale=ja_JP;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>資料編輯格式</p> </td>
   <td><p>編輯資料的格式。 將資料寫入為字串或從字串分析資料時，會使用此方法</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>在發佈時管理信函例項</p> </td>
   <td><p>啟用/停用「管理信函」功能（僅適用於發佈伺服器）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用審核</p> </td>
   <td><p>啟用/停用稽核功能。 若為false，則會停用所有動作的稽核記錄</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用讀取審核</p> </td>
   <td><p>啟用/停用資產讀取的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用建立審核</p> </td>
   <td><p>啟用/停用資產建立的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用更新審核</p> </td>
   <td><p>啟用/停用資產更新的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用還原審核</p> </td>
   <td><p>啟用/停用資產還原的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用發佈稽核</p> </td>
   <td><p>啟用/停用資產發佈的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用「另存為草稿」審核</p> </td>
   <td><p>啟用/停用用於儲存信函草稿的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用提交審核</p> </td>
   <td><p>啟用/停用信函提交的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用電子郵件稽核</p> </td>
   <td><p>啟用/停用以電子郵件傳送信函的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用打印審核</p> </td>
   <td><p>啟用/禁用打印信函的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用自訂傳送稽核</p> </td>
   <td><p>啟用/停用自訂信函傳送的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>附件文檔參數名稱</p> </td>
   <td><p>發送至後續流程的附件文檔的參數名稱</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>CM用戶根</p> </td>
   <td><p>包含所有通信管理用戶資產的資料夾的URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的資料夾位置</p> </td>
  </tr>
  <tr>
   <td><p>字母快取大小</p> </td>
   <td><p>指定要保留在快取中的字母數上限。</p> <p>若變更此值，將會導致 <code>in-memory</code> 快取。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何數值</p> </td>
  </tr>
  <tr>
   <td><p>啟用信函快取</p> </td>
   <td><p>啟用/停用信函快取。</p> <p>若變更此值，將會導致 <code>in-memory </code> 快取。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料元素排序</p> </td>
   <td><p>按照信函中的順序，在建立通信介面中保留資料元素的順序</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>支援重新載入</p> </td>
   <td><p>啟用/停用伺服器端轉譯之信函中的重新載入支援。</p> <p>停用此功能將改善信函轉譯效能。</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>臨時資料夾</td>
   <td>臨時資料夾的位置。</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>遠程保存</td>
   <td>將信函例項儲存在指定的處理製作上。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>相容性選項</td>
   <td>格式configname:configvalue的相容性選項（以逗號分隔）。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>調試目錄 </p> <p> </p> </td>
   <td>用於調試的檔案系統資料夾位置。 如果目錄不是 <code>exists</code>，則不會產生除錯轉儲。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
