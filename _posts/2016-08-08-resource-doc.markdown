---
layout: post
title:  "Resource 配置文档"
date:   2016-08-08 14:56:00 +0800
categories: jekyll update
---

# UnitResourceConfig.xml

单位资源配置表，每个标签表示一种单位的资源配置

  * "render_key"。含义：单位资源的名字。取值：字符串；key值。
  * "direction"。含义：单位资源的初始方向。取值：0表示向左，1表示向右。默认值：0。
  * "multi_direction"。含义：单位资源是否为多方向的。取值：布尔值。默认值：1。
  * "transform_on_health"。含义：单位资源是否随健康状况改变。取值：布尔值。默认值：0。
  * "anim_type"。含义：单位资源的类型。取值：枚举{"pvr", "csb"}。
  * "normal_prefix"。含义：健康的单位身体资源前缀。取值：字符串。
  * "shadow_prefix"。含义：单位的影子资源前缀。取值：字符串。
  * "damaged_prefix"。含义：受伤的单位身体资源前缀。取值：字符串。
  * "attck_sound"。含义：单位发出攻击的声音资源。取值：字符串。
  * "hurt_sound"。含义：单位受到伤害的声音资源。取值：字符串。
  * "die_sound"。含义：单位死亡的声音资源。取值：字符串。
  * "body_scale"。含义：单位身体和影子缩放比例。取值：浮点数。默认值：1.f。
  * "effect_scale"。含义：单位绑定的法术特效的缩放比例。取值：浮点数。默认值：1.f。
  * "body_effect_pos_x"。含义：身体特效的绑定位置的x坐标。取值：浮点数；相对锚点的像素值。
  * "body_effect_pos_y"。含义：身体特效的绑定位置的y坐标。取值：浮点数；相对锚点的像素值。
  * "head_effect_pos_x"。含义：头顶特效的绑定位置的x坐标。取值：浮点数；相对锚点的像素值。
  * "head_effect_pos_y"。含义：头顶特效的绑定位置的y坐标。取值：浮点数；相对锚点的像素值。
  * "hp_bar_pos_x"。含义：血条的绑定位置的x坐标。取值：浮点数；相对锚点的像素值。
  * "hp_bar_pos_y"。含义：血条的绑定位置的y坐标。取值：浮点数；相对锚点的像素值。
  * "hp_bar_scale_x"。含义：血条的缩放比例。取值：浮点数。默认值：1.f。


# BulletResourceConfig.xml

子弹资源配置表，每个标签表示一种子弹的资源配置

  * "render_key"。含义：子弹资源的名字。取值：字符串；key值。
  * "resource"。含义：子弹本体的资源文件。取值：字符串。
  * "shadow_resource"。含义：子弹影子的资源文件。取值：字符串。
  * "explode_resource"。含义：子弹爆炸的资源文件。取值：字符串。
  * "explode_sound"。含义：子弹爆炸声音的资源文件。取值：字符串。


# SpellConfig.xml

法术效果资源配置表，每个标签表示一种法术效果的资源配置。

  * "render_key"。含义：法术资源的名字。取值：字符串；key值。
  * "spell_direction"。含义：法术资源的朝向。取值：0表示没有朝向，1表示向左，2表示向右。
  * "spell_position"。含义：法术资源的绑定位置。取值：0表示脚下，1表示身体，2表示头顶。
  * "spell_render_layer"。含义：法术资源的绘制层级。取值：0表示地面，1表示影子，2表示陆地脚下，3表示陆地，4表示空中脚下，5表示空中。
  * "spell_height"。含义：法术资源的绘制高度。取值：整数；地图最小单位。
  * "loop"。含义：法术资源十分为循环动画。取值：布尔值。默认值：1。
  * "foreground_resource"。含义：法术效果的前景资源。取值：字符串。
  * "background_resource"。含义：法术效果的背景资源。取值：字符串。
  * "effect_sound"。含义：法术效果的声音资源。取值：字符串。
