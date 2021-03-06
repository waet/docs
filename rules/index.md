## 前端规范建设

```
文件资源命名规范
    1 文件名采用小写字母组成。
    2 包含多个单词时，使用驼峰命名。
目录命名规范
    1、目录名采用大小写字母。例：myProjectName
    2、有复数结构时，要采用复数命名法。 例：scripts, styles, images, dataModels
css
类名规范
    1、class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
    2、避免过度任意的简写。class 名称应当尽可能短，并且意义明确。
    3、使用有组织的或目的明确的名称
    4、基于最近的父 class 或基本（base） class 作为新 class 的前缀。
    5、使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。
语法规范
    1、为了代码的易读性，在每个声明块的左花括号前添加一个空格。
    2、声明块的右花括号应当单独成行
    3、每条声明语句的 : 后应该插入一个空格
    4、为了获得更准确的错误报告，每条声明都应该独占一行。
    5、所有声明语句都应当以分号结尾。
    6、对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，box-shadow）
    7、对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）
    8、避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;。
    9、十六进制值应该全部小写，例如，#fff。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
    10、尽量使用简写形式的十六进制值，例如，用 #fff 代替 #ffffff。
    11、为选择器中的属性添加双引号，例如，input[type="text"]。只有在某些情况下是可选的，但是，为了代码的一致性，建议都加上双引号。
    12、编码规范为utf-8。
注释规范
单行注释
    1、单独一行：// 与注释文字之间保留一个空格
    2、在代码后面注释： //与代码有一个空格
多行注释
    /** 
    * @param grid {Ext,Grid,Panel} 需要合 
    * 并的Grid,合并Grid的行 - 
    * @param cols {Array} 需要合并列的 
    * Index值，从0开始计数 
    * @param isAllSome {Boolean} 是否两个 
    * tr完全一样才能合并true：完全一样， 
    * false：默认
    * @return volid 
    * @author 
    * @example 
    */ @param 参数名｛参数类型｝描述信息 @return {返回类型} 描述信息 @author 作者信息 [附属信息：日期，邮箱] @version XX XX XX @example 示例代码

js
变量命名规范
1、小驼峰式
    命名语义化，尽可能利用英文单词或缩写。
    常量命名规范
1、采用大写字母，包含多个单词时，单个单词之间使用‘_’分割
    const MAX_COUNT = 10; const URL = 'http://www.baidu.com';
函数命名规范
    1、普通函数使用小驼峰式 例：studentInfo, userInfo
    2、构造函数使用大驼峰式 例：StudentInfo, UserInfo
类的成员规范
    1、公共属性和方法：同变量命名方式 -私有属性和方法：前缀为下划线_后面跟公共属性和方法一样的命名方式
    function Student(name) { 
        var theName = name//私有成员 
        //公共方法 
        this.getName = function() {
            return theName 
        }
        this.setName = function() {
            theName = value 
        }
    } 
    var st = new Student('tom'); 
    st.setName('jerry); 
    console.log(st.getName())
脚本规范
    1、尽量避免使用存在兼容性或者消耗资源的方法或属性。比如 eval()、innerText。
    2、URL传参数值为中文字符（未明确字符）需要进行编码。
    3、循环或者条件语句必须使用花括号包围。
    4、禁止使用未定义变量，使用变量前必须先定义。
    5、对于定义过的变量必须使用。
    6、文件编码统一为utf-8,书写过程中，每行代码结束必须有分号。
图片规范
    1、图片命名采用小写，用‘-’进行连接。
    2、能用样式的就不用图片，比如“色块”背景。
    3、命名尽量短，使用缩写，如button用btn，background用bg代替。
    4、图片分为通用图片和模块图片。通用图片放在通用图片的文件夹里面，模块图片放在模块图片的文件夹里面。通用图片命名规范：类别_功能[_状态]；模块图片命名规范：模块_类别[_功能][_状态]。
    5、图片尽量复用。模块图标被复用后，得改名为通用图标命名方式，并迁移到通用文件夹下，防止修改单个模块图标造成其他模块图标混乱。
    6、移除没用到图片，防止项目臃肿。
```
