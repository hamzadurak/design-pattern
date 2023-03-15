# 11.Visitor Pattern (Ziyaretçi Deseni)

Nesne yönelimli programlama (OOP) için bir tasarım desenidir. Bu desen, bir nesne hiyerarşisi içindeki nesnelerin işlenmesini kolaylaştırmak için kullanılır ve her bir nesne, işlemek için ayrı bir ziyaretçi nesnesi tarafından ziyaret edilir. Bu sayede, nesne hiyerarşisindeki farklı türlerdeki nesneler farklı işlevleri yerine getirebilir ve işlevleri esnek bir şekilde değiştirmek mümkün hale gelir.

Bu desenin temelinde, iki ana nesne vardır: ziyaretçi ve nesne. Ziyaretçi nesnesi, her bir nesneyi ziyaret eder ve onun üzerinde işlemler yapar. Nesne nesnesi, ziyaret edilir ve ziyaretçi nesnesine kendi durumunu verir.

Aşağıdaki örnek, bir Shape (Şekil) sınıf hiyerarşisindeki nesneleri işlemek için bir ziyaretçi sınıfı tanımlar:

## Kod

```php
// Shape nesne hiyerarşisindeki nesneleri işlemek için bir ziyaretçi sınıfı
interface ShapeVisitor {
  function visitCircle(Circle $circle);
  function visitRectangle(Rectangle $rectangle);
}

// Shape nesne hiyerarşisindeki temel sınıf
abstract class Shape {
  public abstract function accept(ShapeVisitor $visitor);
}

// Circle sınıfı
class Circle extends Shape {
  public function accept(ShapeVisitor $visitor) {
    $visitor->visitCircle($this);
  }
}

// Rectangle sınıfı
class Rectangle extends Shape {
  public function accept(ShapeVisitor $visitor) {
    $visitor->visitRectangle($this);
  }
}

Bu örnekte, ShapeVisitor arayüzü, ziyaretçi sınıfının implemente etmesi gereken iki fonksiyonu tanımlar: visitCircle() ve visitRectangle(). Shape sınıfı, accept() adlı bir fonksiyon tanımlar ve ShapeVisitor nesnesini parametre olarak alır. Circle ve Rectangle sınıfları, accept() fonksiyonunu uygular ve ziyaretçi nesnesine kendi durumlarını geçirir.

Aşağıdaki örnek, Shape nesne hiyerarşisindeki nesneleri işlemek için bir ziyaretçi sınıfı uygular:

```
## Kod

```php
// Shape nesne hiyerarşisindeki nesneleri işlemek için bir ziyaretçi sınıfı uygulaması
class ShapeAreaVisitor implements ShapeVisitor {
  private $totalArea = 0;

  public function visitCircle(Circle $circle) {
    $this->totalArea += pow($circle->radius, 2) * pi();
  }

  public function visitRectangle(Rectangle $rectangle) {
    $this->totalArea += $rectangle->width * $rectangle->height;
  }

  public function getTotalArea() {
    return $this->totalArea;
  }
}
```

Bu örnekte, ShapeAreaVisitor sınıfı, ShapeVisitor arayüzünü uygular ve visitCircle() ve visitRectangle() fonksiyonlarını tanımlar. Bu fonksiyonlar, ilgili şekillerin alanını hesaplar ve toplam alanı tutmak için bir $totalArea değişkenini kullanır. getTotalArea() fonksiyonu, toplam alanı döndürür.

Aşağıdaki örnek, Shape nesne hiyerarşisindeki nesneleri işlemek için ziyaretçi sınıfını kullanır:

## Kod

```php
// Shape nesne hiyerarşisindeki nesneleri işlemek için ziyaretçi sınıfını kullanma
$shapes = array(new Circle(5), new Rectangle(4, 5), new Circle(2));

$areaVisitor = new ShapeAreaVisitor();
foreach ($shapes as $shape) {
  $shape->accept($areaVisitor);
}

echo "Total area: " . $areaVisitor->getTotalArea();
```

Bu örnekte, $shapes dizisi, Circle ve Rectangle nesnelerini içerir. ShapeAreaVisitor sınıfı, toplam alanı hesaplamak için kullanılır. foreach döngüsü, her bir şekil nesnesini ziyaretçi nesnesine geçirir ve toplam alanı hesaplar. Son olarak, getTotalArea() fonksiyonu, toplam alanı yazdırır.

Bu örnek, basit bir şekil hiyerarşisi için kullanılan bir ziyaretçi deseni örneğidir. Farklı ziyaretçi sınıfları oluşturarak farklı işlemler gerçekleştirmek mümkündür. Bu sayede, şekil hiyerarşisi, farklı işlevlerde kullanılabilir hale gelir ve kodun daha esnek olmasını sağlar.
