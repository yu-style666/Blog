## 在 vscode 使用 eslint

#### 1. vscode 编辑器安装 `eslint` 插件

> <https://github.com/Microsoft/vscode-eslint>

#### 2. 安装 `eslint` 相关依赖（版本仅做参照）

```json
"babel-eslint": "^10.0.1",
"eslint": "^5.16.0",
"eslint-config-airbnb": "^17.1.0",
"eslint-config-prettier": "^4.1.0",
"eslint-loader": "2.1.0",
"eslint-plugin-babel": "^5.3.0",
"eslint-plugin-compat": "^3.1.1",
"eslint-plugin-import": "^2.17.2",
"eslint-plugin-jest": "^22.5.1",
"eslint-plugin-jsx-a11y": "^6.2.1",
"eslint-plugin-react": "^7.12.4",
```

#### 3. 根目录添加 `.eslintrc.js` 文件

```js
module.exports = {
  parser: "babel-eslint",
  extends: [
    "airbnb",
    "prettier",
    "plugin:compat/recommended",
    "plugin:jest/recommended",
  ],
  env: {
    browser: true,
    node: true,
    es6: true,
    mocha: true,
    jest: true,
    jasmine: true,
  },
  parserOptions: {
    ecmaFeatures: {
      experimentalObjectRestSpread: true,
      jsx: true,
      arrowFunctions: true,
      classes: true,
      modules: true,
      defaultParams: true,
    },
    sourceType: "module",
  },
  rules: {
    "import/no-extraneous-dependencies": ["error", { devDependencies: true }],
    "no-console": 0,
    "no-alert": 0,
    camelcase: 0,
    "consistent-return": 0,
    "prefer-template": 0,
    "react/sort-comp": 0,
    "no-param-reassign": ["error", { props: false }],
    "import/prefer-default-export": 0,
    "react/jsx-filename-extension": 0,
    "react/jsx-wrap-multilines": 0,
    "react/no-array-index-key": 0,
    "react/prop-types": 0,
    "react/forbid-prop-types": 0,
    "react/jsx-one-expression-per-line": 0,
    "react/no-danger": 0,
    "import/no-unresolved": [2, { ignore: ["^@/"] }],
    "import/no-cycle": 0,
    "jsx-a11y/no-noninteractive-element-interactions": 0,
    "jsx-a11y/click-events-have-key-events": 0,
    "jsx-a11y/no-static-element-interactions": 0,
    "jsx-a11y/anchor-is-valid": 0,
    "jsx-a11y/media-has-caption": 0,
    "jsx-a11y/alt-text": 0,
    "linebreak-style": 0,
    "import/extensions": 0,
  },
  overrides: [
    {
      files: ["*.test.js", "*.test.ts", "*.test.jsx", "*.test.tsx"],
      env: {
        jest: true, // now **/*.test.js files' env has both es6 *and* jest
      },
      plugins: ["jest"],
      rules: {
        "jest/no-disabled-tests": "warn",
        "jest/no-focused-tests": "error",
        "jest/no-identical-title": "error",
        "jest/prefer-to-have-length": "warn",
        "jest/valid-expect": 0,
      },
    },
  ],
  settings: {
    polyfills: ["fetch", "Promise", "promises", "url", "object-assign"],
  },
};
```

tip：若不生效，尝试重启 `vscode` 开始食用。
