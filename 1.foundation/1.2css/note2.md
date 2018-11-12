# 一些css样式及其属性值
**
当父元素的高度是靠子元素撑开的时候，子元素浮动时，则在父元素使用overflow: hidden可以清除浮动，使得父元素的高度依旧是靠子元素撑开。
当父元素自身设置了height属性值，则在父元素使用overflow: hidden可以使子元素超出父元素的那部分隐藏。**  
## 定位Positioning  
1. position  
  * 适用于除display属性定义为table-column-group | table-column之外的所有元素
  * -static<默认值>对象遵循常规流。此时4个定位偏移属性不会被应用
  * -relative 对象遵循常规流，并且参照自身在常规流中的位置通过top，right，bottom，left这4个定位偏移属性进行偏移时不会影响常规流中的任何元素。
  * -absolute 对象脱离常规流，此时偏移属性参照的是离自身最近的定位祖先元素，如果没有定位的祖先元素，则一直回溯到body元素。盒子的偏移位置不影响常规流中的任何元素，其margin不与其他任何margin折叠。
  * -fixed 与absolute一致，但偏移定位是以窗口为参考。当出现滚动条时，对象不会随着滚动。
  * -center 与absolute一致，但偏移定位是以定位祖先元素的中心点为参考。盒子在其包含容器垂直水平居中。（CSS3）
  * -page 与absolute一致。元素在分页媒体或者区域块内，元素的包含块始终是初始包含块，否则取决于每个absolute模式。（CSS3）
  * -sticky  对象在常态时遵循常规流。它就像是relative和fixed的合体，当在屏幕中时按常规流排版，当卷动到屏幕外时则表现如fixed。该属性的表现是现实中你见到的吸附效果。（CSS3）
  * 说明：
            1,检索对象的定位方式。
            2,当position的值为非static时，其层叠级别通过z-index属性定义。
            3,绝对定位的元素，在top，right，bottom，left属性未设置时，会紧随在其前面的兄弟元素之后，但在位置上不影响常规流中的任何元素.
2. z-index：auto | <integer>
  * 适用于：定位元素。即定义了position为非static的元素
3. top: auto | <length:用长度值来定义距离顶部的偏移量。可以为负值> | <percentage:用百分比来定义距离顶部的偏移量。百分比参照包含块的高度。可以为负值。>
  * 适用于：定位元素。即定义了position为非static的元素
4. right auto | < length> | < percentage>
  * 适用于：定位元素。即定义了 <' position '> 为「非static」的元素
5. bottom auto | < length> | < percentage>
6. left 同上,
7. clip auto<对象无剪切> | < shape :rect(< number>|auto <number>|auto <number>|auto <number>|auto)>   
  * 适用于：绝对定位元素
  * 依据上-右-下-左的顺序提供自对象左上角为(0,0)坐标计算的四个偏移数值，其中任一数值都可用auto替换，即此边不剪切。
  * 上-左 方位的裁剪：从0开始剪裁直到设定值，即 上-左 方位的auto值等同于0；
  * 右-下 方位的裁剪：从设定值开始剪裁直到最右边和最下边，即 右-下 方位的auto值为盒子的实际宽度和高度；
  * 示例：clip:rect(auto 50px 20px auto)
  * 解释：上边不剪切，右边从左起第50个像素开始剪切直至最右边，下边从上起第20个像素开始剪切直至最底部，左边不剪切
  * 说明：
          1，检索或设置对象的可视区域。区域外的部分是透明的。
          2，这个属性将被废弃，推荐使用 clip-path 代替，在过渡阶段，仍然会存在一段时间。
          3，必须将position的值设为absolute或者fixed，此属性方可使用。  

## 布局Layout  
1. display 
* 适用于：所有元素
  *         -none  隐藏对象。与visibility属性的hidden值不同，其不为被隐藏的对象保留物理空间
           -inline <默认值>指定对象为内联元素  内联元素与前后的元素在一行上
           -block  指定对象为块元素
           -list-item 指定对象为列表项目
           -inline-block 指定对象为内联块元素 css2
           -table  指定对象为块元素的表格，类同HTML标签<table> css2
           -inline-table  指定对象作为内联元素级的表格。类同于HTML的<table> css2
           -table-caption   指定对象作为表格标题。类似于HTML的<caption>标签
           -table-cell   指定对象作为表格单元格，类似于HTML的<td> css2
           -table-row   指定对象作为表格行，类同于HTML<tr> css2
           -table-row-group   指定对象作为表格行，类同于HTML标签<tbody> css2
           -table-column    指定对象作为表格列。类同于HTML标签<col> css2
           -table-column-group  指定对象作为表格行组。类同于HTML标签<colgroup>。
           -table-footer-group   指定对象作为表格角注组。类似与<tfoot> css2
           -table-header-group  指定对象作为表格标题组。类似于HTML<thead> css2
           -run-in  更据上下文决定对象时内联对象还是块级对象。CSS3 
           -box   将对象最为弹性伸缩盒显示。（伸缩盒最老版本）CSS3
           -inline-box 将对象作为内联块级弹性伸缩盒显示。 伸缩盒过度版本 c3
           -flexbox   将对象作为弹性伸缩盒显示。 过度版本 c3
           -inline-flexbox  将对象做为内联块级弹性伸缩盒显示。 C3
           -flex 将对象作为弹性伸缩盒显示 新版 c3
           -inline-flex 将对象作为内联弹性块级伸缩盒显示 cs3
       说明：
           1，如果display设置为none，float、position属性定义将不生效。
           2，如果position既不是static也不是relative或者float不是none或者是根元素，当display：inline-table时，display的计算值为table。当display：inline|inline-block|run-in|table-*时，display计算值为block，其他情况为指定值。

2. float： none<默认，设置对象不浮动> | left<设置对象浮在左边> |right<浮在右边>
   * 适用于：所有元素
   * 说明：
            1，如果该属性的值指出了对象时否及如何浮动。请看clear属性
            2，如果float不是none，当display：inline-table时，display的计算值为table；当display:inline | inline-block | run-in | table-* 系时，display的计算值为block，其它情况为指定值；
            float在绝对定位和display为none时不生效

3. clear： none<默认，允许两边都可以有浮动对象> | left<不允许左边有浮动对象> | right |both<两边都不允许>
     * 适用于：块级元素
     * 说明：
            该属性的值指出了不允许有浮动对象的边。

4. visibility:  visible<默认，设置对象可视> | hidden<设置对象隐藏> | collapse<坍方，倒塌。主要用来隐藏表格的行或列。隐藏的行或列能够被其他内容使用。对于表格外的其他对象，其作用相当于hidden>
        说明：
            设置或检索是否显示对象。与display属性不同，此属性为隐藏的对象保留其占据的物理空间。

6. overflow :<overflow-style>
   *  适用于：块容器，伸缩盒容器，grid容器。
   *         -visible： 对溢出内容不做处理，内容可能会超出容器
            -hidden    隐藏溢出容器的内容且不出现滚动条
            -scroll     隐藏溢出容器的内容，溢出的内容将以卷动滚动条的方式呈现
            -auto      当内容没有溢出容器时不出现滚动条，当内容溢出容器时出现滚动条，按需出现滚动条。此为body对象和textarea的默认值。
            -paged-x
            -paged-y
            -paged-x-controls
            -paged-y-controls
            -fragments 
          说明：
             复合属性。检索或者设置对象处理溢出内容的方式。请参阅overflow-x、overflow-y属性
             overflow的效果等同于overflow-x + overflow-y 
             对于table来说，假如table-layout属性设置为fixed，则td对象支持带有默认值为hidden的overflow属性。如果设为hidden，scroll或者auto，
                  那么超出td尺寸的内容将被剪切。如果设为visible，将导致额外的文本溢出到右边或左边（视direction属性设置而定）的单元格。
   
7. overflow-x :同上  
        说明：检索或设置对象处理横向溢出内容的方式。

8. overflow-y ：同上
         说明：检索或设置对象处理纵向溢出内容的方式。
         
## 伸缩盒（Flexible Box 新）  
1. flex： none | <'flex-grow'><'flex-shrink'>?||<'flex-basis'> 
  * 适用于：flex子项
    *        -none：none关键字的计算值为 0 0 auto
              -<'flex-grow'>  用来指定扩展比率，即剩余空间是正值时此[flex子项]相对于[flex容器]里其他[flex子项]能分配到空间的比例，在[flex]属性中该值如果被省略则默认为[0]。
              -<'flex-shrink'> 用来指定收缩比率，即剩余空间是负值时此[flex子项]相对于[flex容器]里的其他[flex子项]能收缩的空间比例。在收缩的时候收缩比率会以收缩基准值加权，在收缩[flex]属性中该值如果被省略则默认为1.
               -<'flex-basis'>  用来指定伸缩基准值，即在根据伸缩比率计算出剩余空间的分布之前，[flex子项]长度的起始数值。在[flex]属性中该值如果被省略则默认为[0%];在[flex属性]中该值如果被指定为[auto],则伸缩基准值的计算是自身的<'width'>设置，如果自身的宽度没有定义，则长度取决于内容。
            说明：
              复合属性。设置或检索弹性盒模型对象的子元素如何分配空间。
                如果缩写[flex:1],则其计算值为[1 1 0%]
                如果缩写[flex:auto]，则其计算值为[1 1 auto]
               如果[flex:none],则其计算值为[0 0 auto]
               如果[flex:0 auto]或者[flex:initial] ,则其计算值为[0 1 auto],即[flex]初始值

2. flex-grow：<number：用数值类定义扩展比率，不允许负值>
   * 默认值是0，适用于flex子项。如果没有显示定义该属性，是不会拥有分配剩余空间权利的。
     *       说明：
                设置会检索弹性盒的扩展比率。更据弹性盒子元素锁设置的扩展因子作为比率来分配剩余空间。

3. flex-shrink ：<number：用数值类定义收缩比率，不允许负值>
    * 默认值是1，适用于flex子项。如果没有显示定义该属性，将会自动按照默认值1在所有因子相加之后计算比率进行空间压缩。
      *      说明：
                设置弹性盒子元素锁设置的收缩因子作为比率来收缩空间。
        
4. flex-basis ：<length ：用长度来定义宽度，不允许负值> | <percentage 用百分比来定义宽度，不允许为负> | auto ：无特定宽度值，取决于其他属性值 | content 基于内容自动计算宽度
  *  默认值：auto 适用于：flex子项
     *       说明：
               设置或检索弹性盒伸缩基准值。
               如果所有子元素的基准值之和大于剩余空间，则会根据每项设置的基准值，按比率伸缩剩余空间

5. flex-flow   <'flex-direction' :定义弹性盒子元素的排列方向> || <'flex-wrap' ： 控制flex容器时单行或者多行>
   *  默认值：看各分拆属性，适用于flex容器
     *         说明：
                  复合属性。设置或检索弹性盒模型对象的子元素排列方式

6. flex-direction ： row | row—reverse | column | column-row—reverse
   *  默认值：row 适用性：flex容器
      *         -row：主轴与行内轴方向作为默认的书写模式。即横向从左到右排列（左对齐）
               -row-reverse：对齐方式与row相反
               -column：主轴与块轴方向作为默认的书写方式。即纵轴向从上往下排列（顶对齐）
               -column-reverse： 对齐方式与column相反
             说明：
                该属性通过定义flex容器的主轴方向来决定flex子项在flex容器中的位置。这将决定flex需要如何进行排列
                该属性的反转取值不影响元素的绘制，语音和导航顺序，只改变流动方向。这与<writing-mode>和<direction>相同
         flex生效需定义<display>为flex或者inline-flex（box或inline-box这是旧的方式）
    
7. flex-wrap ：nowrap | wrap | wrap-reverse
   *  默认值：nowrap 适用于：flex容器
     *          -nowrap：flex容器为单行，该情况下flex子项可能会溢出容器。
               -wrap：flex容器为多行
               -wrap-reverse：反转wrap排列
               说明：
                 该属性控制flex容器时单行或者多行，同时横轴的方向决定了新行堆叠的方向。

8. align-content  flex-start | flex-end | center | space-between |space-around | stretch <伸展，延伸>
    * 默认值：stretch  
       *        -flex-start：各行向弹性盒容器的起始位置堆叠。弹性盒容器中第一行的侧轴起始边界紧靠该弹性盒容器的侧轴起始边界，之后的每一行都紧靠住前一行。
               -flex-end： 各行弹性盒容器的结束位置堆叠。弹性盒容器中最后一行的侧轴起结束界紧靠住该弹性盒容器的侧轴结束边界，之后的每一行都紧靠住前面一行。
               -center ： 各行向弹性盒容器的中间位置堆叠。各行两两紧靠住同时在弹性盒容器中居中对齐，保持弹性盒容器的侧轴起始内容边界和第一行之间的距离与该容器的侧轴结束内容边界与第最后一行之间的距离相等。（如果剩下的空间是负数，则各行会向两个方向溢出的相等距离。）
               -space-between： 各行在弹性盒容器中平均分布。如果剩余的空间是负数或弹性盒容器中只有一行，该值等效于flex-start。在其它情况下，第一行的侧轴起始边界紧靠住弹性盒容器的侧轴起始内容边界，最后一行的侧轴结束边界紧靠住弹性盒容器的侧轴结束内容边界，剩余的行则按一定方式在弹性盒窗口中排列，以保持两两之间的空间相等。
               -space-around：各弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。如果剩余空间是负数或弹性盒容器中只有一行，该值等效于center。其他情况下，各行会按照一定方式在弹性盒容器中排列，以保持两两之间的空间相等，同时第一行前面及最后一行后面的空间是其他空间的一半。
               -stretch：各行将会伸展以占用剩余空间。如果剩余空间是负数，该值等效于flex-start。在其他情况下，剩余空间被所有行平分
             说明：
                当伸缩容器的侧轴还有多余空间时。本属性可以用来调准伸缩行在伸缩容器里的对其方式。这与调准伸缩项目在主轴上对其的方式的<'justify-content'>属性类似。请注意本属性在只有一行的伸缩容器上没有效果。
                
           
9. align-items
10. align-self
11. justify-content
12. order