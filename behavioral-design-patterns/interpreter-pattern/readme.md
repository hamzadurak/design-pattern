# 3.Interpreter Pattern (Tercüman Deseni)

Bir dilin semantik yapısını temsil etmek için kullanılır. Bu desen, bir dizi belirli amaç için tasarlanmış sınıfı kullanır ve her bir sınıf, belirli bir semantik yapıya sahip bir dilin bir parçasını yorumlayabilir.

Bu desenin amacı, bir dili yorumlamak için bir çözüm sağlamaktır. Bu, programın çalışma zamanında belirli bir dili okumak ve yorumlamak için kullanılabilir.

Örneğin, bir metin dosyasındaki belirli bir ifadeyi yorumlamak için Interpreter Pattern kullanılabilir. Bu desen, ifadeyi okuyabilir, semantik yapısını analiz edebilir ve sonra işlem yapabilir.

## Kod

```php
interface Expression {
  public function interpret($context);
}

class Number implements Expression {
  private $number;

  public function __construct($number) {
    $this->number = $number;
  }

  public function interpret($context) {
    $context->add($this->number);
  }
}

class Plus implements Expression {
  public function interpret($context) {
    $context->add($context->pop() + $context->pop());
  }
}

class Minus implements Expression {
  public function interpret($context) {
    $context->add(- $context->pop() + $context->pop());
  }
}

class Context {
  private $stack = array();

  public function pop() {
    return array_pop($this->stack);
  }

  public function push($number) {
    array_push($this->stack, $number);
  }

  public function add($number) {
    array_push($this->stack, $number);
  }

  public function result() {
    return array_pop($this->stack);
  }
}

$context = new Context();
$expression = new Number(5);
$expression->interpret($context);
$expression = new Number(3);
$expression->interpret($context);
$expression = new Plus();
$expression->interpret($context);
echo $context->result(); // Output: 8
```

Bu örnekte, matematiksel ifadeleri yorumlamak için üç farklı sınıf kullanıyoruz: Number, Plus ve Minus. Number sınıfı, bir sayıyı yorumlamak için kullanılır ve sembolik ifadeyi bağlamına ekler. Plus ve Minus sınıfları, toplama ve çıkarma sembolik ifadeleri için kullanılır ve bağlamdaki sayıları işlemlerini gerçekleştirir.

Context sınıfı, yorumlama işlemi için gereken bağlamı sağlar. Bu sınıf, bir yığın kullanarak sembolik ifadeleri depolar ve sonucu hesaplar.

Son olarak, örnek bir hesaplama yapmak için sınıfları birleştiriyoruz. Öncelikle, Context sınıfı ile bir bağlam oluşturuyoruz. Daha sonra, Number sınıfı ile 5 ve 3 sayılarını bağlama ekliyoruz. Son olarak, Plus sınıfı ile bağlamdaki sayıları toplayarak sonucu hesaplıyoruz ve ekrana yazdırıyoruz.

Interpreter Pattern, belirli bir dilin semantik yapısını temsil etmek için kullanılabilir ve yorumlama işlemini gerçekleştirmek için bir çözüm sağlar. Bu desen, metin işleme, matematiksel hesaplamalar, veritabanı sorguları ve daha birçok alanda kullanılabilir.