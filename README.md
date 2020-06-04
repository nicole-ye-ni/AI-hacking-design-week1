# 读书笔记及架构图
论文选择：Automatic Design of Colors for Magazine Covers
***

### 杂志封面设计中颜色应用的两个方面：
Harmony（geometric structure for text color）  
Semantics（text color selection for specific cover images）  

### 参考的颜色理论（摘要）：
#### Color harmony  
+ Itten: complementary contrast concept
+ Matsuda: hue and tone template

#### Color semantics
+ Kobayashi:   
  Color Image Scale;  
  3-color combination;  
  hue, value, chroma → soft, hard & cold, warm;   
  descriptor-adjective
  
### 应用- 封面文字配色
#### 阶段一：根据颜色互补规则来选取标题颜色
+ 根据设计师的直觉修改色轮
+ 把底图从sRGB空间转换到HSV空间，计算底图的颜色直方图
+ 选取直方图中最高频率颜色的相反颜色作为masthead颜色（在修改的色轮上选取）
+ 根据Matsuda提出的V和Y模型选择两种masthead临近颜色作为其他标题的颜色
#### 阶段二：根据易读性规则来修改标题颜色
+ 转换到CIELab颜色空间，比较文字和背景的lightness
+ 如果lightness相近（有一个shreshold），则替换颜色，否则保持不变
+ 如果替换颜色，进一步评估背景的lightness是否高于某个值，来确定颜色替换成黑或白
### 应用- 根据语义对应的颜色组合选择封面图片
+ 把RGB颜色切分成8\*8\*8=512块
+ 从RGB颜色空间通过变换得到Kobayashi直方图
+ 计算所有三色组合（来自Kobayashi，130种基础色构成1170种组合）在Kobayashi直方图中的分布
+ 将1170种组合对应到180种labels
+ 将180种labels对应到15种templates
+ 最后根据label的位置得出给定image在Kobayashi's Color Image Scale中的位置

-------------
### 架构图
![架构图](https://github.com/nicole-ye-ni/AI-hacking-design-week1/blob/master/%E6%9E%B6%E6%9E%84%E5%9B%BE1.jpg)

--------------
### 个人观点
+ 语义（semantics）和格调（color moods）只作用于封面底图的选择，而没有影响标题配色的选择吗？是否可以增加语义影响标题配色这一功能？
+ Figure 3.a的流程图中，似乎只照顾到了masthead的legibility，因为只有masthead的颜色修改是严格对照对masthead所在背景的色调和明度进行的。
