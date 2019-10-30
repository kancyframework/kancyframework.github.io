## 渠道基础信息查询



**调用方向：**

- VFP -> VFTS

**简要描述：**

- 渠道基础信息查询接口

**请求URL：**

- `/channel/basedata/list`

**环境信息**

- 测试环境：http://10.139.60.80:9587/
- 生产环境：http://10.10.41.190:9587/

**请求方式：**

- POST

<br/>

**参数：**

| 字段          | 说明       | 必填 | 数据类型 | 备注 |
| ------------- | ---------- | ---- | -------- | ---- |
| pageSize | 每页显示大小 | N    | int   | 默认为10 |
| currentPage | 当前页 | N    | int   | 默认为1|
| productCode | 产品代码 | Y    | String   |  PDCD000012：豆豆钱<br>PDCD000032：卡卡贷；<br>PDCD000079：维信闪贷；|
| belongMonth      | 所属月份     | N    | String   |  例如：201909 |
| businessDate | 业务日期 | N  | String   |  例如：2019-09-01    |
注：belongMonth和businessDate必须传一个，两个都传时，businessDate必须在belongMonth内。

<br/>

**请求示例**

```
{
	"productCode" : "PDCD000012",
	"currentPage":1,
	"pageSize":2
	"businessDate" : "2019-09-01"
}
```

<br/>

**返回参数：** 

|参数名|类型|说明|
|:-----  |:-----|-----|
|success  |bool   |true 成功 false 失败  |
|code  |string   |0000 成功 |
|message  |string   |具体描述|
|timestamp  |long   |时间戳|
|data  |List<PageInfo>   |数据体|

**PageInfo**

|参数名|类型|说明|
|:-----  |:-----|-----|
|pageSize|long|一页多少条数据|
|currentPage|long|当前页|
|total|long|总条数|
|pageCount|long|总页数|
|rows |List<Row>   |数据 |

**Row**

| 字段         | 说明         | 必填  | 数据类型   | 备注       |
| ------------ | ------------ | ----- | ---------- | ---------- |
|businessDate|业务日期|Y|String|2019-09-01|
|productName|产品名称|Y|String|豆豆钱|
|supplierName|供应商名称|Y|String|供应商名称001|
|settleType|结算方式|Y|String|GPA交单|
|channelName|渠道名称|Y|String||
|registerNumber|注册数量|Y|int||
|firstBillNumber|首次交单数量|Y|int||
|firstCreditSucessNumber|首次授信通过数量|Y|int||
|loanNumber|放款数量|Y|int||
|loanAmount|放款总金额|Y|double|保留2位小数|
|firstLoanNumber|首贷数量|Y|int||
|firstLoanAmount|首贷总金额|Y|double|保留2位小数|
|reLoanNumber|再贷数量|Y|int||
|reLoanAmount|再贷总金额|Y|double|保留2位小数|
|firstLoanCpsRate|首贷CPS费率|Y|double|保留4位小数,真实值|
|reLoanCpsRate|再贷CPS费率|Y|double|保留4位小数,真实值|
|cpaRate|CPA费率|Y|double|保留4位小数,真实值|
|channelCostAmount|渠道费用|Y|double|保留2位小数|


 **成功返回示例**

```json
{
	"code": "SYS00000",
	"data": {
		"currentPage": 1,
		"pageCount": 1070,
		"pageSize": 2,
		"total": 2139,
		"rows": [
			{
				"businessDate": "2019-08-01",
				"channelCostAmount": 253621.11,
				"channelName": "66钱庄",
				"cpaRate": 0.0000,
				"firstBillNumber": 184,
				"firstCreditSucessNumber": 816,
				"firstLoanAmount": 48732.67,
				"firstLoanCpsRate": 3.0000,
				"firstLoanNumber": 405,
				"loanAmount": 10457.28,
				"loanNumber": 624,
				"productName": "豆豆钱",
				"reLoanAmount": 21484.62,
				"reLoanCpsRate": 5.0000,
				"reLoanNumber": 749,
				"registerNumber": 808,
				"settleType": "CPS首贷再贷",
				"supplierName": "供应商名称001"
			},
			{
				"businessDate": "2019-08-01",
				"channelCostAmount": 769.20,
				"channelName": "77信用",
				"cpaRate": 1.2000,
				"firstBillNumber": 641,
				"firstCreditSucessNumber": 396,
				"firstLoanAmount": 33260.47,
				"firstLoanCpsRate": 0.0000,
				"firstLoanNumber": 1479,
				"loanAmount": 66794.46,
				"loanNumber": 370,
				"productName": "豆豆钱",
				"reLoanAmount": 78013.59,
				"reLoanCpsRate": 0.0000,
				"reLoanNumber": 992,
				"registerNumber": 195,
				"settleType": "CPA交单",
				"supplierName": "供应商名称001"
			}
		]
	},
	"message": "操作成功!",
	"success": true,
	"timestamp": 1571129928659
}

```
注：找不到数据时，data返回空集合：[]

 **错误返回示例**

``` json
{
  "success": false,
  "code": "9999",
  "message": "查询失败",
  "timestamp":15435435435
}
```

**备注**

- 更多返回错误代码请看首页的错误代码描述
