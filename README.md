# ELEX Mobile GDP SDK For Android #

## 支付 ##

1. 将payelexmobile.jar引入工程
2. 在AndroidManifest.xml中配置网络访问权限并添加一个activity：`com.elextech.payment.android.PayelexMobileMall`。
3. 对com.elextech.payment.android包中的Payelex进行初始化，初始化需要四个参数：
	* appid:	游戏id
	* uid:		玩家id
	* CallbackGame:	回调函数
	* isTest: 是否为测试环境标识
4. 发起支付：

	```
	Intent intent = new Intent(context,PayelexMobileMall.class);
	intent.putExtra("vamount", 75);	//道具、商品数量
	intent.putExtra("description", "crystals");	//道具、商品描述
	intent.putExtra("gross", "0.99");	//商品总价，交易金额
	intent.putExtra("currency", "USD");	//交易货币标识
	intent.putExtra("productId", "p4");	//产品编号
	startActivity(intent);
	```

5. 支付成功后，会调用回调函数中的onSuccess()方法，其中参数为成功支付的订单。