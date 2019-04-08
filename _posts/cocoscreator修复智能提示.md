官方自动生成的creator.d.ts 文件存在一行代码与ts版本不兼容导致使用vscode编写js脚本没有自动提示

creator.d.ts 有问题代码
```
export function Class(options?: {name?: string; extends?: Function; ctor?: 
Function; __ctor__?: Function; 
properties?: any, statics?: any; mixins?: 
Function[], editor?: {executeInEditMode?: boolean; requireComponent?: 
Function; menu?: string; executionOrder?: number; disallowMultiple?: 
boolean; playOnFocus?: boolean; inspector?: string; icon?: 
string; help?: string; }; update?: Function; lateUpdate?: 
Function; onLoad?: Function; start?: Function; onEnable?: 
Function; onDisable?: Function; onDestroy?: Function; onFocusInEditor?: 
Function; onLostFocusInEditor?: Function; resetInEditor?: 
Function; onRestore?: Function; _getLocalBounds?: Function; }): 
Function;
```

将此段代码修改为如下即可恢复自动提示:
```
export function Class(options?: {name?: string; extends?: Function; ctor?: 
Function;
properties?: any, statics?: any, mixins?: 
Function[], editor?: {executeInEditMode?: boolean, requireComponent?: 
Function, menu?: string, executionOrder?: number, disallowMultiple?: 
boolean, playOnFocus?: boolean, inspector?: string, icon?: 
string, help?: string, }, update?: Function, lateUpdate?: 
Function, onLoad?: Function, start?: Function, onEnable?: 
Function, onDisable?: Function, onDestroy?: Function, onFocusInEditor?: 
Function, onLostFocusInEditor?: Function, resetInEditor?: 
Function, onRestore?: Function, _getLocalBounds?: Function, }): 
Function;
```

原因:
将;号改为,号 ,去掉生成的特殊字符不匹配 

http://www.cocoachina.com/bbs/read.php?tid-1730995.html