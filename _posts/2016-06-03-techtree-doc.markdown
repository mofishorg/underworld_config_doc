---
layout: post
title:  "TechTree 配置文档"
date:   2016-06-03 18:45:26 +0800
categories: jekyll update
---

> 更新日志
>
> 6.17.2016  
> 1. 为绝大部分添加了name属性。  
> 2. 去除了所有下属标签，改用名字关联。  
> 3. 删除了一些冗余标签。  
>

<br/>

## 约定


1. 标签：表示配置时的xml标签。
2. 属性：xml标签的属性。
3. 取值：属性的值域类型。
4. 下属标签：表示被另一个标签包围的标签。
5. 融合标签：表示去除自己的标签明，将自己的所有属性写在另一个标签内部的标签。
6. key值：表示在相同位置不能重复的字符串值。
7. 布尔值：取值为0或1的取值
8. 枚举：有限的几个字符串的集合
9. option属性：有的时候可以不配置的属性，提供默认值。

- - -
<br/>



## 标签


# `<faction>`

（FactionType标签，复数）。含义：描述单个势力特性的配置标签。

  * "name"（Name属性）。含义：势力的名字。取值：字符串；key值（不能重复）。


# `<resource>`

（ResourceType标签，复数）。含义：描述单个战斗时资源的配置标签。

  * "name"（Name属性）。含义：资源的名字。取值：字符串；key值。
  * "class"（Class属性）。含义：资源的类别，主要来用以区分资源的消耗方式。取值：枚举{"holdable","consumable"}，holdable表示资源以占有的方式消耗，如人口；consumable表示资源以花费的方式消耗，如金币。
  * "max"（Max属性，option）。含义：资源的上限。取值：整数。默认值：-1表示无上限。


# `<armor>`

（ArmorType标签，复数）。含义：描述单位护甲类型的配置标签。
  
  * "name"（Name属性）。含义：护甲类型的名字。取值：字符串；key值。


# `<armor_rule>`
（护甲规则标签，唯一）。含义：描述护甲规则的配置标签。

  * "armor_base_positive"（ArmorBasePositive属性）。含义：护甲为正数时计算公式的基础值。取值：整数。
  * "armor_factor_positive"（ArmorFactorPositive属性）。含义：护甲为正数时计算公式的因数值。取值：浮点数。
  * "armor_base_negative"（ArmorBaseNegative属性）。含义：护甲为负数时计算公式的基础值。取值：整数。



# `<effect_alias>`
（EffectAlias标签，复数）。含义：effectType的游戏性分类的配置标签。

  * "name"（Name属性）。含义：效果归类的名字。取值：字符串；key值。
  * "unique"（Unique属性，option）。含义：该效果归类是否为独占性的，即该归类的多个同事效果仅能有一个生效。取值：布尔值。默认值：0。


# `<buff>`
（BuffType标签，复数）。含义：描述单个buff的配置标签。

  * "alias"（Alias属性）。含义：buff的类别。取值：字符串；key指。
  * "unique_on_unit"（UniqueOnUnit属性，option）。含义：该类buff是否在单个单位上仅有一个生效。取值：布尔值。默认值：0。
  * "name"（Name属性）。含义：buff的名字。取值：字符串；key值。
  * "level"（Level属性）。含义：buff在自身类别中的等级。取值：整数。
  * "deliver_nature"（DeliverNature属性）。含义：buff的deliverNature类别（有益、有害等）。取值：枚举deliver_nature。
  * "deliver_class"（DeliverClass属性）。含义：buff的deliverClass类别（魔法、物理）。取值：枚举deliver_class
  * "span_type"（SpanType属性）。含义：buff的持续时间的类别。取值：枚举{"eternal","limited","loads","limited_and_loads"}, eternal表示持续时间为永久；limited表示持续时间为有限；loads表示在buff使用次数消耗完之后buff消失；limited_and_loads表示buff使用次数消耗完之后buff消失，并且持续时间有限。
  * "span"（Span属性，option）。含义：buff的持续时间，仅仅在SpanType为limited或limited_and_loads时有效，单位为秒。取值：整数；时间最小单位。默认值：0。
  * "max_overlay"（MaxOverlay属性，option）。含义：buff的最大叠加次数。取值：整数。默认值：1。
  * "dispelable"（Dispelable属性，option）。含义：该类buff是否能被驱散。取值：布尔值。默认值：1。
  * "render_key"（RenderKey属性，option）。含义：该buff的绘制资源名字。取值：字符串；key值。默认值：空。
  * "buff_effect_names"（BuffEffectNames属性，option）。含义：该buff可以产生的效果的名字列表。取值：字符串；形式："BuffEffectName;BuffEffectName;..."。默认值：0。


# `<buff_effect>`
 （BuffEffect标签）。含义：描述属于buff的效果的配置标签。

  * "buff_effect_name"（BuffEffectName属性）。含义：buff效果的名字。取值：字符串；key值。
  * "buff_effect_condition"（BuffEffectCondition属性）。含义：buff的效果的生效的条件。取值：枚举{"immediate","loop","schedule","end","dispel"}，immediate表示在buff生效同时立即生效的效果；loop表示按照一定时间循环生效的效果；schedule表示按照一定时间定时生效一次的效果；timing表示在特定时机除非生效的效果；end表示在buff结束时生效的效果；dispel表示在buff被驱散时生效的效果（不包含buff结束）。
  * "buff_effect_time"（BuffEffectTime属性，option）。含义：buff效果的生效时间，仅仅在buff_effect_condition为loop或schedule的时候有效。取值：浮点数。默认值：0。
  * "buff_effect_loads"（BuffEffectLoads属性，option）。含义：该buff效果的生效次数，取值-1时为无限制。取值：整数。默认值：-1。
  * "is_damage"（IsDamage属性，option）。含义：该buff效果是伤害还是持续效果，当为buff内容标签应为`<damage>`；否则为`<effect>`。取值：布尔值。默认值：0。
  * "buff_effect_content_name"（BuffEffectContentName）。含义：该buff效果内容的名字，`<effect>`&`<damage>`标签的名字。取值：字符串；key值。


# `<damage>`
（damage标签）。含义：描述伤害或治疗的配置标签。

  * "damage_name"（DamageName属性）。含义：damage的名字。取值：字符串；key值。
  * "damage_value"（DamageValue属性）。含义：伤害或治疗的值。取值：DynamicValue。
  * "damage_nature"（DamageNature属性）。含义：damage为伤害还是治疗。取值：枚举{"heal","hurt"}。
  * "deliver_class"（DeliverClass属性，option）。含义：damage的deliver_class类别，仅在damage_nature为hurt有意义。取值：枚举deliver_class。默认值：undefined
  * "damage_distance"（DamageDistance属性，option）。含义：伤害的距离类别（远程、近战），仅在damage_nature为hurt有意义。取值：枚举{"faraway, nearby"}。默认值：undefined。
  * "feature_names"（FeatureNames属性，option）。含义：这次伤害/治疗附带的特性。取值：字符串；形式："FeatureName;FeatureName;..."。默认值：空。


# `<effect>`
（effect标签）。含义：描述持续效果的配置标签（主要用于buff）。

  * "effect_name"（EffectName属性）。含义：效果的名字。取值：字符串；key值。
  * "class"（Class属性）。含义：效果的效果类别。取值：枚举{"alter_attr","set_state","add_feature"}，alter_attr表示该效果为改变单位属性；set_state表示该效果为设置单位状态；damage表示效果使单位经受伤害或治疗。
  * "alias_name"（AliasName属性，option）。含义：本效果属于的EffectAlias的名字。取值：字符串：key值。默认值：空。
  * "ref_value"（RefValue属性，option）。含义：这个持续效果的参考值，用于unique的持续效果做比较。取值：整数。默认值：0。
  * 当class为alter_attr时
     * "attr_name"（AttrName属性）。含义：效果所改变的单位属性。取值：枚举attribute_type。
     * "value"（Value属性）。含义：效果所改变的单位属性的值。取值：LiteralValue。
  * 当class为set_state时
     * "state_name"（StateName属性）。含义：效果所设置的单位状态。取值：枚举state_type。
  * 当class为add_feature时
     * "feature_name"（FeatureName属性）。含义：效果为单位添加的特性的名字。取值：字符串；key值。


# `<passive>`
（PassiveType标签，复数）。含义：描述单个被动技能的配置标签。

  * "alias"（alias属性）。含义：该被动技能的归类名称，不同等级的同一技能被称为同一被动技能归类。取值：字符串；key值。
  * "name"（name属性）。含义：该被动技能的唯一名称。取值：字符串；key值。
  * "level"（level属性）。含义：该被动技能的等级。取值：整数，[1 - max_level]。
  * "buff_types"（BuffTypes属性，option）。含义：该被动技能活跃时给持有者提供的buff种类。取值：字符串；形式，"BuffName;BuffName;..."。默认值：空。
  * "aura_types"（AuraTypes属性，option）。含义：该被动技能活跃时给持有者持有的光环种类。取值：字符串；形式，"AuraName;AuraName;..."。默认值：空。
  * "addon_types"（AddonTypes属性，option）。含义：该被动技能给持有者提供的加成。取值：字符串；形式，"AddonName;AddonName;..."。默认值：空。
  * "desc"（Desc属性，option）。含义：该被动技能的文字描述。取值：字符串。


# `<aura>`
（Aura标签）。含义：描述单个光环的配置标签。

  * "name"（Name属性）。含义：光环的名字。取值：字符串；key值。
  * "radius"（Radius属性）。含义：光环的半径。取值：整数值；地图最小单位。
  * "buff_name"（BuffName属性）。含义：光环提供的buff名称。取值：字符串；key值。
  * 融合标签：`<condition>`，描述该光环影响目标的筛选条件。


# `<spell>`
（SpellType标签，复数）。含义：描述单个主动技能的配置标签。

  * "alias"（alias属性）。含义：该主动技能的归类名称，不同等级的同一技能称为同一主动技能归类。取值：字符串；key值。
  * "spell_name"（SpellName属性）。含义：该主动技能的唯一名称。取值：字符串；key值。
  * "level"（Level属性）。含义该主动技能的等级。取值：整数，[1 - max_level]。
  * "deliver_class"（DeliverClass属性）。含义：技能的deliver_class类别，（魔法、物理）。取值：枚举deliver_class。
  * "to_dead"（ToDead属性，option）。含义：技能是否队死亡单位释放。取值：布尔值。默认值：0。
  * "cast_distance"（CastDistance属性）。含义：技能的施法距离。取值：整数（地图最小单位）；-1为无距离限制。
  * "cast_type"（CastType属性）。含义：技能选取锚点的类别。取值：枚举{"self","position","unit","unit_but_self","position_or_unit"}，self表示技能永远选取施法者为锚点；postion表示技能选取指定位置为锚点；unit表示技能选取某个单位为锚点；unit_but_self表示技能选取除施法者以为的某个目标为锚点；position_or_unit表示技能选取位置或者某个单位为锚点；（不含二次选择操作的法术，锚点均为self）  
  * "immediate_elements"（ImmediateElements属性，option）。含义：技能释放时立即放出的技能元素。取值：字符串；形式，"SpellElement;SpellElement;..."。SpellElement取值。形式："{0},{1},{2}"，{0}为布尔值，表示技能元素是对施法者释放还是对锚点释放，值为1时表示对施法者；{1}为字符串，取值为SpellPattern的name属性；{2}为整数，表示该技能元素一次释放的生效次数。
  * "desc"（Desc属性，option）。含义：技能的文字描述。取值：字符串。
  * "ai"（AI属性，option）。含义：技能AI规则描述名字。取值：字符串；key值。
  * 融合标签：`<condition>`，该法术施放的限制条件，仅检查条件，不做概率判定；`<skill>`，该法术的技能信息。


# `<spell_pattern>`
（SpellPattern标签，复数）。含义：描述单词施法效果的配置标签。

  * "name"（Name属性）。含义：施法效果的名字。取值：字符串；key值。
  * "class"（SpellPatternClass属性）。含义：施法效果的模式类别。取值：枚举{"target","target_position_circle","all"}，target表示对施法；target_position_circle表示对施法目标位置为圆心的圆形范围内的单位施法；all表示对战场上所有单位施法。
  * "contetn_name"（ContentName属性）。含义：施法效果的内容的名字。取值：字符串；key值。
  * 当class为target_position_circle时
    * "radius"（radius属性）。含义：选取圆形范围的半径。取值：整数（地图最小单位）。
  * 融合标签：`<condition>`，描述选取施法目标限制条件。


# `<spell_content>`
（spellContent标签）。含义：施法内容的描述。

  * "name"（name属性）。含义：施法内容的名字。取值：字符串；key值。
  * "spell_content_class"（spellContentClass属性）。含义：施法内容的类型。取值：枚举{"damage","bullet", "summon","revive","magic"}，damage表示对目标施加伤害；bullet表示对目标放出子弹；summon表示召唤单位；revive表示复活单位；magic表示释放魔法实例。
  * 当spell_content_class为damage时
     * "spell_content_damage_name"（SpellContentDamageName属性）。含义：施加的伤害的名字。取值：字符串；key值。
  * 当spell_content_class为bullet时
     * "to_position"（ToPosition属性，option）。含义：是向单位发出子弹还是向位置发出子弹。取值：布尔值。默认值：0。
     * "spell_content_damage_name"（SpellContentDamageName属性）。含义：子弹所传递的伤害的名字。取值：字符串；key值。
     * "spell_content_bullet_name"（SpellContentBulletName属性）。含义：子弹类型的名字。取值：字符串；key值。
  * 当spell_content_class为summon时
     * "summon_count"（SummonCount属性，option）。含义：召唤的单位的个数。取值：整数。默认值：1。
     * 融合标签： `<unit_setting>`，单数，召唤单位的描述。
  * 当spell_content_class为magice时
     * "magic_name"（MagicName属性）。含义：魔法实例的类型名字。取值：字符串；key值。
     * "is_attach_to_holder"（IsAttachToHolder属性，option）。含义：魔法实例是否绑定在目标上。取值：布尔值。默认值：0。

# `<spell_ai_description>`
（SpellAIDescription标签）。含义：描述spell的AI规则。

  * "name"（name属性）。含义：AI描述的名字。取值：字符串；key值。
  * "scenario"（scenario属性）。含义：法术的释放场景。取值：枚举{"in_battle","all"}，in_battle表示在战斗中；all表示任何时间。
  * 融合标签：`<condition>`，描述选择施法目标的筛选条件；`<heuristic>`，描述选择施法目标的优先评价方法。


# `<magic>`
（magic标签）。含义：魔法实例的描述。

  * "name"（name属性）。含义：魔法实例的名字。取值：字符串；key值。
  * "span_type"（SpanType属性）。含义：魔法实例的持续时间类型。取值：枚举{"eternal","limited"}，elernal表示魔法实例永远持续；limited表示魔法实例有持续时间。
  * "span"（Span属性，option）。含义：魔法实例的持续时间，仅在SpanType为limited时有效。取值：整数；时间单位。默认值：0。
  * "render_key"（RenderKey属性，option）。含义：魔法实例的绘制资源名称。取值：字符串；key值。默认值：空。
  * "aura_names"（AuraNames属性，option）。含义：魔法实例包含的光环类型名字。取值：字符串；形式，"AuraName;AuraName;..."。默认值：空。
  * "magic_effect_names"（MagicEffectNames属性，option）。含义：魔法实例所释放的效果的名字。取值：字符串；形式，"MagicEffectName;MagicEffectName;..."。默认值：空。


# `<magic_effect>`
（MagicEffect标签）。含义：魔法实例所释放的单个效果。

  * "magic_effect_condition"（MagicEffectCondition属性）。含义：魔法实例释放效果的时机类型。取值：枚举{"loop","schedule"}，loop表示循环释放；schedule表示定时释放。
  * "magic_effect_spell_pattern_name"（MagicEffectSpellPatternName属性）。含义：魔法实例释放效果的名字（spell_pattern名字）。取值：字符串；key值。
  * "magic_effect_time"（MagicEffectTime属性，option）。含义：魔法实例释放效果的时机。取值：整数；时间单位。默认值：0。


# `<unit>`
（Unit标签）。含义：描述单个单位的配置标签。

  * "name"（Name属性）。含义：该单位的名字。取值：字符串；key值。
  * "class"（UnitClass属性）。含义：该单位的类别。取值：枚举{"warrior","hero","building","core"}。
  * "race"（UnitRace属性）。含义：该单位的种族。取值：字符串；key值。
  * "talent_name"（TalentName属性，option）。含义：该单位的天赋名称。取值：字符；key值。
  * "upgrade_talents"（UpgradeTalents属性，option）。含义：该单位可升级到的天赋名称。取值：字符串；形式，"{0};..."，{0}为字符串，取值为单位名称。
  * "rarity"（Rarity属性，option）。含义：该单位的稀有度。取值：整数。默认值：0。
  * "hp"（Hp属性，option）。含义：单位的最大生命值。取值：整数。默认值：0。
  * "field"（Field属性，option）。含义：单位默认处于的field。取值：枚举field_type。默认值：land。
  * "armor_type"（ArmorType属性）。含义：单位的护甲类型。取值：字符串；ArmorType的name属性。
  * "armor"（Armor属性，option）。含义：单位的护甲值。取值：整数。默认值：0。
  * "armor_preference"（ArmorPreference属性，option）。含义：单位的护甲偏好。取值：字符串；ArmorType的name属性。默认值：空。
  * "armor_preference_factor"（ArmorPreferenceFactor属性，option）。含义：单位的护甲偏好系数。取值：LiteralValue。默认值：p:0。
  * "magical_defense"（MagicalDefense属性，option）。含义：单位魔抗值。取值：整数。默认值：0。
  * "sight"（Sight属性，option）。含义：单位视野半径。取值：整数（地图最小单位）。默认值：0。
  * "attackSight"（AttackSight属性）。含义：单位警戒半径。取值：整数（地图最小单位）。
  * "size"（Size属性，option）。含义：单位碰撞体积边长。取值：整数（地图最小单位）。默认值：0。
  * "height"（Height属性，option）。含义：单位的Z轴高度。取值：整数（地图最小单位）。默认值：0。
  * "reward"（reward属性，option）。含义：单位被杀死时奖励的资源。取值：字符串；形式，"{0}:{1};..."，{0}为字符串，取值为ResourceType的name，{1}为整数，表示所需资源数量。默认值：空。
  * "occupy"（Occupy属性，option）。含义：单位的碰撞体积十分生效。取值：布尔值。默认值：1。
  * "passive_names"（PassiveNames属性，option）。含义：单位具有的被动技能名称。取值：字符串；形式："PassiveTypeName;PassiveTypeName;..."。默认值：空。
  * "spell_names"（SpellNames属性，option）。含义：单位具有的主动技能名称。取值：字符串；形式："SpellTypeName;SpellTypeName;..."。默认值：空。
  * "produce_names"（ProduceNames属性，option）。含义：单位具有的生产技能的名称。取值：字符串；形式："SkillTypeName;SkillTypeName..."。默认值：空。
  * "skill_names"（SkillNames属性，option）。含义：单位具有的基础技能的名称。取值：字符串；形式："ProduceTypeName;ProduceTypeName..."。默认值：空。
  * "feature_names"（FeatureNames属性，option）。含义：单位具有的特性的名称。取值：字符串；形式："FeatureGroupName;FeatureGroupName..."。默认值：空。
  * "max_level"（MaxLevel属性，option）。含义：单位的最大等级。取值：整数。默认值：0。
  * "max_quality"（MaxQuality属性，option）。含义：单位的组大品质。取值：整数。默认值：0。
  * "max_talent_level"（MaxTalentLevel属性，option）。含义：单位的最大天赋等级。取值：整数。默认值：0。
  * "render_key"（RenderKey属性）。含义：单位的绘制资源名称。取值：字符串；key值。


# `<unit_setting>`
（unit_setting标签）。含义：单位的生成信息。

  * "unit_setting_name"（name属性）。含义：单位的名字。取值：字符串；key值。
  * "unit_setting_level"（level属性，option）。含义：单位的属性。取值：整数。默认值：0。
  * "unit_setting_quality"（quality属性，option）。含义：单位的品质。取值：整数。默认值：0。
  * "unit_setting_talent"（talent属性，option）。含义：单位的天赋等级。取值：整数。默认值：0。


# `<unit_upgrade>`
（UnitUpgread标签）。含义：描述单位的升级信息的配置标签。

  * "upgrade_class"（UpgradeClass属性）。含义：升级的类型。取值：枚举{"level", "quality", "talent"}，level表示等级上升，quality表示品质上升，talent表示天赋上升。
  * "unit_name"（UnitName属性）。含义：改等级信息所属于的单位的名字。取值：字符串；key值。
  * "upgrade_index"（UpgradeIndex属性）。含义：等级的序号。取值：整数[1 - maxIndex]。
  * 融合标签：`<addon>`，该等级对单位的加成。

          
 # `<addon>`
 （Addon标签）。含义：描述对单位的加成信息的配置标签。

  * "name"（name属性）。含义：该加成信息的名字。取值：字符串；key值。
  * "attribute_addons"（AttributeAddons属性，option）。含义：加成信息所更改的单位属性。取值：字符串；形式："{0}:{1};..."，{0}取值枚举attribute_type，{1}取值为LiteralValue。默认值：空。
  * "passive_addons"（PassiveAddons属性，option）。含义：加成信息所提供的被动技能。取值：字符串；形式："PassiveTypeName;PassiveTypeName;..."。默认值：空。
  * "spell_addons"（PassiveAddons属性，option）。含义：加成信息所提供的主动技能。取值：字符串；形式，"SpellTypeName;SpellTypeName;..."。默认值：空。
  * "feature_addons"（FeatureAddons属性，option）。含义：加成信息所提供的特性。取值：字符串；形式，"FeatureGroupName;FeatureGroupName;..."。默认值：空。


# `<skill>`
（skill标签）。含义：描述单位的基本技能的配置标签。

  * "name"（Name属性，option）。含义：基本技能的名字。取值：字符串。默认值：空。
  * "preperform"（Preperform属性）。含义：基本技能的前摇时间。取值：整数；时间单位。
  * "perform"（Perform属性）。含义：基本技能的施放时间。取值：整数；时间单位。
  * "cd"（Cd属性）。含义：基本技能的冷却时间。取值：浮点数；单位为秒。
  * "class"（Class属性）。含义基本技能的类别。取值：枚举{"stop","move","attack","cast","die","produce"}，stop表示单位静止技能；move表示单位的移动技能；attack表示单位的攻击技能；cast表示单位的spell技能，仅在作为`<spell>`的融合标签时使用；die表示单位的死亡技能；produce表示单位的生产技能，仅在作为`<produce_unit>`的融合标签时使用。
  * 当class为attack时
     * "min_damage"（MinDamage属性）。含义：攻击力下限。取值：整数。
     * "max_damage"（MaxDamage属性）。含义：攻击力上限。取值：整数。
     * "range"（Range属性）。含义：攻击范围。取值：整数（地图最小单位）。
     * "fields"（Fields属性）。含义：攻击可达的Field。取值：1为对地，2为对空，3为对地对空。
     * "unit_classes"（UnitClasses属性）。含义：可攻击的Unit类型。取值：整数；一共4位从高到低表示core，building，hero，warrior。
     * "deliver_class"（DeliverClass属性，option）。含义：伤害的DeliverClass类别。取值：枚举deliver_class。默认值：undefined。
     * "damage_distance"（DamageDistance属性）。含义：伤害的DamageDistance类别。取值：枚举damage_distance。
     * "bullet_name"（BulletName属性，option）。含义：该次攻击是否有子弹以及子弹信息。取值：字符串；key值。默认值：空。
  * 当class为move时
     * "speed"（Speed属性）。含义：移动速度。取值：整数；地图最小单位/秒。
  * 当class为die时
     * "occupy"（Occupy属性，option）。含义：单位死亡后碰撞体积是否还生效。取值：布尔值；1表示死后碰撞体积依然生效。默认值：0。


# `<produce_unit>`
（ProduceUnit标签）。含义：描述单位的生产技能，效果为生产其他单位。

  * "produce_name"（ProduceName属性）。含义：生产技能的名字。取值：字符串；key值。
  * "produce_cost"（ProduceCost属性，option）。含义：生产一次的资源消耗。取值：字符串；形式，"{0}:{1};..."，{0}为字符串，取值为ResourceType的name，{1}为整数，表示所需资源数量。
  * "produce_desc"（ProduceDesc属性）。含义：生产技能的文字描述。取值：字符串。
  * 融合标签：`<skill>`，描述生产技能的基本信息。`<unit_setting>`，描述所生产的单位。


# `<bullet>`
（Bullet标签）。含义：描述子弹的配置标签。

  * "name"（name属性）。含义：子弹的名字。取值：字符串；key值。
  * "speed"（Speed属性）。含义：子弹的飞行速度。取值：整数；地图最小单位/秒。
  * "radius"（Radius属性，option）。含义：子弹半径。取值：整数；地图最小单位。默认值：0。
  * "sweep_on_the_way"（SweepOnTheWay属性，option）。含义：子弹是否会击中沿路的单位。取值：布尔值；1表示会击中。默认值：0。
  * "sweep_count"（SweepCount属性，option）。含义：子弹最多击中的单位数量。取值：整数；-1表示无限制。默认值：-1。
  * "deliver_nature"（DeliverNature属性，option）。含义：子弹影响的单位类型。取值：deliver_nature枚举。默认值：enemy。
  * "height"（Height属性，option）。含义：子弹的飞行高度。取值：浮点数。默认值：0。
  * "explode_radius"（ExplodeRadius属性，option）。含义：子弹的爆炸范围。取值：整数；地图单位。默认值：0。
  * "render_key"（RenderKey属性，option）。含义：子弹的绘制资源。取值：字符串；key值。


# `<feature_group>`
（FeatureGroup标签）。含义：判定时机相同的一组feature，这些feature的生效时机可以不同。

  * "name"（Name属性）。含义：特性组的名字。取值：字符串；key值。
  * "determine_timing"（DeterimingTiming属性）。含义：特性组的判定时机。取值：timing枚举。
  * "feature_type_names"（FeatureTypeNames属性，option）。含义：，复数，属于特性组的各个特性的名字。取值：字符串；形式："FeatureTypeName;FeatureTypeName;..."。默认值：空。
  * 融合标签：`<condition>`，特性的触发条件。

          
# `<feature>`
（feature标签）。含义：描述特性的配置标签。

  * "feature_name"（FeatureName属性）。含义：特性的名字。取值：字符串；key值。
  * "effect_timing"（EffectTiming属性）。含义：该特性的生效时机。取值：timing枚举。
  * "type"（Types属性）。含义：特性的效果类别。取值：枚举{"damage_enhance","damage_reduce","drain","splash","rebound","pierce","multiple","extra_damage","miss","add_buff","cast_spell","dispel","reflect","counter","tough"}，"damage_enhance"为增加攻击伤害；"damage_reduce"为减少攻击伤害；"drain"为攻击吸血；"splash"为攻击溅射；"rebound"为攻击弹射；"pierce"为穿透；"multiple"为多重攻击；"extra_damage"为额外伤害；"miss"为未命中；"add_buff"为添加buff;"dispel"为驱散buff；"reflect"为反弹伤害；"counter"为反击；"tough"为坚毅；"cast_spell"为施放法术。
  * "render_key"（RenderKey属性，option）。含义：特性触发时的绘制资源名称。取值：字符串；key值。默认值：空。
  * 当type为damage_enhance时
     * "value"（Value属性）。含义：伤害增加值。取值：DynamicValue。
  * 当type为damage_reduce时
     * "value"（Value属性）。含义：伤害减少值。取值：DynamicValue。
  * 当type为drain时
     * "value"（Value属性）。含义：吸血值。取值：DynamicValue。
  * 当type为splash时
     * "value"（Value属性）。含义：溅射值。取值：DynamicValue。
     * "range"（Range属性）。含义：溅射范围。取值：DynamicValue；地图单位。
  * 当type为rebound时
     * "value"（Value属性）。含义：弹射值。取值：DynamicValue。
     * "range"（Range属性）。含义：弹射范围。取值：DynamicValue；地图单位。
     * "count"（Count属性）。含义：弹射次数。取值：DynamicValue。
  * 当type为pierce时（未完成）
  * 当type为multiple时
     * "value"（Value属性）。含义：分裂伤害值。取值：DynamicValue。
     * "range"（Ranges属性）。含义：分裂伤害范围。取值：DynamicValue；地图单位。
     * "count"（Count属性）。含义：分裂伤害数量。取值：DynamicValue。
  * 当type为extra_damage时
     * "value"（Value属性）。含义：额外伤害值。取值：DynamicValue。
     * "deliver_class"（DeliverClass属性）。含义：额外伤害的DeliverClass类别。取值：枚举deliver_class。
  * 当type为add_buff时
     * "buff_type_name"（BuffTypeName属性）。含义：添加buff的名字。取值：字符串；key值。
     * "overlay"（Overlay属性，option）。含义：添加buff的层数。取值：整数。默认值：1。
     * "is_to_self"（IsToSelf属性，option）。含义：buff是添加给自己还是给对方。取值：布尔值。默认值：0表示不是对自己添加。
  * 当type为reflect时
     * "value"（Value属性）。含义：反弹伤害值。取值：DynamicValue。
  * 当type为tough时
     * "value"（Value属性）。含义：最高伤害值。取值：DynamicValue。
  * 当type为cast_spell时
     * "spell_name"（spellName属性）。含义：释放的法术名。取值：字符串；key值。
     * "is_to_self"（IsToSelf属性，option）。含义：释放法术的对象是否为自己。取值：布尔值。默认值：0。
  * 当type为dispel时
     * "deliver_nature"（DeliverNature属性，option）。含义：驱散buff是有益的还是有害的。取值：DeliverNature枚举，默认值：neutral。


# `<condition>`
（condition标签）。含义：触发战斗元素的限制条件。

  * "probability"（Probability属性，option）。含义：条件的触发概率。取值：整数[0 - 100]。默认值：undefined。
  * "deliver_nature"（DeliverNature属性，option）。含义：条件的敌我关系。取值：deliver_nature枚举。默认值：neutral。
  * "conditions"（Conditions属性，option）。含义：条件的限制条件。取值：字符串；形式："Condition|Condition|......."。
  * Condition取值。形式："type:{0};target:{1};condition:{2}"，{0}描述条件的类型，取值为枚举{"unit_race","unit_class","armor_type","field_type","unit_hp","unit_lose_hp","unit_has_buff","unit_not_has_buff","deliver_class","damage_distance"}；{1}描述条件作用的目标，取值为枚举{"owner","opposite","damage"}；{2}描述条件的具体值，当条件为枚举条件时{2}的形式为"is:(not:)枚举值,枚举值,..."，当条件为数字值的时候{2}的形式为">(<)(=)LiteralValue"。


# `<heuristic>`
（heuristic标签）。含义：根据自身和目标生成评价值的启发函数。

  * "heuristic_element_names"（HeuristicElementNames，option）。含义：描述启发函数的评价值的名字，评价值的权重按heuristic_element的先后顺序逐渐降低。取值：字符串；形式："HeuristicElementName;HeuristicElementName;..."。默认值空。


# `<heuristic_element>`
（HeuristicElement标签）。含义：描述启发函数的一个启发值。

  * "heuristic_element_name"（HeuristicElementName属性，option）。含义：启发值得名字。取值：字符串；key值。
  * "type"（type属性）。含义：启发值的类型。取值：枚举{"literal","less_then_ref_value","equal_to_ref_value","larger_then_ref_value"}，literal表示直接值；less_then_ref_value表示是否比参考值小的判断所产生的布尔值；equal_to_ref_value表示是否和参考值相等的判断所产生的布尔值；larger_then_ref_value表示是否比参考值高的判断所产生的布尔值。
  * "ref_value"（RefValue属性，option）。含义：启发值的参考值。取值：整数。默认值：0。
  * "descending"（Descending属性，option）。含义：启发值是否是值越大越优秀。取值：整数。默认值：1。
  * "value"（Value属性）。含义：启发值的取值。取值：DynamicValue。

- - -
<br/>


## 取值


  * deliver_nature枚举。含义：敌我类别的枚举。值域："ally"（友军），"enemy"（敌人）,"neutral"（友军和敌人）。
  * deliver_class枚举。含义：伤害类别的枚举。值域："physical"（物理），"magical"（魔法）。
  * timing枚举。含义：战斗时机的枚举。值域："attack"（攻击时）,"settle_attack_damage_r1"（结算攻击伤害第一轮)，"settle_attack_damage_r2"（结算攻击伤害第二轮），"release_attack"（攻击被释放时），"be_attack"（被攻击时），"hit"（击中时），"be_hit"（被击中时），"settle_hurt_damage_r1"（结算受到伤害第一轮），"settle_hurt_damage_r2"（结算受到伤害第二轮）， "hurt"（造成伤害时），"be_hurt"（被伤害时），"kill"（杀死单位时），"be_kill"（被杀死时），"heal"（治疗时），"be_heal"（被治疗时），"settle_cure_damage_r1"（结算受到治疗第二轮），"cure"（造成恢复生命），"be_cure"（被恢复生命）
  * field_type枚举。含义：单位所处的图层。值域："land"（陆地），"air"（天空）。
  * attribute_type枚举。含义：单位的属性种类。值域："max_hp"，"max_mp"，"sight"，"attack_sight"，"armor"，"magical_defense"，"attack_damage"，"attack_range"，"attack_speed"，"move_speed"。
  * state_type枚举。含义：单位的状态的种类。值域："unstoppable"，"physical_immune"，"magical_immune"，"holly"，"Immortal"，"unmoveable"，"stun"，"silence"，"disarm"
  * LiteralValue取值。含义：直接数值取值。形式："p:整数"或者"整数"，前者表示基础值的百分比，后者表示直接值。
  * DynamicValue取值。含义：动态数值取值。形式："LiteralValue"或者"d:target:{0};type:{1};v:{2};template:{3}"，前者等同于LiteralValue；后者{0}表示动态值的判断目标，取值枚举{"owner","opposite"}，{1}表示动态值得取值方式，取值为枚举{"literal","hp",""max_hp", "armor", "attack_damage","attack_speed"}，{2}表示取值后相乘的系数，取值为LiteralValue（百分比形式），{3}表示取值应用于的Literal模板，取值为LiteralValue。



