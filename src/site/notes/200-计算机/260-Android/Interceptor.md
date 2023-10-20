---
dg-publish: true
date: 2023-10-07
tags:
  - Retrofit/Interceptor
---
## 添加公共参数
```
class CommonParametersInterceptor : Interceptor {  
    override fun intercept(chain: Interceptor.Chain): Response {  
        LogUtils.i("添加参数拦截器")  
        //获取请求request  
        val request: Request = chain!!.request()  
        //获取请求request的创建者builder实例  
        val builder = request.newBuilder()  
        //请求头添加参数  
        if (App.token.isNotEmpty()) {  
            builder.addHeader("Authorization", App.token)  
        }  
  
        val body = request.body  
        //为Post表单请求设置公共参数  
        if (body is FormBody) {  
            val formBodyBuilder = FormBody.Builder()  
            for (i in 0..<body.size) {  
                formBodyBuilder.addEncoded(body.encodedName(i), body.encodedValue(i))  
            }  
            //添加公共参数  
            formBodyBuilder.add("denseStatus", "0")  
  
            for (i in 0..<formBodyBuilder.build().size) {  
                LogUtils.i("参数打印[${formBodyBuilder.build().encodedName(i)}:${formBodyBuilder.build().encodedValue(i)}]")  
            }  
            builder.post(formBodyBuilder.build())  
        }  
  
        return chain.proceed(builder.build())  
    }  
}
```

## 参考资料
[Retrofit2如何在Post、Get、Header上设置固定参数 | 公共参数 - 碎月 - 博客园](https://www.cnblogs.com/mesmerize/p/16067955.html)