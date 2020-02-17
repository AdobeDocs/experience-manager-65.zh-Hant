---
title: 將HTML5表格儲存為草稿
seo-title: 將HTML5表格儲存為草稿
description: 將HTML5表格儲存為草稿，並在稍後階段繼續填寫表格。
seo-description: 將HTML5表格儲存為草稿，並在稍後階段繼續填寫表格。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將HTML5表格儲存為草稿 {#saving-an-html-form-as-a-draft}

您可以將HTML5表格儲存為草稿，然後在稍後階段繼續填寫表格。 Forms Portal可讓任何使用者儲存和還原HTML5表格。 要啟用「另存為草稿」功能，請將以下配置添加到配置檔案節點：

## 「自訂描述檔」允許「另存為草稿」功能 {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms現成可用，提供「另存 **為草稿** 」描述檔。 您可以使用「另存為草稿」描述檔來轉換表單，以啟用HTML5表單的草稿功能。 您可以在 [Forms Manager中指定表單的HTML演算描述檔](/help/forms/using/introduction-managing-forms.md)。

若要為現有的自訂描述檔啟用「另存為草稿」 [功能](/help/forms/using/custom-profile.md)，請新增下列屬性至您的自訂描述檔節點：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字串</td>
   <td>true</td>
   <td><p>啟用另存為繪製特徵</p> <p>的URL。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字串</td>
   <td>true</td>
   <td><p>允許上傳附件</p> <p>和此個人檔案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單 {#drafts-storage-and-listing}

啟用表單的「另存為草稿」功能後；保存表單時，表單會列在「草稿和提 [交」元件中](/help/forms/using/draft-submission-component.md)。 您可以檢索並開始填寫「草稿和提交」元件中保存的表單。

要為「草稿」和「提交」元件啟用表單清單，請向配置檔案節點添加以下屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字串</td>
   <td>true</td>
   <td>若要讓草稿和表格在提交後列在<br /> Forms Portal的「草稿和提交」元件中</td>
  </tr>
 </tbody>
</table>

依預設，AEM Forms會在「發佈」例項的/content/forms/fp節點中，儲存與表單草稿和提交相關聯的使用者資料。 您可以新增自訂儲存提供者，以取得詳細資訊，請參閱「草稿 [和提交的自訂儲存」元件](/help/forms/using/adding-custom-storage-provider-forms.md)。
