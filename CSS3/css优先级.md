**css优先级，可以给选择器分配权值：**

- id选择器的权值为100
- class、属性和伪类选择器的权值为10
- 标签选择器的权值为1
- 权值较大的优先级越高
- 比较样式时，将对应的选择器权值相加，大的优先级高
- 权值相同的，根据从上往下的原则，后定义的优先级高
- 特殊！important，优先级最高