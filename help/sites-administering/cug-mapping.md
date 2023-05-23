---
title: 6.5中的自定義AEM用戶組映射
seo-title: Custom User Group Mapping in AEM 6.5
description: 瞭解自定義用戶組映射在中的工AEM作方式。
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 6.5中的自定義AEM用戶組映射 {#custom-user-group-mapping-in-aem}

## 與CUG（自定義用戶組）相關的JCR內容比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>舊版AEM本</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><p>屬性：cq:cug已啟用</p> <p>聲明節點類型：不適用，剩餘屬性</p> </td>
   <td><p>授權:</p> <p>節點：rep:cug節點類型rep:CugPolicy的策略</p> <p>聲明節點類型：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 驗證:</p> <p>混合類型：花崗岩：驗證必需</p> </td>
   <td><p>為了限制讀訪問，專用CUG策略應用於目標節點。</p> <p>注：策略只能應用於已配置的支援路徑。</p> <p>名為rep:cugPolicy和類型rep:CugPolicy的節點受保護，無法使用常規JCR API調用編寫；改用JCR訪問控制管理。</p> <p>請參閱 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">此頁</a> 的子菜單。</p> <p>要強制對節點執行身份驗證要求，只需添加混合類型花崗岩：AuthenticationRequired。</p> <p>注：僅在配置的支援路徑下受尊重。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cug主體</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：rep:principalNames</p> <p>聲明節點類型：rep:CugPolicy</p> </td>
   <td><p>包含允許讀取受限CUG下內容的主體名稱的屬性受保護，不能使用常規JCR API調用編寫；改用JCR訪問控制管理。</p> <p>請參閱 <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">此頁</a> 的上界。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugLoginPage</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：花崗岩：loginPath（可選）</p> <p>聲明節點類型：花崗岩：驗證必需</p> </td>
   <td><p>定義了混合類型花崗岩：AuthenticationRequired的JCR節點可以選擇定義替代登錄路徑。</p> <p>注：僅在配置的支援路徑下受尊重。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cug領域</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td>不適用</td>
   <td>不再支援新實施。</td>
  </tr>
 </tbody>
</table>

## OSGi服務比較 {#comparison-of-osgi-services}

**舊版AEM本**

標籤：Adobe花崗岩封閉用戶組(CUG)支援

名稱：com.day.cq.auth.impl.Cug支援實施

**AEM 6.5**

* 標籤：Apache Jackrabbit Oak CUG配置

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy =必需

* 標籤：Apache Jackrabbit Oak CUG排除清單

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy =必需

* 名稱：com.adobe.granite.auth.requirement.impl.RequirementService
* 標籤：Adobe花崗岩認證要求和登錄路徑處理程式

   名稱：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy =必需

**評論**

* 配置CUG授權並啟用/禁用評估。
配置不應受CUG授權影響的主體的排除清單的服務。

   >[!NOTE]
   > 
   >如果 `CugExcludeImpl` 未配置， `CugConfiguration` 退回到預設值。

   如果有特殊需要，可以插入自定義CugExclude實現。

* OSGi元件實現LoginPathProvider，該元件向LoginSelectorHandler顯示匹配的登錄路徑。 它具有對RequirementHandler的強制引用，該RequirementHandler用於註冊觀察器，該觀察器通過花崗岩：AuthenticationRequired混合類型偵聽儲存在內容中的更改的身份驗證要求。
* 實現RequirementHandler的OSGi元件，用於通知SlingAuthenticator對身份驗證要求的更改。

   由於此元件的配置策略為REQUIRE，因此只有在指定了一組受支援的路徑時才激活它。

   啟用服務將啟動RequirementService。

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
