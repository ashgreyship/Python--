# 基础语法

## 基础语法

测试用例在测试用例表中定义，由关键字组成。关键字从测试库文件、资源文件中导入，或者在测试用例文件的关键字表（Keywords）中定义。

测试用例表的第一列是测试用例名。测试用例从包含测试用例名的行开始，直到下一个包含测试用例名的行或测试用例表结束。测试用例名不要包含通配符`?`、`*`，它们通常用于选择执行部分测试用例，例如`--test 'Example *'`运行所有名字以`Example`开头的测试用例。测试用例表表头和第一个测试用例之间不能包含其他内容。

测试用例表的第二列通常是关键字。在利用关键字返回的值设置变量的场景，第二列及后续列可能是变量名，然后才是关键字。无论哪种情况，关键字后面的列通常包含关键字的参数。

```python
# 配置表 导入第三方库
*** Settings ***
# 库名称 大小写敏感
Library   SeleniumLibrary


# 测试用例定义在表中---Test Case
# 表名称首字母大写---中间有空格
*** Test Cases ***
# 用例名称顶格来写，用例主体另起一行，并且有两个以上空格
testcase1

    # 关键词参数需要与关键词空两格以上
    log to console  执行用例1

search test
    [Documentation]  打开浏览器
    [Tags]  浏览器测试用例标签
    open browser   https://www.baidu.com/  chrome
    # 设置隐式等待
    set selenium implicit wait   10
    # 元素定位方式，值 或者元素定位方式=值
    input text  id=kw  松勤\n
    click element  id=su
    # 搜索结果页面校验
    ${actual}  get text  id=1
    log to console  ${actual}
    # 判断实际结果是否包括预期结果
    should contain  ${actual}     松勤网
    close browser
```

## 测试用例表中的设置

测试用例可以有自己的设置。设置名和关键字一样在第二列，设置的值在后续的列中。测试用例中的设置名用方括号包围以便和关键字区分。设置名列表如下：

* `[Documentation]`：测试用例说明。
* `[Tags]`：测试用例标签。
* `[Setup]`、`[Teardown]`：测试用例的setup、teardown。
* `[Template]`：指定使用的模板关键字，测试用例中只包含作为模板关键字的参数的数据。
* `[Timeout]`：测试用例超时时间。

设置名大小写不敏感，允许设置名和方括号之间存在空格。

带设置的测试用例举例：

```text
*** Test Cases ***
Test With Settings
    [Documentation]    Another dummy test
    [Tags]             dummy owner-lmz
    Log                Hello, world!
```

## 设置表（Settings）中与测试用例相关的设置

设置表中存在如下与测试用例相关的设置（注意没有方括号包围），对测试文件中所有测试用例都生效：

* `Force Tags`、`Default Tags`：测试用例中配置项`[Tags]`的强制补充值和默认值。
* `Test Setup`、`Test Teardown`：测试用例中配置项`[Setup]`和`[Teardown]`的默认值。
* `Test Template`：测试用例中默认使用的模板关键字。
* `Test Timeout`：测试用例中配置项`[Timeout]`的默认值。

## 关键字的参数

关键字可以接收不同的参数，参数可以有默认值，这些都取决于关键字如何实现。关键字的文档中通常包含其参数的使用说明。`Libtool`或`javadoc`工具可以自动生成文档。

### 位置参数

位置参数在关键字文档中通过逗号分割的参数名区分，例如`first, second, third`。位置参数本身叫什么名字无所谓，重要的是参数的位置，但是参数名也最好能够解释位置参数的意义。使用关键字的时候，提供的参数个数要和关键字文档中说明的参数个数一致。

下面的例子中，使用`OperatingSystem`库中的`Create Directory`和`Copy File`关键字，分别需要一个参数（`path`）和两个参数（`source`、`destination`）。`Builtin`库中的`No Operation`关键字不需要参数。

```text
*** Test Cases ***
Example
    Create Directory    ${TEMPDIR}/stuff
    Copy File           ${CURDIR}/file.txt    ${TEMPDIR}/stuff
    No Operation
```

### 默认值

有默认值的参数，在关键字文档中参数名和默认值以`=`号分割，例如`name=default value`。有默认值的参数后面不能有位置参数。

下面的例子中，`Create File`关键字参数为`path, content=, encoding=UTF-8`：

```text
*** Test Cases ***
Example
    Create File    ${TEMPDIR}/empty.txt
    Create File    ${TEMPDIR}/utf-8.txt         Hyvä esimerkki
    Create File    ${TEMPDIR}/iso-8859-1.txt    Hyvä esimerkki    ISO-8859-1
```

### 参数个数可变

关键字可以接收任意多个参数，所谓`varargs`。位置参数、带默认值的参数可以和`varargs`共存，`varargs`通常在参数列表的最后。在关键字文档中`varargs`通过一个星号开头的`*varargs`描述。

`OperatingSystem`库中的关键字`Remove Files`和`Join Paths`，参数描述分别是`*paths`和`base, *paths`：

```text
*** Test Cases ***
Example
    Remove Files    ${TEMPDIR}/f1.txt    ${TEMPDIR}/f2.txt    ${TEMPDIR}/f3.txt
    @{paths} =    Join Paths    ${TEMPDIR}    f1.txt    f2.txt    f3.txt    f4.txt
```

### 命名参数

调用关键字时，命名参数`arg=value`可以明确为关键字的哪个参数赋值。命名参数大小写敏感（参数名必须大小写一致），空格敏感（等号左边不允许有空格，等号右边的空格会被当做参数值的一部分）。  
调用用户自定义的关键字，命名参数不能使用`${}`装饰参数名。比如关键字的参数是`${arg1}=first, ${arg2}=second`，如果为`arg1`参数提供参数值，必须是`arg1=first`的形式。  
位置参数不能出现在命名参数后面。命名参数之间的相对顺序无关紧要。

#### 命名参数与变量

命名参数的参数名和参数值都可以使用变量。如果变量是标量（scalar variable），标量会原样传递给关键字，不会被转换为字符串。比如关键字的参数是`arg=${object}`，会把`${object}`对象原样传递给关键字，而不是将`${object}`转换为字符串后传递给关键字。  
如果命名参数的参数名包含变量，先解析这些变量，再进行关键字的参数匹配。

命名参数需要明确写出`=`符号，只有参数值不算是命名参数，即使参数值包含`foo=bar`的形式。关键字定义包含其他关键字时尤其需要注意。例如，关键字`Run Program`通过数组形式`@{args}`接收任意多个参数，再把任意多个参数用同样的语法`@{args}`传给关键字`Run Process`，测试用例中调用`Run Program`使用的`named=value`命名参数形式可能不会被正确地识别：

```text
*** Test Cases ***
Example
    Run Program    shell=True    # This will not come as a named argument to Run Process

*** Keywords ***
Run Program
    [Arguments]    @{args}
    Run Process    program.py    @{args}    # Named arguments are not recognized from inside @{args}
```

要在关键字间传递命名参数，需要使用自由命名参数（free named argument），自由命名参数也可以传递位置参数。

#### 对命名参数转义

有时位置参数的值可能是`foo=bar`的形式，如果恰好还有一个带默认值的参数`foo`，会造成关键字参数值的错误解析。使用转义语法`foo\=bar`可以明确不使用命名参数语法，为位置参数提供参数值。

#### 支持命名参数的场景

导入库文件、调用关键字都支持使用命名参数。用户自定义关键字和大多数测试库关键字支持命名参数。唯一例外是基于Java使用了静态库API的库中的关键字。`Libdoc`生成的文档会说明库是否支持命名参数。

下面的例子，展示了在引入库文件（`Telnet`）时、调用自定义关键字和测试库中的关键字时，如何提供命名参数：

```text
*** Settings ***
Library    Telnet    prompt=$    default_log_level=DEBUG

*** Test Cases ***
Example
    Open connection    10.0.0.42    port=${PORT}    alias=example
    List files         options=-lh
    List files         path=/tmp    options=-l

*** Keywords ***
List files
    [Arguments]        ${path}=.    ${options}=
    Execute command    ls ${options} ${path}
```

### 自由命名参数（Free Named Argument）

自由命名参数，也叫自由关键字参数或`kwargs`。关键字可以用一个参数接收所有符合命名参数语法的参数值。支持自由命名参数语法的场景与支持命名参数语法的场景相同。  
基于Python的关键字的自由命名参数语法是`**kwargs`，用户自定义关键字的自由命名参数语法是`&{kwargs}`。  
自由命名参数的参数名和参数值都支持变量，但是自由命名参数的参数名必须是字符串。

下面的例子中，`Process`库中的`Run Process`关键字，参数描述为`command, *arguments, **configuration`：

```text
*** Test Cases ***
Free Named Arguments
    Run Process    program.py    arg1    arg2    cwd=/home/user
    Run Process    program.py    argument    shell=True    env=${ENVIRON}
1234
```

在命名参数教程中提到的传递位置参数和命名参数问题，可以通过自由命名参数解决：

```text
*** Test Cases ***
Free Named Arguments
    Run Program    arg1        arg2          cwd=/home/user
    Run Program    argument    shell=True    env=${ENVIRON}

*** Keywords ***
Run Program
    [Arguments]    @{args}       &{config}
    Run Process    program.py    @{args}    &{config}
```

### 强制名字参数

强制名字参数的思想来自[Python的强制关键字参数](https://www.python.org/dev/peps/pep-3102)。Robot Framework的关键字可以约束带默认值的参数，在调用时必须使用命名参数语法提供参数值，例如：

```text
*** Test Cases ***
Named-only Arguments
    Run Program    arg1        arg2          # 'shell' is False (default)
    Run Program    argument    shell=True    # 'shell' is True
*** Keywords ***
Run Program
    [Arguments]    @{args}       ${shell}=False
    Run Process    program.py    @{args}    shell=${shell}
```

## 失败

测试用例中任何一个关键字失败，会导致测试用例失败。测试用例失败会终止测试用例的执行，如果存在teardown的话执行清理，再继续执行下一个测试用例。如果测试用例失败时不想立即终止测试用例的执行，可以使用可继续的失败（continuable failure）。

测试用例的失败错误消息从失败的关键字中获取。  
在可继续的失败场景中，测试用例可以失败多次，此时错误消息是多次失败的错误消息的组合。为了提高可读性，测试报告中较长的错误消息自动从中间截断，但是完整的错误消息在日志文件中仍然可见。  
错误消息是纯文本格式，也可以包含HTML。HTML格式使用`*HTML*`标记开启，在最终的测试报告和测试日志中，不会出现标记符号`*HTML*`。例如：

```text
*** Test Cases ***
Normal Error
    Fail    This is a rather boring example...
HTML Error
    ${number} =    Get Number
    Should Be Equal    ${number}    42    *HTML* Number is not my <b>MAGIC</b> 
```

## 测试用例名和文档

一个测试套内的测试用例名字唯一。在测试用例中、用户自定义关键字中、测试用例的setup和teardown中，都可以使用自动变量`${TEST_NAME}`获取测试用例名。

`[Documentation]`为测试用例添加文档。文档会出现在命令行输出、测试日志、测试报告中。文档可以使用HTML格式，支持使用变量。

如果说明文档被分隔到多列，同一行的单元格被空格拼接到一起。这在使用HTML格式或者每一列比较狭窄时非常有用。如果文档被分隔到多行，多行之间通过换行符拼接到一起。如果行尾已经以`\n`结束或者包含一个反斜线转义符（`\`，表示续行），则不会再添加换行符。例如：

```text
*** Test Cases ***
Simple
    [Documentation]    Simple documentation
    No Operation

Formatting
    [Documentation]    *This is bold*, _this is italic_  and here is a link: http://robotframework.org
    No Operation

Variables
    [Documentation]    Executed at ${HOST} by ${USER}
    No Operation

Splitting
    [Documentation]    This documentation    is split    into multiple columns
    No Operation

Many lines
    [Documentation]    Here we have
    ...                an automatic newline
    No Operation
123456789101112131415161718192021
```

## 测试用例标签

标签是简单又强大的测试用例分类机制。标签内容是任意文本，具体功能为：

* 标签展示在测试报告、测试日志、测试用例中，属于测试用例元信息。
* 测试用例统计，每个标签下的测试用例总数、通过数、失败数自动统计。
* 通过标签包含或排除某些测试用例的执行。
* 通过标签可以指定关键性测试用例，关键性测试用例会影响测试结论是通过还是失败。

下面介绍如何设置标签：

* 设置表（Settings）中的`Force Tags`： 测试文件中所有测试用例都追加该标签。如果在测试套初始化文件中使用`Force Tags`，测试套中所有测试用例都追加该标签。
* 设置表中的`Default Tags`：测试用例中没有`[Tag]`标签的，都使用`Default Tags`的标签。测试套初始化文件不支持`Default Tags`标签。
* 测试表中的`[Tags]`标签（注意有方括号）：配置测试用例的标签，不包含设置表中`Defaults Tags`的标签。 `[Tags]`使用空值或`NONE`也可以覆盖设置表中`Default Tags`的设置。
* `--settag`命令行选项：所有被执行的测试用例附加该选项指定的标签。
* `Set Tags`、`Remove Tags`、`Fail`、`Pass Execution`关键字：这些`Builtin`库中的关键字可以在测试用例执行过程中动态修改测试用例的标签。

虽然标签内容允许是任意值，但是它们通常被标准化为全小写，并删除所有的空格。标签值可以包含变量（前提是变量存在）。

```text
*** Settings ***
Force Tags      req-42
Default Tags    owner-john    smoke

*** Variables ***
${HOST}         10.0.1.42

*** Test Cases ***
No own tags
    [Documentation]    This test has tags owner-john, smoke and req-42.
    No Operation

With own tags
    [Documentation]    This test has tags not_ready, owner-mrx and req-42.
    [Tags]    owner-mrx    not_ready
    No Operation

Own tags with variables
    [Documentation]    This test has tags host-10.0.1.42 and req-42.
    [Tags]    host-${HOST}
    No Operation

Empty own tags
    [Documentation]    This test has only tag req-42.
    [Tags]
    No Operation

Set Tags and Remove Tags Keywords
    [Documentation]    This test has tags mytag and owner-john.
    Set Tags    mytag
    Remove Tags    smoke    req-*
12345678910111213141516171819202122232425262728293031
```

### 保留标签

RF框架的保留标签以`robot:`开头，用户使用的标签不要包含这个前缀。目前框架中只有两个保留标签：`robot:exit`用于测试用例的平滑结束，`robot:no-dry-run`用于抑制演练（dry run）模式，演练模式不会真正执行测试库中的关键字，只用于测试数据的语法验证。

## 测试用例setup和teardown

setup是测试用例执行前的准备动作，teardown是测试用例执行后的清理动作。RF框架的setup和teardown是两个关键字。如果准备动作和清理动作需要很多步骤才能完成，定义更高级的关键字或者使用`Builtin`库中的`Run Keywords`关键字依次调用更多的关键字。

即使测试用例执行失败，teardown中的清理动作也会执行。另外，即使teardown中的某个关键字执行失败，后面的关键字也会继续执行。这种“失败后继续”的功能可以在其他关键字中开启，在teardown中默认开启。

设置表（Settings）中`Test Setup`和`Test Teardown`设置可以为一个测试用例文件中的所有测试用例配置setup和teardown。测试用例表中每个测试用例自己的`[Setup]`和`[Teardown]`可以覆盖`Test Setup`和`Test Teardown`的设置。`[Setup]`、`[Teardown]`后面没有关键字意味着setup和teardown不做任何操作，或者使用`NONE`明确说明。

```text
*** Settings ***
Test Setup       Open Application    App A
Test Teardown    Close Application

*** Test Cases ***
Default values
    [Documentation]    Setup and teardown from setting table
    Do Something

Overridden setup
    [Documentation]    Own setup, teardown from setting table
    [Setup]    Open Application    App B
    Do Something

No teardown
    [Documentation]    Default setup, no teardown at all
    Do Something
    [Teardown]

No teardown 2
    [Documentation]    Setup and teardown can be disabled also with special value NONE
    Do Something
    [Teardown]    NONE

Using variables
    [Documentation]    Setup and teardown specified using variables
    [Setup]    ${SETUP}
    Do Something
    [Teardown]    ${TEARDOWN}
1234567891011121314151617181920212223242526272829
```

setup和teardown要执行的关键字可以是变量，这使得可以在不同的环境上通过命令行参数令setup、teardown执行不同的操作。

> 测试套可以有自己的setup、teardown，测试套的setup在所有测试用例及子测试套的执行前执行，teardown在他们执行后执行。

## 测试模板

采用测试模板的测试用例是数据驱动型。关键字驱动的测试用例由关键字及其可能的参数组成，采用测试模板的测试用例只包含模板关键字的参数，能够做到同样的关键字在每个测试用例文件中只出现一次，而不用出现在每个测试用例中。

模板关键字接受位置参数、命名参数、嵌入到关键字名中的参数。不能使用变量定义模板。

### 基本用法

例如下面的例子中，两个测试用例其实是一样的：

```text
*** Test Cases **
Normal test case
    Example keyword    first argument    second argument

Templated test case
    [Template]    Example keyword
    first argument    second argument
1234567
```

测试用例可以使用`[Template]`定义模板关键字。设置表（Settings）中`Test Template`设置会对测试用例文件中的所有测试用例生效。测试用例的`[Template]`设置会覆盖设置表的`Test Template`设置。为`[Template]`提供空值或者`NONE`表示测试用例不使用模板关键字。

如果包含模板关键字的测试用例有很多行参数数据，模板关键字依次被应用到参数数据的每一行，每次都执行相同的关键字。如果某行参数数据导致包含模板关键字的测试用例失败，剩余的数据还会继续执行。常规测试用例中也可以开启这种“失败后继续”的功能，包含模板关键字的测试用例是自动开启的。

一个使用设置表中`Test Template`指定的模板关键字的例子如下：

```text
*** Settings ***
Test Template    Example keyword

*** Test Cases ***
Templated test case
    first round 1     first round 2
    second round 1    second round 2
    third round 1     third round 2
12345678
```

包含模板关键字的测试用例，仍然支持参数默认值、`varargs`、命名参数、自由命名参数等。在参数或参数值中使用变量的支持也和之前一样。

### 模板关键字名字包含嵌入的参数

模板的关键字支持在关键字名字中嵌入参数，例如：

```text
*** Test Cases ***
Normal test case with embedded arguments
    The result of 1 + 1 should be 2
    The result of 1 + 2 should be 3

Template with embedded arguments
    [Template]    The result of ${calculation} should be ${expected}
    1 + 1    2
    1 + 2    3

*** Keywords ***
The result of ${calculation} should be ${expected}
    ${result} =        Calculate     ${calculation}
    Should Be Equal    ${result}     ${expected}
1234567891011121314
```

模板关键字有嵌入参数时，为模板关键字提供的参数个数，必须和关键字本身定义的参数个数一致，但不一定和关键字本身定义的参数名一致：

```text
*** Test Cases ***
Different argument names
    [Template]    The result of ${foo} should be ${bar}
    1 + 1    2
    1 + 2    3

Only some arguments
    [Template]    The result of ${calculation} should be 3
    1 + 2
    4 - 1

New arguments
    [Template]    The ${meaning} of ${life} should be 42
    result    21 * 2
1234567891011121314
```

### 带for循环的模板

如果模板使用了for循环，也支持“失败后继续”，即使循环中某个步骤失败，后续的步骤也会继续执行。例如：

```text
*** Test Cases ***
Template and for
    [Template]    Example keyword
    FOR    ${item}    IN    @{ITEMS}
        ${item}    2nd arg
    END
    FOR    ${index}    IN RANGE    42
        1st arg    ${index}
    END
123456789
```

## 不同的测试用例风格

涉及流程的测试用例可以采用关键字驱动或行为驱动。为同样的流程测试多组不同的输入可以采用数据驱动。

### 关键字驱动

即本文介绍的通常由多个关键字及其参数组成的测试用例形式。一般流程是系统初始化，然后在系统中执行测试操作，最后验证系统表现符合预期。

### 数据驱动

如果多个测试用例调用同一个关键字，区别只是输入、输出数据不同，就可以采用借助测试模板的数据驱动形式，例如：

```text
*** Settings ***
Test Template    Login with invalid credentials should fail

*** Test Cases ***                USERNAME         PASSWORD
Invalid User Name                 invalid          ${VALID PASSWORD}
Invalid Password                  ${VALID USER}    invalid
Invalid User Name and Password    invalid          invalid
Empty User Name                   ${EMPTY}         ${VALID PASSWORD}
Empty Password                    ${VALID USER}    ${EMPTY}
Empty User Name and Password      ${EMPTY}         ${EMPTY}
12345678910
```

> 根据[85.Robot Framework测试数据基本语法](https://blog.csdn.net/a464057216/article/details/104370180)对测试数据表的说明，与`*** Test Cases ***`同行的USERNAME、PASSWORD都会被忽略，起到了注释作用。

上面的测试用例包含6个不同的测试用例，每个测试用例都包含非法的用户名、密码组合。下面是另一种写法：

```text
*** Test Cases ***
Invalid Password
    [Template]       Login with invalid credentials should fail
    invalid          ${VALID PASSWORD}
    ${VALID USER}    invalid
    invalid          whatever
    ${EMPTY}         ${VALID PASSWORD}
    ${VALID USER}    ${EMPTY}
    ${EMPTY}         ${EMPTY}
123456789
```

### 行为驱动

测试用例可以写得像需求文档，这样非技术人员也可以维护。这种可执行测试的需求，可以用在验收测试驱动的开发中。

行为驱动开发流行`GIVEN-WHEN-THEN`的格式，在`GIVEN`中进行系统初始化，在`WHEN`中进行系统测试，在`THEN`中进行系统状态验证。如果某个环节需要更多步骤，使用`and`或`but`关键字。例如：

```text
*** Test Cases ***
Valid Login
    Given login page is open
    When valid username and password are inserted
    and credentials are submitted
    Then welcome page should be open
```

