
### Solid prensibi nedir?

Nesne yönelimli programala ve yazılım geliştirme'de SOLID prensibleri önemli rol oynar 
aynı zamanda SOLID prensibleri, bir yazılımın yeniden kullanılabilrmesi sürdürülebilmesi ve okunabilir olmasını sağlar


### Solid Prensibi neden kullanılır?

Solid yazılım prensibleri Robert C. Martin tarafından geliştirilmiştir ve yazılımın bakımını ve tasarımını geliştirmek için tasarlanmıştır.


### SOLID'in 5 temel prensibi

(S)ingle Responsibility Principle  

(O)pen/Closed Principle  

(L)iskov ‘s Substitution Principle  

(I)nterface Segregation Principle  

(D)ependency Inversion Principle 

Bu prensiplerin kısaca neler olduğundan bahsedelim:

1. Single Responsibility Principle  

Güzel bir kod yazmak için ne kadar özen gösterilsede, önümüze her zaman kendi geliştirmiş olduğumuz projeşer çıkmıyor
Tek bir class'a yazılmış yüzlerce hatta binlerce satır kodu okuyup anlamaya çalışmak zorunda kalabiliyoruz

Böyle durumlarda arkadaşlarınızla şöyle konuşmalar geçer

Projede biraz optimizasyon yapsak mı?  
– Çalışıyorsa hiç dokunmayalım.  
Projenin içindeki yapılar diğer yapılara o kadar bağımlıdırki; küçük bir değişikliğin neleri etkileyeceğini  
kestirmeniz çok zor bir hal alır, böyle projeler çöp proje olarak görülür.

Tek sorumluluk prensibine uyarsanız binlerce satırlık class'larınız ve methodlarınız olmaz. Her bir class'ın  
her bir methodun sadece tek yaptığı iş vardır böylece bir değişiklik yapmak için nedeniniz olmuş olur.

2. Open/Closed Principle

Yazılım geliştirirken kullandığımız varlıkların kodların değişime kapalı gelişimlerin ise açık olması ilkesidir.
Örnek olarak: bir loglama altyapısı oluşturduğunuzu düşününveritabanında XML kayıt tutuyosunuz daha sonra event loglara log tutmaya ihtiyaç duyduğunuzda sadece eventloglara kayıt tutan kodları yazmanız yeterli olacak kodda değişiklik yapmadan bu yapı sisteme entegre olur. 


3. Liskov Substitution

Herhangi bir değişiklik yapmadan kolamanızda alt sınıfları, türedikleri üst sınıfların yerine kullanabiliriz.
Türeyen sınıf ana sınıfın tüm özelliklerini ve metotlarını aynı işlebi gösterecek şekilde kulanabilme ve kendine ait yeni özellikler barındırabilir.

4. Interface Segregation

bu prensib bize sorumlulukları tek bir arayüzünde tutmaktansa özelleştirilmiş birden fazla arayüz oluşturmamızı söyler .

5.Dependency Inversion  

Bir sınıfın, metodun ya da özelliğin, onu kullanan diğer sınıara karşı olan bağımlılığı en aza  
indirgenmelidir.  Yüksek seviye sınıarda bir davranış değiştiğinde, alt seviye davranışların bu değişime  
uyum sağlaması gerekir. Üst Seviye Sınıar -> Soyutlama Katmanı -> Düşük Seviye Sınıarı Peki, bütün  
bu sorunlardan kurtulmanın yolu nedir ? Cevap: Dependency Inversion, yani üst sınıar, alt seviyeli  
sınıara bağlı olmamalı, çözüm ise her ikisi de soyut kavramlar üzerinden yönetilebilmelidir.  Yüksek  
seviye ve düşük seviye sınıar arasında bir soyutlama katmanı oluşturabiliriz.  
