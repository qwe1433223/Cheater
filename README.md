### 作用

>   自动化刷课（江西技能职业培训平台），这个是江西教育部官方的哦，大部分专科院校高三时都得刷，然后混个证书

### 使用方法

>   在项目目录下放上你的帅照并且命名为：人脸.jpg	（注意需要是jpg格式的哦）
>
>   将密码设置为qwe123456后
>
>   ./cheater.py --account 18888888888
>
>   一键运行，然后就不用管了，但是问题是每天只能刷8小时，你可以把这脚本添加到启动项或计划个任务，然后在接口那看响应包是否包含（已刷满八小时之类的字样），然后让其休眠到第二天开刷。
>
>   可轻松实现一键刷到课程结束

### 项目思路

https://jiangxi.zhipeizaixian.com/study/video?class_id=30136&course_id=2850&unit_id=180344
https://jiangxi.zhipeizaixian.com/study/video?class_id=课程ID&course_id=用户ID&unit_id=视频ID

/studies/study?video_id=179764&u=14833273&time=0&start=1&unit_id=180345&class_id=30136
/studies/study?video_id=179765&u=14833273&time=180&start=1&unit_id=180346&class_id=30136
https://apistudy.wozhipei.com/studies/study?video_id=视频ID&u=用户ID&time=观看时长&unit_id=视频ID&class_id=课程ID
video_id和unit_id都是视频ID，因为它们是随着视频集数而自增1的。
观看时长可以填60即可，不用增长

Response.Headers CONTAINS "X-Traceid:" AND Request.Method CONTAINS "post"

登录步骤：
    请求公钥：
    https://api.cloud.wozhipei.com/auth/user/v1/public_key

    HTTP/1.0 200
    Date: Mon, 16 Oct 2023 04:02:16 GMT
    Content-Type: application/json
    Connection: close
    Set-Cookie: acw_tc=0a09669216974289366243535ee469495c0bbaeb9ff60d358a3d22c6f8d28d;path=/;HttpOnly;Max-Age=1800
    Vary: Accept-Encoding
    Vary: Origin
    Vary: Access-Control-Request-Method
    Vary: Access-Control-Request-Headers
    Access-Control-Allow-Origin: https://account-jiangxi.zhipeizaixian.com
    Access-Control-Allow-Credentials: true
    Vary: Origin
    Vary: Access-Control-Request-Method
    Vary: Access-Control-Request-Headers
    Set-Cookie: SERVERID=469ad262ffcdf772c0113022ff4db2e4|1697428936|1697428936;Path=/
    
    登录包：
    POST /auth/user/v1/login HTTP/1.0
    Host: api.cloud.wozhipei.com
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
    Accept: application/json, text/plain,*/*
    Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
    Accept-Encoding: gzip, deflate
    Content-Type: application/json
    Content-Length: 465
    Origin: https://account-jiangxi.zhipeizaixian.com
    Referer: https://account-jiangxi.zhipeizaixian.com/
    Sec-Fetch-Dest: empty
    Sec-Fetch-Mode: cors
    Sec-Fetch-Site: cross-site
    Te: trailers
    Connection: keep-alive
    
    {"account":"18107909060","appKey":"WEB","sid":1018,"type":1,"authOpenId":"","authType":"","publicKey":"04401e0715604a4c50eac1fa9790087efd8715c5124ce03d1f41a40a247809eaedaffe091ee91d726388f9a8ba3571240c145296c82ef41d76a3c7c5acf08fd0f8","password":"8dbf36e8da9e09377bb5a396cdd8d506559628cb1d3b6728a084a9ebe13f2a4217038a7bcc640c7574766ab83af9a12579e1adfac6dfadd403884fa6c3313edb703074728307b41d170d0ceb9decd86156d4cb351e006b00d65544beb897cf450175c911e334e20ba709b695"}
    返回：
    HTTP/1.0 200
    Date: Mon, 16 Oct 2023 04:02:17 GMT
    Content-Type: application/json
    Connection: close
    Set-Cookie: acw_tc=0a09669216974289370045644ee46367aafe6b048268ba39cd5cff914b48bd;path=/;HttpOnly;Max-Age=1800
    Vary: Accept-Encoding
    Vary: Origin
    Vary: Access-Control-Request-Method
    Vary: Access-Control-Request-Headers
    Access-Control-Allow-Origin: https://account-jiangxi.zhipeizaixian.com
    Access-Control-Allow-Credentials: true
    Vary: Origin
    Vary: Access-Control-Request-Method
    Vary: Access-Control-Request-Headers
    Set-Cookie: SERVERID=469ad262ffcdf772c0113022ff4db2e4|1697428937|1697428937;Path=/
    
    {"success":true,"messageCode":"200","message":"æä½æåï¼","data":{"accessToken":"eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NDI4OTM3LCJhdWQiOiJXRUIiLCJleHAiOjE3MDAwMjA5MzcsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.3vk4oX7iRzCB3L0ZkcZHBgxl2B8RHnzvTdBUPqM7rMIFhrm_1s7LKlef6RKeU6mF","appKey":"WEB","userCode":"16946203APEK9QTC","sid":1018,"refreshToken":"","cloginB":false}}

刷新token为刷视频可用token


POST /users/update-access-token HTTP/1.0
Host: apif.wozhipei.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Client-Type: pc
Authorization-Platform: eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTI1NDAzLCJhdWQiOiJXRUIiLCJleHAiOjE3MDAxMTc0MDMsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.DDJab68L-6eMvu3fytQ9u0pwEsErr8IyAxqMCbBk40PkPVyu4VDrlfnOGGDO4-g-
Authorization: Bearer eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTI1NDAzLCJhdWQiOiJXRUIiLCJleHAiOjE3MDAxMTc0MDMsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.DDJab68L-6eMvu3fytQ9u0pwEsErr8IyAxqMCbBk40PkPVyu4VDrlfnOGGDO4-g-
X-User-Type: 1
Content-Length: 2
Origin: https://jiangxi.zhipeizaixian.com
Referer: https://jiangxi.zhipeizaixian.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Te: trailers
Connection: keep-alive

{}


人机验证：

HTTP/1.0 403 Forbidden
Date: Tue, 17 Oct 2023 03:04:25 GMT
Content-Type: application/json; charset=UTF-8
Connection: close
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: Content-Type, Authorization, X-Api-Version, X-Client-Type, X-Site-Alias, X-Site-Sp, X-Organization,X-Organization-Code,AUTHORIZATION-PLATFORM,X-User-type,WTAuthorization,X-BSaas-Code
Access-Control-Allow-Credentials: true
Access-Control-Allow-Methods: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS
Allow: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS
Access-Control-Request-Method: GET, POST, PUT, DELETE, HEAD, OPTIONS
Access-Control-Request-Headers: *
Access-Control-Max-Age: 86400
Access-Control-Expose-Headers: X-Pagination-Total-Count, X-Pagination-Page-Count, X-Pagination-Current-Page, X-Pagination-Per-Page, Link
cache-control: no-store
X-Traceid: 8a6b1647e6564ebe
Set-Cookie: _csrf=23f69e2e7e51a51cbd38f400307961968fe32d602255f9970f0975e761f554a8a%3A2%3A%7Bi%3A0%3Bs%3A5%3A%22_csrf%22%3Bi%3A1%3Bs%3A32%3A%22KaKebltCqirYZB4jHoC7sZB8QcDdGFVp%22%3B%7D; path=/; HttpOnly; SameSite=Lax

{"name":"Forbidden","message":"请人机验证","code":2002,"status":403}

发送人机验证

POST /supervises/smart-new HTTP/1.0
Host: apif.wozhipei.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Client-Type: pc
Authorization: Bearer eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTA2NzE4LCJhdWQiOiJXRUIiLCJleHAiOjE3MDAwOTg3MTgsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.orzeD_Su9p0LqJ8Aswhp0VuMAj7yXowtUlI17KP2uFX6Zn2OkRvs-QSlWFLmx2L6
X-User-Type: 1
Content-Length: 69
Origin: https://jiangxi.zhipeizaixian.com
Referer: https://jiangxi.zhipeizaixian.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Te: trailers
Connection: keep-alive

{"code":"2","course_id":"2850","unit_id":"180336","class_id":"30136"}


根据course_id以及class_id获得课程信息 unit_id

GET /courses/test-preview?course_id=2850&class_id=30136 HTTP/1.0
Host: apif.wozhipei.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Client-Type: pc
Authorization: Bearer eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTI4Mzc2LCJhdWQiOiJXRUIiLCJleHAiOjE3MDAxMjAzNzYsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.OvKJVr0CTPMypMYDFI5Arf0IfQMbE0tdkgfCxHZaNnFiOtp10t5OBC9-sqMJ_N7J
X-User-Type: 1
Origin: https://jiangxi.zhipeizaixian.com
Referer: https://jiangxi.zhipeizaixian.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Te: trailers
Connection: keep-alive


根据unit_id和clas_id获取 video_id

GET /course-units/180344?class_id=30136 HTTP/1.0
Host: apif.wozhipei.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Client-Type: pc
Authorization: Bearer eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTI4Mzc2LCJhdWQiOiJXRUIiLCJleHAiOjE3MDAxMjAzNzYsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.OvKJVr0CTPMypMYDFI5Arf0IfQMbE0tdkgfCxHZaNnFiOtp10t5OBC9-sqMJ_N7J
X-User-Type: 1
Origin: https://jiangxi.zhipeizaixian.com
Referer: https://jiangxi.zhipeizaixian.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Te: trailers
Connection: keep-alive


获取class_id和course_id


GET /student-center/study HTTP/1.0
Host: apif.wozhipei.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Client-Type: pc
Authorization: Bearer eyJhbGciOiJIUzM4NCJ9.eyJqdGkiOiJqd3RfaWQiLCJzdWIiOiIxNjk0NjIwM0FQRUs5UVRDIiwiaWF0IjoxNjk3NTMzODk1LCJhdWQiOiJXRUIiLCJleHAiOjE3MDAxMjU4OTUsInNpZCI6MTAxOCwidHlwZSI6IlVTRVIiLCJncm91cFR5cGUiOjF9.1H2FMUeX_38LasxFp7_muUzbmi61_PvRzKO6kvXhL780Hu_Jdvc9YHKgi6D4Twz-
X-User-Type: 1
Origin: https://jiangxi.zhipeizaixian.com
Referer: https://jiangxi.zhipeizaixian.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Te: trailers
Connection: keep-alive
