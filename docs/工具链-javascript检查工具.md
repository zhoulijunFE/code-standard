# 工具链-javascript检查工具

对代码进行静态检查，发现和修复不符合规范的代码。

## 代码配置
### eslint配置代码
#####  1）新增eslintrc.js文件配置

<pre>
module.exports = {
  root: true,
  env: {
    node: true,
  },
  parserOptions: {
    parser: "babel-eslint",
    sourceType: "module"
  },
  extends: [
    "standard",
    "plugin:vue/recommended"
  ],
  plugins: [
    "vue",
    "html"
  ],
  rules: {
    "generator-star-spacing": "off",
    "space-before-function-paren": "off"
  }
};
</pre>

#####  2）新增.eslintignore文件配置

<pre>
/build/
/docker/
/dist/
/elevate/
/public/
</pre>

#####  3）package.json中添加

<pre>
// 安装
 "eslint-config-standard": "^12.0.0",
 "eslint-plugin-babel": "^5.3.0",
 "eslint-plugin-html": "^5.0.3",
 "eslint-plugin-import": "^2.17.2",
 "eslint-plugin-node": "^8.0.1",
 "eslint-plugin-promise": "^4.1.1",
 "eslint-plugin-standard": "^4.0.0",
 "eslint-plugin-vue": "^5.0.0",
 "eslint-loader": "^2.1.2"
 
// scripts新增配置
"lint": "eslint --ext .js  --ext .vue src/"
执行： npm run lint 终端显示错误、警告
 
"lint": "eslint --fix --ext .js --ext .vue src/"
自动修复，提升效率
</pre>

### 通过vue-cli 添加eslint新增配置
##### package.json中添加

<pre>
// 安装
"@vue/cli-plugin-babel": "^3.6.0",
"@vue/cli-plugin-eslint": "^3.6.0",
"@vue/cli-service": "^3.6.0"
 
// scripts配置调整
"lint": "vue-cli-service lint"
</pre>

##### vue.config.js中添加

<pre>
lintOnSave: env === 'development',
每次保存时执行校验的选项是默认开启的
</pre>

## Git提交检查
使用git hook调用eslint进行代码规范验证，引入lint-staged进行增量检查， 不规范的代码无法提交到仓

##### package.json中新增配置
<pre>
// 安装
 "husky": "^3.0.8",
 "lint-staged": "9.4.2"
 
// husky配置
 "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "src/**/*": [
      "npm run lint"
    ]
  }
</pre>

## 构建检查
##### webpack.config.base.js添加构建检查
<pre>
{
  test: /\.(js|vue)$/,
  loader: 'eslint-loader',
  enforce: 'pre', // vue-loader之前处理，编译有错误vue-loader不执行
  include: [resolve('src'), resolve('test')]
}
</pre>