

## 1说明

​   原子类css用起来嘎嘎爽，像tailwindcss、unocss、windcss等构建开发小项目贼快了，uniapp项目普遍都比pc端项目小，而且要兼容多端开发的特点，项目小、快速开发的特点比较突出。

​   由于tailwindcss、unocss、windcss等在移动端的使用体验目前不太友好，比如对移动端兼容性不太好，如.w-1/2在小程序端属于特殊字符，会报错；还会存在特殊报错;再如tailwindcss的单位是rem换算其它单位复杂，但是unocss可以在配置文件种的rules种使用正则生成样式，并且改变单位，有兴趣的可以去官网看下；

​ 基于以上原因，那就自己用**最少的代码**手敲一套**原子类css**，共计约1100个左右的常用样式；

​ 关于增加1100个左右的样式会不会增加项目体积，新项目的大小约8kb,加上1100个样式后为45kb；

​ github仓库地址：[wfxt0911/atomicClass: 原子类css (github.com)](https://github.com/wfxt0911/atomicClass)

​ 如果该示例对你有启发，希望您给个**Star**

###   1.1 使用方法

都是最基础的scss，其中/src/styles/generate.scss是循环生成的样式，/src/styles/expand.scss是其它常用且无法循环生成的样式

直接在App.vue种引入即可，请注意增加*lang*="scss"属性

```vue
<style lang="scss">
/*每个页面公共css */
@import './styles/generate.scss';
@import './styles/expand.scss';
</style>
```

### 1.2 generate配置项说明

| 变量               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| $num               | //循环计数器，                                               |
| $sum:              | //循环次数，用于控制生成calss的数量                          |
| $step              | //步长，由于设计稿2rpx=1px，故此处步长为2                    |
| $pixis:            | //单位                                                       |
| $color_name_list   | //颜色名称数组，_list结尾的都代表数据                        |
| $color_list        | //颜色值数组， 如需拓展，长度必须和$color_name_list的长度一致 |
| $size_name_list    | //尺寸数组                                                   |
| ￥text_size_list   | //字体大小数组 ，如需拓展，长度必须和$size_name_list的长度一致 |
| $rounded_size_list | //圆角数组，如需拓展，长度必须和$size_name_list的长度一致    |



## 2 类名详情

### 2.1.宽度、高度

宽度和高度的使用完全一致，只需要字母w替换成h即可，其中w-p-{val}的p代表的意思是precentage百分比的意思；

tailwindcss的取名为.w-1/2,但是/字符会在wx小程序等不兼容,故使用.w-p-1来代替

| class     | {val}可选值          | 实际样式                   | 示例            |
| --------- | -------------------- | -------------------------- | --------------- |
| w-{val}   | 0-30;以及（1-30）*10 | 如w-1实际为width:2rpx      | w-1;w-200;w-300 |
| h-{val}   | 0-30;以及（1-30）*10 | 如h-100实际为height:200rpx | h-1;h-200;h-300 |
| w-full    |                      | width:100%                 | w-full          |
| w-screen  |                      | width:100vw                |                 |
| w-p-{val} | 1-10                 | width:10%;                 | w-p-1           |

### 2.2 margin、padding、border

margin、padding、border使用完全一致；m为margin;p为padding,border为border

示例：p-2;px-3;pr-3;border-3;border-r-3;border-l-3;

| class    | {val}可选值 | 实际样式                                        | 示例  |
| -------- | ----------- | ----------------------------------------------- | ----- |
| m-{val}  | 0-30;       | 如m-1实际为margin:2rpx                          | m-1;  |
| mx-{val} | 0-30;       | 如mx-1实际为margin-left:2rpx;margin-right;2rpx; | mx-1; |
| my-{val} | 0-30;       | 如my-1实际为margin-left:2rpx;margin-right;2rpx; | my-1; |
| mt-{val} | 0-30;       | 如mt-1实际为margin-top:2rpx;                    | mt-1; |
| mr-{val} | 0-30;       | 如mt-1实际为margin-right:2rpx;                  | mt-1; |
| mb-{val} | 0-30;       | 如mb-1实际为margin-bottom:2rpx;                 | mb-1; |
| ml-{val} | 0-30;       | 如ml-1实际为margin-left:2rpx;                   | ml-1; |
|          |             |                                                 |       |

### 2.3 background-color、color

background-color和color使用完全一致，只需要bg字母换成text即可，如text-black、text-blue-3 ；

{val}值越大，颜色越浅色；

默认支持5种颜色，可自行拓展；如下图所示拓展pink的示例;

```scss
//颜色数组，可拓展，下方2个数组长度必须一致
$color_name_list: "blue", "green", "yellow", "red", "gray";
$color_list: #007aff, #4cd964, #f0ad4e, #dd524d, #636e72;

//拓展多一个颜色pink
$color_name_list: "blue", "green", "yellow", "red", "gray","pink";
$color_list: #007aff, #4cd964, #f0ad4e, #dd524d, #636e72,#f78fb3;
```



| class         | {val}可选值 | 实际样式                | 示例      |
| ------------- | ----------- | ----------------------- | --------- |
| bg-black      |             | background-color: #000; |           |
| *bg-white*    |             | background-color: #fff; |           |
| bg-blue       |             |                         |           |
| bg-blue-{val} | 1-9         |                         | bg-bule-3 |

### 2.4 border-radius 、font-size

如下所示,共计"xs", "sm", "base", "lg", "xl", "2xl", "3xl", "4xl", "5xl"九种尺寸;

border-radius 与font-size的用法完全一致；

同样您也可以自己拓展，拓展方法如同bg拓展;

```scss
$size_name_list: "xs", "sm", "base", "lg", "xl", "2xl", "3xl", "4xl", "5xl";
$text_size_lset: 12, 13, 14, 16, 18, 24, 36, 48, 56;//圆角
$rounded_size_lset: 5, 8, 10, 12, 16, 24, 36, 48, 56;//字体大小
```

| class           | {val}可选值                                                | 实际样式 | 示例       |
| --------------- | ---------------------------------------------------------- | -------- | ---------- |
| text-{val}      | "xs", "sm", "base", "lg", "xl", "2xl", "3xl", "4xl", "5xl" |          | text-xl    |
| *rounded*-{val} | "xs", "sm", "base", "lg", "xl", "2xl", "3xl", "4xl", "5xl" |          | rounded-lg |

### 2.5 定位相关

#### 2.5.1方向

top\left\right\bottom使用方法完全一致

| class   | {val}可选值 | 实际样式  | 示例 |
| ------- | ----------- | --------- | ---- |
| t-{val} | 0-30        | top:40rpx | t-20 |
|         |             |           |      |

#### 2.2.2其它

完全参照tailwindcss命名

| class    | 实际样式            | 备注 |
| -------- | ------------------- | ---- |
| static   | position: static;   |      |
| fixed    | position: fixed;    |      |
| absolute | position: absolute; |      |
| relative | position: relative; |      |
| sticky   | position: sticky;   |      |

### 2.6 flex布局

完全参照tailwindcss命名

| class                 | 实际样式                                                    | 备注 |
| --------------------- | ----------------------------------------------------------- | ---- |
| flex                  | display: flex;                                              |      |
| *flex-center*         | display: flex; justify-content: center;align-items: center; |      |
| flex-1                | }flex: 1 1 0%;                                              |      |
| flex-auto             | flex: 1 1 auto;                                             |      |
| flex-row              | flex-direction: row;                                        |      |
| flex-col              | flex-direction: column;                                     |      |
| justify-start         | justify-content: flex-start;                                |      |
| justify-end           | justify-content: flex-end;                                  |      |
| justify-center        | justify-content: center;                                    |      |
| justify-between       | justify-content: space-between;                             |      |
| justify-around        | justify-content: space-around;                              |      |
| justify-evenly        | justify-content: space-evenly;                              |      |
| justify-items-start   | justify-items: start;                                       |      |
| justify-items-end     | justify-items: end;                                         |      |
| justify-items-center  | justify-items: center;                                      |      |
| justify-items-stretch | justify-items: stretch;                                     |      |
|                       |                                                             |      |
|                       |                                                             |      |
|                       |                                                             |      |
|                       |                                                             |      |

### 2.7 浮动

| class       | 实际样式      | 备注 |
| ----------- | ------------- | ---- |
| float-right | float: right; |      |
| float-left  | float: left;  |      |
| float-none  | float: none;  |      |
| *clearfix*  |               |      |

### 2.8元素样式

完全参照tailwindcss命名

| class          | 实际样式               | 备注 |
| -------------- | ---------------------- | ---- |
| *block*        | display: block;        |      |
| *inline-block* | display: inline-block; |      |
| *inline*       | display: inline;       |      |
|                |                        |      |

### 2.9 字体拓展

完全参照tailwindcss命名

| class        | 实际样式             | 备注 |
| ------------ | -------------------- | ---- |
| text-left    | text-align: left;    |      |
| text-center  | text-align: center;  |      |
| text-right   | text-align: right;   |      |
| text-justify | text-align: justify; |      |
| *text-bold*  | font-weight: 700;    |      |
|              |                      |      |

#### 2.10 行高

| class           | {val}可选值 | 实际样式         | 示例         |
| --------------- | ----------- | ---------------- | ------------ |
| *leading*-{val} | 1-30        | line-height:10px | *leading*-10 |
|                 |             |                  |              |

