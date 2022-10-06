---
title: 在HTML5表單中使用手寫簽名
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5表單在觸控式裝置上日益使用，一項常見需求是支援簽名。 在行動裝置上簽署檔案已成為在行動裝置上簽署表單的公認方式。
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 在HTML5表單中使用手寫簽名{#using-scribble-signature-in-html-forms}

HTML5表單在觸控式裝置上日益使用，一項常見需求是支援簽名。 划線（用手寫筆或手指書寫）正成為在移動設備上簽署表格的一種接受方式。 HTML5表單和Forms Designer現在啟用表單上有手寫簽名欄位的選項。 在瀏覽器中呈現表單時，您可以使用手寫筆、滑鼠或觸控來登入這些欄位。

## 如何使用手寫簽名欄位設計表單 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中開啟表單。
1. 將「簽名手寫」欄位拖放到頁面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >呈現欄位時，會反映在Forms Designer中選取的欄位Dimension。 不過，已呈現的簽名框的尺寸是根據欄位的長寬比計算的，而不是根據Forms Designer中指定的尺寸。

1. 配置簽名手寫欄位。

   依預設，「簽名手寫」欄位會將地理位置資訊標示為iPad上簽署程式期間的必填項目（其他裝置亦可選用）。 此預設行為可透過變更 `geoLocMandatoryOnIpad` 屬性。 此旅館在簽名手寫欄位中提供額外資訊。 修改步驟如下：

   1. 在表單上，選擇簽名手寫欄位。
   1. 選取 **XML源** 標籤。

      >[!NOTE]
      >
      >要開啟「XML源」頁簽，請按一下 **檢視** > **XML源**.

   1. 找出 `<ui>` 標籤 `<field>` 標籤並修改原始碼，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 選取 **設計檢視** 標籤。 在確認方塊上，按一下 **是**.
   1. 儲存表單。

1. 在支援的裝置/案頭瀏覽器上轉譯表單。

## 與手寫簽名進行介面 {#interfacing-with-the-scribble-signatures}

### 正在簽署 {#signing}

將簽名手寫欄位添加到表單並呈現後，按一下或點選該欄位將開啟一個對話框。 用戶可以使用滑鼠、手指或手寫筆，在由點狀矩形指定的繪製區中手寫簽名。

![地理位置](assets/geolocation.png)

**答：** 筆刷 **B.** 橡皮擦 **C.** 地理位置 **D.** 地理位置資訊

### 地理標籤 {#geo-tagging}

在建立手寫文字時按一下地理位置圖示會將地理位置和時間資訊嵌入欄位中。

>[!NOTE]
依預設，在iPad上，必須內嵌地理位置資訊。

在iPad上，預設不會顯示地理位置圖示，當您按一下「 」時，地理位置資訊會自動內嵌 **確定**.

若是iPad，此設定可透過修改 `geoLocManadatoryOnIpad` 參數 `0`，在欄位的init參數中。

* 當地理位置資訊是強制性的時，向用戶呈現縮小的繪製區域。 使用者點按時會新增地理位置文字 **確定** 表徵圖。
* 在其它情況下，向用戶呈現完全可拉延區域。 如果用戶選擇嵌入地理位置資訊，則調整此區域的大小以容納地理位置文本。

### 清除簽名 {#clearing-a-signature}

使用此功能時，使用者可以按一下 **橡皮擦** 圖示來清除欄位，然後重新開始。 如果新增地理位置資訊，也會清除。

### 保存簽名 {#saving-a-signature}

按一下 **確定** 圖示會將手寫體儲存為欄位中的影像。 影像和值可提交至伺服器以供進一步處理。 使用者點按後 **確定**，手寫欄位被鎖定。 無法使用手寫介面工具集再次編輯簽名。

點選或按一下「手寫」欄位會以唯讀模式開啟對話方塊。

![3](assets/3.png)

### 選擇筆大小 {#selecting-pen-size}

按一下 **筆刷** 表徵圖以顯示可用筆大小的清單。 按一下或點選筆大小以使用相應的筆。

### 從表單中刪除簽名 {#delete-signatures-from-the-form}

要從表單中刪除簽名：

* （行動裝置）長按簽名欄位，然後在確認對話方塊上，點選 **是**.
* （案頭）暫留在簽名欄位上，按一下 **取消** 圖示，然後在確認對話方塊上，按一下 **是**.
