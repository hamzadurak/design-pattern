# 5.Singleton Pattern (Tek Nesne Deseni)

Bir sınıfın sadece bir örneğinin (instance) oluşturulmasını sağlayan bir tasarım desenidir. Bu örneğe, programın herhangi bir yerinden erişilebilir ve tek bir noktadan kontrol edilebilir.

Bu tasarım deseni, özellikle kaynak tüketen nesnelerin (resource-intensive objects) yalnızca bir kez yaratılması gerektiğinde ve buna ek olarak farklı bölümlerden veya sınıflardan aynı örneğe erişmenin gerekli olduğu durumlarda kullanılır.

## Kod

```php
class Singleton {
  private static $instance = null;

  private function __construct() {
    // Private constructor to prevent instantiation from outside
  }

  public static function getInstance() {
    if (self::$instance == null) {
      self::$instance = new Singleton();
    }

    return self::$instance;
  }

  public function sayHello() {
    echo "Hello, world!";
  }
}

// Usage
$instance1 = Singleton::getInstance();
$instance1->sayHello();

$instance2 = Singleton::getInstance();
$instance2->sayHello();

// The following will output true, indicating that $instance1 and $instance2 refer to the same object.
var_dump($instance1 === $instance2);
```

Bu örnekte, Singleton sınıfı, private erişim belirleyicisiyle özel bir yapıcı (constructor) yöntemi kullanarak sınıfın dışarıdan doğrudan oluşturulmasını önler.

getInstance() yöntemi, tek bir örnek oluşturmak için çağrılır ve önceki bir örnek varsa, mevcut örneği döndürür. sayHello() yöntemi, örnekten "Hello, world!" mesajı yazdırmak için kullanılır.

Bu örnekte, getInstance() yöntemi sınıfın tek bir örneğini döndürdüğünden, $instance1 ve $instance2 değişkenleri aynı nesneye referans eder ve var_dump() işlevi bu nesnelerin eşit olduğunu doğrular.