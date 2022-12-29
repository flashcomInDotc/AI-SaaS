# FlashAI SaaS API



# API List

<a id='顶部'></a>

[Adding Outbound Call](#Adding Outbound Call)

[One-Click to Pause Outbound Call](#One-Click to Pause Outbound Call)

[One-Click to Restart Outbound Call](#One-Click to Restart Outbound Call)

[One-Click to Stop Outbound Call](#One-Click to Stop Outbound Call)

[A Phone Call Delete from Outbound Call](#A Phone Call Delete from Outbound Call)

<a href='#Obtaining Users Script Names'>Obtaining User's Script Names</a>

<a href='#Obtaining Users Script Parameter Variables'>Obtaining User's Script Parameter Variables</a>

<a href='#Obtaining Users Line List'>Obtaining User's Line List</a>

<a href='#Check the Batch Call Summary By Searching Batch Number'>Check the Batch Call Summary By Searching  Batch Number</a>

<a href='#Check the Batch Line Dialing Summary By Searching  Batch Number'>Check the Batch Line Dialing Summary By Searching  Batch Number</a>

<a href='#Check the Batch Mobile list By Searching Batch Number'>Check the Batch Mobile list By Searching Batch Number</a>

<a href='#Check the Batch Call list By Searching Batch Number'>Check the Batch Call list By Searching Batch Number</a>

<a href='#Check CallBack Details'>Check CallBack Details</a>

<a href='#Check Agent Group and Agent'>Check  Agent'Group and Agent</a>

<a href='Adding Agent Dialing Task'>Adding Agent' Dialing Task</a>

## Adding Outbound Call

<a href='#顶部'>Back to Top</a><a id='Adding Outbound Call'> </a>

### Basic Information

**Path：**/addPlan

**Method：**POST

**API Description：**

### Request Parameters

**Headers**

| **Parameters Name** | Parm Values      | Y/N（Necessary） | Example | Remarks |
| ------------------- | ---------------- | ---------------- | ------- | ------- |
| Content-Type        | application/json | Y                |         |         |
| **Body**            |                  |                  |         |         |

| Name           | Category | Y/N（Necessary） | Remarks                                                      |
| -------------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId       | string   | Y                | Assigned user clientId                                       |
| nonce          | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp      | number   | Y                | Timestamp                                                    |
| signType       | string   | Y                | Encryption method                                            |
| sign           | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| userId         | number   | Y                | Userid                                                       |
| batchName      | string   | Y                | Batch name，Only one under the user                          |
| botenceId      | string   | Y                | Script Template id                                           |
| callDate       | string   | Y                | The date of the outbound call，For example, if I want to dial on March 26, 2018, the value will be 20180326. If empty value is sent or only date is sent, the field is invalid and will be added to the dialing queue according to the time dialed. |
| callHour       | string   | Y                | The dialing time of Outbound Call, the sendable value's unit in Hour,separated by an English comma (,). For example, if I want to call from 9am-11am (excl.) and 1pm-2pm (excl.), the content to pass is 9,10,13. |
| clear          | number   | Y                | Clear or not Uncompleted Plan during the same day' night, the senable value could be "0" and "1". "0" means Not-Clear, "1" means Clear. |
| api            | boolean  | N                |                                                              |
| lineIds        | string   | N                | Support Multiple lines                                       |
| mobileList     | string   | Y                | The format is: phone number ^ Additional data ^ Parameter 1- Parameter 2- Parameter 3 |
| recall         | number   | Y                | Two types. "0" means  non-recall, "1" means recall           |
| recallParams   | string   | N                | Bound to recall,  if the recall is equal to 1,it has to have a value. If it is empty, it does not participate in encryption |
| notifyUrl      | string   | N                | Callback URL                                                 |
| notifyBatchUrl | string   | N                | Batch callback URL                                           |

### Return Data

| Name            | Category | Y/N（Necessary） | Remarks                                 |
| --------------- | -------- | ---------------- | --------------------------------------- |
| code            | string   | Y                | “0“ means success, other failures       |
| msg             | string   | Y                | Description of the exception            |
| success         | boolean  | Y                | Success or Failure                      |
| body            | object   | Y                |                                         |
| -failMobileInfo | string   | Y                | The information of Failed Cell Phone    |
| -rightCount     | number   | Y                | Successful numbers of the current batch |
| -failCount      | number   | Y                | Failed numbers of the current batch     |

## One-Click to Pause Outbound Call

<a href='#顶部'>Back to Top</a><a id='One-Click to Pause Outbound Call'> </a>

### Basic Information

**Path：** /batchPlanPause

**Method：** POST

**API Description：**

### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |

### Return Data

| Name    | Category | Y/N（Necessary） | Remarks                           |
| ------- | -------- | ---------------- | --------------------------------- |
| code    | string   | Y                | “0“ means success, other failures |
| msg     | string   | Y                | Description of the exception      |
| success | boolean  | Y                | Success or Failure                |
| body    | object   | N                |                                   |



## One-Click to Restart Outbound Call

<a href='#顶部'>Back to Top</a><a id='One-Click to Restart Outbound Call'> </a>

### Basic Information

**Path：** /batchPlanRestart

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |

### Return Data

| Name    | Category | Y/N（Necessary） | Remarks                           |
| ------- | -------- | ---------------- | --------------------------------- |
| code    | string   | Y                | “0“ means success, other failures |
| msg     | string   | Y                | Description of the exception      |
| success | boolean  | Y                | Success or Failure                |
| body    | object   | N                |                                   |



## One-Click to Stop Outbound Call

<a href='#顶部'>Back to Top</a><a id='One-Click to Stop Outbound Call'> </a>

### Basic Information

**Path：** /batchPlanStop

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |

### Return Data

| Name    | Category | Y/N（Necessary） | Remarks                           |
| ------- | -------- | ---------------- | --------------------------------- |
| code    | string   | Y                | “0“ means success, other failures |
| msg     | string   | Y                | Description of the exception      |
| success | boolean  | Y                | Success or Failure                |
| body    | object   | N                |                                   |



## A Phone Call Delete from Outbound Call

<a href='#顶部'>Back to Top</a><a id='A Phone Call Delete from Outbound Call'> </a>

### Basic Information

**Path：** /batchPhoneDelete

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |
| phoneList | string   | Y                | phone1^phone 2                                               |

### Return Data

| Name    | Category | Y/N（Necessary） | Remarks                           |
| ------- | -------- | ---------------- | --------------------------------- |
| code    | string   | Y                | “0“ means success, other failures |
| msg     | string   | Y                | Description of the exception      |
| success | boolean  | Y                | Success or Failure                |
| body    | object   | N                |                                   |



## Obtaining User's Script Names

<a href='#顶部'>Back to Top</a><a id='Obtaining Users Script Names'> </a>

### Basic Information

**Path：** /getBotence

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |

### Return Data

| Name         | Category | Y/N（Necessary） | Remarks                              |
| ------------ | -------- | ---------------- | ------------------------------------ |
| code         | string   | Y                | “0“ means success, other failures    |
| msg          | string   | Y                | Description of the exception         |
| success      | boolean  | Y                | Success or Failure                   |
| body         | object   | N                |                                      |
| -botenceList | string   | Y                | List of Script Name，Splicing with\| |



## Obtaining User's Script Parameter Variables

<a href='#顶部'>Back to Top</a><a id='Obtaining Users Script Parameter Variables'> </a>

### Basic Information

**Path：** /queryPlanParams

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |

### Return Data

| Name          | Category | Y/N（Necessary） | Remarks                                                      |
| ------------- | -------- | ---------------- | ------------------------------------------------------------ |
| code          | string   | Y                | “0“ means success, other failures                            |
| msg           | string   | Y                | Description of the exception                                 |
| success       | boolean  | Y                | Success or Failure                                           |
| body          | object   | N                |                                                              |
| -paramSeqLsit | string   | Y                | Returning as paramSeqLsit information, in the following form：paramName^seq^paramType |



## Obtaining User's Line List

<a href='#顶部'>Back to Top</a><a id='Obtaining Users Line List'> </a>

### Basic Information

**Path：** /getCallLine

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |

### Return Data

| Name      | Category | Y/N（Necessary） | Remarks                           |
| --------- | -------- | ---------------- | --------------------------------- |
| code      | string   | Y                | “0“ means success, other failures |
| msg       | string   | Y                | Description of the exception      |
| success   | boolean  | Y                | Success or Failure                |
| body      | object   | N                |                                   |
| -lineList | string   | Y                | List of Line, Splicing with\|     |



## Check the Batch Call Summary By Searching  Batch Number

<a href='#顶部'>Back to Top</a><a id='Check the Batch Call Summary By Searching  Batch Number'> </a>

### Basic Information

**Path：** /getBatchPlanCallSummary

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |

### Return Data

| Name         | Category | Y/N（Necessary） | Remarks                                |
| ------------ | -------- | ---------------- | -------------------------------------- |
| code         | string   | Y                | “0“ means success, other failures      |
| msg          | string   | Y                | Description of the exception           |
| success      | boolean  | Y                | Success or Failure                     |
| body         | object   | N                |                                        |
| -batchName   | string   | Y                | Batch's name，Only one under the user  |
| -acceptCount | number   | Y                | Nember of Cell. received by the system |
| -endCount    | number   | Y                | Number of Cell. in Completion          |
| -planCount   | number   | Y                | Nember of Cell. In the Plan            |



## Check the Batch Line Dialing Summary By Searching Batch Number

<a href='#顶部'>Back to Top</a><a id=Check the Batch Line Dialing Summary By Searching Batch Number> </a>

### Basic Information

**Path：** /getBatchSummaryGroupByLine

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |

### Return Data

| Name         | Category | Y/N（Necessary） | Remarks                                                      |
| ------------ | -------- | ---------------- | ------------------------------------------------------------ |
| code         | string   | Y                | “0“ means success, other failures                            |
| msg          | string   | Y                | Description of the exception                                 |
| success      | boolean  | Y                | Success or Failure                                           |
| body         | object   | N                |                                                              |
| -batchName   | string   | Y                | Batch's name，Only one under the user                        |
| -lineSummary | string   | Y                | Line id ^Number of Cell. Received ^ Number of completed calls using this Line^<br/>Last call time using this line lineId^totalNum^e ndCount^lastCallT ime |



## Check the Batch Mobile list By Searching Batch Number

<a href='#顶部'>Back to Top</a><a id=Check the Batch Mobile list By Searching Batch Number> </a>

### Basic Information

**Path：** /getBatchPlanList

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name        | Category | Y/N（Necessary） | Remarks                                                      |
| ----------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId    | string   | Y                | Assigned user clientId                                       |
| nonce       | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp   | number   | Y                | Timestamp                                                    |
| signType    | string   | Y                | Encryption method                                            |
| sign        | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName   | string   | Y                | Batch's name，Only one under the user                        |
| phoneStatus | number   | N                | Status 1- Planning, 2- Completed, 3- Processing Failed       |
| page        | number   | Y                | PageNumber                                                   |
| pageNum     | number   | Y                | The Max number of items, 5000 per page                       |

### Return Data

| Name         | Category | Y/N（Necessary） | Remarks                                                      |
| ------------ | -------- | ---------------- | ------------------------------------------------------------ |
| code         | string   | Y                | “0“ means success, other failures                            |
| msg          | string   | Y                | Description of the exception                                 |
| success      | boolean  | Y                | Success or Failure                                           |
| body         | object   | N                |                                                              |
| -batchName   | string   | Y                | Batch's name，Only one under the user                        |
| -batchCount  | string   | Y                | Cell. Number, the Cell. Number successfully received by the system |
| -mobileList  | string   | Y                | Mobile List, The format is: phone number ^ Additional data ^ Parameter 1- Parameter 2- Parameter 3 |
| -phoneStatus | number   | Y                | 1- Planning, 2- Completed, 3- Processing Failed              |
| -totalPage   | number   | Y                | Total Pages                                                  |
| -totalRecord | number   | Y                | Total number of datasets after searching by condition        |
| -page        | number   | Y                | Current page number                                          |
| -pageNum     | number   | Y                | Number of entries per page                                   |

mobileList is an array of objects spliced in the following format.
"phone1^attach1^params11-params12-
params13^custName1^custCompany1^1**|**phone2^attach2^params11-params12-
params13^custName2^custCompany2^1."
The array objects in the mobileList are split by "|", the parameters are split by ^, and the items in the additional parameters are split by "-".

## Check the Batch Call list By Searching Batch Number

<a href='#顶部'>Back to Top</a><a id=Check the Batch Call list By Searching Batch Number> </a>

### Basic Information

**Path：** /getBatchPlanCallList

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |
| notifyUrl | string   | Y                | Callback URL                                                 |
| page      | number   | Y                | PageNumber                                                   |
| pageNum   | number   | Y                | The Max number of items, 5000 per page                       |

### Return Data

| Name         | Category | Y/N（Necessary） | Remarks                                                      |
| ------------ | -------- | ---------------- | ------------------------------------------------------------ |
| code         | string   | Y                | “0“ means success, other failures                            |
| msg          | string   | Y                | Description of the exception                                 |
| success      | boolean  | Y                | Success or Failure                                           |
| body         | object   | N                |                                                              |
| -batchName   | string   | Y                | Batch's name，Only one under the user                        |
| -batchCount  | string   | Y                | Cell. Number, the Cell. Number successfully received by the system |
| -callList    | string   | Y                | Call List，Format as: mobile number^outbound date^call time^hang up time^answer time^call duration^intent tag^intent note^F class details^...... |
| -totalPage   | number   | Y                | Total Pages                                                  |
| -totalRecord | number   | Y                | Total number of datasets after searching by condition        |
| -page        | number   | Y                | Current page number                                          |
| -pageNum     | number   | Y                | Number of entries per page                                   |

callList is an array spliced together. The format is as follows:
"callStartTime1^handupTime1...**|**callStartTime1^handupTime1.^.."
The array objects in callList are divided by "|" and the parameters are divided by ^. In particular, the data in detailList is divided by "$" and the parameters are divided by _.

botAnswerText1-botAnswerTime1-customerSayText1-
customerSayTime1$botAnswerText2-botAnswerTime2-customerSayText2-
customerSayTime2

## Check CallBack Details

<a href='#顶部'>Back to Top</a><a id=Check CallBack Details> </a>

### Basic Information

**Path：** /getPhoneDetail

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName | string   | Y                | Batch's name，Only one under the user                        |
| phone     | string   | Y                | Phone Number                                                 |

### Return Data

| Name    | Category | Y/N（Necessary） | Remarks                           |
| ------- | -------- | ---------------- | --------------------------------- |
| code    | string   | Y                | “0“ means success, other failures |
| msg     | string   | Y                | Description of the exception      |
| success | boolean  | Y                | Success or Failure                |
| body    | object   | N                |                                   |

## Check Agent'Group and Agent

<a href='#顶部'>Back to Top</a><a id=Check Agent Group and Agent> </a>

### Basic Information

**Path：** /queryAgentGroup

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name      | Category | Y/N（Necessary） | Remarks                                                      |
| --------- | -------- | ---------------- | ------------------------------------------------------------ |
| clientId  | string   | Y                | Assigned user clientId                                       |
| nonce     | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp | number   | Y                | Timestamp                                                    |
| signType  | string   | Y                | Encryption method                                            |
| sign      | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |

### Return Data

| Name             | Category | Y/N（Necessary） | Remarks                           |
| ---------------- | -------- | ---------------- | --------------------------------- |
| code             | string   | Y                | “0“ means success, other failures |
| msg              | string   | Y                | Description of the exception      |
| success          | boolean  | Y                | Success or Failure                |
| body             | object   | N                |                                   |
| -records         | list     | Y                | Agents' List                      |
| --agentGroupId   | string   | Y                | Agent Group Numebr                |
| --agentGroupName | string   | Y                | Agent Group Name                  |
| --agentId        | string   | Y                | Agent' Number                     |
| --agentName      | string   | Y                | Agent' Name                       |

## Adding Agent' Dialing Task

<a href='#顶部'>Back to Top</a><a id=Adding Agent Dialing Task> </a>

### Basic Information

**Path：** /addAgentPlan

**Method：** POST

**API Description：**


### Request Parameters

**Headers**

| Param Name   | Param Values     | Y/N（Necessary） | Example | Remarks |
| ------------ | ---------------- | ---------------- | ------- | ------- |
| Content-Type | application/json | Y                |         |         |
| **Body**     |                  |                  |         |         |

| Name         | Category | Y/N（Necessary） | Remarks                                                      |
| ------------ | -------- | ---------------- | ------------------------------------------------------------ |
| clientId     | string   | Y                | Assigned user clientId                                       |
| nonce        | string   | Y                | 6-bit random string（Alphanumeric combinations, No repetition allowed within 10 minutes） |
| timestamp    | number   | Y                | Timestamp                                                    |
| signType     | string   | Y                | Encryption method                                            |
| sign         | string   | Y                | Signed string: MD5 (related variables ascii sorted spliced +clientSecret) |
| batchName    | string   | Y                | Batch's name，Only one under the user                        |
| agentGroupId | string   | Y                | Agent Group Numebr                                           |
| addType      | string   | Y                | Type of task addition                                        |
| agentId      | string   | Y                | Agent' Number                                                |
| callType     | string   | N                | 0 - no direct outbound call, 1 - direct outbound call        |
| mobileList   | string   | Y                | The format is: phone number ^ Additional data ^ Parameter 1- Parameter 2- Parameter 3 |
| notifyUrl    | string   | N                | Callback URL                                                 |

### Return Data

| Name            | Category | Y/N（Necessary） | Remarks                                 |
| --------------- | -------- | ---------------- | --------------------------------------- |
| code            | string   | Y                | “0“ means success, other failures       |
| msg             | string   | Y                | Description of the exception            |
| success         | boolean  | Y                | Success or Failure                      |
| body            | object   | N                |                                         |
| -failMobileInfo | string   | Y                | The information of Failed Cell Phone    |
| -rightCount     | number   | Y                | Successful numbers of the current batch |
| -failCount      | number   | Y                | Failed numbers of the current batch     |
