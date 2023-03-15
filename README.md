# React Snippets Angile Code

关注 `react` 开发中细微动作的提效工具

> 除了 `【snippets】【翻译】【AngileCode】`模块，`【组件提示】【className提示】` 依赖 `.angilecoderc` 或者自定义的 JSON 配置文件.

## 内置的 `snippets`

一些常用的代码可以用内置的命令调用出来，节约时间，开箱即用

> [内置的 snippets 原作者地址 vscode-react-typescript-boilerplate](https://github.com/Magssch/vscode-react-typescript-boilerplate)

1. acreact
   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/acreact.gif)
2. acreactprops
   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/acreactprops.gif)
3. acstate
   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/acstate.gif)
4. aceffect
   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/aceffect.gif)
5. acmodule
   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/acmodule.gif)

## 内置的 `翻译`

单词想不起来，命名又不想用 a1 b2 ? 那 `AngileCode的 翻译`适合你

> 翻译采用 **有道翻译【默认】 -（暂时只支持词语，不支持长句）** 或者 **Google 翻译 -（支持长句，各种复杂句，科学上网才会生效）**

可通过 AngileCode 配置切换

选中要翻译的单词或者逗号隔开的单词，点击小图标（或者 `Cmd + F12` on macOS or `Ctrl+F12` on Windows and Linux），即可完成翻译

-   可通过设置，保留翻译前文字，多个单词默认返回驼峰命名

![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/BatchTranslation.gif)

## 内置的 `快捷结构输入`

-   通常我们在写布局时，特别使用 css module 时，在输入 className，会有以下的反复操作
    [反复删除逗号，style 属性重复书写]
    ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/className1.gif)

-   很是费时费力，有了 angileCode 现在你可以这么操作 (可以设置多个类名)
    ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/classNameAngileCode.gif)

-   还可以通过设置保留命名的类名，方便 `copy` 到相应的 css 位置, 当然我们还可以设置[全局 className 提示](#常用--公用-classname-配置-angilecoderc)
    ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/classNameCopyAngileCode.gif)

当然 AngileCode 还支持同级 `符号："|"`【目前只支持一级】 子父级`符号：">"` 常用的 style / attr 属性 **常用代码**
![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/sonattr.gif)

-   如果你没有使用 `css module` 的习惯，可以在配置中关闭 `style.` 这种形式命名
    ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/closeModuleStyle.gif)

```javascript
// 快捷属性输入
div(attr=`ariahidden: "2", className:'test'`)
// 快捷style输入
div(style={{color: 'red', fontSize: 14}}).classname

// 常用布局
div().flexclass.attrclass > div().nodeleft | div(style={{color: 'red'}}).noderight

div().textRequired > div(attr=`ariahidden: "2", className:'test'`) | div(style={{color: 'red'}}).right

div().item > 属性：| b(style={{color: 'red'}}).sd > {}
```

## 以下是通过配置 `.angilecoderc` 或者自定义文件路径 获取的功能

> Tips： `${1:内容}` 理解为光标所在的第一个位置，内容可为空，不为空说明当前内容可全部被替换 **(可设置多个)**，`${2:内容}` 为按下 tab 键的第二个位置 **(可设置多个)**，以此类推`${n+:内容}`

数据结构要求如下

```typescript
interface IDescribe {
    // 可选项
    options: string[];
    // 描述
    description: string;
    // 传参类型
    parameterType: string;
    // 默认值
    defaultValue: string;
}

interface IAttributes {
    [AttributesName: string]: IDescribe;
}

interface IComponentParametersItem {
    // 是否是代码片段 目前仅支持 < 开头【组件类型】
    snippet?: Boolean;
    // 描述
    description: string;
    // 默认属性
    defaults?: string[];
    // 子集 字符串
    content?: string;
    // 类型集合
    attributes?: IAttributes[];
}

interface IComponentParameters {
    [componentName: string]: IComponentParametersItem;
}

interface ClassNameItem {
    // 类名
    label: string;
    // 描述
    description: string;
}

interface IComponentClassName {
    // 组件 配置
    component?: IComponentParameters;
    // classname 配置
    classname?: ClassNameItem[];
}
```

```javascript
// 示例代码 <IComponentClassName>
{
    "component": {
        // 组件名称
        "Button": {
            // 默认属性值 <?:可选参数 string[]>
            "defaults": ["type='primary'", "onClick={() => {${1:}}}"],
            // 内置的属性 <?:可选参数 [name:srting]: {}>
            "attributes": {
                "type": {
                    // 属性值 string[]
                    "options": ["primary", "dashed", "danger", "link"],
                    // 描述 string
                    "description": "设置按钮类型",
                    // 类型  string
                    "parameterType": "string",
                    // 默认值  string
                    "defaultValue": "-"
                },
                "size": {
                    "options": ["small", "large", "default"],
                    "description": "设置按钮大小",
                    "parameterType": "string",
                    "defaultValue": "default"
                }
            },
            // 组件描述 string
            "description": "按钮用于开始一个即时操作。",
            // 组件内部填充的数据 string
            "content": "这是个按钮的内容${2:}"
        },
        "表格": {
            // 设置成 true 时，自动转成 snippet, content目前仅支持 < 开头【组件类型】
            "snippet": true,
            "description": "表格",
            "content": "<Form.Item>$1</Form.Item>"
        },
        "ac-Popover": {
            "snippet": true,
            "description": "通用Table",
            "content": "<Popover content={${1:}} title=\"${2:title}\">\n    <Button type=\"primary\" onClick={() => {${3:}}}>${3:Hover me}</Button>\n  </Popover>"
        }
    },
    "classname": [
        {
            "label": "textRequired",
            "description": "文本必填项"
        },
        {
            "label": "fixAntTabletHeadThStyle",
            "description": "修改Tabal > thead 边距/背景色"
        }
    ]
}
```

## 常用 / 公用 组件配置 `.angilecoderc`

通过配置 JSON 中的 `component`，来达到快捷输入。以上述配置 JSON `component` 示例如下：

-   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/angilecodercComponent.gif)

Ac-Popover 片段 演示光标 **配合 prettier 会有很好的效果**

-   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/AcPopover.gif)

Button 片段 演示属性

-   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/ButtonAttr.gif)

## 常用 / 公用 className 配置 `.angilecoderc`

常用的 `className` 类名记不得？可通过参数配置，配合 AngileCode 输入 （"`.`"） 调用配置, 使我们拥有找公用 class 的能力

以上述配置 JSON `classname` 示例如下：

-   ![avatar](https://gitee.com/Alisa_home/angile-vscode/raw/master/images/classname.gif)

### **以上就是目前 `AngileCode` 全部内容 希望能帮助到你!**
