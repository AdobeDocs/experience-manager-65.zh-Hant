---
title: 測試 — 何時與誰？
description: 測試以及專案開發的不同階段可能會涉及各種角色。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 測試 — 何時與誰？{#testing-when-and-with-whom}

測試以及專案開發的不同階段可能會涉及各種角色。

<table>
 <tbody>
  <tr>
   <td>測試團隊</td>
   <td>負責…… </td>
   <td>當……</td>
  </tr>
  <tr>
   <td>開發團隊</td>
   <td>開發團隊負責您的單元測試和一些整合測試。</td>
   <td>這些測試會先出現在鏈中，但在開發期間會重複/延伸。</td>
  </tr>
  <tr>
   <td>品質保證團隊</td>
   <td><p>您需要品質保證團隊（無論大小）才能進行功能和效能測試。</p> <p>這些是中立、專屬的測試者 — 軟體的金科玉律永遠要求開發人員永遠不應測試自己的工作。</p> <p>此團隊的成員可來自「日」專案團隊、合作夥伴及/或您的客戶團隊。</p> </td>
   <td><p>測試人員應能使用第一個函式版本（如有可能）。 雖然提早發佈臨時版本可能會產生許多錯誤，但它可以就關鍵問題提供早期意見回饋。</p> </td>
  </tr>
  <tr>
   <td>客戶測試團隊</td>
   <td><p>根據選取的專案模型，可能會計畫讓客戶團隊成員參與測試，尤其是來自客戶網站的作者。</p> <p>這是有利的，因為它：</p>
    <ul>
     <li><p>已提供客戶開發專案的經驗。</p> </li>
     <li><p>提供客戶的早期意見回饋。</p> </li>
     <li><p>使用者通常以先前的經驗來表達他們的需求；儘早讓客戶參與測試，會以<i>實際操作</i>的經驗來增加他們的新專案體驗。</p> </li>
    </ul> </td>
   <td><p>同樣地，早期參與也是好事，但客戶使用的任何版本都應該穩定，並具備合理的功能。</p> <p>第一印象總是很重要的。</p> </td>
  </tr>
 </tbody>
</table>
