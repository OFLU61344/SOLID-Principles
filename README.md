# Özet

### Solid Prensibi nedir?
SOLID prensipleri, yazılım geliştirme ve özellikle nesne yönelimli programlama (OOP) alanında önemli bir rol oynar.
SOLID prensipleri, yazılımın esnek, sürdürülebilir, okunabilir ve yeniden kullanılabilir olmasını sağlamak için geliştirilen bir dizi tasarım prensibidir.

### Solid Prensibi neden kullanılır
Solid Yazılım Prensipleri, Robert C. Martin tarafından geliştirilen ve yazılım geliştirme sürecinde kullanılması önerilen prensiplerdir ve yazılımın kalitesini ve bakımını kolaylaştırmak için tasarlanmıştır.
Bu prensipler yazılım geliştirme sürecinde kullanılan temel ilkelerdir.

### Solid Prensibi ne işe yarar?
Martin yazısında başarılı bir yazılım ürününün değişen ve gelişen olduğunu belirtmiştir. Ancak değiştikçe karmaşıklaşan yazılım ürünü kabul gören bir durum değildir. 
SOLID ilkelerinin genel amacı, mühendislerin yazılımın bir alanını diğerlerini etkilemeden değiştirmelerini sağlamak için bağımlılıkları azaltmaktır.


**_dünya üzerinde standart kabul edilen 5 temel prensibi bilmemiz gerekiyor._**


1. (S)ingle Responsibility Principle

2. (O)pen/Closed Principle

3. (L)iskov ‘s Substitution Principle

4. (I)nterface Segregation Principle

5. (D)ependency Inversion Principle

Solid'e ek olarak Kiss, Yangi, Dry, Reuse Release Equivalence, Common Closure prensipleri de bulunmaktadır.

Bu prensiplerin kısaca neler olduğundan bahsedelim:

**1.Single Responsibility Principle**

Kaliteli kod yazmak için ne kadar özen göstersek de, çalışma hayatında önümüze sadece kendi geliştirmiş olduğumuz projeler gelmiyor. Tek bir class içerisinde yazılmış binlerce satır kodu okuyup anlamaya çalışmak (belki sadece küçük bir revizyon için) zorunda kalabiliyoruz. Böyle durumlarda ekip arkadaşlarınızla aranızda şöyle konuşmalar geçtiği olur:

+ Projede biraz optimizasyon yapsak mı?  
– Çalışıyorsa hiç dokunmayalım.

Projenin içindeki yapılar diğer yapılara o kadar bağımlıdırki; küçük bir değişikliğin neleri etkileyeceğini kestirmeniz çok zor bir hal alır, böyle projeler çöp proje olarak görülür. içerisindeki class'ları ve methodları alıp başka bir projede kullanamazsınız.

Tek sorumluluk prensibine uyarsanız binlerce satırlık class'larınız ve methodlarınız olmaz. Her bir class'ın her bir methodun sadece tek yaptığı iş vardır böylece bir değişiklik yapmak için nedeniniz olmuş olur.

**2.Open/Closed Principle**

Açık kapalı prensibi, yazılım geliştirirken kullandığımız varlıkların (class, method vs.) gelişime açık, kodların ise değişime kapalı olması ilkesidir. Örneğin; bir loglama altyapısı oluşturduğunuzu düşünün, Veritabanına ve XML’e kayıt tutuyorsunuz. Daha sonradan Eventloglara da log tutma ihtiyacı hissettiğinizde, sadece Eventloglara kayıt tutan kodları yazmanız yetecek, kodunuzda hiçbir değişiklik yapmadan bu yapı sisteme entegre olacak. Bunun için uygulayacağımız çözüm şu şekilde olabilir:

![image](https://github.com/OFLU61344/SOLID-Principles/assets/118263276/60c93667-90a8-4cec-b68d-23d12196908a)

