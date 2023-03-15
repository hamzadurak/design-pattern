# 7.Flyweight Pattern (Hafif Nesne Deseni)

Birçok benzer nesne yaratmak yerine, bir örnek nesne oluşturup, bu nesneyi birden fazla yerde kullanarak bellek kullanımını azaltmayı amaçlayan bir tasarım desenidir. Bu nesne, durumunu paylaşan nesnelerin özelliklerini depolamak için kullanılır.

Flyweight Pattern'ın temel fikri, benzer nesnelerin ortak durumlarını, mümkün olduğunca az sayıda nesne ile paylaşmaktır. Böylece bellek kullanımı azalır ve uygulamanın performansı artar.

Flyweight Pattern'ın birkaç bileşeni vardır:

1.Flyweight sınıfı: Bu sınıf, durumunu paylaşan nesnelerin özelliklerini depolar.

2.ConcreteFlyweight sınıfı: Bu sınıf, Flyweight sınıfından türetilir ve durumunu paylaşan nesnelerin özelliklerini belirler.

3.FlyweightFactory sınıfı: Bu sınıf, ConcreteFlyweight nesnelerinin bir havuzunu tutar ve bu nesneleri yönetir.

## Kod

```php
// Flyweight sınıfı
class CarModel {
  private $model;

  public function __construct($model) {
    $this->model = $model;
  }

  public function getModel() {
    return $this->model;
  }
}

// FlyweightFactory sınıfı
class CarFactory {
  private $models = array();

  public function getCarModel($model) {
    // Eğer daha önce oluşturulmuşsa, havuzda olanı döndür
    if (array_key_exists($model, $this->models)) {
      return $this->models[$model];
    }
    // Eğer daha önce oluşturulmamışsa, yeni bir tane oluştur ve havuza ekle
    else {
      $carModel = new CarModel($model);
      $this->models[$model] = $carModel;
      return $carModel;
    }
  }
}

// Kullanım
$carFactory = new CarFactory();
$car1 = $carFactory->getCarModel("Mercedes");
$car2 = $carFactory->getCarModel("Mercedes");

// Her iki değişken de aynı nesneye işaret eder
var_dump($car1 === $car2); // true
```

Bu örnekte, CarModel sınıfı, Flyweight sınıfını temsil eder. CarFactory sınıfı, FlyweightFactory sınıfını temsil eder. getCarModel() fonksiyonu, durumunu paylaşan nesnelerin özelliklerini depolamak için kullanılır. Car1 ve Car2 nesneleri, aynı havuzdaki aynı CarModel nesnesine işaret eder. Bu sayede, bellek kullanımı azaltılır ve performans artırılır.

Yukarıdaki örnekte, CarModel sınıfı, sadece bir modeli temsil etmektedir. Ancak gerçek dünyadaki bir senaryoda, bir model için birçok özellik ve metot olacaktır. Bu durumda, CarModel sınıfı daha karmaşık hale gelebilir. Ancak temel fikir aynı kalır: Benzer nesnelerin ortak durumunu paylaşarak bellek kullanımını azaltmak.

Flyweight Pattern, özellikle büyük ölçekli uygulamalarda ve yüksek trafikli web sitelerinde performansı artırmak için kullanılabilir. Ancak uygulamanın ihtiyaçlarına bağlı olarak, bu desenin kullanılması gerekmeyebilir.