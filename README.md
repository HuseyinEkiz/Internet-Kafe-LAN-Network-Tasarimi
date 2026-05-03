Internet Kafe Ag Tasarimi 
Bilisim Teknolojileri Departmani 
BLM2006 - Bilgisayar Aglarina Giris 
PROJE FINAL RAPORU 
Internet Kafe LAN (Local Area Network) Tasarimi 
 
Grup Uyeleri 
Huseyin Ekiz - 170424051 
Cem Anil Erdem - 170424041 
 
Ders 
BLM2006 - Bilgisayar Aglarina Giris 
 
Kullanilan Araclar 
Cisco Packet Tracer 
 
Tarih 
Mayis 2026 
 
Icindekiler 
1.	Giris 
2.	Yontem 
2.1	Proje Kapsami ve Hedefler 
2.2	Kullanilan Teknolojiler ve Yazilimlar 
2.3	Ag Tasarim Asamalari 
3.	Bulgular 
3.1	VLAN Yapilandirmasi 
3.2	NAT ve Internet Erisimi 
3.3	Firewall Entegrasyonu 
3.4	Kablosuz Ag (Wi-Fi) Destegi 
4.	Sonuc 
5.	GitHub 
6.	Kaynakca 
  
1.	Giris 
Bu proje, bir internet kafenin tum bilgisayar sistemlerinin, sunucularinin ve ag cihazlarinin guvenilir, kesintisiz ve yuksek performansli bir ag altyapisi uzerinden birbirleriyle iletisim kurmasini saglamak amaciyla tasarlanmis bir LAN (Local Area Network - Yerel Alan Agi) mimarisini icermektedir. 
 
Gunumuz internet kafelerinde es zamanli olarak onlarca kullanici ag kaynaklarini yogun bicimde kullanmaktadir. Bu durum, ag yonetimini, guvenligini ve erisebilirligi kritik bir muhendislik sorunu haline getirmektedir. Geleneksel duz (flat) ag mimarileri, buyuk olcekli ortamlarda yayin firtinaları, yetersiz guvenlik izolasyonu ve olceklenebilirlik sorunlarina yol acmaktadir. 
 
Bu proje kapsaminda gelistirilen cozum; VLAN tabanli ag segmentasyonu, NAT ile internet erisimi, Firewall ile guvenlik ve kablosuz (Wi-Fi) erisim noktalari bilesenlerini bir arada kullanarak pratik duzeyde bir internet kafe agi ortaya koymaktadir. 
 
Tum tasarim ve simulasyon calismalari Cisco Packet Tracer ortaminda gerceklestirilmis; konfigurasyonlar IOS komut satiri arayuzu (CLI) kullanilarak uygulanmistir. 
 
2.	Yontem 
2.1	Proje Kapsami ve Hedefler 
Proje asagidaki temel hedefleri karsilayacak bicimde tasarlanmistir: 
•	Internet kafe genelinde birimleri mantiksal olarak ayiran VLAN yapisi olusturmak 
•	NAT araciligiyla tum ic agin guvenli bicimde internete cikisini saglamak 
•	Firewall ile yetkisiz erisimleri engellemek ve ag guvenligini saglamak 
•	Kablosuz erisim noktalari ile mobil kullanicilara ag erisimi sunmak 
 
2.2	Kullanilan Teknolojiler ve Yazilimlar 
Proje boyunca kullanilan temel teknolojiler ve araclar asagidaki tabloda ozetlenmistir: 
 
Teknoloji / Arac 	Amac / Kullanim Alani 
Cisco Packet Tracer 	Ag simulasyonu ve topoloji tasarimi 
VLAN (802.1Q) 	Ag segmentasyonu ve yayin alani kontrolu 
NAT / PAT 	Ic IP adreslerin internet uzerinde gizlenmesi 
Firewall 	Guvenlik bolgesi yonetimi 
Wi-Fi (802.11) 	Kablosuz istemci erisimi 
 
2.3	Ag Tasarim Asamalari 
Proje asagidaki asamalar izlenerek gelistirilmistir: 
 
Asama 1 - Gereksinimlerin Belirlenmesi 
Internet kafenin ag ihtiyaclari analiz edilmis; musteri, personel ve yonetim kullanici kategorileri belirlenmistir. Her kategori icin ayri VLAN ve guvenlik politikalari tanimlanmistir. 
 
Asama 2 - Topoloji Tasarimi 
Iki katmanli ag modeli (Dagitim - Erisim) benimsenin. Dagitim katmaninda yonlendirici ve anahtarlar, erisim katmaninda uc cihazlara bagli katman-2 anahtarlar konumlandirilmistir. 
 
Asama 3 - Konfigurasyon ve Test 
Cisco Packet Tracer uzerinde tum cihazlar konfiguere edilmis; baglanti testleri ping ve simulasyon modu araciligiyla dogrulanmistir. 
 
3.	Bulgular 
Bu bolumde projenin teknik uygulamalarindan elde edilen bulgular bilesen bazinda aktarilmaktadir. Her alt bolum ilgili teknolojinin nasil yapilandirildigini ve elde edilen sonuclari aciklamaktadir. 
 
3.1	VLAN Yapilandirmasi 
Internet kafe agi asagidaki VLAN'lara bolunmustur. Her VLAN bir internet kafe birimini ya da kullanici grubunu temsil etmekte; ayri yayin (broadcast) alani olusturarak ag guvenligini ve performansini artirmaktadir. 
 
VLAN ID 	Ad 	Bolum / Kullanim 	Ag Adresi 
20 	PERSONEL 	Personel Bilgisayarlari 	192.168.20.0/24 
30 	MUSTERI 	Musteri Bilgisayarlari 	192.168.30.0/24 
40 	SUNUCU 	Sunucu Odasi (DNS, DHCP, Web) 	192.168.40.0/24 
50 	MISAFIR 	Misafir Wi-Fi Erisimi 	192.168.50.0/24 
 
Trunk baglantilar (802.1Q) anahtarlar ile yonlendirici arasinda yapilandirilmis; her trunk portta tum VLAN'larin gecisine izin verilmistir. Her VLAN icin ayri IP adresi araligi tanimlanarak broadcast domainler birbirinden yalitilmistir. 
 
3.2	NAT ve Internet Erisimi 
Ic agdaki ozel (private) IP adreslerinin internete cikabilmesi icin Sinir Yonlendiricisi (Border Router) uzerinde NAT/PAT (Port Address Translation) yapilandirilmistir. 
 
•	Ic (inside) arayuz: LAN'a bagli yonlendirici arayuzu 
•	Dis (outside) arayuz: ISS baglanti arayuzu 
•	Overload (PAT) ile tek bir genel IP uzerinden tum ic kullanicilar internete cikmaktadir 
•	NAT cevirimleri show ip nat translations komutuyla dogrulanmistir 
 
3.3	Firewall Entegrasyonu 
Firewall, internet kafe agini internetten ayiran guvenlik sinirına (perimeter) konumlandirilmistir. Guvenlik bolgeleri (security zones) asagidaki gibi tanimlanmistir: 
 
Bolge 	Guvenlik Duzeyi 	Aciklama 
Inside 	100 (En Yuksek) 	Internet kafe ic agi - tam guvenilir 
Outside 	0 (En Dusuk) 	Internet - guvensiz 
 
Firewall politikalari; disaridan iceriye gelen trafigi varsayilan olarak engeller, iceriden disariya giden trafige ise izin verir. Bu sayede ic ag, internet kaynakli tehditlere karsi korunmaktadir. 
 
3.4	Kablosuz Ag (Wi-Fi) Destegi 
Internet kafenin ortak alanlarina (musteri salonu, bekleme kosesi, giris) kablosuz erisim noktalari (AP) yerlestirilmistir. Her erisim noktasi ilgili VLAN'a trunk baglanti uzerinden baglanmis; SSID politikalari kullanici grubuna gore ayrilmistir. 
 
•	KampusNet_Personel: Personel VLAN (20) - sifrelenmis WPA2 
•	KampusNet_Musteri: Musteri VLAN (30) - sifrelenmis WPA2 
•	KampusNet_Misafir: Misafir VLAN (50) - acik, internet erisimi kisitli 
 
4.	Sonuc 
Bu proje kapsaminda bir internet kafe icin gercekci bir LAN mimarisi tasarlanmis ve Cisco Packet Tracer ortaminda basariyla simule edilmistir. Uygulanan cozum; ag guvenligi, NAT ile internet erisimi ve kablosuz baglanti gibi temel ag gereksinimlerini karsilamaktadir. 
 
VLAN segmentasyonu ile ag trafigi mantiksal olarak izole edilmis; farkli kullanici gruplari (yonetim, personel, musteri, misafir) birbirinden ayrilmistir. NAT/PAT yapilandirmasi sayesinde tum ic kullanicilar tek bir genel IP adresi uzerinden guvenli bicimde internete erisebilmektedir. 
 
Firewall entegrasyonu ile disaridan gelen yetkisiz erisimler engellenmiş; ic agin guvenligi saglanmistir. Kablosuz erisim noktalari araciligiyla ise mobil kullanicilara da ag erisimi sunulmustur. 
 
Sonuc olarak tasarlanan ag mimarisi; yonetilebilir, guvenli ve internet kafenin temel ihtiyaclarini karsilayan islevsel bir yapi ortaya koymaktadir. 
 
5.	GitHub 
Projeye ait tum Cisco Packet Tracer dosyalari (.pkt) ve bu rapor asagidaki GitHub deposuna yuklenmistir. Depo baglantisi ve yukleme dogrulamasi asagida verilmektedir. 
 
GitHub Deposu Baglantisi: 
https://github.com/HuseyinEkiz/Internet-Kafe-LAN-Network-Tasarimi/ 
 
6.	Kaynakca 
[1]	Forouzan, B. A. (2022). Data Communications and Networking (5. Baski). McGraw-Hill. 
[2]	Stallings, W. (2021). Data and Computer Communications (10. Baski). Pearson. 
[3]	Cisco Networking Academy. (2024). CCNA: Introduction to Networks. Cisco NetAcad. 
[4]	Cisco Systems. (2024). NAT Configuration Guide - Cisco IOS XE. Cisco Press. 
