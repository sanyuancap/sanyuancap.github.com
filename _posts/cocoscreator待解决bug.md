1. 复制粘贴结点后，顺序会打乱
    cocoscreator v2.0.8和v2.1.0都存在这个问题，当一次性复制多个父节点（父节点a和b，a的zorder在b的下方），并且粘贴，会存在粘贴后的父节点，a的zorder变成了b的上方，顺序会倒序排列。

2. 点击绑定控件后，不能直接跳转（不方便操作）
    点击属性检查器，只会显示当前可见区域内的控件可以高亮，但是如果该控件不在可见区域内，不能直接跳转。

3. 编辑器设置大于代码读取：例如设置字体颜色，

4. label 向上对齐时被切

vivo Y66 6.0.1版本，只有在这个版本下，label坐标错乱。其余版本正常显示


5. render-engine.js

performance warning: clear called with no buffers in bitmask

WebGL:too many errors, no more errors will be reported to the console for this context.


