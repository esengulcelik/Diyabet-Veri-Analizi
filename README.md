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

Github Hesabım: https://github.com/esengulcelik

#Kütüphaneler
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns
# 1. Veri Setini Yükleme ve Kopyalama

#df_: İlk yüklenen veri setini tutar. df: df_ veri setinin bir kopyasıdır 
df_=pd.read_csv(filepath_or_buffer="/kaggle/input/diabetes-health-indicators-dataset/diabetes_binary_5050split_health_indicators_BRFSS2015.csv")
df=df_.copy()
df
df.isnull().sum() #veri setindeki her bir sütundaki eksik (NaN) değerlerin sayısını döndürür.
Bu kod, verilen df veri setinin her bir hücresinden rastgele %3'ünün eksik değer olarak işaretlenmesini sağlar.

import random 
def add_random_missing_values(dataframe: pd.DataFrame,
                              missing_rate: float = 0.05) -> pd.DataFrame:
    """Turns random values to NaN in a DataFrame.

    To use this function, you need to import pandas, numpy and random libraries.

    Args:
        dataframe (pd.DataFrame): DataFrame to be processed.
        missing_rate (float): Percentage of missing value rate in float format. Defaults 0.05

    Returns:
        df_missing (pd.DataFrame): Processed DataFrame object.

    """
    # Get copy of dataframe
    df_missing = dataframe.copy()

    # Obtain size of dataframe and number total number of missing values
    df_size = dataframe.size
    num_missing = int(df_size * missing_rate)

    # Get random row and column indexes to turn them NaN
    for _ in range(num_missing):
        row_idx = random.randint(0, dataframe.shape[0] - 1)
        col_idx = random.randint(0, dataframe.shape[1] - 1)

        df_missing.iat[row_idx, col_idx] = np.nan

    return df_missing
df=add_random_missing_values(dataframe=df,
                            missing_rate=0.03)
df.isnull().sum() #Eksik değerleri ekledik. Toplam eksik değerler gözüküyor.

# 2. Keşifçi Veri Analizi
df.head(n=3) #ilk 3 satırı gösterir.

df.tail() #son 5 satırı gösterir.
df.shape #veri setinin boyut, satır ve sütun sayısı.
print(df.columns) #Veri setindeki sütunların isimleri.
print(len(df.columns)) #sütun sayısı.
print(type(df.columns)) #veri setinin türü.
Veri seti 70692 satır ve 22 sütundan oluşmakta olup, 0’dan 70691’e kadar indislenmiştir. Tüm sütunlar float64 veri tipinde görünmesine rağmen, bazı sütunlar (örneğin, Sex, GenHlth, Income, Education) kategorik veriyi temsil ediyor. Bu sütunlar detaylı incelenerek gerekli dönüştürmeler yapılabilir. Veri setinde eksik değerler bulunmaktadır; örneğin, Diabetes_binary sütununda 2077 eksik veri bulunurken, HighBP sütununda bu sayı 2183’tür. Eksik değer oranı genellikle düşüktür. Eksik veriler, ortalama, medyan veya mod ile doldurulabilir ya da veri kaybını minimize etmek için farklı yöntemler uygulanabilir. Genel olarak veri seti, sağlık durumlarını analiz etmeye uygundur.
df.info() # #DataFrame'inin genel bilgilerini özetler. Bu komut, veri setindeki her sütunun veri tipini, null (eksik) değer sayısını ve toplam satır sayısını gösterir. 
#Bu sütunların kategorik değer olması gerekli.Çünkü kategorik değerler genellikle belirli grupları veya sınıfları temsil eder.
categorical_columns = [
    "Diabetes_binary", "HighBP", "HighChol", "CholCheck", "Smoker",
    "Stroke", "HeartDiseaseorAttack", "PhysActivity", "Fruits",
    "AnyHealthcare", "NoDocbcCost", "DiffWalk", "Sex", "Education", "Income"
]
df[categorical_columns] = df[categorical_columns].astype('category') 
#Bu satır, veri setindeki categorical_columns listesinde belirtilen sütunları kategorik veri türüne dönüştürür, yani bu sütunların her birini category veri tipi olarak işler.

print(df.select_dtypes(include=['category']).columns)

df.info()
diabetes_counts = df['Diabetes_binary'].value_counts()
print(diabetes_counts)

print(f"Diyabetli Kişi Sayısı: {diabetes_counts[1]}")
print(f"Diyabetsiz Kişi Sayısı: {diabetes_counts[0]}")
* BMI (Vücut Kitle İndeksi): Ortalama BMI değeri 29.85 olup, bu değer genel olarak aşırı kilolu kategorisine işaret eder. Değerler arasında standart sapma 7.12'dir ve minimum değer 12, maksimum değer ise 98'dir. Verilerin çeyrek dağılımı (25%, 50%, 75%) incelendiğinde, çoğu bireyin BMI değerinin 25 ile 33 arasında olduğu görülmektedir.
* Sebze Tüketimi (Veggies): Veriler, bireylerin %78.9’unun düzenli olarak sebze tükettiğini göstermektedir . Çoğu kişi sebze tükettiğinden dolayı dağılım oldukça dardır ve verinin büyük kısmı 1'de toplanmıştır.
* Aşırı Alkol Tüketimi (HvyAlcoholConsump): Katılımcıların sadece %4.3’ü aşırı alkol tüketmektedir. Bu değer, toplumun büyük çoğunluğunun alkolü aşırı tüketmediğini göstermektedir.
* Genel Sağlık Durumu (GenHlth): Ortalama genel sağlık değerlendirmesi 2.83 olup, 1 ile 5 arasında değişmektedir. Bu, bireylerin genel sağlık durumlarının orta düzeyde olduğunu göstermektedir.
* Zihinsel Sağlık (MentHlth): Son 30 günde ortalama 3.76 kötü ruh sağlığı günü rapor edilmiştir. Ancak, standart sapma 8.16 ile oldukça yüksektir, bu da zihinsel sağlık durumunun bireyler arasında büyük farklılıklar gösterdiğini ifade eder.
* Fiziksel Sağlık (PhysHlth): Ortalama fiziksel rahatsızlık günü 5.81 olup, standart sapma 10.05’tir. Çoğu birey fiziksel sağlık sorunları yaşamazken, bazı bireylerde bu sorunların yoğun olduğu görülmektedir.
* Yaş (Age): Katılımcıların yaşları 1 ile 13 arasında kategorize edilmiştir. Ortalama yaş kategorisi 8.58'dir. Veriler, katılımcıların genelde orta yaş ve üzeri bireylerden oluştuğunu göstermektedir.
df.describe().T #pandas DataFrame'inin sayısal sütunları hakkında temel istatistiksel özet bilgilerini (ortalama, standart sapma, min, max, çeyrekler) verir ve .T ile bu bilgileri transpoze ederek satırları sütunlara dönüştürür.
df.isnull().sum().sum() #toplam eksik değer sayısı.
df.notnull().sum().sum() #eksik olmayan değer sayısı
# 3. Grafikler
# 3.1 Histogram Grafiği
Eksik Değerleri doldurmak için öncelikle sayısal değerler de histogram grafiğine bakıyorum. Eğer veri simetrikse ve normal dağılıyorsa mod genellikle daha anlamlıdır. Çünkü medyan, normal dağılımda ortadaki değeri verir ve daha az etkilenir. Eğer verinin dağılımı simetrik değil ve sola doğru (negatif çarpıklık) yada sağa doğru(pozitif çarpıklık) ise, yani daha fazla düşük değer varsa ve uç değerler yüksekse, medyan kullanmak genellikle daha uygun olacaktır. 
# Sayısal sütunlar için histogramlar
numeric_columns = df.select_dtypes(include=['float64', 'int64']).columns

for column in numeric_columns:
    plt.figure(figsize=(8, 6))
    df[column].hist(bins=30, edgecolor='black')
    plt.title(f'{column} Histogram')
    plt.xlabel(column)
    plt.ylabel('Frequency')
    plt.show()

# Kategorik sütunlar için bar grafikleri
categorical_columns = df.select_dtypes(include=['category']).columns

for column in categorical_columns:
    plt.figure(figsize=(8, 6))
    df[column].value_counts().plot(kind='bar', edgecolor='black')
    plt.title(f'{column} Bar Chart')
    plt.xlabel(column)
    plt.ylabel('Frequency')
    plt.show()

Histogram grafiği sonucunda sayısal değerler de medyan ile doldurmaya karar verdim. Kategorik değerlerde ise mod kullandım.
# Kategorik sütunları doldurmak için mod (en sık görülen değer) kullandım.
for column in categorical_columns:
    df[column] = df[column].fillna(df[column].mode()[0])

# Sayısal sütunları doldurmak için medyan kullandım.
numeric_columns = df.select_dtypes(include=['float64', 'int64']).columns
df[numeric_columns] = df[numeric_columns].fillna(df[numeric_columns].median())

df.isnull().sum() #Boş değerleri doldurdum, artık boş değerler yok.
# 3.2. Korelasyon Isı Haritası (Heatmap):
BMI ile HighBP ve HighChol arasında orta düzeyde pozitif bir korelasyon var, bu da yüksek BMI'nin bu sağlık sorunlarıyla bağlantılı olduğunu gösteriyor.
Diabetes_binary(diyabet var/yok) ile HighBP, BMI ve GenHlth arasında anlamlı pozitif korelasyonlar mevcut. Bu, yüksek tansiyon, yüksek BMI ve kötü genel sağlık durumunun diyabetle ilişkili olduğunu işaret ediyor.
Negatif korelasyonlar (Income ve Diabetes_binary gibi) ise sosyoekonomik durumun diyabet etkileyebileceğini gösteriyor.
Bu iki grafik, diyabet risk faktörlerinin (örneğin, BMI, tansiyon, kolesterol) hem bireysel hem de genel eğilimler açısından analizini destekler. Korelasyon haritası ise modelleme için hangi değişkenlerin önemli olabileceğine dair bir fikir verir.
correlation_matrix = df.corr()
plt.figure(figsize=(12, 8))  # Boyutlandırma
sns.heatmap(correlation_matrix, annot=True, fmt=".2f", cmap="coolwarm", cbar=True)
plt.title("Korelasyon Isı Haritası")
plt.show()
# 3.3. Bar Grafiği
import matplotlib.pyplot as plt
#Bu grafik, kategorik değişkenlerin frekanslarını görselleştirmek amacıyla hazırlanmıştır. Her bir bar grafiği, belirli bir kategorik sütundaki benzersiz değerlerin (örneğin 0 ve 1) sayısını göstermektedir.

# Kategorik sütunları filtreleme
categorical_columns = df.select_dtypes(include=['category']).columns

# Bar grafikleri oluşturma
plt.figure(figsize=(20, 15))  # Genel figür boyutu
for i, column in enumerate(categorical_columns, 1):
    plt.subplot((len(categorical_columns) + 2) // 3, 3, i)  # Alt grafikleri düzenleme
    df[column].value_counts().plot(kind='bar', color='skyblue', edgecolor='black')
    plt.title(f"{column} - Bar Grafiği")
    plt.xlabel(column)
    plt.ylabel("Frekans")
    plt.xticks(rotation=45)

plt.tight_layout()  # Grafik düzenlemesi
plt.show()

# 3.4. Gruplandırılmış bar grafiği:
Yüksek tansiyona sahip bireylerde diyabet oranı (1) belirgin şekilde daha yüksek, olmayan bireylerde (0) diyabet oranı daha düşük. Yüksek tansiyon, diyabetle ilişkili önemli bir risk faktörü olabilir.
Sigara kullananlar (1) ile kullanmayanlar (0) arasında diyabet oranı benzerdir.Sigara, bu grafikte diyabet üzerinde çok belirgin bir farklılık yaratmıyor gibi görünüyor.
Kalp hastalığı geçiren bireylerde (1), diyabet oranı çok yüksek, olmayan bireylerde (0), diyabet oranı daha düşük. Kalp hastalıkları, diyabetle güçlü bir şekilde ilişkili olabilir.
Genel olarak Yüksek tansiyon, yüksek kolesterol, felç, ve kalp hastalıkları, diyabetle doğrudan ilişkili faktörler gibi görünüyor.
Fiziksel aktivite ve meyve tüketimi gibi sağlıklı yaşam alışkanlıkları, diyabet riskini azaltmada güçlü bir rol oynayabilir.
import seaborn as sns

# Kategorik sütunlar
categorical_columns = ['HighBP', 'HighChol', 'CholCheck', 'Smoker', 'Stroke', 
                       'HeartDiseaseorAttack', 'PhysActivity', 'Fruits']

# Grafik oluşturma
plt.figure(figsize=(20, 15))  # Büyük bir alan için
for idx, column in enumerate(categorical_columns, 1):
    plt.subplot(3, 3, idx)  # 3x3 grid formatında yerleşim
    sns.countplot(data=df, x=column, hue='Diabetes_binary', palette='viridis')
    plt.title(f'Diabetes_binary - {column} Dağılımı')
    plt.xlabel(column)
    plt.ylabel('Frekans')

plt.tight_layout()
plt.show()

# BMI kategorilerini oluşturma
bins = [0, 18.5, 24.9, 29.9, 100]
labels = ['Zayıf', 'Normal', 'Aşırı Kilolu', 'Obez']
df['BMICategory'] = pd.cut(df['BMI'], bins=bins, labels=labels, right=False)
# 3.5. BMI Kategorilerine Göre Diyabet ve Diyabetsiz Oranı(Bar Grafiği):
Bu grafik, BMI kategorilerinde diyabetli ve diyabetsiz bireylerin oranlarını gösteriyor. Verilere göre:
Zayıf ve Normal BMI kategorilerinde diyabetsiz bireylerin oranı oldukça yüksekken, diyabetli bireylerin oranı düşük.
Aşırı Kilolu kategorisinde diyabetli bireylerin oranı artıyor.
Obez kategorisinde diyabetli bireylerin oranı çok daha yüksek ve diyabetsiz bireylerin oranı düşüyor.
Bu durum, obezite ve diyabet arasındaki güçlü ilişkiyi açıkça göstermekte. BMI arttıkça diyabet riski de yükseliyor.

# BMI kategorilerinin diyabet oranlarını hesaplayıp normalize etme
bmi_diabetes = df.groupby(['BMICategory', 'Diabetes_binary']).size().unstack(fill_value=0)
bmi_diabetes_normalized = bmi_diabetes.div(bmi_diabetes.sum(axis=1), axis=0)  # Normalize edilerek

# Yığılmış çubuk grafiği
bmi_diabetes_normalized.plot(kind='bar', stacked=True, color=['skyblue', 'salmon'], figsize=(8, 6))
plt.title('BMI Kategorilerine Göre Diyabetli ve Diyabetsiz Oranı')
plt.xlabel('BMI Kategorisi')
plt.ylabel('Oran')
plt.xticks(rotation=0)
plt.legend(['Diyabetsiz', 'Diyabetli'])
plt.show()

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
# Diabetes_binary değişkenini sayısal türe dönüştürüyoruz.
df['Diabetes_binary'] = pd.to_numeric(df['Diabetes_binary'], errors='coerce')

# Pivot tabloyu oluştur.
pivot_table = df.pivot_table(
    values='Diabetes_binary',  # Hangi değişkenin değerlerini hesaplamak istiyoruz
    index='HighBP',            # Satırlarda Yüksek Tansiyon
    columns='PhysActivity',    # Sütunlarda Fiziksel Aktivite
    aggfunc='mean'             # Ortalama diyabet oranını hesapla
)

# Tabloyu görselleştirme
plt.figure(figsize=(10, 6))
sns.heatmap(pivot_table, annot=True, fmt=".2f", cmap="coolwarm", cbar=True)
plt.title("HighBP ve PhysActivity Kombinasyonlarına Göre Diyabet Oranı")
plt.xlabel("PhysActivity (Fiziksel Aktivite)")
plt.ylabel("HighBP (Yüksek Tansiyon)")
plt.show()

Bu veri seti için lojistik regresyon ve destek vektör makineleri (SVM) gibi modeller önerilebilir. Lojistik regresyon, özellikle veriler arasında doğrusal ilişkiler olduğunda etkili olan basit ve yorumlanabilir bir modeldir. Diyabet gibi ikili sınıflandırma problemleri için uygun olup, modelin çıktısı kolayca yorumlanabilir. 
