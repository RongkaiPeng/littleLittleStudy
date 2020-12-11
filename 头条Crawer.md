##  1.拦截规则

1.所有的url前面都加上了_signature, SDK 会拦截所有使用 XMLHTTPRequest 发送的请求，包括第三方库发出的，

[tea-sdk][default] {
  "user_unique_id": "6831716492610913805",
  "web_id": "6831716492610913805",
  "ssid": "4bddb1f0-3466-4d54-bc5a-a9c1cffbc192"
}

2.页面通过ajax动态加载，可以通过XHR文件找到热点的相关题目，进行初步提取，要进行数据类型转换

> <img src="C:\Users\q1171\AppData\Roaming\Typora\typora-user-images\image-20200609145338802.png" style="zoom:30%;"  name="头条热点关键字抓取"/>

3. cp前几位为时间戳对应的16进制转换

4. 首页每一步ajax都会生成一个时间戳

   >
   >
   >_02B4Z6wo001017eboRwAAIBB9GWrsA-1VVO3nqWAALMU4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT7482
   >
   >_02B4Z6wo00101ryy-mgAAIBA.0zwxO9lbk68t.7AAPHS4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT747f
   >
   >_02B4Z6wo001016ZlVRQAAIBB5ZtfuDy.qaemYFGAALeB4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT7498
   >
   >_02B4Z6wo00101nuHUQgAAIBAOHlbpyNTeM57glWAAMAa4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT749b
   >
   >_02B4Z6wo00101ezaiYQAAIBDrySDKhkS1n3s340AACXc4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT7409
   >
   >_02B4Z6wo00101My.72wAAIBCj0Hlww1spqzMuuvAAG3H4BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT74b0

   BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT74

每个时间戳有==_02B4Z6wo00101==，==BWGDgvWCz1Zdmxw9GzuJuZUsoprrCZ2WzKdXgiP661airoMThw7jKveKo5FviJqisgMUfu8v3Lgrr-Co-3rKa.trY5fbP5vZT74==相同，应该是由同种浏览器参数返回的结果，只有最末尾两位和中间不同，可以考虑是时间戳改变的后果，在浏览器返回的参数里面，排除cookie，同一台电脑cookie不变，

1. as: A1253E7F00FB5A1
2. cp: 5EF0BBE5CA618E1
3. max_behot_time: 1592774771
4. _signature: HydBGQAAQdv4ULkfSI78HB8nQQ

5.头条存储的cookie字段

6.加密信息代码片段

https://s3a.pstatp.com/toutiao/static/js/page/index_node/index.af62e2274e2538bd9f4d.js

paragraphs 1 

line 534, line 845

signature line462

https://unpkg.pstatp.com/byted/secsdk-captcha/2.9.0/build/captcha.js



## 2. 利用selenium驱动浏览器

https://github.com/01ly/TTBot

1.下载对应的chromedriver，

>  部分想法：
>
> 可以设置不加载图片
>
> 利用全选（alt+A）复制在txt文档，根据关键字检索（不感兴趣和评论之间）
>
> 对应具体文章（怎么点进去？）可以用 ‘微信’ 和 ‘ 收藏 评论’ 关键字截取









##  3.移动端网页爬取

加密措施简单，signature简单爆炸

<img src="C:\Users\q1171\AppData\Roaming\Typora\typora-user-images\image-20200622215644173.png" alt="image-20200622215644173" style="zoom:67%;" />

标题全部为unicode编码，转码即可

<img src="C:\Users\q1171\AppData\Roaming\Typora\typora-user-images\image-20200622215724387.png" alt="image-20200622215724387" style="zoom:67%;" />

https://s3.pstatp.com/growth/mobile_list/js/index_eed0410cfea495eb697c.js   paragraphs 14   

> line 838
>
> ```javascript
> var c = {
>     tag: e,
>     ac: "wap",
>     count: 20,
>     format: "json_raw",
>     as: (0, Z.default)().as,
>     cp: (0, Z.default)().cp,
>     max_behot_time: "append" === a ? u : void 0,
>     min_behot_time: "prepend" === a ? l : void 0,
>     _signature: (0, re.sign)(u || ""),
>     i: u || ""
> };
> ```

