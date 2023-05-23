---
title: 通信管理配置屬性
seo-title: Correspondence Management Configuration Properties
description: 本主題說明如何使用特定於解決方案的配置修改Asset Composer。 本主題詳細介紹了可編輯的屬性及其說明、預設值和可接受值。
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

要配置這些屬性，請在瀏覽器中開啟以下URL: `https://<server>:<port>/<contextPath>/system/console/configMgr` 選擇 **通信管理配置**。

Tergement Management具有以下配置屬性：

<table>
 <tbody>
  <tr>
   <th><p><strong>屬性</strong></p> </th>
   <th><p><strong>說明</strong></p> </th>
   <th><p><strong>預設</strong></p> </th>
   <th><p><strong>可接受值</strong></p> </th>
  </tr>
  <tr>
   <td><p>縮排</p> </td>
   <td>模組上的縮進<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意數字</p> </td>
  </tr>
  <tr>
   <td>最小寬度</td>
   <td>使用除羅馬字型大小外的編號清單時，要應用於項目符號/編號欄位的最小寬度</td>
   <td>8.0mm</td>
   <td>任意數字</td>
  </tr>
  <tr>
   <td><p>羅馬數字最小寬度</p> </td>
   <td><p>使用羅馬數字時要應用於項目符號/數字欄位的最小寬度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意數字</p> </td>
  </tr>
  <tr>
   <td>格式副本類型</td>
   <td>「建立對應」應用程式用於呈現字母預覽的格式副本類型。 </td>
   <td>HTML格式副本</td>
   <td>HTML格式副本/PDF格式副本</td>
  </tr>
  <tr>
   <td><p>啟用CCRPDF突出顯示</p> </td>
   <td><p>在「建立對應」應用程式中啟用PDF加亮</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>目標突出顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的目標突出顯示類型</p> </td>
   <td><p>邊界</p> </td>
   <td><p>邊框/填充/無</p> </td>
  </tr>
  <tr>
   <td><p>目標突出顯示顏色</p> </td>
   <td><p>「建立對應」應用程式中的目標高亮顏色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>內容突出顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的內容突出顯示類型</p> </td>
   <td><p>填充</p> </td>
   <td><p>邊框/填充/無</p> </td>
  </tr>
  <tr>
   <td><p>內容突出顯示顏色</p> </td>
   <td><p>「建立對應」應用程式中的內容突出顯示顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>欄位突出顯示類型</p> </td>
   <td><p>「建立對應」應用程式中的欄位突出顯示類型</p> </td>
   <td><p>填充</p> </td>
   <td><p>邊框/填充/無</p> </td>
  </tr>
  <tr>
   <td><p>欄位高亮顏色</p> </td>
   <td><p>「建立對應」應用程式中的欄位高亮顏色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式為R;G;B的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>應用程式超時</p> </td>
   <td><p>應用程式超時（秒）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意數字</p> </td>
  </tr>
  <tr>
   <td><p>PDF文檔參數名稱</p> </td>
   <td><p>後處理中PDF文檔的參數名稱</p> </td>
   <td><p>在PDFoc中</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XML資料參數名稱</p> </td>
   <td><p>後處理中XML文檔（資料）的參數名稱</p> </td>
   <td><p>在XMLDoc中</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XDP文檔參數名稱</p> </td>
   <td><p>發送到後處理的XDP文檔的參數名稱</p> </td>
   <td><p>在XDPDoc中</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>重定向URL參數名稱</p> </td>
   <td><p>從後續進程發送的重定向URL的參數名稱此值可以是任何字串變數名稱</p> </td>
   <td><p>重定向URL</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交類型</p> </td>
   <td><p>PDF提交類型(在從「建立對應」應用產品提交時生成的PDF類型)</p> </td>
   <td><p>非交互</p> </td>
   <td><p>交互/非交互</p> </td>
  </tr>
  <tr>
   <td><p>優化資料字典實例</p> </td>
   <td><p>支援優化資料字典實例b/w伺服器和客戶端的傳輸</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>自動更正不一致 </p> </td>
   <td><p>啟用後，它將自動處理字母分配中可能的不一致</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>使用已配置的資料格式</p> </td>
   <td><p>控制是否使用配置的資料編輯格式和資料顯示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>資料顯示格式</p> </td>
   <td><p>指定資料的區域設定特定顯示格式</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=truelocale=de_DE;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator=。;numberUseGroupSeparator=truelocale=fr_FR;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator= ;numberUseGroupSeparator=truelocale=ja_JP;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>資料編輯格式</p> </td>
   <td><p>編輯資料格式。 當將資料寫入字串或從字串分析資料時使用</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>在發佈時管理信函實例</p> </td>
   <td><p>啟用/禁用管理信函功能（僅適用於發佈伺服器）</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用審核</p> </td>
   <td><p>啟用/禁用審核功能。 如果為false，則禁用所有操作的審核日誌</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用讀審核</p> </td>
   <td><p>啟用/禁用資產讀取的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用建立審核</p> </td>
   <td><p>啟用/禁用資產建立的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用更新審核</p> </td>
   <td><p>啟用/禁用資產更新的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用還原審核</p> </td>
   <td><p>啟用/禁用資產還原的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用發佈審核</p> </td>
   <td><p>啟用/禁用資產發佈的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用「另存為草稿審核」</p> </td>
   <td><p>啟用/禁用用於保存信函草稿的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用提交審核</p> </td>
   <td><p>啟用/禁用信函提交的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用電子郵件審核</p> </td>
   <td><p>啟用/禁用電子郵件信函的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用打印審核</p> </td>
   <td><p>啟用/禁用打印信函的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>啟用自定義交貨審核</p> </td>
   <td><p>啟用/禁用信函自定義傳遞的審核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>附件文檔參數名稱</p> </td>
   <td><p>發送到後處理的附件文檔的參數名稱</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>CM用戶根</p> </td>
   <td><p>包含所有Tergement Management用戶資產的資料夾的URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的資料夾位置</p> </td>
  </tr>
  <tr>
   <td><p>字母快取大小</p> </td>
   <td><p>指定要保留在快取中的字母的最大數。</p> <p>更改此值將導致清除 <code>in-memory</code> 快取。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何數值</p> </td>
  </tr>
  <tr>
   <td><p>啟用字母快取</p> </td>
   <td><p>啟用/禁用字母快取。</p> <p>更改此值將導致清除 <code>in-memory </code> 快取。</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>資料元素排序</p> </td>
   <td><p>按字母中的順序在建立對應介面時保留資料元素排序</p> </td>
   <td><p>true</p> </td>
   <td><p>真/假</p> </td>
  </tr>
  <tr>
   <td><p>支援重新載入</p> </td>
   <td><p>啟用/禁用在伺服器端呈現的字母中的重新載入支援。</p> <p>禁用此功能將提高字母呈現效能。</p> </td>
   <td><p>false</p> </td>
   <td><p>真/假</p> <p> </p> </td>
  </tr>
  <tr>
   <td>臨時資料夾</td>
   <td>臨時資料夾的位置。</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>遠程保存</td>
   <td>將字母實例保存到指定的處理作者。</td>
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
   <td>用於調試的檔案系統資料夾位置。 如果目錄不 <code>exists</code>，將不生成調試轉儲。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
