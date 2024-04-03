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


## Diğer bilgiler

### Solid prensipleri 5 madde altında toplanır.

**S**  – _Single Responsibility Principle (SRP)_: Nesnenin sadece bir sorumluluğu olmalıdır.  
**O**  –  _Open/Closed Principle (OCP)_: Nesne genişlemeye açık, değişikliklere kapalı olmalıdır.  
**L**  –  _Liskov ‘s Substitution Principle (LSP)_: Programdaki nesnelerin, programın çalışmasında sorun yaratmadan kendine alt örnekleri ile değiştirilebilir olmasıdır. Bu aynı zamanda sözleşmeyle tasarım (Design by Contract ) olarak bilinir.  
**I**  –  _Interface Segregation Principle (ISP)_: Nesnelerin ihtiyaç duymadıkları Interface’lerinden mümkün olduğunca ayrıştırılmasıdır.  
**D**  –  _Dependency Inversion Principle (DIP)_: Yüksek seviyeli sınıflar, düşük seviyeli sınıflara bağlı olmamalı, her ikisi de soyut kavramlara bağlı olmalıdır.

### Şimdi hepsiyle ilgili basit birer örnek yaparak daha somut şekilde ele almaya çalışalım.

 **1. Single Responsibility Principle (SRP):**  Nesnelerin yalnızca tek bir sorumluluğu olmalıdır. Bunun nedeni geliştirmenin daha modüler olması, değişikliğin daha kolay yapılabilmesi, daha yönetilebilir bir kod ortaya çıkarmasıdır. Mümkün olduğunca isterler analiz edilerek parçalara ayrılmalı ve çözüm için yalnızca bir sorumluluğu olan fonksiyonlar kullanılmalıdır. Kısaca tek bir metot altında yüzlerce işlem ve yüzlerce model manipülasyonu olmamalıdır. Bu prensibi uygulamaya çalışmak hem gereksinimlerin iyi analiz edilmesini hem de ileride yapılacak geliştirmeler de ilgili nesneyi bulmayı ve değişiklik yapmayı kolaylaştıracaktır.

Örneğin, iki sayıyı toplamak isteyelim fakat önce sayılar 0 dan küçük mü diye bakalım, herhangi biri küçükse hata , değilse işlemin sonucunu döndürelim.

Önce .net core projemizi oluşturalım. Ben bunun için cmd / komut satırı kullanacağım.

``
dotnet new console -o PrensipIsmi (- o parametresi name icin verilir.)
``

Dosyalarımızı oluşturalım ve daha sonra içlerine girerek 5 madde için de yukarıda ki kalıp ile projemizi açalım. Ben projemi vsCode ile açacağım.
````
mkdir SolidPrenciples
cd SolidPrenciples
dotnet new console -o SingleResponsibility
dotnet new console -o Open-Closed
dotnet new console -o LiskovsSubstitution
dotnet new console -o InterfaceSegregation
dotnet new console -o DependencyInversion

cd SingleResponsibility -- Diğer maddeler icinde bu iki adim uygulanacaktir. Cd komutu ile klasörlerin icerisine girebiliriz.
dotnet new console -o SingleResponsibility

code . (Visual Studio Code icerisinde acmak icin gereken komut)
````
Yukarıda ki komutları genel bir bilgi olması için yazdım. Bundan sonra ilgili sınıfları paylaşacağım. Classlar bölünebilir fakat ben örneğin daha iyi anlaşılması için ilgili classları aynı dosyada kullanacağım. Örnek üstünden devam edelim
````
public class OldStyleClass
{
    public int Sum(int a ,int b)
    {
        if (!IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a+b;
    }

    private bool IsValid(int a ,int b)
    {
        return a<0 || b<0 
               ? false
               :true;
    }
}
````
Birde bunun prensip uygulanmış haline bakalım.
````
public class ClassWithPrenciple
{
    const string ErrorMessage="Input is not valid";
    ValidationClass validation=new ValidationClass();
    public int Sum(int a ,int b)
    {
        if (!validation.IsValid(a,b))
            throw new Exception(ErrorMessage);
        
        return a+b;
    }

}
````

````
public class ValidationClass{
    public bool IsValid(int a ,int b)
    {
        return a<0 || b<0 
               ? false
               :true;
    }
}
````
Şimdi şöyle düşünelim validasyon kuralımızın mantığı değişti. Prensip uygulanmamış sınıfımızda bunun için ana class da değişiklik yapmamız gerekirken prensip uygulanmış class da yalnızca ilgili metodu değiştirmemiz yeterli olacak.

**2. Open/Closed Principle (OCP):**  Klasik cümle ile nesneler genişlemeye açık değişikliğe kapalı olmalıdır. Bu cümle ilk okunduğunda tam olarak anlaşılamayabilir. Bu yüzden somut bir örnek üzerinden daha anlaşılır bir şekilde anlatmaya çalışacağım. Örneğimiz de toplama yanında çıkarma da yapmak istediğimizi düşünelim. Bunun için eski tarzda koda dokunarak değişiklikler yapmamız, birden fazla yere dokunmamız gerekecek. Buna ek olarak çarpma işlemi yapmak istediğimizde de yine aynı işlemleri gerçekleştirmek zorunda kalacağız.

````
public enum OperationType{
    Sum,
    Substract
}
public class OldStyleClass
{
    private Sum sum=new Sum();
    private Substract substract=new Substract();

    public int Operation(int a, int b, OperationType operation){
        switch (operation)
        {
            case OperationType.Sum:
            return sum.SumNumbers(a,b);
            //break;
            case OperationType.Substract:
            return substract.SubstractNumbers(a,b);

            default:
            throw new Exception("Invalid Operation");
            
        }
    }
}

public class Sum {
    public int SumNumbers(int a ,int b)
    {
        if (!IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a+b;
    }

    private bool IsValid(int a ,int b)
    {
        return a<0 || b<0 
               ? false
               :true;
    }
} 
public class Substract {
    public int SubstractNumbers(int a ,int b)
    {
        if (!IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a-b;
    }

    private bool IsValid(int a ,int b)
    {
        //Your Logic
        return a<0 || b<0 
               ? false
               :true;
    }
} 
````
Gördüğünüz gibi yeni bir işlem için bile ne kadar çok noktaya dokunup, değişiklik ve ekleme yaptık.Yeni bir işlemler geldiğinde bunları tekrarlamamız gerekecek. Şimdi bu işlemleri open-closed prensipine uygun hale getirelim.
````
public interface IOperation
{
     int Operation(ValidationClass validation,int a,int b);     
}
public class SumNumbers : IOperation
{
    public int Operation(ValidationClass validation,int a,int b)
    {
            if (!validation.IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a+b;
    }
}
public class SubstractNumbers : IOperation
{
    public int Operation(ValidationClass validation,int a,int b)
    {
            if (!validation.IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a-b;
    }
}

public class ClassWithPrensicple
{
    private IOperation operation;
    private ValidationClass validation=new ValidationClass();
    public ClassWithPrensicple(IOperation _operation)
    {
      operation=_operation;
    }

    public int PrenciplesAreGood(int a,int b){
        return  operation.Operation(validation,a,b);
    }
}
````

````
public interface IOperation
{
     int Operation(ValidationClass validation,int a,int b);     
}
public class SumNumbers : IOperation
{
    public int Operation(ValidationClass validation,int a,int b)
    {
            if (!validation.IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a+b;
    }
}
public class SubstractNumbers : IOperation
{
    public int Operation(ValidationClass validation,int a,int b)
    {
            if (!validation.IsValid(a,b))
            throw new Exception("Input is not valid");
        
        return a-b;
    }
}

public class ClassWithPrensicple
{
    private IOperation operation;
    private ValidationClass validation=new ValidationClass();
    public ClassWithPrensicple(IOperation _operation)
    {
      operation=_operation;
    }

    public int PrenciplesAreGood(int a,int b){
        return  operation.Operation(validation,a,b);
    }
}
````

Kodumuzu daha genişlemeye açık bir hale getirdik. Yeni bir işlem daha gelse bile yapmamız gereken sadece IOperation interface sinden türeterek Operation methodunu işleme göre düzenlemek.

**3.Liskov ‘s Substitution Principle (LSP):** Alt sınıflar türetildikleri sınıfların nesneleriyle yer değiştirdiğinde aynı davranışı sergilemeli yani türetildikleri sınıfın tüm özelliklerini kullanmalıdır. Bu prensip bize base classlarda gereksiz kodların olmaması gerektiğini söyler. Şimdi Player dan türeyen iki sınıfımız olsun ve bu sınıfta KickTheBall ve KeepTheBall adında iki metod olsun. Burada prensip uygulanmaz ise base class da gereksiz kodlar bulunacak.  
Bu yüzden bu gibi durumlarda base class da türeyen sınıfların hepsinin kullanacağı özellikleri tutmalı, spesifik durumlar için ise ayrı class yada interface üzeriden ilerlemeliyiz.

````
public abstract class Player{
    public virtual string KickTheBall(){
        return "kick the ball";
    }
    public virtual string KeepTheBall(){
        return "keep the ball";
    }
}
public class Striker : Player
{
    public override string KickTheBall()
    {
        return "Striker kicked the ball";
    }
}
public class Goalkeeper : Player
{
    public override string KeepTheBall()
    {
         return "Goalkeeper kept the ball";
    }

    public override string KickTheBall()
    {
        return "Goalkeeper kicked the ball";
    }
}
````
Gördüğünüz gibi burada striker aslında ihtiyaç duymadığı KeepTheBall metodunu barındırmakta ve normal şartlarda bu fonksiyonu kullanamayacak, bu fonksiyonda exception fırlatması gerekecektir. Yani aslında gereksiz bir kod kalabalığı ve kod yönetimi açısından ek bir efor oluşacaktır, bunun nedeni base classda aslında gereksiz bir metod bulunmasıdır. Aşağıdaki gibi bir yapı kurulması daha sağlıklı olacaktır.
````
public abstract class Player{
    public virtual string KickTheBall(){
        return "kick the ball";
    }
}
public interface IKeepTheBall{
      string Keep();
}
public class Striker : Player
{
    public override string KickTheBall()
    {
        return "Striker kicked the ball";
    }
}
public class Goalkeeper : Player,IKeepTheBall
{
    public override string KickTheBall()
    {
        return "Goalkeeper kicked the ball";
    }
    public string Keep()
    {
       return "Goalkeeper kept the ball";
    }
}
````
Yani sözün özü base class da ortak olarak kullanılmayacak özellikleri barındırmayın.

**4. Interface Segregation Principle (ISP):**  Nesnelerin ihtiyaç duymadıkları interface lerinden münkün olduğunca ayrıştırılmasıdır. Eğer interfacelerin tüm metodları implemente edilen sınıfta kullanılmıyorsa interfaceleri bölmek gerekir. Şimdi ISuperHero adında bir interfacemiz olduğunu düşünelim. Bu interface de Costume,Power,BatMobile ve Fly adında 4 metod bulunsun ve süper kahraman özelliği olan iki karakter Batman ve Süperman bu yetenekleri alsın.
````
public interface ISuperHero
{
    string Costume();
    string Power();
    string BatMobile();
    string Fly();
}
public class Batman : ISuperHero
{
    public string BatMobile()
    {
        return "I can use BatMobile";
    }
    public string Power()
    {
        return "My power is my money :D ";
    }
    public string Costume()
    {
        return "My Costume is dark";
    }
    public string Fly()
    {
        return "I can not fly";
    }
}
public class SuperMan : ISuperHero
{
    public string BatMobile()
    {
       return "I can not use BatMobile";
    }
    public string Power()
    {
        return "I am from Krypton. Is that enough? ";
    }

    public string Costume()
    {
       return "My Costume is red and blue";
    }

    public string Fly()
    {
        return "I can fly";
    }
}
````
Fakat burada bir problem var. İkisi de kostüm kullanır,güçleri vardır ama batman uçamaz ve süperman batmobile kullanmaz. O yüzden interfaceler ayrıştırılarak aşağıdaki hale getirilir. Böylece interfacelerde gereksiz özellikler barındırılmamış olur.
````
public interface ISuperHero
{
    string Costume();
    string Power();
}
public interface IBatMobile{
     string UseBatMobile();
}
public interface IFly{
     string FlyToSomeWhere();
}
public class Batman : ISuperHero,IBatMobile
{
    public string UseBatMobile()
    {
        return "I can use BatMobile";
    }
    public string Power()
    {
        return "My power is my money :D ";
    }
    public string Costume()
    {
        return "My Costume is dark";
    }
}
public class SuperMan : ISuperHero,IFly
{
    public string Costume()
    {
       return "My Costume is red and blue";
    }
  public string Power()
    {
        return "I am from Krypton. Is that enough? ";
    }
    public string FlyToSomeWhere()
    {
        return "I can fly";
    }
}
````

**5. Dependency Inversion Principle (DIP):** Yüksek seviyeli sınıflar, düşük seviyeli sınıflara bağlı olmamalı, her ikisi de soyut kavramlara bağlı olmalıdır. Örneğin validasyon yapan bir sınıfımız olsun. Toplama için sayılardan herhangi biri için 0 dan küçük mü? Bölme için ise herhangi biri 0 mı diye kontrol etsin?  
Burada aşağıdaki gibi bir yapı oluşturulursa, düşük seviyeli sınıflara bağımlı bir yapı oluşturulmuş olur. Yani aşağıda ki validation classı bi anlamda SumValidation ve DivideValidation sınıflarına bağımlı haldedir.

````
public enum OperationTypes{
    Sum,
    Divide
}

public class SumValidation{
    public bool IsValid(int a,int b){
        return a<0||b<0
               ? true
               :false;
    }
}
public class DivideValidation{
    public bool IsValid(int a,int b){
        return a==0||b==0
               ? true
               :false;
    }
}

public class Validation{
    SumValidation sumValidation=new SumValidation();
    DivideValidation divideValidation=new DivideValidation();
    public bool IsValid(OperationTypes operationType,int a,int b)
    {
        switch (operationType)
        {
            case OperationTypes.Sum:
            return sumValidation.IsValid(a,b);
            
            case OperationTypes.Divide:
            return divideValidation.IsValid(a,b);
            
            default:
            throw new Exception("Invalid Operation type");
        }
    }
}
````
Peki aşağıda ki gibi bir yapı kursak ve validation sınıfımız düşük seviyeli sınıflara bağımlı olmasa daha güzel olmaz mı?

````
public interface IOperationValidation{
      bool IsValid(int a,int b);
}
public class SumValidation:IOperationValidation
{
    public bool IsValid(int a,int b){
        return a<0||b<0
               ? true
               :false;
    }
}
public class DivideValidation:IOperationValidation
{
    public bool IsValid(int a,int b){
        return a==0||b==0
               ? true
               :false;
    }
}

public class Validation
{
    private IOperationValidation operationValidation ;
    public Validation(IOperationValidation _operationValidation)
    {
        operationValidation=_operationValidation;
    }
    public bool IsValid(int a,int b)
    {
        return operationValidation.IsValid(a,b);
    }
}
````

Evet arkadaşlar, yazılım ile ilgilenenlerin bilmesi gerektiğini düşündüğüm temel konulardan birini detaylandırdık. Umarım faydalı olmuştur.
