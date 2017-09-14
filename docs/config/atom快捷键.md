
## atom 快捷键

### 对应关系
⌘ : Command key
⌃ : Control key
⌫ : Delete key
← : Left arrow key
→ : Right arrow key
↑ : Up arrow key
↓ : Down arrow key
⌥ : Option or Alt key
↩ : Return or Enter key
⇧ : Shift key

### 编辑器
+ ctrl-shift-p 打开命令行
+ ctrl-n 新开文件页面
+ ctrl-shift-n 新开编辑器页面
+ ctrl-w 关闭当前文件
+ ctrl-shift-w 关闭编辑器
+ ctrl-a 全选当前文件
+ ctrl-\ 隐藏目录树
+ ctrl-tab 切换标签
### 编辑行
+ ↑ + enter 向下打开一行
+ ↑ + ⌘ +enter 向上打开一行
+ ctrl-up/down 选中行上/下移
+ ctrl-/ 注释行
+ ctrl-shift-d 复制行
+ ⌘ + d 删除行
+ shift-up/down 选中行向上/下
+ ctrl-j 行与后面行合并

+ ⌥ + ⇧ + ↑/↓  多行光标选中
### 编辑字段
+ ctrl-d 匹配下一个
+ ctrl-shift-f 全局替换
### 文件
+ ctrl-b 最近打开的文件
+ ctrl-t/p 查找项目中文件
+ ctrl-o 打开文件
+ ctrl-shift-o 打开文件夹
### 保存
+ ctrl-s 保存
+ ctrl-shift-s 另存为


## keymap.CSON
> 'atom-text-editor':
  'cmd-d': 'editor:delete-line'
  'ctrl-d': 'editor:duplicate-lines'
  'shift-enter': 'editor:newline-below'
  'shift-cmd-enter': 'editor:newline-above'
  'shift-cmd-down': 'editor:move-line-down'
  'shift-cmd-up': 'editor:move-line-up'
  'ctrl-/': 'editor:toggle-line-comments'
  'alt-shift-up': 'editor:add-selection-above'
  'alt-shift-down': 'editor:add-selection-below'

'body':
  'ctrl-s': 'core:save'


'atom-workspace':
  'ctrl-d': 'editor:duplicate-lines'
