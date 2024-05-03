---
title: 在HTML5表單中使用手寫簽名
description: HTML5表單越來越多地用於觸控裝置，常見的要求之一就是支援簽名。 在行動裝置上簽署檔案已成為在行動裝置上簽署表單的普遍方式。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 在HTML5表單中使用手寫簽名{#using-scribble-signature-in-html-forms}

HTML5表單越來越多地用於觸控裝置，常見的要求之一就是支援簽名。 在行動裝置上簽署表單時，塗寫（使用手寫筆或手指書寫）已成為一種可接受的方式。 HTML5 forms和Forms Designer現在可啟用在表單上有手寫簽名欄位的選項。 當表單在瀏覽器中呈現時，人們可以使用手寫筆、滑鼠或觸控來登入這些欄位。

## 如何使用手寫簽名欄位設計表單 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中開啟表單。
1. 將「簽名草稿」欄位拖放到頁面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >呈現欄位時，會反映在Forms Designer中選取欄位的Dimension。 不過，已演算簽名方塊的維度是根據欄位的外觀比例計算，而非根據Forms Designer中指定的維度。

1. 設定「簽名草寫」欄位。

   依預設，「簽名草稿」欄位會在iPad上的簽署程式期間，將地理位置資訊標示為必要（其他裝置則為選用）。 此預設行為可透過變更 `geoLocMandatoryOnIpad` 屬性。 此屬性在「簽名草寫欄位」中顯示為額外專案。 修改它的步驟如下：

   1. 在表單上，選取簽名草寫欄位。
   1. 選取 **XML來源** 標籤。

      >[!NOTE]
      >
      >若要開啟「XML來源」標籤，請按一下 **檢視** > **XML來源**.

   1. 找到 `<ui>` 標籤中的變數 `<field>` 標籤並修改原始程式碼，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 選取 **設計檢視** 標籤。 在確認方塊中，按一下 **是**.
   1. 儲存表單。

1. 在支援的裝置/案頭瀏覽器上轉譯表單。

## 與手寫簽名連線 {#interfacing-with-the-scribble-signatures}

### 簽署 {#signing}

在將簽名草寫欄位新增至表單並呈現後，按一下或點選該欄位會開啟一個對話方塊。 使用者可以使用滑鼠、手指或手寫筆，在虛線矩形所指定的繪製區域中塗寫簽名。

![地理位置](assets/geolocation.png)

**答：** 筆刷 **B.** 橡皮擦 **C.** 地理位置 **D.** 地理位置資訊

### 地理標籤 {#geo-tagging}

建立塗鴉時按一下地理位置圖示，會將地理位置和時間資訊內嵌到欄位中。

>[!NOTE]
>
在iPad上，預設會強制內嵌地理位置資訊。

在iPad上，地理位置圖示預設不會顯示，而且當您按一下時，地理位置資訊會自動內嵌 **確定**.

若是iPad，您可以修改 `geoLocManadatoryOnIpad` 引數至 `0`，此欄位為初始引數。

* 當地理位置資訊是強制性的時，使用者會看到一個縮小的繪製區域。 使用者按一下時新增地理位置文字 **確定** 圖示加以標示。
* 在其他情況下，使用者會看到一個完整可繪製區域。 如果使用者選擇嵌入地理位置資訊，此區域會調整大小以容納地理位置文字。

### 清除簽名 {#clearing-a-signature}

使用此功能時，使用者可以按一下 **橡皮擦** 圖示以清除欄位，然後重新開始。 如果新增了地理位置資訊，該資訊也會被清除。

### 儲存簽名 {#saving-a-signature}

按一下 **確定** 圖示會將塗鴉儲存為欄位中的影像。 影像和值可以提交至伺服器以供進一步處理。 使用者按一下後 **確定**，會鎖定草寫欄位。 無法使用塗鴉Widget再次編輯簽名。

點選或按一下「塗鴉」欄位會以唯讀模式開啟對話方塊。

![3](assets/3.png)

### 選取筆大小 {#selecting-pen-size}

按一下 **筆刷** 圖示來顯示可用筆大小的清單。 按一下筆大小以使用對應的筆。

### 從表單中刪除簽章 {#delete-signatures-from-the-form}

若要從表單中刪除簽章：

* （行動裝置）長按簽名欄位，然後在確認對話方塊上，選取 **是**.
* （案頭）將游標暫留在簽名欄位上，按一下 **取消** 圖示，然後在確認對話方塊上，按一下 **是**.
