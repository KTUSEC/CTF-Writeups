### Login Admin

Sayfanın kaynağı incelendiğinde comment olarak `/?debug=true` görülmüştür.  
![web_login_admin_page_source.png](Hacktrick24/assets/web_login_admin_page_source.png)

Sayfaya `/?debug=true` ile gidildiğinde sunucudaki PHP kodları dönmektedir. PHP kodu incelendiğinde flag'ı vermek için `user@localhost` ve `password` ile kullanıcı bilgileriyle POST isteği yollanması gerekmekte ve bu kullanıcının Session bilgilerindeki 'admin' anahtarı 'true' değerine sahip olması gerekmektedir. Kod, `extract()` fonksiyonunu kullanarak kullanıcının yolladığı POST değerleri değişkenlere atılmaktadır.  
![web_login_admin_debug_true.png](Hacktrick24/assets/web_login_admin_debug_true.png)

Gereken bilgileri içeren bir POST isteği hazırlanıp 'admin' değerini değiştirmek için `_SESSION[admin]` adında parametre eklenmiştir ve değerli true atanmıştır.  
![web_login_admin_burp_param_setup.png](Hacktrick24/assets/web_login_admin_burp_param_setup.png)
İstek gönderildiğinde flag dönmektedir.  


**Flag:** _GOP{php_not_death}_