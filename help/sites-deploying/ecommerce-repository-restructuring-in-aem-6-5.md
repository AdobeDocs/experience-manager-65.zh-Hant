---
title: AEM 6.5中的E-Commerce存放庫重組
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5中適用於E-Commerce的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# AEM 6.5中的E-Commerce存放庫重組{#e-commerce-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM電子商務解決方案的存放庫變更相關的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

## 6.5版升級 {#with-upgrade}

### 產品、訂單、集合、分類、送貨方法和付款方法資料 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>您可以使用 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">緩慢移轉</a> 移轉E-Commerce資料的工作。</p> <p>它會執行下列步驟：</p>
    <ul>
     <li>會調整對舊位置的參照，以指向新位置</li>
     <li>將內容從舊位置移動到新位置</li>
     <li>移除舊位置，以最終啟動整個系統中新位置的使用</li>
    </ul> <p>工作所涵蓋的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>若為大型目錄，Adobe建議您透過將下列Java™系統屬性傳遞至AEM來個別執行商務移轉工作：</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>移轉後，請重新啟動AEM。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>
