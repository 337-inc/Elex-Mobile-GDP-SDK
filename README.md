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

## 交叉推广 ##

1. 将elexcpb.jar加入到Android工程。

2. 将res中的所有elex相关的xml复制到工程中相同的目录下。请不要更改这些XML的文件名以及其中各组件的ID。其余的可以由开发者根据游戏的风格进行调整。如果需要做代码混淆，需要把R文件过滤掉。

3. 在AndroidManifest.xml中配置权限：`android.permission.INTERNET`、`android.permission.ACCESS_WIFI_STATE`

4. 在游戏初始化时调用com.elextech.cpb.Cpbelex的init方法，包含三个参数：
	* c为游戏当前的Activity，
	* id为游戏的推广id，
	* callback为Cpbelex.CpbCallback接口的实例，用于回调。

5. 广告展示：
直接调用Cpbelex的show方法即可。

6. 查询是否可以发奖：
调用Cpbelex的check方法，来检查是否有可以给与玩家的奖励。当有可以给与的奖励时，会调用callback中的onFinish方法，参数为奖励的详细信息。可将check方法放在游戏activity的onResume方法中，也可以每隔一段时间就调用一次，由开发者自行控制。

7. 玩家完成目标的操作：
Cpbelex的finishEvent方法用于告知CPB系统该玩家已经达成了游戏定义的目标。参数eventid为游戏在CPB后台配置后所得到的ID。需要开发者在玩家达成既定目标时调用。

