# 4.Composite Pattern (Bileşik Deseni)

Yapısında birbirine bağımlı olan nesnelerin hiyerarşik olarak düzenlenmesine ve bir arada kullanılmasına olanak sağlayan bir tasarım desenidir. Bu desen, bir ana nesne içinde bulunan birden çok alt nesne kümesi oluşturarak, bu nesnelerin hiyerarşik bir şekilde kullanılmasına izin verir. Bu desen, bir nesne grubu ile tek bir nesne arasında bulunan farklılıkları gizleyerek, nesne yönetiminde kolaylık sağlar.

Örneğin, bir ağaç yapısını ele alalım. Bu yapının kökü, dalları ve yapraklarından oluşur. Bileşik deseni kullanarak, kökün altındaki her düğümü (dal veya yaprak) bir bileşen olarak ele alabilir ve bu bileşenleri başka bileşenlerle birleştirebilirsiniz. Bu, her düğümün, herhangi bir düğümün yapısını değiştirmeden ağacın farklı parçalarına dahil edilebileceği anlamına gelir.

## Kod

```php
<?php
// Component Class
abstract class Shape {
    public function add(Shape $shape) {}
    public function remove(Shape $shape) {}
    abstract public function draw();
}

// Composite Class
class Composite extends Shape {
    private $shapes;

    public function __construct() {
        $this->shapes = array();
    }

    public function add(Shape $shape) {
        array_push($this->shapes, $shape);
    }

    public function remove(Shape $shape) {
        $index = array_search($shape, $this->shapes);
        array_splice($this->shapes, $index, 1);
    }

    public function draw() {
        foreach ($this->shapes as $shape) {
            $shape->draw();
        }
    }
}

// Leaf Class
class Circle extends Shape {
    public function draw() {
        echo "Circle drawn.<br/>";
    }
}

// Client code
$circle1 = new Circle();
$circle2 = new Circle();
$circle3 = new Circle();

$composite = new Composite();
$composite->add($circle1);
$composite->add($circle2);
$composite->add($circle3);

$composite->draw();
```

Bu örnekte, bileşik deseni kullanarak bir şekil hiyerarşisi oluşturulmuştur. Shape sınıfı, bileşenlerin soyut bir temsilcisidir. Composite sınıfı, bileşenlerin gruplarını yönetir ve bileşik yapının temelini oluşturur. Circle sınıfı, yaprak düğümlerdir ve draw() fonksiyonunu uygularlar. Son olarak, Client kodu bileşik yapının kullanımını gösterir. Bu örnekte, bir bileşik nesne oluşturulur ve içine üç adet çember eklenir. Son olarak, bileşik nesnenin draw() fonksiyonu çağrılır ve çizı ettirirken bileşik nesne, içinde bulunan çemberleri çizdirir.

Bu örnek, bileşik desenin bir uygulamasını göstermektedir. Bileşik desen, özellikle yapının hiyerarşik olduğu durumlarda, nesne yönetiminde kolaylık sağlayan bir tasarım desenidir. Bu desen sayesinde, nesne gruplarını tek bir nesne gibi ele alabilir ve grupların yönetimini basitleştirebilirsiniz.