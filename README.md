TRENDYOL ÇOK SATANLAR GİYİM KATEGORİSİ VERİ ÇEKME OTOMASYONU

Açıklama: Bu proje ile trendyol.com web sitesindeki çok satanlar giyim kategorisindeki 100 ürünün verilerini çekip istenen formata getirip google sheets tablouna kayıt eden bir n8n otomasyonu oluşturdum.

Çözüm Özeti: Bu n8n otomasyonu manuel olarak çalıştırılacak şekilde ayarlandı. Çalıştırıldığında ilk olarak, önceki çalışmadan Google Sheets tablosunda kalmış olan verileri temizlemek için Clear Sheet node’u çalışıyor. Bu aşamadan sonra, veriye ulaşma kısmında pagination içeren API isteğinde gerekli değişiklikleri yapabilmek için 1’den 5’e kadar giden bir array oluşturuluyor. Ardından, API’deki gerekli değişiklikleri yapan kod ile birlikte HTTP Request gönderilerek toplamda 100 ürünün tüm verileri JSON formatında çekiliyor. Elde edilen bu veriler, JavaScript kodları ile istenilen formata dönüştürülüyor ve en sonunda Google Sheets dosyasına kaydediliyor.

Karşılaşılan Sorunlar ve Çözümleri: 

1-Benim çok satanlar giyim kategorisine ulaşmamı sağlayan URL şu şekildeydi: https://www.trendyol.com/cok-satanlar?type=bestSeller&webGenderId=1
Ancak bu sayfa ilk yüklendiğinde sadece 20 ürün ekrana geliyor, sonrasında aşağı kaydırıldıkça yeni ürünler yükleniyordu.

Çözüm: Öncelikle bu sorunun üstesinden gelmek için otomatik olarak aşağı kaydırma işlemini gerçekleştirebilecek bulut tabanlı bir tarayıcı kullanmayı denedim, ancak bu kısımda başarılı olamadım. Sonrasında yaptığım araştırmalarda, web siteleri infinite scroll yapıları kullandığında aslında arka planda sitenin API’lerine pagination ile istek gönderildiğini öğrendim. Daha sonra benim projemde kullanılan API’nin şu şekilde olduğunu fark ettim:
https://apigw.trendyol.com/discovery-web-searchgw-service/category-top-ranking/personalized-products?page=1&channelId=1
ve burada page parametresinin 1, 2, 3, 4, 5 şeklinde değerler alabildiğini buldum.

2- Verilerimi çekip düzenledikten sonra kayıt ettiğim Google Sheets tablosunda, bir sonraki çalıştırmada veriler önceki verilere ek olarak yazılıyordu. Yani her çalıştırmada, değişiklik olsun ya da olmasın, tablomda 100 satır ürün ve verisi ekleniyordu. Ancak bu şekilde olmasını istemiyordum.

Çözüm: Bu nedenle bir Clear Sheet node’unu flow’umun en sonuna ekledim, ancak bu şekilde yaptığımda çalışma sona erdiğinde tablom temizlenmiş oluyordu. Bu yüzden, yaptığım akıl yürütme sonucunda, çalıştırılır çalıştırılmaz eski verileri kaldırması adına Clear Sheet node’unu flow’un en başına ekledim.

Çalıştırma Adımları
1-	Bu GitHub reposunu bilgisayarınıza klonlayın
2-	n8n arayüzünüzü açın ve Import From File seçeneğini kullanarak repodaki trendyolveri.json dosyasını içeri aktarın.
3-	Execute Workflow butonuna basarak akışı manuel olarak çalıştırın.
4-	Verilerin kayıt edildiği Google Sheets dosyasına erişmek için aşağıdaki linke tıklayın.

https://docs.google.com/spreadsheets/d/14J0wV7lfWEB0QV4oAYuqRBcVVARfr4Wdg2RA3oF1O-o/edit?usp=sharing

