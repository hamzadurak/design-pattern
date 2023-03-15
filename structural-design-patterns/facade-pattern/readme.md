# 3.Facade Pattern (Yüz Deseni)

Bir yazılım bileşeninin karmaşık alt sistemlerinin arayüzlerini basitleştirmek için kullanılır. Bu desen, bir alt sistemdeki işlemleri yapan karmaşık kodları, bir arayüz üzerinde basitleştirilmiş ve daha anlaşılır bir şekilde sunarak kullanıcıya kolaylık sağlar.

Bu desen, alt sistemlerin doğrudan kullanılmasının karmaşıklığını azaltır ve bir arayüz aracılığıyla erişim sağlar. Bu sayede, alt sistemlerin değiştirilmesi veya güncellenmesi durumunda, kullanıcıya yansıtılmadan arka planda yapılan değişikliklerin minimum düzeyde kalması sağlanır.

## Kod

```php
<?php

// Alt sistemlerimizden biri
class Subsystem1
{
    public function operation1()
    {
        echo "Subsystem 1 operation\n";
    }
}

// Alt sistemlerimizden biri
class Subsystem2
{
    public function operation2()
    {
        echo "Subsystem 2 operation\n";
    }
}

// Facade sınıfımız
class Facade
{
    private $subsystem1;
    private $subsystem2;

    public function __construct(Subsystem1 $subsystem1 = null, Subsystem2 $subsystem2 = null)
    {
        $this->subsystem1 = $subsystem1 ?: new Subsystem1();
        $this->subsystem2 = $subsystem2 ?: new Subsystem2();
    }

    public function operation()
    {
        $this->subsystem1->operation1();
        $this->subsystem2->operation2();
    }
}

// Kullanımı
$facade = new Facade();
$facade->operation();
```

Yukarıdaki örnekte, Subsystem1 ve Subsystem2 olarak adlandırılan iki farklı alt sisteme sahibiz. Facade sınıfı ise bu alt sistemlerin işlemlerinin basitleştirilmiş bir arayüzünü sunar.

Örneğimizde, Facade sınıfının operation() metodunda Subsystem1 ve Subsystem2 alt sistemlerinin işlemleri çağrılıyor. Kullanımı ise oldukça basit; Facade sınıfını çağırdığımızda alt sistemlerin işlemleri arka planda yapılıyor ve kullanıcının işlemi sadece Facade sınıfı aracılığıyla gerçekleştirdiği anlaşılıyor.