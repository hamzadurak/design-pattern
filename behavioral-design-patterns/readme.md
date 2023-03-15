# Behavioral Design Patterns (Davranışsal Tasarım Desenleri)

Yazılım geliştirme sürecindeki belirli davranışların düzenlenmesi için kullanılan tekrar eden çözümlerdir. Bu tasarım
desenleri, yazılım uygulamalarında oluşturulan nesnelerin ve sınıfların birbirleriyle etkileşimini yönetmek için
kullanılır.

Bu desenler, yazılım geliştiricilerin programların karmaşıklığını azaltmalarına ve daha organize bir yapı
oluşturmalarına yardımcı olur. Ayrıca kodun tekrar kullanılabilirliğini ve bakımını kolaylaştırır.

Behavioral Design Patterns, farklı tiplerdeki davranışları ele alır. Örneğin, observer pattern, bir nesnenin durumundaki
değişiklikleri takip etmek için kullanılırken, iterator pattern, bir koleksiyon içindeki elemanlara erişmek için
kullanılır. Diğer örnekler arasında, command pattern, bir işlemin gerçekleştirilmesini başlatmak ve işlemi sırayla
yürütmek için kullanılırken, state pattern, bir nesnenin durumunu değiştirmek için kullanılır.

Behavioral Design Patterns, yazılım geliştirme sürecinde sıkça kullanılan bir dizi desendir ve geliştiricilerin yazılım
uygulamalarının daha sürdürülebilir, anlaşılır ve bakımı kolay hale gelmesine yardımcı olur.

[1.Chain of Responsibility Pattern (Sorumluluk Zinciri Deseni)](behavioral-design-patterns/chain-of-responsibility-attern):
Belirli bir işlemi gerçekleştirmek için birden
fazla nesnenin birbirine bağlandığı bir desendir. Bu desen, bir işlemi gerçekleştirmek için nesneler arasında bir
hiyerarşi oluşturur.

[2.Command Pattern (Komut Deseni)](behavioral-design-patterns/command-pattern):
Bir işlemin gerçekleştirilmesini başlatmak ve işlemi sırayla yürütmek için
kullanılır. Bu desen, kullanıcı arayüzlerindeki düğmeler veya menüler gibi komutları temsil etmek için sıklıkla
kullanılır.

[3.Interpreter Pattern (Tercüman Deseni)](behavioral-design-patterns/interpreter-pattern):
Belirli bir dil veya sözdizimi ile ifade edilen komutları yorumlamak
için kullanılır. Bu desen, özel bir dili veya ifadeyi yürütmek için bir yorumlayıcı kullanılması gerektiğinde
kullanılır.

[4.Iterator Pattern (Yineleyici Deseni)](behavioral-design-patterns/iterator-pattern):
Bir koleksiyon içindeki elemanlara erişmek için kullanılır. Bu desen,
farklı veri yapılarının üzerinde gezinmeyi kolaylaştırır.

[5.Mediator Pattern (Aracı Deseni)](behavioral-design-patterns/mediator-pattern):
Farklı nesneler arasındaki iletişimi yönetmek için kullanılır. Bu desen,
nesneler arasındaki bağımlılıkları azaltarak kodun daha esnek ve sürdürülebilir olmasını sağlar.

[6.Memento Pattern (Anımsatıcı Deseni)](behavioral-design-patterns/memento-pattern):
Bir nesnenin geçerli durumunu kaydedip geri yüklemek için kullanılır. Bu
desen, bir işlemin geri alınması veya tekrarlanması gerektiğinde kullanılır.

[7.Observer Pattern (Gözlemci Deseni)](behavioral-design-patterns/observer-pattern):
Bir nesnenin durumundaki değişiklikleri takip eden ve diğer nesnelerin bu
değişikliklerden etkilendiği bir desendir.

[8.State Pattern (Durum Deseni)](behavioral-design-patterns/state-pattern):
Bir nesnenin durumunu değiştirmek için kullanılır. Bu desen, nesnenin durumuna
göre farklı davranışlar sergilemesine olanak tanır.

[9.Strategy Pattern (Strateji Deseni)](behavioral-design-patterns/strategy-pattern):
Farklı algoritmaların veya stratejilerin kullanılabilmesine izin veren bir
desendir. Bu desen, bir işlemin birden fazla farklı şekilde gerçekleştirilebileceği durumlarda kullanılır.

[10.Template Method Pattern (Şablon Yöntemi Deseni)](behavioral-design-patterns/template-method-pattern):
Belirli bir işlemin çeşitli aşamalarını tanımlayan ve bu
aşamaların alt sınıflar tarafından özelleştirilebileceği bir desendir.

[11.Visitor Pattern (Ziyaretçi Deseni)](behavioral-design-patterns/visitor-pattern):
Farklı nesne tiplerini ziyaret eden ve her biri için farklı davranışlar
sergileyen bir desendir. Bu desen, nesneler arasında gezinirken farklı işlemler yapmak için kullanılır.