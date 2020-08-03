# HTTP request&response

| 参数/函数 | Get | Post | Put | Delete |
| :--- | :--- | :--- | :--- | :--- |
| url | 有 | 有 | 有 | 有 |
| params | 有 |  |  |  |
| data |  | 有 | 有 |  |
| json |  | 有 |  |  |
| headers | 有 | 有 | 有 | 有 |
| cookies | 有 | 有 | 有 | 有 |

#### params 参数（查询字符串参数）

传递的是字典，自动编码为表单

#### data 参数（消息体参数）

* 传递的是字典，自动编码为表单 
* 传递的是字符串，直接发布出去

#### json参数（消息体参数）

* 传递的是字典，自动编码为json 字符串，相当于：json.dumps\(dict\)
* 传递的是字符串，加双号后直接发布出去

#### headers参数（请求头参数）

传递字典格式即可

#### cookies参数（请求头中的cookies参数）

传递字典格式即可



## 构造请求参数

* 口诀1：params参数，传入的是字典，自动编码为表单。 
* 口诀2：data参数，传入的是字典，自动编码为表单。 
* 口诀3：data参数，传入的是字符串，按原格式直接发布出去。 
* 口诀4：json参数，传入的是字典，自动编码为json字符串。 
* 口诀5：json参数，传入的是字符串，添加双引号后，按原格式直接发布出去。 
* 口诀6：headers参数，传递的是字典格式
* 口诀7：如果接口文档要求content-type 为表单，心里默念：key和value间用（=等号），参数之间用（&连接符）
* 口诀8：如果接口文档要求content-type 为json字符串，心里默念：key和value间用（:冒号），参数之 间用（&连接符）
* 口诀9：其实json参数完全可以用data参数替代的。json参数做了一个把字典格式转换为json字符串的操 作
* 即： data=json.dumps\(dictPayload\) 等同于 json=dictPayload

