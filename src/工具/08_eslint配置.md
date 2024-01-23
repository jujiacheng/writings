```JavaScript
/**
 * 规则说明见 https://cn.eslint.org/docs/rules/
 * eslint-plugin-import 规则见 https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/default.md
 *
 * "off" 或 0 - 关闭规则
 * "warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
 * "error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)
 *
 * @see prettier-rules
 * @doc https://prettier.io/docs/en/options.html
 */
module.exports = {
  env: {
    browser: true,
    node: true,
    commonjs: true,
    "jest/globals": true,
  },
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: "module",
  },
  plugins: ["react", "@typescript-eslint", "prettier", "jest", "@gw/goodwe"],
  ecmaFeatures: {
    // 箭头函数
    arrowFunctions: true,
    // 解构赋值
    destructuring: true,
    // class
    classes: true,
    // 函数默认参数
    defaultParams: true,
    // 块级作用域, let const
    blockBindings: true,
    // use module
    modules: true,
    // 属性名简写
    objectLiteralComputedProperties: true,
    // 对象字面量表达
    objectLiteralShorthandMethods: true,
    // 函数默认值
    restParams: true,
    // 展开运算符
    spread: true,
    // 是否使用for of
    forOf: true,
    // 是否使用generator
    generators: true,
    // es6的 模板字符 `xx`
    templateStrings: true,
    // function开启super
    superInFunctions: true,
    // 对象扩展
    experimentalObjectRestSpread: true,
    // 可以使用jsx
    jsx: true,
    // 是否允许return表达式，返回一个全局属性
    globalReturn: false,
    // binary
    binaryLiterals: true,
  },
  rules: {
    // 使用驼峰
    camelcase: 1,
    // 禁用为声明的变量
    "no-undef": 2,
    // 禁止扩展原生类型，比如添加Object的原型
    "no-extend-native": 2,
    // 禁止在return语句中，使用赋值
    "no-return-assign": 2,
    // 自动调整import顺序
    "import/order": 0,
    // 禁止导入未在package.json中声明的依赖，可能是父级中有声明
    "import/no-extraneous-dependencies": 0,
    // commonjs的require与esm不同，可以提供运行时的动态解析，虽然有的场景需要使用，但建议还是静态化
    "import/no-dynamic-require": 0,
    // 某些文件解析算法运行省略引用文件扩展名，此处不需要强干预
    "import/extensions": 0,
    // 导入模块是文本文件系统的模块，此处关闭，避免eslint不认识webpack alias
    "import/no-unresolved": 0,
    // 当模块只有1个导出的时候，更喜欢使用export default，而不是命名导出
    "import/prefer-default-export": 0,
    // 禁止出现未使用的变量
    "no-unused-vars": [2, { vars: "all", args: "none" }],
    // 强制generate函数中的 * 周围使用一致的空格
    "generator-star-spacing": 0,
    // 禁止使一元操作符，此处不需要禁止
    "no-plusplus": 0,
    // 要求使用命名的function表达式，此处不需要
    "func-names": 0,
    // 禁止使用console.log，某些场景可能需要console打印日志
    "no-console": 0,
    // 强制在parseInt中使用基数参数，此处可以不需要
    radix: 0,
    // 禁止正则表达式中使用控制语句，比如：/\x1f/
    "no-control-regex": 2,
    // 禁止使用continue，有些情况可能需要
    "no-continue": 0,
    // 禁止使用debugger，生产环境是不允许的，开发环境可以支持debugger
    "no-debugger": process.env.NODE_ENV === "production" ? 2 : 0,
    // 禁止对function参数进行赋值，此处不强求，会警告
    "no-param-reassign": 1,
    // 禁止标识符出现 '_'， 有时候lodash会出现，此处不强求，会警告
    "no-underscore-dangle": 1,
    // 要求require写在代码最上方，可能会先需要动态require的情况，此处给出警告
    "global-require": 1,
    // 定义变量，要求使用let, const，而不是 var
    "no-var": 2,
    // 要求所有的var，必须在作用域的顶部
    "vars-on-top": 2,
    // 优先使用对象和数组解构
    "prefer-destructuring": 1,
    // 禁止不必要的字符串字面量或模板字面量链接
    "no-useless-concat": 1,
    // 禁止声明与外层作用域同名的变量
    "no-shadow": 2,
    // 要求for in中，必须出现一个if语句，而不去过滤结果，可能出现bug，此处不需要
    "guard-for-in": 0,
    // 禁止使用特定语法，可以参考：https://cn.eslint.org/docs/rules/no-restricted-syntax
    "no-restricted-syntax": 1,
    // 强制方法必须有返回值，实际上是不一定
    "consistent-return": 0,
    // 判断相等，必须使用 === ，而不是 ==
    eqeqeq: 2,
    // 禁止出现未使用过的表达式
    "no-unused-expressions": 1,
    // 在块级作用域外访问块内的变量，是否提示
    "block-scoped-var": 1,
    // 禁止多次声明，同一个变量
    "no-redeclare": 2,
    // 强制回调函数使用箭头函数
    "prefer-arrow-callback": 1,
    // 强制数组的回调方法中，需要return
    "array-callback-return": 1,
    // 要求switch语句，需要有default分支
    "default-case": 2,
    // 禁止在循环中，出现function声明和表达式
    "no-loop-func": 2,
    // 禁止case语句落空
    "no-fallthrough": 2,
    // 禁止连接赋值，let a = b = c = 1;
    "no-multi-assign": 2,
    // 禁止 if单独出现在 else语句中，else if会更加清晰
    "no-lonely-if": 2,
    // 禁止在字符串中不规范的空格，注释除外
    "no-irregular-whitespace": 2,
    // 要求使用const声明不再修改的变量
    "prefer-const": 2,
    // 禁止不必要的转义字符
    "no-useless-escape": 2,
    // 禁用array构造函数，可以参考：https://eslint.org/docs/rules/no-array-constructor#disallow-array-constructors-no-array-constructor
    "no-array-constructor": 0,
    // 要求或禁止字面量中的方法属性简写
    "object-shorthand": 0,
    // 禁止直接调用Object.prototype内置属性
    "no-prototype-builtins": 2,
    // 禁止多层嵌套三元表达式
    "no-nested-ternary": 2,
    // 禁止对String, Number, Boolean使用new操作符，没有任何理由将这些基本类型包装成构造函数
    "no-new-wrappers": 2,
    // promise reject的原因，需要通过Error对象包装
    "prefer-promise-reject-errors": 1,
    // 禁止使用label语句
    "no-labels": 2,
    // 格式化
    "prettier/prettier": 2,
    // jest no disabled
    "jest/no-disabled-tests": 1,
    // jest no focus
    "jest/no-focused-tests": 2,
    // jest no identical
    "jest/no-identical-title": 2,
    // jest prefer have
    "jest/prefer-to-have-length": 1,
    // jest expect
    "jest/valid-expect": 2,
    // 关闭eslint rule，使用下面一个rule {@link https://stackoverflow.com/questions/63818415/react-was-used-before-it-was-defined}
    "no-use-before-define": 0,
    // 禁止在定义变量之前使用变量
    "@typescript-eslint/no-use-before-define": 2,
    "@gw/goodwe/no-use-params": 2,
  },
};
```