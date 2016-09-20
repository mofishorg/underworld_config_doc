---
layout: post
title:  "TechTree_HMM 配置文档"
date:   2016-06-27 11:30:00 +0800
categories: jekyll update
---

## 标签


# `<card>`

（CardType标签，复数）。含义：描述单个在战斗中可以使用的卡牌。

  * "id"（Id属性）。含义：卡牌的id。取值：整数；key值。
  * "name"（Name属性）。含义：卡牌的名字。取值：字符串；key值。
  * "card_class"（CardClass属性）。含义：卡牌的类型。取值：枚举{"tower","spell","summon","hero"}，tower表示防御塔卡牌，spell表示法术卡牌，summon表示召唤单位卡牌。
  * "cost"（Cost属性）。含义：卡牌的使用花费。取值：字符串；形式："{0}:{1};...."，{0}为字符串，表示花费资源的名字；{1}为整数，表示花费资源的数量。
  * "recover_span"（RecoverSpan属性，option）。含义：卡牌的使用CD。取值：整数；单位为时间单位最小值。默认值：0。
  * "spell_name"（SpellName属性，option）。含义：卡牌所对应的法术，仅在card_class为spell时有效。取值：字符串；key值。默认值：空。
  * "summon_count"（SummonCount属性，option）。含义：卡牌召唤出的单位的数量，仅在card_class为summon时有效。取值：整数。默认值：1。
  * "desc"（Desc属性，option）。含义：卡牌的描述文字。取值：字符串。默认值：空。
  * 下属标签：`<unit_setting>`，单数，召唤单位的等级按照这个标签的描述。仅在card_class为tower或summon或hero时生效。


# `<card_addon>`

  (CardAddon标签，复数)。含义：描述卡牌升级信息。

  * "id"（Id属性）。含义：卡牌的id。取值：整数：key值。
  * "level"（level属性）。含义：等级。取值：整数。
  * "spell_name"（SpellName属性，option）。含义：升级后卡牌对应的法术，仅在card_class为spell时有效。取值：字符串；key值。默认值：空。
  * 下属标签：`<unit_setting>`，单数，升级后卡牌对应的单位，召唤单位的等级按照这个标签的描述。仅在card_class为tower或summon或hero时生效。


# `<unit_setting>`

(UnitSetting)。含义：由卡牌决定的单位等级描述。

  * 融合标签：`<unit_setting>`，描述单位信息，见*《TechTree 配置文档》*。


  