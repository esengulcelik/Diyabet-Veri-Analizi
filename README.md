# Diyabet Keşifçi Veri Analizi

Bu veri seti, bireylerin sağlık durumlarını incelemek ve diyabet riskiyle ilişkili faktörleri analiz etmek için hazırlanmıştır. Veri seti; yaş, cinsiyet, fiziksel aktivite, yüksek tansiyon gibi değişkenlerin yanı sıra bireylerin diyabet durumu (ikili: 0 veya 1) gibi bilgileri içermektedir. Veri seti, diyabetin risk faktörlerini anlamak ve sağlıklı yaşam tarzı değişiklikleri için çıkarımlar yapmak amacıyla kullanılabilir.
# Değişkenler
* Diabetes_binary: Katılımcının diyabet hastası olup olmadığını belirler.
* HighBP: Katılımcının yüksek tansiyona sahip olup olmadığını belirtir.
* HighChol: Katılımcının kolesterol seviyesinin yüksek olup olmadığını belirtir.
* CholCheck: Katılımcının kolesterol ölçümü yaptırıp yaptırmadığını belirtir.
* BMI: Katılımcının vücut ağırlığına göre sağlık durumunu değerlendirir.
* Smoker: Katılımcının sigara kullanıp kullanmadığını belirtir.
* Stroke: Katılımcının inme geçirmiş olup olmadığını belirtir.
* HeartDiseaseorAttack: Kalp hastalığı veya kalp krizi geçirme durumunu değerlendirir.
* PhysActivity: Katılımcının fiziksel aktivite yapıp yapmadığını belirtir.
* Fruits: Katılımcının düzenli olarak meyve yiyip yemediğini belirtir.
* Veggies: Katılımcının düzenli olarak sebze yiyip yemediğini belirtir.
* HvyAlcoholConsump: Katılımcının ağır alkol tüketip tüketmediğini belirtir.
* AnyHealthcare: Katılımcının herhangi bir sağlık hizmetine erişim durumunu belirtir.
* NoDocbcCost: Katılımcının maliyet nedeniyle doktora gidememe durumunu belirtir.
* GenHlth: Katılımcının genel sağlık durumunu değerlendirdiği bir ölçümdür.
* MentHlth: Katılımcının ruh sağlığının kötü olduğu gün sayısını belirtir.
* PhysHlth: Katılımcının fiziksel sağlığının kötü olduğu gün sayısını belirtir.
* DiffWalk: Katılımcının yürümede zorluk çekip çekmediğini belirtir.
* Sex: Katılımcının cinsiyetini belirtir.
* Age: Katılımcının yaşını belirtir.
* Education: Katılımcının eğitim seviyesini belirtir.
* Income: Katılımcının gelir seviyesini belirtir.

Veri seti, sağlık analizleri yapmak, diyabet riskini değerlendirmek ve ilişkili sağlık faktörlerini belirlemek için oldukça kullanışlıdır. Özellikle çapraz tablolar ve görselleştirme yöntemleriyle diyabet riski üzerindeki etkiler analiz edilebilir.

Kaggle Veri Seti: https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset

Kaggle Linki: https://www.kaggle.com/code/esenglelik/diyabet-sagl-k-gostergeleri

Github Hesabım: https://github.com/esengulcelik



# 1. Veri Setini Yükleme ve Kopyalama
df_: İlk yüklenen veri setini tutar. df: df_ veri setinin bir kopyasıdır 

Veri seti 70692 satır ve 22 sütundan oluşmakta olup, 0’dan 70691’e kadar indislenmiştir. Tüm sütunlar float64 veri tipinde görünmesine rağmen, bazı sütunlar (örneğin, Sex, GenHlth, Income, Education) kategorik veriyi temsil ediyor. Bu sütunlar detaylı incelenerek gerekli dönüştürmeler yapılabilir. Veri setinde eksik değerler bulunmaktadır; örneğin, Diabetes_binary sütununda 2077 eksik veri bulunurken, HighBP sütununda bu sayı 2183’tür. Eksik değer oranı genellikle düşüktür. Eksik veriler, ortalama, medyan veya mod ile doldurulabilir ya da veri kaybını minimize etmek için farklı yöntemler uygulanabilir. Genel olarak veri seti, sağlık durumlarını analiz etmeye uygundur.


* BMI (Vücut Kitle İndeksi): Ortalama BMI değeri 29.85 olup, bu değer genel olarak aşırı kilolu kategorisine işaret eder. Değerler arasında standart sapma 7.12'dir ve minimum değer 12, maksimum değer ise 98'dir. Verilerin çeyrek dağılımı (25%, 50%, 75%) incelendiğinde, çoğu bireyin BMI değerinin 25 ile 33 arasında olduğu görülmektedir.
* Sebze Tüketimi (Veggies): Veriler, bireylerin %78.9’unun düzenli olarak sebze tükettiğini göstermektedir . Çoğu kişi sebze tükettiğinden dolayı dağılım oldukça dardır ve verinin büyük kısmı 1'de toplanmıştır.
* Aşırı Alkol Tüketimi (HvyAlcoholConsump): Katılımcıların sadece %4.3’ü aşırı alkol tüketmektedir. Bu değer, toplumun büyük çoğunluğunun alkolü aşırı tüketmediğini göstermektedir.
* Genel Sağlık Durumu (GenHlth): Ortalama genel sağlık değerlendirmesi 2.83 olup, 1 ile 5 arasında değişmektedir. Bu, bireylerin genel sağlık durumlarının orta düzeyde olduğunu göstermektedir.
* Zihinsel Sağlık (MentHlth): Son 30 günde ortalama 3.76 kötü ruh sağlığı günü rapor edilmiştir. Ancak, standart sapma 8.16 ile oldukça yüksektir, bu da zihinsel sağlık durumunun bireyler arasında büyük farklılıklar gösterdiğini ifade eder.
* Fiziksel Sağlık (PhysHlth): Ortalama fiziksel rahatsızlık günü 5.81 olup, standart sapma 10.05’tir. Çoğu birey fiziksel sağlık sorunları yaşamazken, bazı bireylerde bu sorunların yoğun olduğu görülmektedir.
* Yaş (Age): Katılımcıların yaşları 1 ile 13 arasında kategorize edilmiştir. Ortalama yaş kategorisi 8.58'dir. Veriler, katılımcıların genelde orta yaş ve üzeri bireylerden oluştuğunu göstermektedir.

# 3. Grafikler
# 3.1 Histogram Grafiği
Eksik Değerleri doldurmak için öncelikle sayısal değerler de histogram grafiğine bakıyorum. Eğer veri simetrikse ve normal dağılıyorsa mod genellikle daha anlamlıdır. Çünkü medyan, normal dağılımda ortadaki değeri verir ve daha az etkilenir. Eğer verinin dağılımı simetrik değil ve sola doğru (negatif çarpıklık) yada sağa doğru(pozitif çarpıklık) ise, yani daha fazla düşük değer varsa ve uç değerler yüksekse, medyan kullanmak genellikle daha uygun olacaktır. 

Histogram grafiği sonucunda sayısal değerler de medyan ile doldurmaya karar verdim. Kategorik değerlerde ise mod kullandım.

# 3.2. Korelasyon Isı Haritası (Heatmap):
BMI ile HighBP ve HighChol arasında orta düzeyde pozitif bir korelasyon var, bu da yüksek BMI'nin bu sağlık sorunlarıyla bağlantılı olduğunu gösteriyor.
Diabetes_binary(diyabet var/yok) ile HighBP, BMI ve GenHlth arasında anlamlı pozitif korelasyonlar mevcut. Bu, yüksek tansiyon, yüksek BMI ve kötü genel sağlık durumunun diyabetle ilişkili olduğunu işaret ediyor.
Negatif korelasyonlar (Income ve Diabetes_binary gibi) ise sosyoekonomik durumun diyabet etkileyebileceğini gösteriyor.
Bu iki grafik, diyabet risk faktörlerinin (örneğin, BMI, tansiyon, kolesterol) hem bireysel hem de genel eğilimler açısından analizini destekler. Korelasyon haritası ise modelleme için hangi değişkenlerin önemli olabileceğine dair bir fikir verir.

# 3.3. Bar Grafiği
Bu grafik, kategorik değişkenlerin frekanslarını görselleştirmek amacıyla hazırlanmıştır. Her bir bar grafiği, belirli bir kategorik sütundaki benzersiz değerlerin (örneğin 0 ve 1) sayısını göstermektedir.

# 3.4. Gruplandırılmış bar grafiği:
Yüksek tansiyona sahip bireylerde diyabet oranı (1) belirgin şekilde daha yüksek, olmayan bireylerde (0) diyabet oranı daha düşük. Yüksek tansiyon, diyabetle ilişkili önemli bir risk faktörü olabilir.
Sigara kullananlar (1) ile kullanmayanlar (0) arasında diyabet oranı benzerdir.Sigara, bu grafikte diyabet üzerinde çok belirgin bir farklılık yaratmıyor gibi görünüyor.
Kalp hastalığı geçiren bireylerde (1), diyabet oranı çok yüksek, olmayan bireylerde (0), diyabet oranı daha düşük. Kalp hastalıkları, diyabetle güçlü bir şekilde ilişkili olabilir.
Genel olarak Yüksek tansiyon, yüksek kolesterol, felç, ve kalp hastalıkları, diyabetle doğrudan ilişkili faktörler gibi görünüyor.
Fiziksel aktivite ve meyve tüketimi gibi sağlıklı yaşam alışkanlıkları, diyabet riskini azaltmada güçlü bir rol oynayabilir.


# 3.5. BMI Kategorilerine Göre Diyabet ve Diyabetsiz Oranı(Bar Grafiği):
Bu grafik, BMI kategorilerinde diyabetli ve diyabetsiz bireylerin oranlarını gösteriyor. Verilere göre:
Zayıf ve Normal BMI kategorilerinde diyabetsiz bireylerin oranı oldukça yüksekken, diyabetli bireylerin oranı düşük.
Aşırı Kilolu kategorisinde diyabetli bireylerin oranı artıyor.
Obez kategorisinde diyabetli bireylerin oranı çok daha yüksek ve diyabetsiz bireylerin oranı düşüyor.
Bu durum, obezite ve diyabet arasındaki güçlü ilişkiyi açıkça göstermekte. BMI arttıkça diyabet riski de yükseliyor.


Çapraz tablo sayesinde fiziksel aktivite ve yüksek tansiyon kombinasyonunun diyabet üzerindeki etkisini görebiliriz.
* values: Diabetes_binary değişkenini analiz etmek için kullanıyoruz.
* index: Yüksek Tansiyon (HighBP) değişkeni satırda yer alıyor.
* columns: Fiziksel Aktivite (PhysActivity) sütunda yer alıyor.
* aggfunc: Ortalama oranı görmek için 'mean' kullanıyoruz.

Isı haritası ile sonuçları görselleştiriyoruz. 

* HighBP = 0 ve PhysActivity = 0: Diyabet oranı %38.
* HighBP = 0 ve PhysActivity = 1: Diyabet oranı %24 (en düşük oran). Bu, fiziksel aktivitenin düşük tansiyon grubunda diyabet oranını azalttığını gösterebilir.
* HighBP = 1 ve PhysActivity = 0: Diyabet oranı %71 (en yüksek oran). Yüksek tansiyon ve fiziksel aktivite eksikliği diyabet riskini artırıyor gibi görünüyor.
* HighBP = 1 ve PhysActivity = 1: Diyabet oranı %60. Fiziksel aktivite, yüksek tansiyon grubunda diyabet oranını bir miktar azaltmış.
Sonuç olarak, hem yüksek tansiyon hem de fiziksel aktivite eksikliği diyabet oranını artırmaktadır. Fiziksel aktivitenin diyabet oranını azaltıcı etkisi, özellikle düşük tansiyon grubunda daha belirgin görülmektedir.


Diyabet, dünya çapında milyonlarca insanı etkileyen kronik bir hastalıktır. Diyabeti erken tespit etmek, hastalığın ilerlemesini önlemek ve sağlık maliyetlerini düşürmek için önemli bir adımdır.
Bu veri setine dayalı bir tahmin modeli şu problemlere çözüm sağlayabilir:

Erken Teşhis: Hastaların verilerine dayanarak diyabet riskini tahmin edebiliriz. Bu, bireylere erken teşhis ve tedavi planlaması sağlar.
Kişiselleştirilmiş Tedavi Önerileri: Model çıktıları, bireyler için özelleştirilmiş yaşam tarzı değişiklikleri veya tedavi önerileri sunmada kullanılabilir.

Bu model, aşağıdaki alanlarda sağlık sektörüne değer katabilir:

Hastaneler ve Klinikler: Risk grubu analizlerini otomatikleştirerek hasta kabul süreçlerini hızlandırabilir.
Sağlık ve Fitness Uygulamaları: Kullanıcılarına risk analiz raporları ve önleyici sağlık tavsiyeleri sunabilir.

Önerilen Makine Öğrenimi Algoritması ve Nedenleri

Logistic Regression:
Diyabet tahmini gibi ikili sınıflandırma problemleri için basit, hızlı ve yorumlanabilir bir modeldir. 
Random Forest:
Özellikler arasındaki karmaşık ilişkileri modelleyebilir. Aynı zamanda, eksik değerler veya aykırı değerler gibi problemlere karşı dayanıklıdır.
KNN (K-Nearest Neighbors):
Diyabet risk faktörleri arasında benzerliklere dayanarak tahmin yapabilir. Ancak büyük veri setlerinde daha yüksek hesaplama maliyeti yaratabilir.

Veri seti göz önünde bulundurulduğunda, Logistic Regression veya Random Forest önerilir. Çünkü bu algoritmalar:
Bu veri setinde olduğu giib ikili sınıflandırma probleminde ve çoklu veri tipleri (sürekli ve kategorik) üzerinde etkili çalışabilir.

Sonuç ve Öneriler
Model Performansı, proje başarı kriteri olarak doğruluk, hassasiyet (precision), hatırlama (recall) ve F1 skorları gibi metrikler kullanılmalıdır. Örneğin, modelin pozitif diyabet vakalarını doğru tahmin etme oranı (recall) özellikle önemlidir.
