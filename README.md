# 前端项目规范

本规范结合团队开发经验总结提炼而成，旨在增强团队开发协作、提高代码质量和开发效率。

<!--### Emoji图标指引-->

<!--> ⭐️表示一定要遵守的内容-->

### 目录
- [开发环境](#1-开发环境)
    - [系统环境](#11-系统环境)
    - [VS Code环境](#12-vs-code环境)
- [项目规范](#2-项目规范)
    - [项目结构](#21-项目结构)
    - [命名](#22-命名)
    - [其他](#23-其他)
- [代码风格](#3-代码风格)
    - [JavaScript](#31-javascript)
    - [HTML](#32-htmlcss)
    - [CSS](#33-csssass)
    - [Vue](#34-vue)

## 1. 开发环境

### 1.1 系统环境

- nodejs版本保持v8.x以上，若项目中的`package.json` -> [engines](https://docs.npmjs.com/files/package.json#engines)有对node版本的要求，则按该要求切换版本。

    > 安装[nvm](https://github.com/creationix/nvm)(Mac)或[n](https://github.com/tj/n)(Windows)进行nodejs版本切换。
    
    > 如在安装过node_modules后切换版本，node-sass在编译的时候回报错，可运行`npm rebuild node-sass`解决

### 1.2 VS Code环境

⭐️必备插件：
- Vetur

    <details>
    <summary>Vetur配置推荐</summary>
    
    ```javascript
    {
        "vetur": {
            "format": {
                // 默认格式化插件配置
                "defaultFormatter": {
                    "html": "js-beautify-html",
                    "css": "prettier",
                    "postcss": "prettier",
                    "scss": "prettier",
                    "less": "prettier",
                    "js": "prettier",
                    "ts": "prettier"
                },
                "defaultFormatterOptions": {
                    "js-beautify-html": {
                        // 格式化时强制属性断行
                        "wrap_attributes": "force-aligned"
                    }
                }
            }
        },
    }
    ```
    </details>
- ESLint 开启保存时自动修改

    <details>
    <summary>ESLint配置推荐</summary>
    
    ```javascript
    {
        // An array of language ids which should be validated by ESLint
        "eslint.validate": [{ //list of extensions to validate
                "language": "html",
                "autoFix": true
            },
            {
                "language": "vue",
                "autoFix": true //Autofix any fixable errors when linting
            },
            {
                "language": "javascript",
                "autoFix": true
            },
            {
                "language": "javascriptreact",
                "autoFix": true
            }
        ],
        // 保存时自动修复
        "eslint.autoFixOnSave": true,
    }
    ```
    </details>
    
- prettier 格式化代码插件

    <details>
    <summary>prettier配置推荐</summary>
    
    ```javascript
    {
        "prettier": {
            // 使用单引号
            "singleQuote": true,
            // 行尾不加分号
            "semi": false,
            // 缩进用两个空格
            "tabWidth": 2,
            "eslintIntegration": "prettier-eslint"
        },
    }
    ```
    </details>

推荐插件：
- Better Comments 优化注释体验
- Code Runner 直接在编辑时运行代码
- GitLens git增强工具

⭐️ESLint检查出的错误一定要处理

## 2. 项目规范

### 2.1 项目结构

- 请围绕产品功能/页面/组件，而不是围绕角色来组织文件。

    **不规范**
    ```
    .
    ├── controllers
    |   ├── product.js
    |   └── user.js
    ├── models
    |   ├── product.js
    |   └── user.js
    ```
    
    **规范**
    
    ```
    .
    ├── product
    |   ├── index.js
    |   ├── product.js
    |   └── product.test.js
    ├── user
    |   ├── index.js
    |   ├── user.js
    |   
    ```
    
- 通用的工具方法放在`@/utils`目录内。

    > utils内只放和业务逻辑无关的公共方法
    
    > 只在某组件内或业务目录内公用的方法，不应放在此目录，应放在业务目录内
    
- ⭐️只在某个业务功能中通用的组件/样式/配置/mixin，放在该业务目录下，不应放在外层。


### 2.2 命名

- 文件名和目录名使用中划线连接（like-this）。
- 变量和方法命名使用驼峰命名（camelCase）
- className使用中划线命名 [常用命名推荐](https://guide.aotu.io/docs/name/classname.html#%E5%B8%B8%E7%94%A8%E5%91%BD%E5%90%8D%E6%8E%A8%E8%8D%90)


### 2.3 其他

- 单文件代码超过500行，或单方法代码超过80行，建议检查是否可精简、拆分。


## 3. 代码风格

### 3.1 JavaScript
- JS使用[JavaScript Standard Style](https://standardjs.com/rules-zhcn.html#javascript-standard-style)，并使用ESLint代码检查
- Vue新建项目时选择`ESLint + Standard config`，配合VS Code的ESLint插件，保存时自动格式化
- 普通项目在命令行输入`eslint --init`初始化`.eslintrc`文件
- 随着代码的变化，始终保持注释的相关性。删除那些注释掉的代码块。
- 使用有意义容易搜索的命名，避免缩写名称。对于函数使用长描述性命名。功能命名应该是一个动词或动词短语，需要能清楚传达意图的命名。
    - 如果函数返回布尔值，可以`can`、`has`、`is`开头，比如`canRead`、`isValid`等。
    - 如果获取或者设置某个值，可以`get`、`set`开头，比如`getData`、`setName`
    - 常量名全部大写
    - 构造函数首字母大写
    - 禁止下划线和驼峰混合命名
- 善用注释

    > 注释是你自己与你的小伙伴们了解代码写法和目的的唯一途径。特别是在写一些看似琐碎的无关紧要的代码时，由于记忆点不深刻，注释就变得尤为重要了。
    
    > 注释的目的：提高代码的可读性，从而提高代码的可维护性
    
    > 注释的原则：如无必要，勿增注释；如有必要，尽量详尽
    
    - 关键函数要加多行注释，解释用途、参数、返回值。
    - 遇到实现特殊功能或者解决怪异问题的地方，建议在注释中写明代码这么写的原因。
    

### 3.2 HTML

- 参考[编码规范 by @mdo](https://codeguide.bootcss.com)
- 标签中统一使用双引号，等号两侧不能有空格

### 3.3 CSS/SASS

- 注释参考[在 css 中什么是好的注释？](http://web.jobbole.com/94046/)
- 注意避免自己写的样式污染全局样式
    > 在Vue中使用`scoped`或嵌套最外层以当前模块命名，或使用[BEM命名约定](https://github.com/Tencent/tmt-workflow/wiki/%E2%92%9B-%5B%E8%A7%84%E8%8C%83%5D--CSS-BEM-%E4%B9%A6%E5%86%99%E8%A7%84%E8%8C%83)
- className使用中划线命名，id使用驼峰命名，id禁止在样式表中使用，css一律使用class定义
- 尽量减少class的嵌套层级，嵌套最多不能超过5层


### 3.4 Vue

⭐️遵守官方[Style Guide](https://vue.docschina.org/v2/style-guide/)

## 4. 测试（完善中）

## 5. 部署（完善中）


#### 参考：

- [Aotu.io](https://guide.aotu.io/index.html)
- [https://codeguide.bootcss.com/#css-classes](https://codeguide.bootcss.com/#css-classes)
- [elsewhencode/project-guidelines](https://github.com/elsewhencode/project-guidelines/blob/master/README-zh.md)
- [https://segmentfault.com/a/1190000000502593](https://segmentfault.com/a/1190000000502593)
- [https://my.oschina.net/yunqi/blog/1802300](https://my.oschina.net/yunqi/blog/1802300)
- [http://web.jobbole.com/94046/](http://web.jobbole.com/94046/)