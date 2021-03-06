---
title: 適用於Communities元件的OSGi事件
seo-title: 適用於Communities元件的OSGi事件
description: 會傳送可觸發非同步接聽程式的OSGi事件
seo-description: 會傳送可觸發非同步接聽程式的OSGi事件
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 4%

---

# Communities元件的OSGi事件{#osgi-events-for-communities-components}

## 概覽 {#overview}

當成員與Communities功能互動時，會傳送可觸發非同步接聽程式的OSGi事件，例如通知或遊戲化（計分和簽章）。

元件的[SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)例項會將事件記錄為`actions`，而發生於`topic`。 SocialEvent包含傳回與動作相關聯的`verb`的方法。 `actions`和`verbs`之間存在&#x200B;*n-1*&#x200B;關係。

對於版本中傳送的Communities元件，下表說明為每個可用`topic`定義的`verbs`。

## 主題和動詞{#topics-and-verbs}

[日](calendar-basics-for-developers.md)
歷元件 `topic`SocialEvent = com/adobe/cq/social/calendar

| **動詞** | **說明** |
|---|---|
| POST | 成員建立日曆事件 |
| 新增 | 日曆事件上的成員注釋 |
| 更新 | 編輯成員的日曆事件或注釋 |
| 刪除 | 會刪除成員的日曆事件或注釋 |

[注](essentials-comments.md)
釋ComponentSocialEvent  `topic`= com/adobe/cq/social/comment

| **動詞** | **說明** |
|---|---|
| POST | 成員建立注釋 |
| 新增 | 成員對評論的答復 |
| 更新 | 編輯成員的注釋 |
| 刪除 | 會刪除成員的注釋 |

[檔案](essentials-file-library.md)
程式庫 `topic`元件SocialEvent = com/adobe/cq/social/fileLibrary

| **動詞** | **說明** |
|---|---|
| POST | 成員建立資料夾 |
| 附加 | 成員上傳檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 刪除 | 成員刪除資料夾或檔案 |

[論](essentials-forum.md)
壇元 `topic`件SocialEvent = com/adobe/cq/social/forum

| **動詞** | **說明** |
|---|---|
| POST | 成員建立論壇主題 |
| 新增 | 成員對論壇主題的答復 |
| 更新 | 編輯成員的論壇主題或回復 |
| 刪除 | 會刪除成員的論壇主題或回復 |

[日](blog-developer-basics.md)
記帳元 `topic`件SocialEvent = com/adobe/cq/social/journal

| **動詞** | **說明** |
|---|---|
| POST | 會員建立部落格文章 |
| 新增 | 部落格文章上的成員評論 |
| 更新 | 編輯會員的部落格文章或評論 |
| 刪除 | 會員的部落格文章或評論被刪除 |

[QnA ](qna-essentials.md)
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **動詞** | **說明** |
|---|---|
| POST | 成員建立QnA問題 |
| 新增 | 成員建立QnA答案 |
| 更新 | 編輯成員的QnA問題或答案 |
| 選擇 | 已選擇成員的答案 |
| 取消選擇 | 已取消選擇成員的答案 |
| 刪除 | 會員的QnA問題或答案將被刪除 |

[審](reviews-basics.md)
閱ComponentSocialEvent  `topic`= com/adobe/cq/social/review

| **動詞** | **說明** |
|---|---|
| POST | 成員建立審核 |
| 更新 | 已編輯成員的審核 |
| 刪除 | 會刪除成員的審核 |

[評](rating-basics.md)
分ComponentSocialEvent  `topic`= com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 新增評等 | 會員的內容已評級 |
| 移除評等 | 會員的內容已降級 |

[投票](essentials-voting.md)
元件 `topic`SocialEvent = com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 添加投票 | 會員的內容被投票 |
| 刪除投票 | 會員的內容被投票否決 |

**已啟用協**
調的元 `topic`件SocialEvent = com/adobe/cq/social/moderation

| **動詞** | **說明** |
|---|---|
| 拒絕 | 拒絕成員的內容 |
| 標示為不適當 | 會標籤成員的內容 |
| 取消標幟為不適當 | 會取消標籤成員的內容 |
| 接受 | 會員的內容由版主批准 |
| 關閉 | 成員關閉對編輯和回復的注釋 |
| 開啟 | 成員重新開啟注釋 |

## 自訂元件事件{#events-for-custom-components}

對於自訂元件，必須將[SocialEvent抽象類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)擴展為d，將元件的事件記錄為`topic`發生的`actions`。

自訂事件會覆寫方法`getVerb()`，以便為每個`action`傳回適當的`verb`。 針對動作傳回的`verb`可為常用的`POST`，或專用於元件的`ADD RATING`。 `actions`和`verbs`之間存在&#x200B;*n-1*&#x200B;關係。

>[!NOTE]
>
>確保自訂擴充功能的註冊排名低於產品中任何現有實作。

### 自訂元件事件{#pseudo-code-for-custom-component-event}的虛擬碼

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## 篩選活動資料流資料的範例EventListener {#sample-eventlistener-to-filter-activity-stream-data}

您可以監聽事件，以修改活動資料流中顯示的內容。

下列虛擬碼範例將從活動資料流中移除「注釋」元件的DELETE事件。

### EventListener {#pseudo-code-for-eventlistener}的虛擬碼

需要[最新的Feature Pack](deploy-communities.md#latestfeaturepack)。

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```
