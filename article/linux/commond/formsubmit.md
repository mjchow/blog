

```
//URL
//-------PC
/coupon/view/formsubmit
/haodianshop/coupon/view/formsubmit

//-------wap
/coupon/view/wapformsubmit
/wap/coupon/view/formsubmit
```



* /coupon/view/formsubmit
* /haodianshop/coupon/view/formsubmit

```java
new JsonResultDto(false,201,"not normal submit");
new JsonResultDto(false,102);						//优惠券信息有误
new JsonResultDto(false,103,couponStatusErrorMsg);	//优惠券状态异常
new JsonResultDto(false,104);						//账号申领数量超限制
new JsonResultDto(false,110);						//防止并发提示的错误信息
new JsonResultDto(false,112);						//订单生成失败
new JsonResultDto(false,104);						//金币支付失败 金币不够 或者 扣除金币失败
new JsonResultDto(false,200);						//订单数已满
new JsonResultDto(false,105);						//没有取到code
```

