---
title: "Java Static Metodu"
comments: true
excerpt: "Java Static Metodu Nedir? Hangi Durumlarda Kullanılır?"
header:
  teaser: "assets/images/equality.png"
  og_image: /assets/images/page-header-og-image.png
  overlay_image: /assets/images/unsplash-image-4.jpg
  overlay_filter: 0.5 #rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  #cta_label: "More Info"
  #cta_url: "https://unsplash.com"
categories:
  - Java
tags:
  - main method
last_modified_at: 2018-06-06T15:12:19-04:00
toc: true
toc_label: "SAYFA İÇERİĞİ"
---



**ÖNEMLİ :** Kendim için aldığım notlar. Umarım size de bir faydası olur. Kullanılan her bir makale referans olarak eklenmiştir.
{: .notice}


Birçok yerde ``static`` değiştiricisiyle karşılaşmışızdır. Hatta bu anahtar kelimeyi hem metodlar için hemde değişkenler için kullanmışızdır.

* Peki bu ne anlama geliyor?
* Hangi durumlarda static anahtar kelimesini kullanmamız gerekir?
* JVM static yöntem ve değişkenleri nasıl ve nerede saklar?

## Değişkenler


**Dinamik Değişkenler-Instance Variables (Anlık değişkenler/Statik Olmayan Alanlar):** Aynı sınıf şablonundan birdizi nesne oluşturulduğunda, bunların her biri, ayrı ayrı kendi dinamik değişkenlerine sahiptir. Teknik olarak, nesneler, kendi durumlarını "statik olmayan alanlara", yani ``statik`` anahtar kelime olmadan beyan edilen alanlara depolar. Statik olmayan alanlar da ``Instance Variables/dinamik değişkenler`` olarak bilinir. Çünkü tuttuğu değerler bir sınıfın her örneğine, bir başka değişle her nesneye özgüdür;

**Sınıf Değişkenleri-Class Variables (Statik Alanlar):** Bazen, tüm nesneler için ortak olan değişkenlere sahip olmak istersiniz. Bu statik anahtar kelimesi ile gerçekleştirilir. Beyanında ``statik`` değiştiriciye sahip olan alanlara statik alanlar(*static fields*) veya sınıf değişkenleri(*class variables*) denir. Herhangi bir nesneden ziyade sınıfla ilişkilendirilirler. Sınıfın her örneği, bellekte sabit bir konumda bulunan bir sınıf değişkenini paylaşır. Herhangi bir nesne, bir sınıf değişkeninin değerini değiştirebilir, ancak sınıf değişkenleri, sınıfın bir örneğini oluşturmadan da manipüle edilebilir. Bu, derleyiciye, sınıfın kaç kez örneklendirildiğine bakılmaksızın, bu değişkenin tam olarak varlığını sürdüren bir kopyası olduğunu söyler. Buna ek olarak ``final`` anahtar kelimesinin eklenmesi değişkenin değerinin değişmeyeceği anlamına gelir.

{% highlight java %}
static int num = 6;
{% endhighlight %}

Yukarıdaki ``static`` field örneğinde num adında bir değişken tanımlanmış ve 6 değeri bu değişkene atanmıştır. Bu static değere sahip sınıf üzerinden bu değere tekrar erişilmek istendiğinde bu değer tekrar alınır. Buna ek olarak bu değer istendiğinde değiştirilebilir. Aşağıdaki örnekte bunu daha detaylı anlatacağım. Bu ifadeye birde ``final`` anahtar kelimesi eklenirse bu ifade artık bellekte sabitlenir ve değişmez. Yani tek bir değerle ilklendirilebilir. ``final`` örneğine en güzel örnek pi sayısı olabilir. Bilindiği üzere pi sayısı sabittir ve değişmez. Kısacası ``static`` değiştiricisi, ``final`` değiştirici ile birlikte, sabitleri tanımlamak için de kullanılır.

{% highlight java %}
static final double PI = 3.141592653589793;
{% endhighlight %}

**Yerel Değişkenler - Local Variables :**
Bir nesne kendi durumunu *fields* larda nasıl sakladığı gibi, bir yöntem geçici durumunu yerel değişkenlerde saklar. Yerel bir değişkenin deklarasyon syntax'ı, bir field'ın deklarasyonuna benzerdir (örneğin, int num = 0;). Yerel olarak bir değişken belirten özel bir anahtar kelime yoktur; bu belirleme tamamen değişkenin beyan edildiği yerden yani bir yöntemin açılış ve kapanış parantezleri arasında gelir. Bu nedenle, yerel değişkenler yalnızca bildirildikleri yöntemlerle görülebilir; sınıfın geri kalanından erişilemezler.

**Parametreler - Parameters :**
Bir yönteme veya oluşturucuya(*constructor*) bilgi aktarmak için kullanılan argümanlar parametre olarak adlandırılır. Bir yöntem veya *constructor* için deklarasyon, bu yöntem veya *constructor* için bağımsız değişkenlerin sayısını ve türünü bildirir.

{% highlight java %}
public String methodA(int num) {
    // method body goes here
}
{% endhighlight %}

Yukarıdaki örnektede görüleceği üzere methodA'yı kullanabilmek için int tipinde bir sayıya ihtihacınız olduğu anlamına geliyor. Yani bu şartı sağlamadan bu metodu kullanamazsınız. Aksi halde derleme hatası ile karşılaşırsınız. Unutulmaması gereken en önemli şey, parametrelerin her zaman "alanlar(*fields*)" olarak değil "değişkenler(*variables*)" olarak sınıflandırılmasıdır.

## Static Anahtar Kelimesinin Ne Anlama Geldiğini Bir Örnekte İnceleyelim

Java ile yazılmış en basit programda bile, isteğimiz dışında `static` ifadesini kullandığımız oluyor. Bunu devamlı kullandığımız main metodundan hatırlayabiliriz. ``main`` metodu ile ilgili detaylı bilgi için şu [linkteki](/java/Java-main-method/) yazımı okuyabilirsiniz.

{% highlight java %}
public static void main(String[] args) {
        //code
    }
{% endhighlight %}


Bu ifadeyi metod tanımlarken kullandığımızda, ilgili yöntemin genel anlamıyla bulunduğu sınıfa ait olduğu ve belirli başka bir örnekte olmadığı anlamına gelir. Bunun ne anlama geldiğini daha yakından görmek için, önce ilgili sınıfın her instance'ı için bir kopya olan statik olmayan(*non-static*) alanlara bakalım. Örnek olarak, bankacılık yazılımı yazdığınızı varsayalım. Bir banka hesabı için bir sınıf oluşturmaya ve alanları(*fields*), hesap bakiyesini ve hesap numarasını bildirmeye karar verdiniz.

* non-static(instance) = her nesnede(in each object)

{% highlight java %}
class BankaHesabi{
  int hesapNum;
  double bakiye;
  ...
}
{% endhighlight %}

Her bir farklı banka hesabının kendi hesap numarası ve kendi bakiyesi olması gerekmektedir. Bankanızda, bu sınıfın üç örneğini, veri depolamada üç hesap için oluşturduysanız, böyle görünebilir. Burada her bir örneğin kendi hesap numarası ve bakiyesinin nasıl olduğunu görebiliriz. Bu alanlar statik değildir ve her nesnede oluşurlar.

| Kişiler | Hesap Numarası | Bakiye |
|:--------|:-------:|--------:|
| Görkem   | 100   | 12000   |
| Hasan   | 101   | 12500   |
| Bilal   | 102   | 0   
{: rules="groups"}

{% highlight java %}
class BankaHesabi{
  int hesapNum;
  double bakiye;
  int sonHesapNum;
}
{% endhighlight %}

Şimdi, bu yazılımı yazarken, atama yapmak için bir sonraki hesap numarasını takip etmek istediğinizi varsayalım. Böylece yeni bir hesap oluşturduğunuzda, ona hangi numarayı vereceğinizi bileceksiniz. Eklediğimiz alan yukarıda gösterildiği gibi olursa, bu sonraki hesap numarası için oluşturduğumuz örnek beklediğimiz gibi olmayabilir. Aşağıdaki kodu görüntüleyemiyorsanız lütfen [linke](https://goo.gl/x4udgN) tıklayınız.

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=public%20class%20Banka%20%7B%0A%20%20%20%20public%20static%20void%20main%28String%5B%5D%20args%29%20%7B%0A%20%20%20%20%20%20BankaHesabi%20a1%20%3D%20new%20BankaHesabi%28%29%3B%0A%20%20%20%20%20%20BankaHesabi%20a2%20%3D%20new%20BankaHesabi%28%29%3B%0A%20%20%20%20%20%20BankaHesabi%20a3%20%3D%20new%20BankaHesabi%28%29%3B%0A%20%20%20%20%7D%0A%20%20%20%20%0A%20%20%20%20static%20class%20BankaHesabi%7B%0A%20%20%20%20%20%20int%20hesapNum%3B%0A%20%20%20%20%20%20double%20bakiye%3B%0A%20%20%20%20%20%20int%20sonHesapNum%3B%0A%20%20%20%20%20%20%0A%20%20%20%20%20%20public%20BankaHesabi%28%29%7B%0A%20%20%20%20%20%20%20%20hesapNum%20%3D%20sonHesapNum%3B%0A%20%20%20%20%20%20%20%20sonHesapNum%2B%2B%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%7D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=25&heapPrimitives=nevernest&origin=opt-frontend.js&py=java&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Yukarıdaki kod bloğunda dikkat etmemiz gereken iki şey var. Birincisi yukarıda oluşturduğumuz *BankaHesabı* sınıfının önünde bulunan ``static`` anahtar kelimesidir. Burada sınıfı bu şekilde değiştirmemin sebebi hem static sınıfların kullanımını göstermek hemde static bir ifadenin bazı kurallarından bahsetmek olacaktır.

## Statik Yöntem ve Değişkenler ile Statik Olmayan Değişken ve Yöntemlerin Arasındaki Farklılıklar

Bir Java sanal makinesindeki (JVM) bir sınıfın kullanım ömrü, bir nesnenin kullanım ömrü ile birçok benzerliğe sahiptir. Bir nesne, statik olmayan değişkenlerinin değerleri ile temsil edilen bir duruma sahip olabildiği gibi, bir sınıf, sınıf değişkenlerinin değerleri ile temsil edilen bir duruma sahip olabilir. JVM, başlatma kodunu çalıştırmadan önce statik olmayan(*instance variables , non-static members*) değişkenleri varsayılan başlangıç ​​değerlerine ayarladığı gibi, aynı JVM, başlatma kodunu çalıştırmadan önce sınıf değişkenlerini varsayılan başlangıç ​​değerlerine ayarlar. Ve nesneler gibi sınıflarda, çalışan uygulama tarafından uzun süre başvurulmuyorsa, toplanan çöp durumunda olabilirler. Yine de, sınıflar ve nesneler arasında önemli farklılıklar vardır. Belki de en önemli fark, statik olmayan metodlar ile sınıf metodlarının çağrılma şeklidir: Statik olmayan yöntemler (çoğunlukla) dinamik olarak bağlıdır, ancak sınıf yöntemleri(yani static yöntemler) statik olarak bağlıdır. Üç özel durumda, statik olmayan yöntemler dinamik olarak bağlı değildir:

* statik olmayan ``private``(özel) yöntemlerinin çağrılması,
* kurucu yöntemlerinin çağrılması(constructor)
* ``super`` anahtar kelimesi ile çağrılma

Sınıflar ve nesneler arasındaki diğer bir fark, özel erişim seviyeleri tarafından verilen veri gizleme derecesidir. Bir statik olmayan değişken ``private``(özel) olarak bildirilirse, yalnızca statik olmayan yöntemleri ona erişebilir. Bu, statik olmayan verilerinin bütünlüğünü sağlamanıza ve nesnelerin iş parçacığı güvenliğini sağlamanıza olanak tanır. Programın geri kalanı, bu statik olmayan değişkenlerine doğrudan erişemez, ancak statik olmayan değişkenlerini işlemek için statik olmayan yöntemlerini gözden geçirmelidir. Bir sınıfın iyi tasarlanmış bir nesne gibi davranmasını sağlamak için, sınıf değişkenlerini ``private``(özel) yapabilir ve bunları manipüle eden sınıf yöntemlerini tanımlayabilirsiniz. Yine de, bu şekilde thread güvenliğini ve hatta veri bütünlüğünü garanti edemezsiniz, çünkü belirli bir kodun onlara ``private``(özel) sınıf değişkenlerine doğrudan erişim sağlayan özel bir ayrıcalığı vardır: statik olmayan yöntemler ve hatta statik olmayan değişkenlerin başlatıcıları(*initializers*) , doğrudan bu ``private``(özel) sınıf değişkenlerine erişebilir.

Böylece, statik alanlar ve sınıfların metotları, statik olmayan alanlara ve nesnelerin yöntemlerine pek çok açıdan benzer olsa da, bunları tasarımlarda kullanma şeklinizi etkileyecek önemli farklılıklara sahiptir.

## JVM static yöntem ve değişkenleri nasıl ve nerede saklar?

JDK 8'den önce HotSpot JVM, kalıcı Nesil(*Permanent  Generation*) olarak adlandırılan üçüncü bir nesle(*third generation*) sahipti. Statik yöntemler (aslında tüm yöntemler) ve bunun yanısıra statik değişkenler, heap alanına bitişik(*contiguous*) olan ``Permgen`` adında bir alanda tutulurdu. Kısaca bahsetmem gerekirse, bu alanda sınıf yöntem ve değişkenlerinin yanısıra, sınıfların JVM iç gösterimi(*internal representation*) ve meta verileri ve *interned strings*'ler yer almaktaydı. JDK 8 den sonra bu generation'ının yerini ``metaspace`` almıştır. ``Permgen``den farklı olarak bu alan Java Heap ile bitişik değildir(*Not contiguous*). Metaspace "native memory" den ayrılmıştır ve ``metaspace`` için maksimum alan kullanılabilir sistem hafızasıdır. Fakat bu ``MaxMetaspaceSize`` JVM seçeneği ile sınırlandırılabilir. Yalnız bu hafıza ``Permgen``de sınırlı idi.


[ref1](https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html)
[ref2](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html)
[ref3](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html)
[ref4](https://www.coursera.org/learn/java-programming-design-principles/)