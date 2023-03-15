# 2.Decorator Pattern (Dekoratör Deseni)

Elbise üzerine bir ceket giyerek tarzınızı değiştirirsiniz. Benzer şekilde, bir nesnenin davranışını değiştirmeden ona ek özellikler eklemek istediğinizde, Decorator Pattern kullanılabilir.

Decorator Pattern, nesnelerin davranışını veya özelliklerini, dinamik olarak çalışma zamanında değiştirmenizi sağlayan bir tasarım desenidir. Bu desen, bir nesne üzerinde çalışan işlevselliklerin, nesnenin kendisini değiştirmeden eklenmesini sağlar.

Bu desen, birden fazla özellikli bir nesneye sahip olan durumlarda çok yararlıdır ve bir nesneye dinamik olarak özellikler eklemek için kullanılır. Ayrıca, bu desen, yazılım geliştirme projelerinde çok katmanlı mimarilerin oluşturulmasına da yardımcı olur.

## Kod

```php
<?php

// Temel bileşen arayüzü
interface Coffee {
    public function getCost();
    public function getDescription();
}

// Temel bileşen uygulaması
class SimpleCoffee implements Coffee {
    public function getCost() {
        return 10;
    }

    public function getDescription() {
        return "Simple coffee";
    }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected $decoratedCoffee;

    public function __construct(Coffee $coffee) {
        $this->decoratedCoffee = $coffee;
    }

    public function getCost() {
        return $this->decoratedCoffee->getCost();
    }

    public function getDescription() {
        return $this->decoratedCoffee->getDescription();
    }
}

// Decorator sınıfından türetilen CreamDecorator sınıfı
class CreamDecorator extends CoffeeDecorator {
    public function __construct(Coffee $coffee) {
        parent::__construct($coffee);
    }

    public function getCost() {
        return parent::getCost() + 2;
    }

    public function getDescription() {
        return parent::getDescription() . ", cream";
    }
}

// Decorator sınıfından türetilen VanillaDecorator sınıfı
class VanillaDecorator extends CoffeeDecorator {
    public function __construct(Coffee $coffee) {
        parent::__construct($coffee);
    }

    public function getCost() {
        return parent::getCost() + 3;
    }

    public function getDescription() {
        return parent::getDescription() . ", vanilla";
    }
}

// Test
$simpleCoffee = new SimpleCoffee();
echo $simpleCoffee->getDescription() . " " . $simpleCoffee->getCost() . "\n";

$coffeeWithCream = new CreamDecorator($simpleCoffee);
echo $coffeeWithCream->getDescription() . " " . $coffeeWithCream->getCost() . "\n";

$coffeeWithVanilla = new VanillaDecorator($simpleCoffee);
echo $coffeeWithVanilla->getDescription() . " " . $coffeeWithVanilla->getCost() . "\n";

$coffeeWithCreamAndVanilla = new VanillaDecorator($coffeeWithCream);
echo $coffeeWithCreamAndVanilla->getDescription() . " " . $coffeeWithCreamAndVanilla->getCost() . "\n";
```

Bu örnek kod, temel kahve nesnesini alır ve üzerine farklı özellikler ekleyerek değişik fiyat ve tanımlamalarla yeni kahve nesneleri oluşturur. İlk olarak Coffee adında bir arayüz oluşturulur ve getCost() ve getDescription() adında iki metod tanımlanır. Daha sonra SimpleCoffee sınıfı oluşturulur ve Coffee arayüzünü uygular. Bu sınıf, temel kahve nesnesini temsil eder.

Sonra, CoffeeDecorator adında bir abstract sınıf oluşturulur ve bu sınıf, Coffee arayüzünü uygular. Bu sınıf, decorator sınıflarının temel sınıfıdır ve herhangi bir decorator sınıfı, bu sınıftan türetilir. Decorator sınıfları, constructor metoduna bir Coffee nesnesi alarak çağrılır ve getCost() ve getDescription() metodlarını uygular.

Örneğin, CreamDecorator sınıfı CoffeeDecorator sınıfından türetilir ve getCost() ve getDescription() metodlarını uygular. Bu sınıf, kahveye krema ekleyen bir decorator olarak kullanılabilir. VanillaDecorator sınıfı da CoffeeDecorator sınıfından türetilir ve kahveye vanilya ekleyen bir decorator olarak kullanılabilir.

Örnekte, SimpleCoffee nesnesi oluşturulur ve temel fiyatı ve tanımlaması ekrana yazdırılır. Daha sonra, CreamDecorator sınıfından türetilen coffeeWithCream nesnesi oluşturulur ve bu nesnenin fiyatı ve tanımlaması da ekrana yazdırılır. VanillaDecorator sınıfından türetilen coffeeWithVanilla nesnesi de aynı şekilde oluşturulur ve fiyatı ve tanımlaması ekrana yazdırılır. Son olarak, coffeeWithCreamAndVanilla nesnesi oluşturulur ve bu nesnenin fiyatı ve tanımlaması da ekrana yazdırılır. Bu nesne, önce CreamDecorator sınıfıyla oluşturulan bir nesneye, VanillaDecorator sınıfıyla ekstra bir özellik eklenerek oluşturulur.