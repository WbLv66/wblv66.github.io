# Vscode&#43;clang


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2024/05/25/15/01/ai-generated-8787240_1280.jpg&#34;&gt;}}
# vscode&#43;clang

优势：代码提示更快；可以进行静态分析

## 1. 在ubuntu上安装clang（推荐14及以上，有类型提示）
```
wget https://apt.llvm.org/llvm.sh
chmod u&#43;x llvm.sh
sudo ./llvm.sh 14
或者使用清华源
# 下载脚本
wget https://mirrors.tuna.tsinghua.edu.cn/llvm-apt/llvm.sh
chmod &#43;x llvm.sh
sudo ./llvm.sh 14 all -m https://mirrors.tuna.tsinghua.edu.cn/llvm-apt
```
将clang14和clang&#43;&#43;14设为默认版本
```
 sudo update-alternatives --install /usr/bin/clang&#43;&#43; clang&#43;&#43; /usr/bin/clang&#43;&#43;-14 200
 
 sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-14 200
 
  # 列出已存在的替代项
 sudo update-alternatives --display clang&#43;&#43;

 ```
## 2. 在vscode上安装插件

禁用微软c&#43;&#43;插件的代码提示功能

方法一：删除vscode中提供的c&#43;&#43;插件。

方法二：在setting.json加入&#34;C_Cpp.intelliSenseEngine&#34;: &#34;disabled&#34;,

下载clangd插件和codelldb插件，codelldb插件在安装时会自动额外下载一个包

安装好后在clangd插件设置中勾选enable code completion，在clangd插件设置Arguments里面添加``--compile-commands-dir=${workspaceFolder}/build`` 和 ``--header-insertion=never``，Path设置为``/usr/bin/clangd-14``
## 3. 配置.clang-format

此文件可以帮助代码格式化，放在主目录便可以了，为了让文件能在保存时自动格式化可以在`settings.json`里面写入`&#34;editor.formatOnSave&#34;: true`

如下为我的`.clang-format`配置
```
# 基于那个配置文件
BasedOnStyle: google
# 访问说明符的偏移(public private)
AccessModifierOffset: -4
#缩进宽度
IndentWidth: 4
# 每行字符的限制，0表示没有限制  
ColumnLimit: 80

```
## 4. 配置.clang-tidy

此文件可以进行代码的静态分析，放在主目录便可以了，借助Cmake的输出文件可以让代码的静态分析更加准确。在`CMakeLists.txt`里面写入`set(CMAKE_EXPORT_COMPILE_COMMANDS ON)`

如下为我的`clang-tidy`配置

```
---
Checks: &#39;-*,
        clang-analyzer-core.*,
        clang-analyzer-cplusplus.*,
        modernize-redundant-void-arg,
        modernize-use-bool-literals,
        modernize-use-equals-default,
        modernize-use-nullptr,
        modernize-use-override,
        google-explicit-constructor,
        google-readability-casting,
        readability-braces-around-statements,
        readability-identifier-naming.ClassCase,
        readability-identifier-naming.StructCase,
        readability-identifier-naming.TypedefCase,
        readability-identifier-naming.EnumCase,
        readability-non-const-parameter,
        cert-dcl21-cpp,
        bugprone-undelegated-constructor,
        bugprone-macro-parentheses,
        bugprone-macro-repeated-side-effects,
        bugprone-forward-declaration-namespace,
        bugprone-bool-pointer-implicit-conversion,
        bugprone-misplaced-widening-cast,
        cppcoreguidelines-narrowing-conversions,
        misc-unconventional-assign-operator,
        misc-unused-parameters&#39;
WarningsAsErrors: &#39;&#39;
HeaderFilterRegex: &#39;&#39;
CheckOptions:
  # 现代化（Modernize）
  - key:             modernize-redundant-void-arg
    value:           &#39;true&#39;  # 检查并移除函数声明中冗余的 void 参数。
  - key:             modernize-use-bool-literals
    value:           &#39;true&#39;  # 建议使用布尔字面量 true 和 false 代替整数值 0 和 1。
  - key:             modernize-use-equals-default
    value:           &#39;true&#39;  # 建议在默认构造函数、复制构造函数和赋值运算符中使用 = default，以简化代码。
  - key:             modernize-use-nullptr
    value:           &#39;true&#39;  # 建议使用 nullptr 代替 NULL 或 0 来表示空指针。
  - key:             modernize-use-override
    value:           &#39;true&#39;  # 建议在覆盖基类虚函数时使用 override 关键字，以增加代码的清晰性和安全性。

  # Google 代码风格（Google）
  - key:             google-explicit-constructor
    value:           &#39;true&#39;  # 检查并建议在单参数构造函数中使用 explicit 关键字，以防止隐式转换。
  - key:             google-readability-casting
    value:           &#39;true&#39;  # 检查并建议使用 C&#43;&#43; 风格的类型转换（如 static_cast、dynamic_cast、const_cast 和 reinterpret_cast）代替 C 风格的类型转换。

  # 可读性（Readability）
  - key:             readability-braces-around-statements
    value:           &#39;true&#39;  # 建议在单行语句周围添加大括号，以提高代码的可读性和一致性。
  - key:             readability-identifier-naming.ClassCase
    value:           &#39;CamelCase&#39;  # 类名应使用 CamelCase 风格，例如 MyClassName。
  - key:             readability-identifier-naming.StructCase
    value:           &#39;CamelCase&#39;  # 结构体名应使用 CamelCase 风格，例如 MyStructName。
  - key:             readability-identifier-naming.TypedefCase
    value:           &#39;CamelCase&#39;  # 类型定义应使用 CamelCase 风格，例如 MyTypeDef。
  - key:             readability-identifier-naming.EnumCase
    value:           &#39;CamelCase&#39;  # 枚举名应使用 CamelCase 风格，例如 MyEnumName。
  - key:             readability-non-const-parameter
    value:           &#39;true&#39;  # 检查并标识非 const 参数，以提高代码的可读性和安全性。

  # CERT 安全编码标准（CERT）
  - key:             cert-dcl21-cpp
    value:           &#39;true&#39;  # 检查并标识在头文件中不应包含无命名空间的 using 声明和指令，以防止命名空间污染。

  # Bug 检测（Bugprone）
  - key:             bugprone-undelegated-constructor
    value:           &#39;true&#39;  # 检查并标识未委托的构造函数，以确保构造函数的正确性。
  - key:             bugprone-macro-parentheses
    value:           &#39;true&#39;  # 检查并建议在宏定义中使用括号，以防止潜在的错误。
  - key:             bugprone-macro-repeated-side-effects
    value:           &#39;true&#39;  # 检查并标识宏中重复的副作用，以防止潜在的错误。
  - key:             bugprone-forward-declaration-namespace
    value:           &#39;true&#39;  # 检查并标识命名空间前向声明的潜在问题。
  - key:             bugprone-bool-pointer-implicit-conversion
    value:           &#39;true&#39;  # 检查并标识布尔指针的隐式转换，以防止潜在的错误。
  - key:             bugprone-misplaced-widening-cast
    value:           &#39;true&#39;  # 检查并标识错误的宽化转换，以防止潜在的错误。

  # C&#43;&#43; 核心指南（CppCoreGuidelines）
  - key:             cppcoreguidelines-narrowing-conversions
    value:           &#39;true&#39;  # 检查并标识可能导致数据丢失的窄化转换。

  # 杂项（Miscellaneous）
  - key:             misc-unconventional-assign-operator
    value:           &#39;true&#39;  # 检查并标识不常见的赋值操作符重载，以确保代码的一致性和可维护性。
  - key:             misc-unused-parameters
    value:           &#39;true&#39;  # 检测未使用的参数。
...



```



---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/51dd9c5/  

