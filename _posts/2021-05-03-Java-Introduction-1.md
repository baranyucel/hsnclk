---
title: "Java'ya Giriş 1.1"
comments: true
excerpt: "Bu bölümde, Nesne Yönelimli Programlama, Java yazım jargonu ve Java'nın nasıl çalıştığından bahsedeceğim."
header:
  teaser: "assets/images/equality.png"
  og_image: /assets/images/page-header-og-image.png
  overlay_image: /assets/images/unsplash-image-56.jpg
  overlay_filter: 0.5 #rgba(255, 0, 0, 0.5)
  caption: "Photo by [Quinton Coetzee](https://unsplash.com/photos/AOaDfdSly3g) on Unsplash"
  #cta_label: "More Info"
  #cta_url: "https://unsplash.com"
categories:
  - java-kalitim-polimorfizm
tags:
  - polimorfizm
  - dynamic/late binding(dinamik/geç bağlanma)
  - this keyword
last_modified_at: 2020-02-19T15:12:19-04:00
toc: true
toc_label: "SAYFA İÇERİĞİ"
author: Baran Yücel
---



**ÖNEMLİ :** Kendim için aldığım notlar. Umarım size de bir faydası olur. Kullanılan her bir makale referans olarak eklenmiştir.
{: .notice}

## Nesne Yönelimli Programlama

1960'lı yılların sonuna doğru ortaya çıkan bu yaklaşım, o dönemin yazılım dünyasında beliren bir bunalımın sonucudur. Yazılımların karmaşıklığı ve boyutları sürekli artıyor, ancak belli bir nitelik düzeyi korumak için gereken bakımın maliyeti zaman ve çaba olarak daha da hızlı artıyordu.
NYP'yi bu soruna karşı bir çözüm haline getiren başlıca özelliği, yazılımda modularity i benimsemesidir.  Programlar artık ayrı dosyalar halinde düzenlenebilir hale gelmiştir.


Kısaca nesne yönelimli programlama 4 temel özelliği kendisinde bulundurur.

1. **Soyutlama (Abstraction):** Bir sınıfın özelliklerinin ve davranışlarının tanımlanmasına denir. Örneğin: Bir kişinin adı, soyadı, yaşı, boyu, kilosu, saç rengi gibi özellikleridir. Kişinin yetenekleri davranışları içerisinde yer alır ve metotlar ile saklanır.

```sh
public class Animal {
    public String age;
    public String name;
    void kokuAl(){}
    void yonBul(){}
}
```

2. **Kapsülleme (Encapsulation):** Davranış ve özellikler sınıfta soyutlanır ve saklanır. Kapsülleme ile hangi özellik ve davranışın dışarıdan kullanılacağını belirleyebiliriz. Örneğin: Kişinin bizi ilgilendirmeyen kısımlarını private ederek yani saklayarak gizleyebiliriz. Bu olaya kapsülleme adı verilir.
3. **Miras Alma:** Alt ve üst sınıfın ortak özelliklerinden alabilme sistemine Miras Alma denir. Örneğin; Bir nesneni diğer bir nesne ile ortak özelliklerindeki verileri alabilir.
4. **Çok Biçimlilik:** Alt Sınıf ve Üst Sınıfın özelliklerinden farklı şekilde davranışlar göstermesine Çok Biçimlilik denir. Örneğin; Bir nesnenin diğer bir nesneyle ortak özellikleri olmasına rağmen farklı özelliklerininde tanımlanabilmesine denir.
Java, C ++ ve C # gibi popüler modern dillerin tümü nesneler temel alınarak oluşturulmuştur.


## Örnek

<script src="https://gist.github.com/cortix/f98aeec7543ade829c8a9ad4f1611f32.js"></script>

<script src="https://gist.github.com/cortix/0ff89c934e5886b8fdab890b98a31c8e.js"></script>


``p`` bir Person referansı olsa da, başvurduğu asıl nesne çalışma zamanında Student sınıfına ait olacaktır. Yani ``p.status(1)`` çağrısını yaptığımızda status metodunu çağırmak için Java'nın ilk bakacağı yer Student sınıfı olacaktır. Fakat Student sınıfında böyle bir metodun olmadığını görüyoruz. Fakat Student sınıfı Person sınıfını miras aldığı için, Java bir de Person sınıfına bakacaktır. Person sınıfında status metodunu bulduk. Kaldığımız yerden devam edebiliriz.


status metodunun içine girdiğimizde karşımıza bir if-else ifadesi çıkmaktadır. Burada ``this.isReady(num)`` ifadesi ile karşılaşıyoruz. Peki Person sınıfı içinde ``this`` anahtar kelimesi ne anlama geliyor? ``this`` anahtar kelimesi ile çağırmaya çalıştığımız metot, Person sınıfının içindeki ``isReady`` metodu mu? yoksa Student sınıfı içinde bulunan ``isReady`` metodu mu? Kodu çözümlerken şu anda Person sınıfında olsak da, ``this`` anahtar kelimes çalışma zamanında Student nesnesini temsil etmektedir. Yani ``this`` dinamik olarak Student nesnesine bağlanır. Bu sebepten ötürü tekrardan Student sınıfına dönmemiz gerekecektir. Burada isReady metodu **1>0** dan büyük olduğu için ``true`` bir yanıt döndürecektir. Sonuç ``true`` döndüğü için Person sınıfı içindeki if bloğu içine girecek ve aşağıdaki sonucu alacağız.

```
I am ready: Hasan
```

## this Anahtar kelimesi

Yukarıdaki örnekten devam ederek ``this`` hakkında birkaç bilgi paylaşmak istiyorum. ``System.out.println("I am ready: "+this);`` Burada ``this`` anahtar kelimesinin neden ``toString`` metoduna karşılık geldiğini ve çıktı olarak "Hasan" yazdırdığını sorabilirsiniz. ``this`` anahtar kelimesi bazı durumlarda ``this.isReady`` de olduğu gibi ilgili nesnenin metodunu, bazı durumlarda mevcut nesnenin üye değişkenlerini, bazen de mevcut nesnenin kurucusunu çağırırken kullanırız. Nasıl kullanılırsa kullanılsın her durumda çalışma zamanındaki gerçek nesneyi temsil ettiğini unutmayın.

Peki burada neden sadece ``this`` anahtar kelimesini kullandık. Aslında kullanmasaydık ne olacaktı sorusunu sorsak, kullandığımızda ne olacağını daha net anlayabiliriz. ``this`` anahtar kelimesinin mevcut nesneyi işaret ettiğini söylemiştik. Özünde biz ``this`` anahtar kelimesini yalın olarak kullandığımızda objenin kendisini işaret ederiz. Şayet bunu ekrana yazdırmak istediğimizde şu şekilde bir çıktı ile karşılaşabiliriz.

```
Student@11028347
```
Aslında javanın neden bu şekilde bir isimlendirme yaptığından şu makalelerde bahsetmiştim. [1](/java-hafiza-yonetimi/Java-memory-models-objects1/), [2](/java-hafiza-yonetimi/Java-memory-models-objects/)

Kısaca özet geçecek olursam, java, doğrudan nesneyi yazdırmak istediğimizde Object sınıfının ``toString`` metodunu çağırır.

<script src="https://gist.github.com/cortix/23b3359e32a428f861f322d6167e3bd0.js"></script>

metodun içeriğine baktığımızda döndürülen ifade **sınıfın ismi + @ simgesi + integerdan oluşan bir takım sayı** şeklindedir. Yalnız biz Person sınıfında bu metodu aşağıdaki şekilde geçersiz kıldığımız(override) için;

```java
public String toString(){
    return name;
}
```

``name`` üye değişkenini döndürecektir.


## Referanslar
* [https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#toString()](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#toString())
* [https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html](https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html)
* [https://www.coursera.org/learn/object-oriented-java?specialization=java-object-oriented](https://www.coursera.org/learn/object-oriented-java?specialization=java-object-oriented)
