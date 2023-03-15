# Structural Design Patterns (Yapısal Tasarım Desenleri)

Yazılım tasarımında kullanılan bir desenler grubudur. Bu desenler, yazılımın yapısal bileşenlerinin nasıl bir araya
getirileceği, birbirleriyle nasıl etkileşim kuracakları ve bir arada nasıl çalışacakları gibi konulara odaklanır.

Bu desenlerin amacı, yazılımın yeniden kullanılabilirliğini artırmak, bakımını kolaylaştırmak ve genel olarak yazılımın
daha iyi bir kaliteye sahip olmasını sağlamaktır. Bu desenler, bir yazılımın farklı bileşenlerini daha iyi bir şekilde
organize etmek, aralarındaki ilişkileri netleştirmek ve daha esnek bir yapı oluşturmak için kullanılabilir.

Structural Design Patterns, genellikle üç kategoriye ayrılır:

1.Class Patterns (Sınıf Desenleri): Bu desenler, sınıfların birbirleriyle nasıl ilişkili olduğunu ve nasıl bir arada
kullanılabileceğini tanımlar. Bu desenler arasında, Adapter, Decorator ve Facade desenleri yer alır.

2.Object Patterns (Nesne Desenleri): Bu desenler, nesnelerin nasıl bir araya getirileceği, birbirleriyle nasıl etkileşim
kuracakları ve bir arada nasıl çalışacakları gibi konulara odaklanır. Bu desenler arasında, Composite, Proxy ve Bridge
desenleri yer alır.

3.Structural Patterns (Yapısal Desenler): Bu desenler, nesnelerin nasıl bir araya getirileceği ve birbirleriyle nasıl
etkileşim kuracakları konusuna odaklanır. Bu desenler arasında, Flyweight ve Interpreter desenleri yer alır.

## 1.Class Patterns (Sınıf Desenleri)

[1.Adapter Pattern (Adaptör Deseni)](/structural-design-patterns/adapter-pattern): Bir arayüzü, başka bir arayüzle uyumlu hale getirmek için kullanılan bir
desendir. Bu desen, farklı arayüzleri bir arada kullanmanızı sağlar.

[2.Decorator Pattern (Dekoratör Deseni)](/structural-design-patterns/decorator-pattern): Nesnelerin davranışını dinamik olarak değiştirmek için kullanılan bir
desendir. Bu desen, nesnelerin özelliklerini ve davranışlarını çeşitli şekillerde değiştirmenizi sağlar.

[3.Facade Pattern (Yüz Deseni)](/structural-design-patterns/facade-pattern): Karmaşık bir alt sistem arayüzünü basitleştirmek için kullanılan bir desendir. Bu
desen, bir alt sistemi daha kolay kullanılabilir hale getirerek, sistemin daha esnek ve yeniden kullanılabilir olmasını
sağlar.

## 2.Object Patterns (Nesne Desenleri)

[4.Composite Pattern (Bileşik Deseni)](/structural-design-patterns/composite-pattern): Bir grup nesnenin tek bir nesne gibi davranmasını sağlamak için kullanılan
bir desendir. Bu desen, nesneleri hiyerarşik bir yapıda organize eder ve bu nesneler arasında hiyerarşik ilişkileri
belirler.

[5.Proxy Pattern (Vekil Deseni)](/structural-design-patterns/proxy-pattern): Bir nesneyi temsil etmek ve nesneyle etkileşim kurmak için kullanılan bir
desendir. Bu desen, gerçek nesnenin yerine geçerek nesne hakkında bilgi toplamanızı veya işlemler yapmanızı sağlar.

[6.Bridge Pattern (Köprü Deseni)](/structural-design-patterns/bridge-pattern): Soyutlama katmanını, gerçek uygulama katmanından ayırmak için kullanılan bir
desendir. Bu desen, nesne yönelimli programlama (OOP) prensiplerine uygun olarak, karmaşık bir sistemdeki nesneler
arasındaki bağımlılıkları azaltır.

## 3.Structural Patterns

[7.Flyweight Pattern (Hafif Nesne Deseni)](/structural-design-patterns/proxy-pattern): Nesnelerin bellek kullanımını azaltmak için kullanılan bir desendir. Bu
desen, benzer nesnelerin bellekte yalnızca bir kez oluşturulmasını sağlar ve daha sonra bu nesneleri kullanarak farklı
amaçlar için kullanılabilir.
