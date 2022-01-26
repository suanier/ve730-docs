## 修订记录

| 日期       | 修订版本 | 修改描述 | 作者 |
| ---------- | -------- | -------- | ---- |
| 2021/12/20 | V 1.0.0  | 新建     | 杨升 |

## 目录

```
1. API接口概览和测试数据
2. 接口命名规则
3. 接口说明
	3.1 第三方客户对接说明
		3.1.1 第三方接口凭证获取
		3.1.2 第三方刷卡（手环）登录验证
		3.1.4 维塑推送合成通知消息
		3.1.5 第三方状态码
	3.2 获取维塑接口凭证
		3.2.1 获取维塑接口凭证
		3.2.2 用户信息绑定
	3.3 获取体测文件及数据
		3.3.1 获取体测文件
		3.3.2 获取体成分数据
		3.3.3 获取围度数据
		3.3.4 获取用户脂肪等级
		3.3.5 获取身体评分
	3.5 获取节段文件数据
		3.5.1 获取节段文件
		3.5.2 获取节段数据
	3.6 获取体型预测文件及数据
		3.6.1 获取体型预测文件
		3.6.2 获取预测调节数据
	3.7 获取报告信息
		3.7.1 获取报告信息
	3.8 维塑返回状态码说明
	3.9 合成推送类型与接口关系说明
```

## 1.文档介绍

### 1.1API 接口概览

| 接口                       | 接口功能                                                                                                                                     |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 获取第三方凭证接口         | 获取可访问第三方接口凭证的地址。由第三方客户提供，接口格式、传入返回参数参照 3.1.1                                                           |
| 请求第三方二维码接口       | 用户在设备端完成测量后的结果二维码，由第三方客户提供，接口格式、传入返回参数参照 3.1.2                                                       |
| 第三方刷卡（手环）登录验证 | 维塑服务调用此接口向第三方进行刷卡或手环用户身份验证。由第三方客户提供，接口格式、传入返回参数参照 3.1.3                                     |
| 维塑推送合成通知消息       | 体测、体态、节段分布结果及扫描相关信息，调用此接口向第三方服务推送信息。由第三方客户提供，接口格式、传入返回参数参照 3.1.4                   |
| 获取维塑接口凭证           | 第三方客户调用此接口获取维塑相关接口凭证，vfid 和 vfsecret 从维塑管理平台获取                                                                |
| 用户信息绑定               | 第三方 app 扫描设备端二维码后，在第三方后台验证用户和设备或第三方验证 RFID（手环）用户身份通过后，调用此接口通知维塑后台服务从而发起合成请求 |
| 体测文件数据接口           | 体测模型合成成功，第三方客户调用此接口获取体测模型和数据                                                                                     |
| 节段文件接口               | 节段分布合成成功后，第三方客户调用此接口获取节段分布文件                                                                                     |
| 体型预测接口               | 体型预测合成成功后，第三方客户调用此接口获取体型预测数据                                                                                     |
| 返回状态码说明             | 状态码说明                                                                                                                                   |

### 1.2 测试数据

| 参数名 | 参数值 |
| ------ | ------ |
| key    |        |
| secret | ​      |
|  |
| scanid |        |

## 2. 接口规则

### 2.1 命名规则

https://[域名]/[版本号]/[接口名]

例：[http://api.e730.visbody.com/v1/token](http://api.e560.visbody.com/v1/token)

| 实例                    | 说明   |
| ----------------------- | ------ |
| api.e730.visbodyfit.com | 域名   |
| v1                      | 版本号 |
| token                   | 接口名 |

### 2.2 版本控制

接口版本通过路由控制

```
HTTP GET:
http://api.e730.visbody.com/v1/token
// v2版本
http://api.e730.visbody.com/v2/token
```

### 2.3 POST 提交方式

Content-Type: application/json

## 3. 接口说明

### 3.1 第三方客户对接说明

目前支持 API 对接、刷卡器/扫码器对接 2 种方式。

> 需要在售后管理平台开通第三方对接功能

#### 1. API 对接

**使用说明：**
可通过维塑提供的 API 接口获取用户测量数据。
对接成功后维塑会通过客户配置的 3.1.4 接口推送扫描 ID 等相关信息，客户根据测量项目结果访问对应接口获取数据，合成推送类型与接口关系见 3.9 说明
​

![image.png](https://cdn.nlark.com/yuque/0/2021/png/287793/1640066017083-b740cc34-8a86-4cac-95a0-b302d6629653.png#clientId=u75d3ec2c-c5ba-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=1489&id=ue696885c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1489&originWidth=1974&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143835&status=done&style=none&taskId=u197b4dc4-2111-4320-bbcc-865343e9084&title=&width=1974)

**对接说明：**

- 申请 API 对接权限
- 通过维塑管理平台 API 对接设置配置 3.1.1、3.1.4 接口

#### 2. 刷卡器/扫码器对接

**使用说明： **
设备添加刷卡器或扫码器，可通过刷卡或扫码代替手机扫码动作，需客户自行开发刷卡或扫码的业务逻辑
​

![image.png](https://cdn.nlark.com/yuque/0/2021/png/287793/1640066101453-1b677bb1-a639-47d2-a2f3-a340608276d0.png#clientId=u75d3ec2c-c5ba-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=855&id=u3751c322&margin=%5Bobject%20Object%5D&name=image.png&originHeight=855&originWidth=1136&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127005&status=done&style=none&taskId=ua9a87d7d-65a4-4933-b3e3-4d65f71a23a&title=&width=1136)

**对接说明：**

- 申请 API 对接权限
- 通过维塑管理平台 API 对接设置配置 3.1.1、3.1.3、3.1.4 接口
- 用户刷卡或扫码后通过维塑 3.2.2 接口发起用户信息绑定及合成

​

#### 3.1.1 第三方接口凭证获取 :id=third-token

**接口描述：**

由客户提供获取可访问第三方接口如 3.1.2、3.1.3、3.1.4 等接口的凭证地址

**请求 URL 格式要求：**

- `<http|https>://<域名>/<path>`
- `http://<host>:<port>/<path>`

**请求方式：**

- GET

**参数：**

| 参数名 | 必选 | 类型   | 说明                          |
| ------ | ---- | ------ | ----------------------------- |
| key    | 是   | string | 用户唯一凭证,由第三方提供     |
| secret | 是   | string | 用户唯一凭证密钥,由第三方提供 |

**正常时返回示例**

```
  {
    "code": 0,
    "data": {
      "token": "TOKEN",
      "expires_in": 7200
    }
  }
```

**错误时返回示例**

```
  {
    "code": 30001,
    "error_msg": 'ERROR_MSG'
  }
```

**返回参数说明**

| 参数名     | 类型   | 说明                             |
| ---------- | ------ | -------------------------------- |
| code       | int    | 状态码,返回状态码参考 3.1.5 说明 |
| error_msg  | string | 错误信息                         |
| token      | string | 接口凭证                         |
| expires_in | int    | 凭证有效时间                     |

####

#### 3.1.2 第三方刷卡（扫码器）登录验证 :id=crad-login

**接口描述：**

用户在设备端使用第三方客户的会员卡或扫码器进行登录时，调用此接口向第三方服务进行用户身份验证

**请求 URL 格式要求：**

- `<http|https>://<域名>/<path>`
- `http://<host>:<port>/<path>`

**请求方式：**

- GET

**参数：**

| 参数名    | 必选 | 类型   | 说明           |
| --------- | ---- | ------ | -------------- |
| card_id   | 是   | string | 卡或手环 ID    |
| scan_id   | 是   | string | 扫描 ID        |
| device_id | 是   | string | 设备 ID        |
| token     | 是   | string | 第三方接口凭证 |

**正常时返回示例**

```
  {
    "code": 0,
    "data": {
      "name": "Name",
	  	"sex":1,
	  	"birthday":"2009-10-10",
	  	"height": 170,
	  	"third_uid":"id100000",
    	"type": 1
    }
  }
```

**错误时返回示例**

```
  {
    "code": 30001,
    "error_msg": 'ERROR_MSG'
  }
```

**返回参数说明**

| 参数名    | 类型   | 说明                              |
| --------- | ------ | --------------------------------- |
| code      | int    | 状态码 ,返回状态码参考 3.1.5 说明 |
| error_msg | string | 错误信息                          |
| name      | string | 用户名                            |
| sex       | int    | 性别 1 男 2 女                    |
| birthday  | string | 生日(1990-10-10)                  |
| height    | string | 用户身高                          |
| third_uid | string | 用户唯一标识（只支持数字+字母）   |
| type      | int    | 对接类型 1 刷卡器，2 扫码         |

#### 3.1.4 维塑推送合成通知消息 :id=notify

**接口描述：**

用户在设备端使用第三方客户的会员卡或手环进行登录成功后，体测、体态、节段分布结果及扫描相关信息，调用此接口向第三方服务推送信息

**请求 URL 格式要求：**

- `<http|https>://<域名>/<path>`
- `http://<host>:<port>/<path>`

**请求方式：**

- POST

**参数：**

| 参数名                  | 必选 | 类型   | 说明                                       |
| ----------------------- | ---- | ------ | ------------------------------------------ |
| scan_id                 | 是   | string | 扫描 ID                                    |
| device_id               | 是   | string | 设备 ID                                    |
| time                    | 是   | date   | 完成时间 时间格式 2018-06-25 10:10:10      |
| user_info               | 否   | object | 用户信息                                   |
| age                     | 否   | int    | 年龄                                       |
| birthday                | 否   | string | 生日                                       |
| third_uid               | 否   | string | 用户唯一标识（只支持数字+字母）            |
| sex                     | 否   | string | f 女，m 　男                               |
| height                  | 否   | int    | 身高                                       |
| action_status           | 是   | object | 状态信息                                   |
| measure_status          | 否   | int    | 体测的合成状态，０失败，１成功，２超时     |
| eval_status             | 否   | int    | 体态的合成状态，０失败，１成功，２超时     |
| bia_status              | 否   | int    | 体成分的合成状态，０失败，１成功，２超时   |
| bodypredict_status      | 否   | int    | 体型预测的合成状态，０失败，１成功，２超时 |
| tchar_status            | 否   | int    | 节段分布的合成状态，０失败，１成功，２超时 |
| eval_dynamic_status     | 否   | int    | 劲部的合成状态，０失败，１成功，２超时     |
| eval_dynamic_hip_status | 否   | int    | 髋关节的合成状态，0 失败，1 成功，2 超时   |
| token                   | 是   | string | 第三方接口凭证                             |

**格式如下**

```
{
  "user_info": {
    "age": 26,
    "birthday": "1992-12-12",
    "height": 178,
    "phone": "13812345678",
    "sex": "f"
  },
  "action_status":{
    "measure_status":0,
    "eval_status":0,
    "bia_status":0,
    "bodypredict_status":0,
    "tchar_status":0，
    "eval_dynamic_status":0,
    "eval_dynamic_hip_status":0
  },
  "device_id": "20041910080001",
  "scan_id": "20041910080001-a210136e-1bfb-11ea-b711-00d861a9ecd9",
  "time": "2019-12-11 17:56:15",
  "token": "TOKEN"
}
```

**正常时返回示例**

```
  {
    "code": 0
  }
```

正确接收到通知请求后必须响应，否则维塑服务会发起 3 次重传

**错误时返回示例**

```
  {
    "code": 30001,
    "error_msg": 'ERROR_MSG'
  }
```

**返回参数说明**

| 参数名    | 类型   | 说明                              |
| --------- | ------ | --------------------------------- |
| code      | int    | 状态码 ,返回状态码参考 3.1.5 说明 |
| error_msg | string | 错误信息                          |

#### 3.1.5 第三方状态码

描述：以上接口第三方客户请按以下状态码返回相关状态信息

| 状态码 | 备注         |
| ------ | ------------ |
| 0      | 请求成功     |
| 30001  | 无效的 token |
| 30002  | 刷卡失败     |
| 30003  | 扫码失败     |

### 3.2 获取维塑接口凭证

#### 3.2.1 获取维塑接口凭证 :id=get-token

**接口描述：**

- 用于获取调用维塑接口凭证

**请求 URL：**

- `http://api.plus.visbody.com/v1/token`

**请求方式：**

- GET

**参数：**

| 参数名 | 必选 | 类型   | 说明                                |
| ------ | ---- | ------ | ----------------------------------- |
| key    | 是   | string | 第三方用户唯一凭证，即 vfid         |
| secret | 是   | string | 第三方用户唯一凭证密钥，即 vfsecret |

**正常时返回示例**

```
  {
    "code": 0,
    "data": {
      "token": "TOKEN",
      "expires_in": 3600
    }
  }
```

**错误时返回示例**

```
  {
    "code": 40001,
    "error_msg": 'ERROR_MSG'
  }
```

**返回参数说明**

| 参数名     | 类型   | 说明                           |
| ---------- | ------ | ------------------------------ |
| code       | int    | 状态码,返回状态码参考 3.8 说明 |
| error_msg  | string | 错误信息                       |
| token      | string | 接口凭证                       |
| expires_in | int    | 凭证有效时间 单位秒            |

** vfid、vfsecret 获取方式： **

- 1.开通维塑管理系统账号
- 2.申请开通 API 对接权限
- 3.在维塑管理系统设备对接页根据页面提示完成 API 对接后，获取 vfid、vfsecret

** token 的使用方式 ** 1.在通过 POST 或 GET 请求中以普通参数传入 2.在请求头中添加 Authorization Bearer Token, 以 php 为例

```
$headers[]  =  "Content-Type: application/json";
$headers[]  =  "Authorization: Bearer ". $vfToken;
```

#### 3.2.2 用户信息绑定

**接口描述：**

- 第三方 app 扫描设备端二维码后，在第三方后台验证用户和设备或第三方验证 RFID（手环）用户身份通过后，调用此接口通知维塑后台服务从而发起合成请求

**请求 URL：**

- `http://api.e730.visbody.com/v1/dataBind`

**请求方式：**

- POST

**参数：**

| 参数名    | 必选 | 类型   | 说明                                               |
| --------- | ---- | ------ | -------------------------------------------------- |
| scan_id   | 是   | string | 扫描 ID                                            |
| device_id | 是   | string | 设备 ID                                            |
| third_uid | 是   | string | 第三方用户唯一 Id 字母和数字 长度 8 ~ 40           |
| sex       | 是   | int    | 性别 1 男 2 女                                     |
| height    | 是   | int    | 身高  110 ~ 205 单位 cm                            |
| birthday  | 是   | string | 生日 格式 yyyy-MM-dd 注意周岁范围需在 18 ~ 99 之间 |
| token     | 是   | string | 接口凭证                                           |

**正常时返回示例**

```
  {
    "code": 0,
    "data": {
      "result":TRUE
    }
  }
```

**错误时返回示例**

```
  {
    "code": 40001,
    "error_msg": 'ERROR_MSG'
  }
```

**返回参数说明**

| 参数名    | 类型    | 说明                           |
| --------- | ------- | ------------------------------ |
| code      | int     | 状态码,返回状态码参考 3.8 说明 |
| error_msg | string  | 错误信息                       |
| result    | boolean | 发起合成结果                   |

** token 的使用方式 ** 1.在通过 POST 或 GET 请求中以普通参数传入 2.在请求头中添加 Authorization Bearer Token, 以 php 为例

```
$headers[]  =  "Content-Type: application/json";
$headers[]  =  "Authorization: Bearer ". $vfToken;
```

### 3.3 获取体测文件数据

#### 3.3.1 获取体测文件

**接口描述：**

- 用于获取体测模型、围度 json、模型围度图片文件

**请求 URL：**

- `http://api.e730.visbody.com/v1/measure/file`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "model_url": "MODEL_URL",
      "json_url": "JSON_URL",
	  "pic_measure_url": "PIC_MEASURE_URL",
      "expires_in": 7200
    }
  }
```

**返回参数说明**

| 参数名          | 类型   | 说明                                                                   |
| --------------- | ------ | ---------------------------------------------------------------------- |
| model_url       | string | 体测模型文件路径，文件格式.obj                                         |
| json_url        | string | 围度 json 文件路径，文件格式.json,可配合模型文件展示围度的位置以及数据 |
| pic_measure_url | string | 模型围度图片文件路径，文件格式.jpg                                     |
| expires_in      | int    | 文件路径有效时间（秒）                                                 |

#### 3.3.2 获取体成分数据

**接口描述：**

- 用于获取体测体成分数据

**请求 URL：**

- `http://api.e730.visbody.com/v1/measure/mass`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
    	"WT": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"FFM": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BFM": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LM": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"TBW": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BMI": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"PBF": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BMR": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"WHR": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"SM": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"TM": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"PROTEIN": {"l":10,"m":15,"h":20,"v":30.3,"status":3}，
		"ICW": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"ECW": {"l":10,"m":15,"h":20,"v":30.3,"status":3}
    }
  }
```

**返回参数说明**

| 参数名  | 类型   | 说明                 |
| ------- | ------ | -------------------- |
| WT      | object | 体重（kg）           |
| FFM     | object | 去脂体重（kg）       |
| BFM     | object | 体脂肪量（kg）       |
| LM      | object | 肌肉量（kg）         |
| TBW     | object | 身体水分（kg）       |
| BMI     | object | 身体质量             |
| PBF     | object | 体脂肪率（%）        |
| BMR     | object | 基础代谢量（kcal/d） |
| WHR     | object | 腰臀比               |
| SM      | object | 骨骼肌量（kg）       |
| TM      | object | 无机盐（kg）         |
| PROTEIN | object | 蛋白质（kg）         |
| ICW     | object | 细胞内液（kg）       |
| ECW     | object | 细胞外液（kg）       |

**体成分范围说明**

```
  {
	"l":10,        // 下限值
	"m":15,        // 标准值
	"h":20,        // 上限值
	"v":30.3,      // 测量值
	"status":3     // 状态 1 低，２正常，３高
  }
```

#### 3.3.3 获取围度数据

**接口描述：**

- 用于获取体测围度数据

**请求 URL：**

- `http://api.e730.visbody.com/v1/measure/girth`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "bust_girth": 30.6,
      "waist_girth": 30.8,
	  "hip_girth": 93.8,
	  "left_upper_arm_girth": 90,
	  "right_upper_arm_girth": 99.8,
	  "left_thigh_girth": 58,
	  "right_thigh_girth": 56.2,
	  "left_calf_girth": 37.1,
	  "right_calf_girth": 34.5,
	  "height": 161.1
    }
  }
```

**返回参数说明**

| 参数名                | 类型   | 说明         |
| --------------------- | ------ | ------------ |
| bust_girth            | double | 胸围(cm)     |
| waist_girth           | double | 腰围(cm)     |
| hip_girth             | double | 臀围(cm)     |
| left_upper_arm_girth  | double | 左上臂围(cm) |
| right_upper_arm_girth | double | 右上臂围(cm) |
| left_thigh_girth      | double | 左大腿围(cm) |
| right_thigh_girth     | double | 右大腿围(cm) |
| left_calf_girth       | double | 左小腿围(cm) |
| right_calf_girth      | double | 右小腿围(cm) |
| height                | double | 输入身高(cm) |

#### 3.3.4 获取用户脂肪等级

**接口描述：**

- 用于用户脂肪等级

**请求 URL：**

- `http://api.e730.visbody.com/v1/body/state`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
		"va_grade":9
    }
  }
```

**返回参数说明**

| 参数名   | 类型 | 说明                                                  |
| -------- | ---- | ----------------------------------------------------- |
| va_grade | int  | 内脏脂肪等级(110 正常，1014 过高，14~17 高，>17 超高) |

#### 3.3.5 获取用户身体评分

**接口描述：**

- 用于用户身体评分

**请求 URL：**

- `http://api.e730.visbody.com/v1/body/score`

**请求方式：**

- GET

**参数：**

| 参数名    | 必选 | 类型   | 说明                   |
| --------- | ---- | ------ | ---------------------- |
| token     | 是   | string | 接口凭证               |
| scan_id   | 是   | string | 扫描 ID                |
| scan_type | 是   | int    | 扫描类型 1 体测 2 体态 |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "score": 98
    }
  }
```

**返回参数说明**

| 参数名 | 类型 | 说明     |
| ------ | ---- | -------- |
| score  | int  | 项目评分 |

###

### 3.5 获取节段文件数据

#### 3.5.1 获取节段文件

**接口描述：**

- 用于获取节段文件

**请求 URL：**

- `http://api.e730.visbody.com/v1/seg/spread/file`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "m_file_url":"M_FILE_URL",
	  "m_pic_url":"M_PIC_URL",
	  "f_file_url":"F_FILE_URL",
	  "f_pic_url":"F_PIC_URL",
	  "expires_in":7200
    }
  }
```

**返回参数说明**

| 参数名     | 类型   | 说明                              |
| ---------- | ------ | --------------------------------- |
| m_file_url | string | 节段肌肉分布文件，文件格式 .js    |
| m_pic_url  | string | 节段肌肉分布热力图，文件格式 .jpg |
| f_file_url | string | 节段脂肪分布文件，文件格式 .js    |
| f_pic_url  | string | 节段脂肪分布热力图，文件格式 .jpg |
| expires_in | int    | 文件路径有效时间                  |

#### 3.5.2 获取节段数据

**接口描述：**

- 用于获取节段数据

**请求 URL：**

- `http://api.e730.visbody.com/v1/seg/spread/data`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
    	"BFMLA": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BFMRA": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BFMTR": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BFMLL": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"BFMRL": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LMLA": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LMRA": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LMTR": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LMLL": {"l":10,"m":15,"h":20,"v":30.3,"status":3},
		"LMRL": {"l":10,"m":15,"h":20,"v":30.3,"status":3}
    }
  }
```

**返回参数说明**

| 参数名 | 类型   | 说明                 |
| ------ | ------ | -------------------- |
| BFMLA  | object | 左上肢节段脂肪（kg） |
| BFMRA  | object | 右上肢节段脂肪（kg） |
| BFMTR  | object | 躯干节段脂肪（kg）   |
| BFMLL  | object | 左下肢节段脂肪（kg） |
| BFMRL  | object | 右下肢节段脂肪（kg） |
| LMLA   | object | 左上肢节段肌肉（kg） |
| LMRA   | object | 右上肢节段肌肉（kg） |
| LMTR   | object | 躯干节段肌肉（kg）   |
| LMLL   | object | 左下肢节段肌肉（kg） |
| LMRL   | object | 右下肢节段肌肉（kg） |

**体成分范围说明**

```
  {
	"l":10,        // 下限值
	"m":15,        // 标准值
	"h":20,        // 上限值
	"v":30.3,      // 测量值
	"status":3     // 状态 1 低，２正常，３高
  }
```

### 3.6 获取体型预测文件及数据

#### 3.6.1 获取体型预测文件

**接口描述：**

- 用于获取体型预测文件接口

**请求 URL：**

- `http://api.e730.visbody.com/v1/forecast/file`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "model_url":"MODEL_URL",
	  "expires_in":7200
    }
  }
```

**返回参数说明**

| 参数名     | 类型   | 说明                            |
| ---------- | ------ | ------------------------------- |
| model_url  | string | 体型预测模型文件，文件格式 .obj |
| expires_in | int    | 文件路径有效时间                |

#### 3.6.2 获取预测调节数据

**接口描述：**

- 用于获取体型预测的身体调节量

**请求 URL：**

- `http://api.e730.visbody.com/v1/forecast/adjust`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      "weight":1.8,
	  "body_fat":-2.6,
	  "muscle":-2.6,
	  "gr_weight":75,
	  "gr_body_fat":12.3,
	  "gr_muscle":15.1,
    }
  }
```

**返回参数说明**

| 参数名      | 类型   | 说明           |
| ----------- | ------ | -------------- |
| weight      | double | 体重调节量     |
| body_fat    | double | 体脂肪调节量   |
| muscle      | double | 肌肉调节量     |
| gr_weight   | double | 体重黄金比例   |
| gr_body_fat | double | 体脂肪黄金比例 |
| gr_muscle   | double | 肌肉黄金比例   |

### 3.7 获取报告信息

#### 3.7.1 获取报告信息

**接口描述：**

- 用于获取本次测量报告的结论、建议及测量时间

**请求 URL：**

- `http://api.e730.visbody.com/v1/report/msg`

**请求方式：**

- GET

**参数：**

| 参数名  | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| token   | 是   | string | 接口凭证 |
| scan_id | 是   | string | 扫描 ID  |

**返回示例**

```
  {
    "code": 0,
    "data": {
      	"advice":[
			"别偷懒，加速养成良好的运动饮食习惯。",
			"严重的体态问题将会影响您的正常生活，请教练对您的体态做进一步的评估。",
			"请找专业人士对颈部做进一步筛查。"
		],
		"conclusion":[
			"您目前的体成分状况一般，体型为肌肉型，体脂率偏高，体重正常。",
			"您目前的体态状况较差,存在长短腿,高低肩,头前引,圆肩,骨盆前/后倾的可能性。"，
			"颈椎后伸活动度受限。颈椎前屈活动度过大。"
		],
		"scanTime": "2020-05-09 13:52:06"
    }
  }
```

**返回参数说明**

| 参数名     | 类型   | 说明         |
| ---------- | ------ | ------------ |
| advice     | array  | 建议         |
| conclusion | array  | 结论         |
| scanTime   | string | 报告测量时间 |

注：结论及建议包含所有测量项目，若只做单个项目则只返回单个项目结论及建议

### 3.8 维塑返回状态码说明

维塑的接口响应通过 HTTP 状态码及业务状态码区分，业务状态码在 response body 里标记

| HTTP 状态码 | 业务状态码 | 备注                                                                |
| ----------- | ---------- | ------------------------------------------------------------------- |
| 500         | -1         | 系统繁忙                                                            |
| 200         | 0          | 请求成功                                                            |
| 400         | 40001      | 无效的请求路径                                                      |
| 400         | 40002      | 无效的 vfid 或 secret                                               |
| 400         | 40003      | 无效的 token                                                        |
| 400         | 40004      | 参数错误                                                            |
| 400         | 40005      | 未绑定设备信息                                                      |
| 400         | 40006      | 无效的扫描 ID（扫描 ID 不属于该账号或本次扫描未成功或扫描数据过期） |
| 400         | 40007      | 无效的对比日期                                                      |
| 400         | 40008      | 无接口权限                                                          |
| 400         | 40009      | 扫描 ID 已绑定                                                      |

### 3.9 合成推送类型与接口关系说明

**描述：**

- 第三方客户进行 API 对接配置完成 3.1.4 接口后，用户的每次测量维塑都会通过该接口将相关测量信息推送给第三方，第三方根据测量项目的合成结果 status 访问对应的维塑数据结果接口

**测量项目与合成推送类型关系如下：**

| 用户测量项目 | 合成推送项目                                                 |
| ------------ | ------------------------------------------------------------ |
| 身体成分测量 | bia_status、measure_status、tchar_status、bodypredict_status |
| 静态体态测量 | eval_status                                                  |
| 颈部功能测量 | eval_dynamic_status                                          |
| 髋关节测量   | eval_dynamic_hip_status                                      |

**合成推送类型与接口关系如下：**

| 合成推送项目            | 说明       | 可访问接口                 |
| ----------------------- | ---------- | -------------------------- |
| measure_status          | 体测       | 3.3.1、3.3.3               |
| eval_status             | 体态       | 3.3.5、3.4.1、3.4.2、3.4.3 |
| tchar_status            | 节段分布   | 3.5.1、3.5.2               |
| bodypredict_status      | 体型预测   | 3.6.1、3.6.2               |
| bia_status              | 体成分     | 3.3.2、3.3.4、3.3.5        |
| eval_dynamic_status     | 颈部测量   | 3.4.4                      |
| eval_dynamic_hip_status | 髋关节测量 | 3.4.5                      |

** 3.7.1 接口特别说明：**
报告信息接口，需要所测量项目中至少有一项合成成功
e.g. 1.用户测量身体成分需 bia_status 合成成功 2.用户测量静态体态需 eval_status 合成成功 3.用户测量身体成分及静态体态需等 bia_status、eval_status 中至少有一项合成成功

**其他：**

- 合成未成功或未进行项目测量时访问接口会返回 状态码 40006
