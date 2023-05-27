# vue项目 Eslint + Prettier

参考: [Vue eslint规则](https://github.com/vuejs/eslint-config-vue)，[eslint文档](https://eslint.org/docs/latest/rules/)，[eslint中文文档](https://zh-hans.eslint.org/)

## 依赖安装

`npm i -D prettier eslint eslint-plugin-vue @vue/eslint-config-prettier @vue/eslint-config-typescript`

- `Prettier` 的作用是格式化代码风格，后续加上 VS Code 的 Prettier 插件，可以在保存代码时候，自动格式化代码风格
- `eslint` 是 ESLint 的核心模块，包括 CLI 命令工具
- `eslint-plugin-vue` 是 ESLint 的 Vue.js 语法插件，主要用于检查 Vue 代码文件语法
- `@vue/eslint-config-prettier` 是 ESLint 的 Prettier 配置，主要是联动 Prettier 进行代码规范的格式化
- `@vue/eslint-config-typescript` 是 ESLint 的 TypeScript 配置，主要是检查 Vue.js 项目中的 TypeScript 语法`(项目若未用到Ts语法，则无需安装)`

## 设置 ESlint 配置文件

``` eslint
 off: 关闭规则 0
 warn: 将规则作为警告打开（不影响退出代码） 1
 error: 将规则作为错误打开（触发时退出代码为1）2
```

- 在项目根目录下新建文件，命名为 .eslintrc

``` vue config
module.exports = {
  root: true, # 标识当前配置文件为eslint的根配置文件, 让其停止在父级目录中继续寻找
  env: { # 环境提供预定义的全局变量
    browser: true, # 浏览器全局变量
    es2021: true, # 添加所有ECMAScript 2021 全局变量，并将解析器选项设置为12
    node: true, # nodejs 全局变量和nodejs 作用域
  },
  plugins: ['prettier'], # 配置插件 添加扩展 可省略eslint-plugin-
  extends: [ # 扩展eslint配置
    'plugin:vue/vue3-essential',
    'plugin:prettier/recommended',
    'eslint:recommended',
    '@vue/eslint-config-typescript/recommended',
    '@vue/eslint-config-prettier'

  ],
  parserOptions: {
    ecmaVersion: 'latest', # 设置ECMAScript版本为最新
    sourceType: 'module', # 设置为 （默认） 为'script'|'module' (如果你的的代码在 ECMAScript 模块中)
    ecmaFeatures: {
      jsx: true # 支持jsx
    }
  },
  globals: { # 设置全局变量，若某个全局变量中没有该属性，ESLint就会报错，此时需要往此处添加要辨别的变量  readonly/false——只读 writable/true——可写 off——禁用该全局变量
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly'
  },
  rules: { # 自定义配置项规则
    'vue/multi-word-component-names': 'off', # 关闭eslint检查文件名是否为驼峰命名
    'arrow-spacing': [2, { # 箭头函数中，强制箭头保持一致的间距
      'before': true, 
      'after': true
    }],
    'block-spacing': [2, 'always'], # 在开始之后和结束之前添加空格
    'brace-style': [2, '1tbs', {
      'allowSingleLine': true # 强制一致的大括号样式
    }],
    'camelcase': [0, {
      'properties': 'always' # 驼峰命名规则
    }],
    'comma-dangle': [2, 'never'], # 禁止尾随逗号
    'comma-spacing': [2, { # 逗号前后空格设置
      'before': false, # 不允许逗号前的空格
      'after': true # 逗号后需要有一个空格
    }],
    'comma-style': [2, 'last'], # 一致的逗号样式,在数组元素、对象属性或变量声明之后和同一行上使用逗号
    'curly': [2, 'multi-line'], # 所有控制语句强制一致的大括号样式
    'eqeqeq': ['error', 'always', { 'null': 'ignore' }], # 使用全等判断
    'no-unused-vars': [2, { # 禁止使用未使用的变量
      'vars': 'all',
      'args': 'none'
    }],
    'semi': [2, 'never'], # 禁止末尾分号
    'semi-spacing': [2, { # 设置分号前后间隔
      'before': false,
      'after': true
    }],
    'no-console': 'error' # 禁用console
  },
}

```

## 设置.eslintignore 文件

- 在项目根目录下新建文件，命名为 .eslintignore

```eslintignore
public
dist
*.d.ts
/src/assets
package.json
```

## 设置 Prettier 配置文件

- 在项目根目录下新建文件，命名为 .prettierrc.js

```config
module.exports = {
  "tabWidth": 2,
  "useTabs": false,
  "endOfLine": "auto",
  "singleQuote": true,
  "jsxSingleQuote": true,
  "semi": false,
  "trailingComma": "none",
  "bracketSpacing": true
}
```

## vscode 插件下载

`下载5个插件:`

<!-- - `Vue.volar` Vue 3 官方推荐的 VS Code 开发插件
- `Vue.vscode-typescript-vue-plugin` Vue 3 TypeScript 语法辅助 VS Code 插件
- `dbaeumer.vscode-eslint` ESLint 的 VS Code 插件
- `esbenp.prettier-vscode` Prettier 的 VS Code 插件
- `rvest.vs-code-prettier-eslint` ESLint 联动 Prettier 的 VS Code 插件 -->

- 在项目根目录下新建文件夹.vscode文件夹, 新建extensions.json

```vscode
{
  "recommendations": [
    "Vue.volar",
    "Vue.vscode-typescript-vue-plugin",
    "rvest.vs-code-prettier-eslint",
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode"
  ]
}
```

保存之后若有插件未安装, `vscode`会提醒安装插件

`配置 VS Code 的项目本地配置文件 .vscode/settings.json` 文件 => 首选项 => 设置 => setting.json

```config
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
},
"editor.formatOnSave": true,
"eslint.format.enable": true,
"prettier.configPath": ".prettierrc.js",
"[typescript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[typescriptreact]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[vue]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
```

## Eslint 检查代码问题

`npm run lint`

``` script

{
   "scripts": {
    "lint:eslint": "eslint --cache --max-warnings 0  \"{src,mock,build}/**/*.{vue,js,ts,tsx}\" --fix",
    "lint:prettier": "prettier --write  \"src/**/*.{js,ts,json,tsx,css,scss,vue,html,md}\"",
    "lint": "npm run lint:eslint && npm run lint:prettier --fix"
   }
 }

```

`.gitignore` 添加.eslintcache

## 取消eslint校验(不推荐取消)

找到 `vite.config.js | vue.config.js` 文件。 进行如下设置 `lintOnSave: false` 即可
