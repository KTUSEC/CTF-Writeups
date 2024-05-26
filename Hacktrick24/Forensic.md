### Powershell

Verilen log dosyası analiz edilerek powershell komutu tespit edilmiştir.  
![forensics_powershell_founds_events.png](assets/forensics_powershell_founds_events.png)

Bu komut bat dosyasına kayıtedilerek any.run sitesine yüklenmiştir ve davranışları analiz edilmiştir. Zararlı powershell komutu `176.103.56.89:8080` adresine bağlanmaya çalıştığını tespit edilmiştir.  
![forensics_powershell_any_run.png](assets/forensics_powershell_any_run.png)

**Flag:** _GOP{176.103.56.89:8080}_

###  Amcache

**Soru:** *TR: Nil sabah bilgisayarını açtığında, şirketinin yöneticisi tarafından kendisine "İş Akdinizin Feshi" başlıklı bir mail geldiğini görür ve hemen heyecanla mailin içeriğinde bulunan pdf görünümlü dosyayı açar. Pdf dosyasını açtıktan kısa bir süre sonra, bilgisayarındaki tüm önemli belgelerinin uzantısının değiştiğini ve dosyaları açamadığını görür. Nilin bilgisayarına bu işlemi gerçekleştiren zararlının ismini ve hash (SHA1) değerini bulabilir misin? (Dosyaismi:Sha1)

AmcacheParser ile verilen dosya parse edilir.  
![forensics_amcache_amcache_parser.png](assets/forensics_amcache_amcache_parser.png)

İstenilen program olduğundan dolayı 'İlişkilendirilmemiş dosya girişleri' dosyayı incelenir.  
![forensics_amcache_parse_results.png](assets/forensics_amcache_parse_results.png)

'İlişkilendirilmemiş dosya girişleri' dosyayının 'Name', 'ProductName' ve 'SHA1' sütünleri dikkate alınır.  
![forensics_amcache_cvs_analyze.png](assets/forensics_amcache_cvs_analyze.png)

Aranan program malware olduğundan Microsoft'a ait dosyalar filtrelenir ve geriye kalan dosyalar incelenir.
![forensics_amcache_filter_microsoft.png](assets/forensics_amcache_filter_microsoft.png)
Burada ProductName'i olmayan `vm3dservice.exe` ve `winrar.exe` görülmektedir. ProductName'de yazılan `9.17.06.0005`ve `151040` bilgileri ProductName sütünü boş olduğundan bir önceki sütünden alınmaktadır.

Gerçek Winrar programının bilgileri incelendiğinde uyuşmadığı görülmektedir.  
![forensics_amcache_winrar.png](assets/forensics_amcache_winrar.png)

**Flag:** _GOP{winrar.exe:2c3b2ed20f1e8e630c61109288bd0ac64b5e0329}_
