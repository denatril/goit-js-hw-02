Ödev 2
Ödev 2 — Modül 2 (if/switch/ternary • && || ! • String metotları • Döngüler)
Genel amaç
Koşul kontrolü, string kısaltma, spam kontrolü ve switch ile sabit seçenek yönetimi.
Proje/Teslim standardı
Repo: goit-js-hw-02
Yapı şemaya uygun
Prettier + console temiz
Teslim: repo + pages

— Droid Siparişleri (task-1.js)
Amaç: Müşteri kredisi yetiyorsa siparişi onayla, yetmiyorsa hata döndür.
Ne yapacaksın?
Fonksiyon: makeTransaction(quantity, pricePerDroid, customerCredits)
totalPrice = quantity * pricePerDroid
Eğer totalPrice > customerCredits → "Insufficient funds!"
Değilse → You ordered <quantity> droids worth <totalPrice> credits!
Mentor checklist
Doğru karşılaştırma ve doğru string
Sık hata
>= kullanıp eşit durumda yanlış hata döndürmek (kredi eşitse satın alabilmeli)

— Mesaj Biçimlendirme (task-2.js)
Amaç: Mesaj maxLength’i aşarsa kısalt + "..." ekle.
Ne yapacaksın?
Fonksiyon: formatMessage(message, maxLength)
Eğer message.length <= maxLength → message
Aksi → message.slice(0, maxLength) + "..."
Dikkat
slice 0’dan başlar, maxLength dahil değil (tam istediğimiz).
Boşluk/3 nokta birebir olmalı.
Sık hata
slice(0, maxLength - 3) gibi yanlış yorumlamak (ödev bunu istemiyor)

— Spam kontrolü (task-3.js)
Amaç: Metin “spam” veya “sale” içeriyorsa true.
Ne yapacaksın?
Fonksiyon: checkForSpam(message)
Case-insensitive kontrol:
const normalized = message.toLowerCase()
normalized.includes("spam") || normalized.includes("sale")
Dikkat
toLowerCase() kritik: SPAM, sAlE gibi varyasyonlar var.
Sadece kelime değil, metin içinde geçmesi yeterli.
Sık hata
indexOf(...) > 0 yazmak (0’da bulursa false olur); doğru: !== -1 ya da includes

— Teslimat Maliyeti (task-4.js)
Amaç: switch ile ülkeye göre fiyat döndür, yoksa “Sorry…”
Ne yapacaksın?
Fonksiyon: getShippingCost(country)
switch (country):
China 100
Chile 250
Australia 170
Jamaica 120
default: "Sorry, there is no delivery to your country"
Eşleşenlerde mesaj:
Shipping to <country> will cost <price> credits
Dikkat
break unutulursa “fall-through” olur ve fiyat bozulur.
Ülke isimleri case-sensitive (Germany örneğinde yok).

- Ana hatları okuduktan ve ana hatlardaki ek görevleri çözdükten sonra ödevi yapmaya başlayın.
- Sadece ek materyalleri kendiniz çalıştıysanız bir artı olacaktır (özet hariç).
- Hemen anlamadığınız konulara geri dönmekten çekinmeyin — bilgilerin ilk seferde "çalışmaması" normaldir.
- Ev ödevlerinde, gerekliliklere (görev tanımları) uygun olarak görevleri yerine getiriyoruz.
- **VSC**'de mantıksal operatörlerle çalışın. Boole işleçlerinin doğru veya yanlış yerine işlenenin değerini döndürdüğünü unutmayın.
- Döngülere dikkat edin. `for` ve `for...of`un nasıl çalıştığını anlayın ve `break` ve `continue` ile başa çıkın.


Görev 1. Droid Siparişleri



İşlem dosyası task-1.js içinde bu görevi gerçekleştir.


Tamir droidleri satış istasyonu, satış departmanı için yazılımı yazmaya hazır, yapmanız gereken tek şey, tamir droidleri satın alımı hakkında bir mesaj oluşturan makeTransaction(quantity, pricePerDroid, customerCredits) fonksiyonunu tanımlamaktır.

Çağrılırken üç parametre alacak şekilde tanımlanmıştır:

quantity - sipariş edilen droid miktarı
pricePerDroid - bir droidin fiyatı
customerCredits - müşterinin hesabındaki toplam miktar


Fonksiyonu aşağıdaki gibi tamamla:

Siparişin toplam tutarını (tüm droid siparişlerinin toplam değeri) saklamak için bir değişken tanımla ve bu tutarı hesaplamak için bir ifade ata.
Müşterinin siparişi ödeyip ödeyemeyeceğini kontrol et:
Ödenecek tutar, müşterinin hesabındaki krediden fazla ise fonksiyon, "Insufficient funds!" dizesini döndürmelidir.
Aksi takdirde, işlev "You ordered <quantity> droids worth <totalPrice> credits!" dizesini döndürmelidir, burada <quantity>, sipariş edilen droid miktarıdır ve <totalPrice>, bunların toplam değeridir.
Aşağıdaki kodu alıp, fonksiyonunuzu tanımladıktan sonra doğruluğunu kontrol etmek için yapıştırın. Sonuçlar konsola yazdırılacaktır.



console.log(makeTransaction(5, 3000, 23000)); // "You ordered 5 droids worth 15000 credits!"
console.log(makeTransaction(3, 1000, 15000)); // "You ordered 3 droids worth 3000 credits!"
console.log(makeTransaction(10, 5000, 8000)); // "Insufficient funds!"
console.log(makeTransaction(8, 2000, 10000)); // "Insufficient funds!"
console.log(makeTransaction(10, 500, 5000)); // "You ordered 10 droids worth 5000 credits!"



Bu kodu mentör tarafından kontrol edilmesi için bırak.



Mentörün dikkat edeceği noktalar:

makeTransaction(quantity, pricePerDroid, customerCredits) adında bir fonksiyon tanımlandı.
makeTransaction(5, 3000, 23000) çağrısı "You ordered 5 droids worth 15000 credits!" döndürür.
makeTransaction(3, 1000, 15000) çağrısı "You ordered 3 droids worth 3000 credits!" döndürür.
makeTransaction(10, 5000, 8000) çağrısı "Insufficient funds!" döndürür.
makeTransaction(8, 2000, 10000) çağrısı "Insufficient funds!" döndürür.
makeTransaction(10, 500, 5000) çağrısı "You ordered 10 droids worth 5000 credits!" döndürür.


Görev 2. Mesaj Biçimlendirme



İşlem dosyası task-2.js içinde bu görevi gerçekleştir.


formatMessage(message, maxLength) adında bir işlev(fonksiyon) ilan et, bu işlev bir dizeyi(string) (message parametresi) alır ve maksimum uzunluğa (maxLength parametresi) göre uzunluğunu kontrol eder.



Fonksiyon kodunu aşağıdaki gibi tamamla:

Dize uzunluğu maxLength'e eşit veya daha kısa ise, işlev değişiklik yapmadan orijinal diziyi döndürür.
Eğer uzunluk maxLength'i aşıyorsa, işlev diziyi maxLength karaktere kadar kısaltır, sonuna üç nokta "..." ekler ve kısaltılmış versiyonu döndürür.
Aşağıdaki kodu işlevinizi tanımladıktan sonra yapıştırarak işlevin doğruluğunu kontrol edin. Konsola işlemin sonuçları yazdırılacaktır.



console.log(formatMessage("Curabitur ligula sapien", 16)); // "Curabitur ligula..."
console.log(formatMessage("Curabitur ligula sapien", 23)); // "Curabitur ligula sapien"
console.log(formatMessage("Vestibulum facilisis purus nec", 20)); // "Vestibulum facilisis..."
console.log(formatMessage("Vestibulum facilisis purus nec", 30)); // "Vestibulum facilisis purus nec"
console.log(formatMessage("Nunc sed turpis a felis in nunc fringilla", 15)); // "Nunc sed turpis..."
console.log(formatMessage("Nunc sed turpis a felis in nunc fringilla", 41)); // "Nunc sed turpis a felis in nunc fringilla"



Bu kodu mentör tarafından kontrol edilmesi için bırak.



Mentorun gözden geçirirken dikkat edeceği noktalar:

formatMessage(message, maxLength) fonksiyonu tanımlandı.
formatMessage("Curabitur ligula sapien", 16) fonksiyon çağrısı "Curabitur ligula..." döndürür.
formatMessage("Curabitur ligula sapien", 23) fonksiyon çağrısı "Curabitur ligula sapien" döndürür.
formatMessage("Vestibulum facilisis purus nec", 20) fonksiyon çağrısı "Vestibulum facilisis..." döndürür.
formatMessage("Vestibulum facilisis purus nec", 30) fonksiyon çağrısı "Vestibulum facilisis purus nec" döndürür.
formatMessage("Nunc sed turpis a felis in nunc fringilla", 15) fonksiyon çağrısı "Nunc sed turpis..." döndürür.
formatMessage("Nunc sed turpis a felis in nunc fringilla", 41) fonksiyon çağrısı "Nunc sed turpis a felis in nunc fringilla" döndürür.


Görev 3. Spam kontrolü

Görevi task-3.js dosyasında gerçekleştirin.

checkForSpam(message) adlı fonksiyon, bir dizeyi(string) (message parametresi) alır, içinde yasaklı kelimeler olan (spam ve sale) kelimelerinin varligini kontrol eder ve kontrol sonucunu döndürür. Parametre olarak verilen message dizesindeki kelimeler büyük-küçük harf duyarlı olabilir, örneğin SPAM veya sAlE.

Fonksiyonun kodunu aşağıdaki şekilde tamamla:

Eğer yasaklı kelime (spam veya sale) bulunursa, fonksiyon true değerini döndürür.
Eğer dizede yasaklı kelimeler bulunmuyorsa, fonksiyon false değerini döndürür.


Aşağıdaki kodu al ve fonksiyonun doğru çalışıp çalışmadığını kontrol etmek için kendi fonksiyonunun bildiriminden sonra yapıştır. Konsola işleyiş sonuçları yazdırılacaktır.



console.log(checkForSpam("Latest technology news")); // false
console.log(checkForSpam("JavaScript weekly newsletter")); // false
console.log(checkForSpam("Get best sale offers now!")); // true
console.log(checkForSpam("Amazing SalE, only tonight!")); // true
console.log(checkForSpam("Trust me, this is not a spam message")); // true
console.log(checkForSpam("Get rid of sPaM emails. Our book in on sale!")); // true
console.log(checkForSpam("[SPAM] How to earn fast money?")); // true



Bu kodu mentör tarafından kontrol edilmesi için bırak.



Danışmanın kontrol ederken dikkat edeceği noktalar:

checkForSpam(message) adlı fonksiyonun tanımlanmış olması.
checkForSpam("Latest technology news") çağrısının false döndürmesi.
checkForSpam("JavaScript weekly newsletter") çağrısının false döndürmesi
checkForSpam("Get best sale offers now!") çağrısının true döndürmesi.
checkForSpam("Amazing SalE, only tonight!") çağrısının true döndürmesi.
checkForSpam("Trust me, this is not a spam message") çağrısının true döndürmesi.
checkForSpam("Get rid of sPaM emails. Our book in on sale!") çağrısının true döndürmesi.
checkForSpam("[SPAM] How to earn fast money?") çağrısının true döndürmesi.


Görev 4. Teslimat Maliyeti

task-4.js dosyasında bu görevi yerine getirin.

Kullanıcı ülkesine (parametre olarak country) ürün teslimatının mümkün olup olmadığını kontrol eden ve sonuç hakkında bir mesaj döndüren getShippingCost(country) fonksiyonunu tanımlayın. Kesinlikle switch ifadesini kullanın.

Gönderilen dize formatı "Shipping to <country> will cost <price> credits", burada <country> ve <price> yerine ilgili değerleri yerleştirmek gereklidir.

Ülke listesi ve teslimat maliyeti:

China - 100 kredi
Chile - 250 kredi
Australia - 170 kredi
Jamaica - 120 kredi
Listeden görülebileceği gibi teslimat her yerde mümkün değil. Belirtilen ülke listede yer almıyorsa, işlev "Sorry, there is no delivery to your country" dizesini döndürmelidir.

Fonksiyonunuzu tanımladıktan sonra aşağıdaki kodu alıp yapıştırarak işlevin doğruluğunu kontrol edebilirsiniz. Sonuçlar konsola yazdırılacaktır.



console.log(getShippingCost("Australia")); // "Shipping to Australia will cost 170 credits"
console.log(getShippingCost("Germany")); // "Sorry, there is no delivery to your country"
console.log(getShippingCost("China")); // "Shipping to China will cost 100 credits"
console.log(getShippingCost("Chile")); // "Shipping to Chile will cost 250 credits"
console.log(getShippingCost("Jamaica")); // "Shipping to Jamaica will cost 120 credits"
console.log(getShippingCost("Sweden")); // "Sorry, there is no delivery to your country"



Bu kodu mentör tarafından kontrol edilmesi için bırak.



Denetleme sırasında mentorun dikkat edeceği noktalar:

getShippingCost(country) adında bir fonksiyonun tanımlanmış olması
Fonksiyon içinde switch ifadesinin kullanılması
getShippingCost("Australia") çağrısının "Shipping to Australia will cost 170 credits" dönmesi
getShippingCost("Germany") çağrısının "Sorry, there is no delivery to your country" dönmesi
getShippingCost("China") çağrısının "Shipping to China will cost 100 credits" dönmesi
getShippingCost("Chile") çağrısının "Shipping to Chile will cost 250 credits" dönmesi
getShippingCost("Jamaica") çağrısının "Shipping to Jamaica will cost 120 credits" dönmesi
getShippingCost("Sweden") çağrısının "Sorry, there is no delivery to your country" dönmesi