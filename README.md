### 1.导入multichat


### 2.快速使用

```java
  
  
  1初始化
  
  // String uuid 租户ID，Udesk后台系统获取
 
  //String timestamp 时间戳，由你们后端返回

  //String sign  签名，由你们后端返回
  
  //customer_euid  用户ID是用户的唯一标示，请不要重复，并且只允许使用数字、字母、数字+字母
  
  UdeskSDKManager.getInstance().init(content, uuid, sign, time);
  UdeskSDKManager.getInstance().setCustomerInfo(customer_euid, customer_name);     

  2 客户通过某个商品详情页点击咨询按钮直接和客服进行会话
  
      //进入会话可以设置咨询对象 (可选)
	   //设置咨询的商品 如下：
    private void createProducts() {
        Products products = new Products();
        Products.ProductBean productBean = new Products.ProductBean();
        productBean.setImage("http://img14.360buyimg.com/n1/s450x450_jfs/t3157/63/1645131029/112074/f4f79169/57d0d44dN8cddf5c5.jpg?v=1483595726320");
        productBean.setTitle("Apple iPhone 7");
        productBean.setUrl("http://item.jd.com/3133829.html?cu=true&amp;utm_source…erm=9457752645_0_11333d2bdbd545f1839f020ae9b27f14");
        List<Products.ProductBean.ExtrasBean> extras = new ArrayList<>();

        Products.ProductBean.ExtrasBean extrasBean = new Products.ProductBean.ExtrasBean();
        extrasBean.setTitle("价格");
        extrasBean.setContent("￥6189.00");

        extras.add(extrasBean);
        productBean.setExtras(extras);
        products.setProduct(productBean);

        UdeskSDKManager.getInstance().setProducts(products);

    }
	
	//通过商户ID，咨询商户
     // merchantId  商户ID
    UdeskSDKManager.getInstance().entryChat(content, merchantId);
  
  //提供了历史对话商户列表，提供ConversationFragment，可根据你们app加入，参见demo。
}
```



### 3.离线推送
```java

//App 进入后台时，开启Udesk推送

调用 UdeskSDKManager.getInstance().setCustomerOffline(false);

建议 在application中registerActivityLifecycleCallbacks（ActivityLifecycleCallbacks activityLifecycleCallbacks）来控所有前后台逻辑

```

### 4.混淆配置

``` java
//udesk
-keep class udesk.** {*;} 
-keep class cn.udesk.**{*; } 

//oss
-keep com.alibaba.sdk.**{*; } 
-keep com.google.gson.**{*; } 
-keep org.jxmpp.**{*; } 
-keep  de.measite.minidns.**{*; } 


//smack
-keep class org.jxmpp.** {*;} 
-keep class de.measite.** {*;} 
-keep class org.jivesoftware.** {*;} 
-keep class org.xmlpull.** {*;} 
-dontwarn org.xbill.**
-keep class org.xbill.** {*;} 

//retrofit2

# Platform calls Class.forName on types which do not exist on Android to determine platform.
-dontnote retrofit2.Platform
# Platform used when running on Java 8 VMs. Will not be used at runtime.
-dontwarn retrofit2.Platform$Java8
# Retain generic type information for use by reflection by converters and adapters.
-keepattributes Signature
# Retain declared checked exceptions for use by a Proxy instance.
-keepattributes Exceptions

//freso
-keep class com.facebook.** {*; }  
-keep class com.facebook.imagepipeline.** {*; } 
-keep class com.facebook.animated.gif.** {*; }  
-keep class com.facebook.drawee.** {*; }  
-keep class com.facebook.drawee.backends.pipeline.** {*; }  
-keep class com.facebook.imagepipeline.** {*; }  
-keep class bolts.** {*; }  
-keep class me.relex.photodraweeview.** {*; }  

-keep,allowobfuscation @interface com.facebook.common.internal.DoNotStrip
-keep @com.facebook.common.internal.DoNotStrip class *
-keepclassmembers class * {
    @com.facebook.common.internal.DoNotStrip *;
}
# Keep native methods
-keepclassmembers class * {
    native <methods>;
}

-dontwarn okio.**
-dontwarn com.squareup.okhttp.**
-dontwarn okhttp3.**
-dontwarn javax.annotation.**
-dontwarn com.android.volley.toolbox.**
-dontwarn com.facebook.infer.**


 //其它
-keep class com.tencent.bugly.** {*; } 

```
