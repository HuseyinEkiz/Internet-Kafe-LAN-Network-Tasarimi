# Marmara-Kampüs-CAN-Campus-Area-Network-Tasarimi
Hüseyin Ekiz – 170424051    Cem Anıl Erdem – 170424041

PROJE FİNAL RAPORU
Marmara Kampüsü CAN (Campus Area Network) Tasarımı
 
İçindekiler
1. Giriş
2. Yöntem
   2.1 Proje Kapsamı ve Hedefler
   2.2 Kullanılan Teknolojiler ve Yazılımlar
   2.3 Ağ Tasarım Aşamaları
3. Bulgular
   3.1 VLAN ve Inter-VLAN Yapılandırması
   3.2 OSPF Dinamik Yönlendirme
   3.3 NAT ve İnternet Erişimi
   3.4 ACL ve Güvenlik Politikaları
   3.5 Firewall Entegrasyonu
   3.6 HSRP ile Yüksek Erişilebilirlik
   3.7 EtherChannel ile Bant Genişliği Artırımı
   3.8 Kablosuz Ağ (Wi-Fi) Desteği
4. Sonuç
5. GitHub
6. Kaynakça
 
1. Giriş
Bu proje, Marmara Üniversitesi kampüs sınırları içerisindeki tüm akademik ve idari birimlerin güvenilir, kesintisiz ve yüksek performanslı bir ağ altyapısı üzerinden birbiriyle iletişim kurmasını sağlamak amacıyla tasarlanmış bir CAN (Campus Area Network – Kampüs Alan Ağı) mimarisini içermektedir.
Günümüz üniversite kampüslerinde eş zamanlı olarak yüzlerce cihaz ağ kaynaklarını kullanmaktadır. Bu durum, ağ yönetimini, güvenliğini ve erişilebilirliğini kritik bir mühendislik sorunu hâline getirmektedir. Geleneksel düz (flat) ağ mimarileri, büyük ölçekli ortamlarda yayın fırtınaları, yetersiz güvenlik izolasyonu ve ölçeklenebilirlik sorunlarına yol açmaktadır.
Bu proje kapsamında geliştirilen çözüm; VLAN tabanlı ağ segmentasyonu, Inter-VLAN yönlendirme, OSPF dinamik yönlendirme protokolü, NAT ile internet erişimi, ACL ve Firewall ile katmanlı güvenlik, HSRP ile yedeklilik ve EtherChannel ile yüksek bant genişliği bileşenlerini bir arada kullanarak profesyonel düzeyde bir kampüs ağı ortaya koymaktadır. Kablosuz (Wi-Fi) erişim noktaları ile de mobil kullanıcı desteği sağlanmaktadır.
Tüm tasarım ve simülasyon çalışmaları Cisco Packet Tracer ortamında gerçekleştirilmiş; konfigürasyonlar IOS komut satırı arayüzü (CLI) kullanılarak uygulanmıştır.
 
2. Yöntem
2.1 Proje Kapsamı ve Hedefler
Proje aşağıdaki temel hedefleri karşılayacak biçimde tasarlanmıştır:
•	Kampüs genelinde birimleri mantıksal olarak ayıran VLAN yapısı oluşturmak
•	VLAN'lar arası iletişimi yönetilen yönlendirme ile sağlamak (Inter-VLAN Routing)
•	OSPF protokolü ile dinamik ve ölçeklenebilir yönlendirme gerçekleştirmek
•	NAT aracılığıyla tüm iç ağın güvenli biçimde internete çıkışını sağlamak
•	ACL kuralları ve Firewall ile yetkisiz erişimleri engellemek
•	HSRP ile çekirdek katman yedekliliğini garanti altına almak
•	EtherChannel ile anahtar (switch) bağlantılarında bant genişliğini artırmak
•	Kablosuz erişim noktaları ile mobil kullanıcılara ağ erişimi sunmak

2.2 Kullanılan Teknolojiler ve Yazılımlar
Proje boyunca kullanılan temel teknolojiler ve araçlar aşağıdaki tabloda özetlenmiştir:

Teknoloji / Araç	Amaç / Kullanım Alanı
Cisco Packet Tracer	Ağ simülasyonu ve topoloji tasarımı
VLAN (802.1Q)	Ağ segmentasyonu ve yayın alanı kontrolü
Inter-VLAN Routing	VLAN'lar arası katman-3 iletişim
OSPF	Dinamik yönlendirme protokolü
NAT / PAT	İç IP adreslerin internet üzerinde gizlenmesi
ACL (Standart & Genişletilmiş)	Trafik filtreleme ve erişim denetimi
Firewall (ASA)	Güvenlik bölgesi yönetimi ve saldırı koruması
HSRP	Çekirdek yönlendirici yedekliliği ve failover
EtherChannel (LACP)	Çoklu bağlantı birleştirme ile bant genişliği artırımı
Wi-Fi (802.11)	Kablosuz istemci erişimi

2.3 Ağ Tasarım Aşamaları
Proje aşağıdaki aşamalar izlenerek geliştirilmiştir:
Aşama 1 – Gereksinimlerin Belirlenmesi
Kampüs birimlerinin ağ ihtiyaçları analiz edilmiş; akademik, idari ve misafir kullanıcı kategorileri belirlenmiştir. Her kategori için ayrı VLAN ve güvenlik politikaları tanımlanmıştır.
Aşama 2 – Topoloji Tasarımı
Üç katmanlı hiyerarşik ağ modeli (Çekirdek – Dağıtım – Erişim) benimsenmiştir. Çekirdek katmanda yedekli yönlendiriciler (HSRP), dağıtım katmanında katman-3 anahtarlar ve erişim katmanında uç cihazlara bağlı katman-2 anahtarlar konumlandırılmıştır.
Aşama 3 – Konfigürasyon ve Test
Cisco Packet Tracer üzerinde tüm cihazlar konfigüre edilmiş; bağlantı testleri ping, traceroute ve simülasyon modu aracılığıyla doğrulanmıştır.
 
3. Bulgular
Bu bölümde projenin teknik uygulamalarından elde edilen bulgular bileşen bazında aktarılmaktadır. Her alt bölüm ilgili teknolojinin nasıl yapılandırıldığını ve elde edilen sonuçları açıklamaktadır.
3.1 VLAN ve Inter-VLAN Yapılandırması
Kampüs ağı aşağıdaki VLAN'lara bölünmüştür. Her VLAN bir kampüs birimini ya da kullanıcı grubunu temsil etmekte; ayrı yayın (broadcast) alanı oluşturarak ağ güvenliğini ve performansını artırmaktadır.

VLAN ID	Ad	Bölüm / Kullanım	Ağ Adresi
10	YONETIM	İdari Personel & Yönetim	192.168.10.0/24
20	AKADEMIK	Akademik Birimler & Öğretim Üyeleri	192.168.20.0/24
30	OGRENCI	Öğrenci Laboratuvarları	192.168.30.0/24
40	SUNUCU	Sunucu Odası (DNS, DHCP, Web)	192.168.40.0/24
50	MISAFIR	Misafir Wi-Fi Erişimi	192.168.50.0/24
99	YONETIM_AG	Ağ Yönetim VLAN (Out-of-Band)	192.168.99.0/24

Trunk bağlantılar (802.1Q) anahtarlar ile çekirdek yönlendirici arasında yapılandırılmış; her trunk portta tüm VLAN'ların geçişine izin verilmiştir. Inter-VLAN yönlendirme, çekirdek katman yönlendiricisinde alt arayüzler (subinterface) aracılığıyla sağlanmıştır.
3.2 OSPF Dinamik Yönlendirme
Ağ içindeki yönlendirme, OSPF (Open Shortest Path First) protokolü ile otomatik olarak yönetilmektedir. OSPF, topoloji değişikliklerini dinamik olarak algılayarak yönlendirme tablolarını günceller; statik yönlendirmeye kıyasla çok daha ölçeklenebilir bir çözüm sunar.
•	Tüm iç yönlendiriciler OSPF Alan 0 (Backbone) içinde tanımlanmıştır
•	Her yönlendirici üzerinde network komutları ile ilgili arayüzler OSPF'e dahil edilmiştir
•	Loopback arayüzler OSPF Router-ID olarak kullanılmıştır
•	Komşuluk (neighbor) ilişkileri simülasyon ortamında doğrulanmıştır
3.3 NAT ve İnternet Erişimi
İç ağdaki özel (private) IP adreslerinin internete çıkabilmesi için Sınır Yönlendiricisi (Border Router) üzerinde NAT/PAT (Port Address Translation) yapılandırılmıştır.
•	İç (inside) arayüz: LAN'a bağlı yönlendirici arayüzü
•	Dış (outside) arayüz: İSS bağlantı arayüzü
•	Overload (PAT) ile tek bir genel IP üzerinden tüm iç kullanıcılar internete çıkmaktadır
•	NAT çevirileri show ip nat translations komutuyla doğrulanmıştır
3.4 ACL ve Güvenlik Politikaları
Erişim Denetim Listeleri (ACL) ile belirli trafik akışları izin ya da engel politikalarına tabi tutulmuştur. Proje kapsamında uygulanan güvenlik politikaları şunlardır:
•	Misafir VLAN (50) kullanıcıları yalnızca internete erişebilir; iç ağa erişim engellenmiştir
•	Öğrenci VLAN (30) kullanıcıları sunucu VLAN'ına (40) yalnızca HTTP/HTTPS üzerinden erişebilir
•	Yönetim VLAN (99) yalnızca ağ yöneticisi IP adresinden erişilebilir
•	Genişletilmiş ACL'ler, hedef IP ve port bazında detaylı filtreleme sağlamaktadır
3.5 Firewall Entegrasyonu
Cisco ASA Firewall, kampüs ağını internetten ayıran güvenlik sınırına (perimeter) konumlandırılmıştır. Güvenlik bölgeleri (security zones) aşağıdaki gibi tanımlanmıştır:

Bölge	Güvenlik Düzeyi	Açıklama
Inside	100 (En Yüksek)	Kampüs iç ağı – tam güvenilir
DMZ	50 (Orta)	Sunucu bölgesi – kontrollü erişim
Outside	0 (En Düşük)	İnternet – güvensiz

Firewall politikaları; dışarıdan içeriye gelen trafiği varsayılan olarak engeller, içeriden dışarıya giden trafiğe ise izin verir. DMZ'deki sunuculara belirli servis portları üzerinden dışarıdan erişim statik NAT ile sağlanmaktadır.
3.6 HSRP ile Yüksek Erişilebilirlik
Çekirdek katmanda iki yönlendirici, HSRP (Hot Standby Router Protocol) ile yapılandırılmıştır. Bu sayede aktif yönlendirici arıza verdiğinde, yedek yönlendirici saniyeler içinde devreye girerek ağın kesintisiz çalışması sağlanmaktadır.
•	HSRP Grubu 1: Sanal IP 192.168.10.1 – VLAN 10 geçidi
•	Aktif Router önceliği 110, Standby Router önceliği 100 olarak ayarlanmıştır
•	Preempt özelliği etkinleştirilerek kurtarma sonrası aktif rolün iade edilmesi sağlanmıştır
•	Failover süresi simülasyon testleriyle 10 saniyenin altında ölçülmüştür
3.7 EtherChannel ile Bant Genişliği Artırımı
Çekirdek ve dağıtım katmanı anahtarları arasındaki bağlantılarda EtherChannel (LACP – IEEE 802.3ad) uygulanmıştır. İki fiziksel bağlantı mantıksal olarak birleştirilerek bant genişliği iki katına çıkarılmış ve bağlantı yedekliliği sağlanmıştır.
•	Port-channel 1: Çekirdek Switch – Dağıtım Switch 1 arası (2x FastEthernet)
•	LACP modu active/active olarak yapılandırılmıştır
•	EtherChannel durumu show etherchannel summary ile doğrulanmıştır
3.8 Kablosuz Ağ (Wi-Fi) Desteği
Kampüs genelindeki ortak alanlara (kafeterya, kütüphane, koridorlar) kablosuz erişim noktaları (AP) yerleştirilmiştir. Her erişim noktası ilgili VLAN'a trunk bağlantı üzerinden bağlanmış; SSID politikaları kullanıcı grubuna göre ayrılmıştır.
•	KampusNet_Ogrenci: Öğrenci VLAN (30) – şifrelenmiş WPA2
•	KampusNet_Personel: Akademik VLAN (20) – şifrelenmiş WPA2 Enterprise
•	KampusNet_Misafir: Misafir VLAN (50) – açık, internet erişimi kısıtlı
 
4. Sonuç
Bu proje kapsamında Marmara Üniversitesi kampüsü için gerçekçi bir CAN mimarisi tasarlanmış ve Cisco Packet Tracer ortamında başarıyla simüle edilmiştir. Uygulanan çözüm; ağ güvenliği, yüksek erişilebilirlik, dinamik yönlendirme ve kablosuz bağlantı gibi modern kurumsal ağ gereksinimlerini karşılamaktadır.
VLAN segmentasyonu ile ağ trafiği mantıksal olarak izole edilmiş; Inter-VLAN yönlendirme ile birimler arası kontrollü iletişim sağlanmıştır. OSPF protokolü sayesinde topoloji değişikliklerine otomatik adapte olabilen dinamik bir yönlendirme altyapısı kurulmuştur.
HSRP ile çekirdek katman yedekliliği garanti altına alınmış; EtherChannel ile kritik bağlantılarda yüksek bant genişliği elde edilmiştir. ACL ve Firewall bileşenlerinin entegrasyonu, ağ güvenliğini çok katmanlı biçimde sağlamıştır.
Sonuç olarak tasarlanan ağ mimarisi; yönetilebilir, güvenli, yüksek performanslı ve ölçeklenebilir bir kampüs ağı ihtiyacını karşılamakta olup gerçek dünya uygulamalarına model teşkil edecek niteliktedir.
 
5. GitHub
Projeye ait tüm Cisco Packet Tracer dosyaları (.pkt) ve bu rapor aşağıdaki GitHub deposuna yüklenmiştir. Depo bağlantısı ve yükleme doğrulaması aşağıda verilmektedir.
GitHub Deposu Bağlantısı:
https://github.com/kullanici-adi/BLM2006-CAN-Projesi
Not: GitHub bağlantısı ve yükleme ekran görüntüsü, sunum öncesinde (04 Mayıs 2026 23:59) proje dosyaları yüklendikten sonra bu alana eklenecektir.
 
6. Kaynakça
[1] Forouzan, B. A. (2022). Data Communications and Networking (5. Baskı). McGraw-Hill.
[2] Cisco Systems. (2024). OSPF Configuration Guide – Cisco IOS XE. Cisco Press.
[3] Cisco Systems. (2024). QoS & Security Configuration Guide – Cisco IOS XE. Cisco Press.
[4] Stallings, W. (2021). Data and Computer Communications (10. Baskı). Pearson.
[5] Cisco Networking Academy. (2024). CCNA: Switching, Routing, and Wireless Essentials. Cisco NetAcad.

