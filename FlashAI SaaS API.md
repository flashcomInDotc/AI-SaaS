# FlashAI SaaS API



## 接口列表

<a id='顶部'></a>

[添加拨打任务](#添加拨打任务)

[拨打任务批量暂停](#拨打任务批量暂停)

[拨打任务批量恢复](#拨打任务批量恢复)

[拨打任务批量停止](#拨打任务批量停止)

[拨打任务某个电话删除](#拨打任务某个电话删除)

<a href='#获取用户话术名称'>获取用户话术名称</a>

<a href='#获取用户话术参数变量'>获取用户话术参数变量</a>

<a href='#获取用户线路列表'>获取用户线路列表</a>

<a href='#通过批次号查询该批次的拨打汇总'>通过批次号查询该批次的拨打汇总</a>

<a href='#通过批次号查询该批次线路拨打汇总'>通过批次号查询该批次线路拨打汇总</a>

<a href='#通过批次号查询该批次的号码列表'>通过批次号查询该批次的号码列表</a>

<a href='#通过批次号查询该批次的通话列表'>通过批次号查询该批次的通话列表</a>

<a href='#查询回调详情'>查询回调详情</a>

<a href='#查询坐席组和坐席'>查询坐席组和坐席</a>

<a href='新增人工座席拨打任务'>新增人工座席拨打任务</a>

## 添加拨打任务

<a id='添加拨打任务'> </a>

### 基本信息

**Path：** /addPlan

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称           | 类型    | 是否必须 | 备注                                                         |
| -------------- | ------- | -------- | ------------------------------------------------------------ |
| clientId       | string  | Y        | 分配的用户 clientId                                          |
| nonce          | string  | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)            |
| timestamp      | number  | Y        | 时间戳                                                       |
| signType       | string  | Y        | 加密方式                                                     |
| sign           | string  | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret)       |
| userId         | number  | Y        | 用户id                                                       |
| batchName      | string  | Y        | 批次名称，用户下唯一                                         |
| botenceId      | string  | Y        | 话术模板 id                                                  |
| callDate       | string  | Y        | 外呼电话拨打日期。比 如，我想在 2018 年 3 月 26 日拨打，传的内容为 20180326。如果未传值或 者传的是过去的日期，则 该字段无效，会按照拨打 时间加入到拨号队列。 |
| callHour       | string  | Y        | 外呼电话拨打时间，可传 的值以小时为单位，以英 文逗号(,)分隔。比如， 我想在早上 9 点-11 点(不 含)和下午 1 点-2 点(不 含)拨打，传的内容为 9,10,13。 |
| clear          | number  | Y        | 是否当日夜间清除未完成 计划，可传的值包括 0 和1 共 2 种。0 表示不清除 1 表示清除。 |
| api            | boolean | N        |                                                              |
| lineIds        | string  | N        | 可以支持多条线路                                             |
| mobileList     | string  | Y        | 格式为：手机号码^附加 数据^参数 1-参数 2-参数 3              |
| recall         | number  | Y        | 共 2 种。0 表示不重 播，1 表示重播                           |
| recallParams   | string  | N        | 跟 recall 参数绑定，如 果 recall=1 则必须要有 值 如果为空不参与加密 |
| notifyUrl      | string  | N        | 回调地址                                                     |
| notifyBatchUrl | string  | N        | 批量回调地址                                                 |

### 返回数据

| 名称            | 类型    | 是否必须 | 备注               |
| --------------- | ------- | -------- | ------------------ |
| code            | string  | Y        | 0成功，其他失败    |
| msg             | string  | Y        | 异常描述           |
| success         | boolean | Y        | 是否成功           |
| body            | object  | Y        |                    |
| -failMobileInfo | string  | Y        | 失败手机号信息     |
| -rightCount     | number  | Y        | 当前批次号码成功数 |
| -failCount      | number  | Y        | 当前批次号码失败数 |



## 拨打任务批量暂停

<a href='#顶部'>回到顶部</a><a id=拨打任务批量暂停> </a>

### 基本信息

**Path：** /batchPlanPause

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |

### 返回数据

| 名称    | 类型    | 是否必须 | 备注            |
| ------- | ------- | -------- | --------------- |
| code    | string  | Y        | 0成功，其他失败 |
| msg     | string  | Y        | 异常描述        |
| success | boolean | Y        | 是否成功        |
| body    | object  | N        |                 |



## 拨打任务批量恢复

<a href='#顶部'>回到顶部</a><a id=拨打任务批量恢复> </a>

### 基本信息

**Path：** /batchPlanRestart

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |

### 返回数据

| 名称    | 类型    | 是否必须 | 备注            |
| ------- | ------- | -------- | --------------- |
| code    | string  | Y        | 0成功，其他失败 |
| msg     | string  | Y        | 异常描述        |
| success | boolean | Y        | 是否成功        |
| body    | object  | N        |                 |



## 拨打任务批量停止

<a href='#顶部'>回到顶部</a><a id=拨打任务批量停止> </a>

### 基本信息

**Path：** /batchPlanStop

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |

### 返回数据

| 名称    | 类型    | 是否必须 | 备注            |
| ------- | ------- | -------- | --------------- |
| code    | string  | Y        | 0成功，其他失败 |
| msg     | string  | Y        | 异常描述        |
| success | boolean | Y        | 是否成功        |
| body    | object  | N        |                 |



## 拨打任务某个电话删除

<a href='#顶部'>回到顶部</a><a id=拨打任务某个电话删除> </a>

### 基本信息

**Path：** /batchPhoneDelete

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |
| phoneList | string | Y        | phone1^phone 2                                         |

### 返回数据

| 名称    | 类型    | 是否必须 | 备注            |
| ------- | ------- | -------- | --------------- |
| code    | string  | Y        | 0成功，其他失败 |
| msg     | string  | Y        | 异常描述        |
| success | boolean | Y        | 是否成功        |
| body    | object  | N        |                 |



## 获取用户话术名称

<a href='#顶部'>回到顶部</a><a id='获取用户话术名称'> </a>

### 基本信息

**Path：** /getBotence

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |

### 返回数据

| 名称         | 类型    | 是否必须 | 备注                  |
| ------------ | ------- | -------- | --------------------- |
| code         | string  | Y        | 0成功，其他失败       |
| msg          | string  | Y        | 异常描述              |
| success      | boolean | Y        | 是否成功              |
| body         | object  | Y        |                       |
| -botenceList | string  | Y        | 话术名称列表，\| 拼接 |



## 获取用户话术参数变量

<a href='#顶部'>回到顶部</a><a id=获取用户话术参数变量> </a>

### 基本信息

**Path：** /queryPlanParams

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |

### 返回数据

| 名称          | 类型    | 是否必须 | 备注                                                         |
| ------------- | ------- | -------- | ------------------------------------------------------------ |
| code          | string  | Y        | 0成功，其他失败                                              |
| msg           | string  | Y        | 异常描述                                                     |
| success       | boolean | Y        | 是否成功                                                     |
| body          | object  | Y        |                                                              |
| -paramSeqLsit | string  | Y        | 返回的是 paramSeqLsit 信息，形式如下： paramName^seq^paramType |



## 获取用户线路列表

<a href='#顶部'>回到顶部</a><a id=获取用户线路列表> </a>

### 基本信息

**Path：** /getCallLine

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |

### 返回数据

| 名称      | 类型    | 是否必须 | 备注                 |
| --------- | ------- | -------- | -------------------- |
| code      | string  | Y        | 0成功，其他失败      |
| msg       | string  | Y        | 异常描述             |
| success   | boolean | Y        | 是否成功             |
| body      | object  | Y        |                      |
| -lineList | string  | Y        | 线路列表，用 \| 拼接 |



## 通过批次号查询该批次的拨打汇总

<a href='#顶部'>回到顶部</a><a id=通过批次号查询该批次的拨打汇总> </a>

### 基本信息

**Path：** /getBatchPlanCallSummary

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |

### 返回数据

| 名称         | 类型    | 是否必须 | 备注                 |
| ------------ | ------- | -------- | -------------------- |
| code         | string  | Y        | 0成功，其他失败      |
| msg          | string  | Y        | 异常描述             |
| success      | boolean | Y        | 是否成功             |
| body         | object  | Y        |                      |
| -batchName   | string  | Y        | 批次名称，用户下唯一 |
| -acceptCount | number  | Y        | 系统接收到的号码数量 |
| -endCount    | number  | Y        | 呼叫完成的号码数量   |
| -planCount   | number  | Y        | 计划中的号码数量     |



## 通过批次号查询该批次线路拨打汇总

<a href='#顶部'>回到顶部</a><a id=通过批次号查询该批次线路拨打汇总> </a>

### 基本信息

**Path：** /getBatchSummaryGroupByLine

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |

### 返回数据

| 名称         | 类型    | 是否必须 | 备注                                                         |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| code         | string  | Y        | 0成功，其他失败                                              |
| msg          | string  | Y        | 异常描述                                                     |
| success      | boolean | Y        | 是否成功                                                     |
| body         | object  | Y        |                                                              |
| -batchName   | string  | Y        | 批次名称，用户下唯一                                         |
| -lineSummary | string  | Y        | 线路 id^收到号码数量^使用该线路拨打完成数量^ <br/>使用该线路拨打最后一通时间   lineId^totalNum^e ndCount^lastCallT ime |



## 通过批次号查询该批次的号码列表

<a href='#顶部'>回到顶部</a><a id=通过批次号查询该批次的号码列表> </a>

### 基本信息

**Path：** /getBatchPlanList

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称        | 类型   | 是否必须 | 备注                                                   |
| ----------- | ------ | -------- | ------------------------------------------------------ |
| clientId    | string | Y        | 分配的用户 clientId                                    |
| nonce       | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp   | number | Y        | 时间戳                                                 |
| signType    | string | Y        | 加密方式                                               |
| sign        | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName   | string | Y        | 批次名称，用户下唯一                                   |
| phoneStatus | number | N        | 状态  1-计划中，2-完 成，3-处理失败                    |
| page        | number | Y        | 页码                                                   |
| pageNum     | number | Y        | 每页条数 最大 5000 条                                  |

### 返回数据

| 名称 | 类型    | 是否必须 | 备注                                                         |
| -------------------------------------------------- | ------- | -------- | ------------------------------------------------------------ |
| code                                               | string  | Y        | 0成功，其他失败                                              |
| msg                                                | string  | Y        | 异常描述                                                     |
| success                                            | boolean | Y        | 是否成功                                                     |
| body                                               | object  | Y        |                                                              |
| -batchName                                         | string  | Y        | 批次名称，用户下唯一                                         |
| -batchCount                                        | string  | Y        | 号码数量  系统成功接收到的号码的 数量                        |
| -mobileList                                        | string  | Y        | 手机列表  格式为：手机号码^附加数 据^参数 1-参数 2-参数 3^ 状态 |
| -phoneStatus                                       | number  | Y        | 1-计划中，2-完成,3-处理 失败                                 |
| -totalPage                                         | number  | Y        | 总页码                                                       |
| -totalRecord                                       | number  | Y        | 根据条件查询后的数据集总数                                   |
| -page                                              | number  | Y        | 当前页码                                                     |
| -pageNum                                           | number  | Y        | 每页条数                                                     |

-----

mobileList 为数组对象拼接，格式如下：
"phone1^attach1^params11-params12-
params13^custName1^custCompany1^1**|**phone2^attach2^params11-params12-
params13^custName2^custCompany2^1."
mobileList 中的数组对象以"|"分割，各参数以^分割，对于附加参数中的各项
以"-"分割.

------

## 通过批次号查询该批次的通话列表

<a href='#顶部'>回到顶部</a><a id=通过批次号查询该批次的通话列表> </a>

### 基本信息

**Path：** /getBatchPlanCallList

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |
| notifyUrl | string | Y        | 回调地址                                               |
| page      | number | Y        | 页码                                                   |
| pageNum   | number | Y        | 每页条数 最大 5000 条                                  |

### 返回数据

| 名称 | 类型    | 是否必须 | 备注                                                         |
| -------------------------------------------------- | ------- | -------- | ------------------------------------------------------------ |
| code                                               | string  | Y        | 0成功，其他失败                                              |
| msg                                                | string  | Y        | 异常描述                                                     |
| success                                            | boolean | Y        | 是否成功                                                     |
| body                                               | object  | Y        |                                                              |
| -batchName                                         | string  | Y        | 批次名称，用户下唯一                                         |
| -batchCount                                        | string  | Y        | 号码数量  系统成功接收到的号码的 数量                        |
| -callList                                          | string  | Y        | 通话列表  格式为：手机号码 ^外呼 日期^呼叫时间^挂断时间^ 应答时间^通话时长^意向 标签^意向备注^F 类明细 ^.... |
| -totalPage                                         | number  | Y        | 总页码                                                       |
| -totalRecord                                       | number  | Y        | 根据条件查询后的数据集总数                                   |
| -page                                              | number  | Y        | 当前页码                                                     |
| -pageNum                                           | number  | Y        | 每页条数                                                     |

-------

callList 为数组拼接而成，格式如下：
"callStartTime1^handupTime1...**|**callStartTime1^handupTime1.^.."
callList 中的数组对象以"|"分割，各参数以^分割,特别说明下 detailList 中
数据是以“$”分割，各参数以_分割
botAnswerText1-botAnswerTime1-customerSayText1-
customerSayTime1$botAnswerText2-botAnswerTime2-customerSayText2-
customerSayTime2

--------

## 查询回调详情

<a href='#顶部'>回到顶部</a><a id=查询回调详情> </a>

### 基本信息

**Path：** /getPhoneDetail

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName | string | Y        | 批次名称，用户下唯一                                   |
| phone     | string | Y        | 手机号码                                               |

### 返回数据

| 名称    | 类型    | 是否必须 | 备注            |
| ------- | ------- | -------- | --------------- |
| code    | string  | Y        | 0成功，其他失败 |
| msg     | string  | Y        | 异常描述        |
| success | boolean | Y        | 是否成功        |
| body    | object  | Y        |                 |



## 查询坐席组和坐席

<a href='#顶部'>回到顶部</a><a id=查询坐席组和坐席> </a>

### 基本信息

**Path：** /queryAgentGroup

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称      | 类型   | 是否必须 | 备注                                                   |
| --------- | ------ | -------- | ------------------------------------------------------ |
| clientId  | string | Y        | 分配的用户 clientId                                    |
| nonce     | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp | number | Y        | 时间戳                                                 |
| signType  | string | Y        | 加密方式                                               |
| sign      | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |

### 返回数据

| 名称             | 类型    | 是否必须 | 备注            |
| ---------------- | ------- | -------- | --------------- |
| code             | string  | Y        | 0成功，其他失败 |
| msg              | string  | Y        | 异常描述        |
| success          | boolean | Y        | 是否成功        |
| body             | object  | Y        |                 |
| -records         | list    | Y        | 坐席列表        |
| --agentGroupId   | string  | Y        | 座席组编号      |
| --agentGroupName | string  | Y        | 座席组名称      |
| --agentId        | string  | Y        | 座席编号        |
| --agentName      | string  | Y        | 座席名称        |



## 新增人工座席拨打任务

<a href='#顶部'>回到顶部</a><a id=新增人工座席拨打任务> </a>

### 基本信息

**Path：** /addAgentPlan

**Method：** POST

**接口描述：**


### 请求参数

**Headers**

| 参数名称     | 参数值           | 是否必须 | 示例 | 备注 |
| ------------ | ---------------- | -------- | ---- | ---- |
| Content-Type | application/json | 是       |      |      |
| **Body**     |                  |          |      |      |

| 名称         | 类型   | 是否必须 | 备注                                                   |
| ------------ | ------ | -------- | ------------------------------------------------------ |
| clientId     | string | Y        | 分配的用户 clientId                                    |
| nonce        | string | Y        | 6 位随机字符串(字母数字组 合，10 分钟不允许重 复)      |
| timestamp    | number | Y        | 时间戳                                                 |
| signType     | string | Y        | 加密方式                                               |
| sign         | string | Y        | 签名字符串：MD5(相关变量 ascii 排序拼接 +clientSecret) |
| batchName    | string | Y        | 批次名称，用户下唯一                                   |
| agentGroupId | string | Y        | 坐席组编号                                             |
| addType      | string | Y        | 任务增加类型                                           |
| agentId      | string | Y        | 坐席编号                                               |
| callType     | string | N        | 0-不直接外 呼，1-直接 外呼                             |
| mobileList   | string | Y        | 格式为：手机号码^附加 数据^参数 1-参数 2-参数 3        |
| notifyUrl    | string | N        | 回调地址                                               |

### 返回数据

| 名称            | 类型    | 是否必须 | 备注               |
| --------------- | ------- | -------- | ------------------ |
| code            | string  | Y        | 0成功，其他失败    |
| msg             | string  | Y        | 异常描述           |
| success         | boolean | Y        | 是否成功           |
| body            | object  | Y        |                    |
| -failMobileInfo | string  | Y        | 失败手机号信息     |
| -rightCount     | number  | Y        | 当前批次号码成功数 |
| -failCount      | number  | Y        | 当前批次号码失败数 |


