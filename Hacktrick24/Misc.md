### Where is my key?

**Soru:** _We have a JWT, we know that the start of the keyi is gop. Can you find the noble ke? Example key: gopthisismykey_  
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmbGFnIjoiR09Qe2Zha2VfZmxhZ19pc19oZXJlfSIsImlhdCI6MTcxNTM0MzA1NX0.-49NRjBBo0J6w4lyVkCU5aRE9gztNC0_zSUFRFQsVbM`  
Verilen JWT jwt.io sitesinde incelenmiştir ancak kayda değer herhangi bir bilgi elde edilememiştir.  
![misc_whereismykey_jwt_analyze.png](assets/misc_whereismykey_jwt_analyze.png)

Hashcat programını kullanarak JWT'nin sign key karşısında bruteforce saldırısı gerçekleştirilmeyi çalışılmıştır. Hashcat programında JWT modu 16500 dir.  
![misc_whereismykey_hashcat_help.png](assets/misc_whereismykey_hashcat_help.png)
`hashcat --help | grep -i jwt`

Soruda key'in 'gop' ile başladığı bilgisi verilmiştir. 'rockyou.txt' wordlistesinin başına gop eklenerek bruteforce saldırısı gerçekleştirilmiştir.  
![misc_whereismykey_hashcat_run.png](assets/misc_whereismykey_hashcat_run.png)

`sed -E 's/(.*)/gop\1/' /usr/share/wordlists/rockyou.txt| hashcat -a 0 -m 16500 jwt.txt -`
![misc_whereismykey_hashcat_results.png](assets/misc_whereismykey_hashcat_results.png)

**Flag:** _GOP{gopcartoon13}_

###  Terminal

Verilen html dosyası incelendiğinde obfuscation işlemine tabi tutulan javascript görülmektedir.  
![misc_terminal_javascript.png](assets/misc_terminal_javascript.png)

Javascript 'deobfuscate.io' sitesine verildiğinde 'Obfuscator.io' sitesinden işleme tabi tutulduğunu açıklayan bir mesaj ile karşılaşılmaktadır.  
![misc_terminal_notification.png](assets/misc_terminal_notification.png)

İlgili deobfuscator ile işleme alındığında flag elde edilmektedir.  
![misc_terminal_deobfuscator.png](assets/misc_terminal_deobfuscator.png)

**Flag:** _GOPCTF{r4nd0m_c0mm4nd_1nj3ct10n}_

###  Color Blind

Verilen html dosyasındaki hex değerleri farklı bir dosyaya aktarılmıştır.  
![misc_color_blind_page_source.png](assets/misc_color_blind_page_source.png)

![misc_color_blind_pasted.png](assets/misc_color_blind_pasted.png)
Flag'ın başı 'GOP' olduğunu bilindiğinden dolayı 'GOP' harflerinin hex karşılığı incelenmiştir ve renk değerleriyle bir ilişki aranmıştır. Renk değerlerinin oradaki byte'a karşılık geldiğine tespit edilmiştir.  
![misc_color_blind_analyze.png](assets/misc_color_blind_analyze.png)

Renk değerlerinin ortasındaki byte'lar birleştirilip ASCII formatına çevirilmiştir.  
![misc_color_blind_concated.png](assets/misc_color_blind_concated.png)

**Flag:** _GOP{renk_kodlarindan_flag_alabiliriz_ama_ortasini}_

### Rototo

Verilen şifreli metin rot13 decode yapıldığında flag bulundu.
TBC{sy4t_s0e_olg3_rnfl3p}

**Flag:** _GOP{fl4g_f0r_byt3_easy3c}_

### Brute

Verilen şifreli metin rot23 decode yapıldığında flag bulundu.
JRS{vhcdulq_kdnodul_vdnolglu}

**Flag:** _GOP{sezarin_haklari_saklidir}_

### Music

Videonun içinde kısa süreliğine flag gözüküyor.
![misc_music.png](assets/misc_music.png)

**Flag:** _GOP{dance_monkey}_

### Secret Cat

Verilen png dosyasını foremost aracı ile kullanınca farklı bir fotoğraf daha çıkıyor. Fotoğrafı açtığımızda flag bulundu.
![misc_secret_cat.png](assets/misc_secret_cat.png)

**flag:** _GOP{hidden_img_xd_binwalk}_
