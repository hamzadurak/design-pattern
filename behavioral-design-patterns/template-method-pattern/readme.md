# 10.Template Method Pattern (Şablon Yöntemi Deseni)

bir sınıfın içinde belirli bir algoritmayı tanımlayan ancak bazı adımların alt sınıflar tarafından uygulanabileceği
özelleştirilebilir davranışlar sağlayan bir yazılım tasarım desenidir. Bu desen, bir şablonun temel yapısını tanımlar ve
daha sonra alt sınıfların bu şablonu uyarlamasına izin verir.

Bu desenin amacı, karmaşık bir işlemi sırayla gerçekleştirmek için bir şablon sağlamak ve alt sınıfların belirli
adımları uygulayarak davranışlarını özelleştirmesine izin vermek.

Örnek olarak, bir pasta yapma şablonu düşünebilirsiniz. Şablon, belirli adımların sırayla uygulanmasıyla pasta yapımını
gösterir. Ancak, bu şablonu kullanarak farklı tatlar ve süslemeler ekleyerek pasta yapabilirsiniz. Bu durumda, pasta
şablonu, Template Method Pattern'in bir örneğidir.

Aşağıdaki örnek, Template Method Pattern'i kullanarak bir oyuncak robot üretim sürecini simüle eder. Robot sınıfı, bir
Robot şablonu olarak hareket eder ve alt sınıflar bu şablonu uyarlayarak özelleştirir.

## Kod

```php
abstract class Robot {
 
  public final function buildRobot() {
    $this->buildHead();
    $this->buildBody();
    $this->addArms();
    $this->addLegs();
  }
 
  protected abstract function buildHead();
 
  protected abstract function buildBody();
 
  protected abstract function addArms();
 
  protected abstract function addLegs();
 
}
 
class SimpleRobot extends Robot {
 
  protected function buildHead() {
    echo "Simple Robot Head Created\n";
  }
 
  protected function buildBody() {
    echo "Simple Robot Body Created\n";
  }
 
  protected function addArms() {
    echo "Simple Robot Arms Added\n";
  }
 
  protected function addLegs() {
    echo "Simple Robot Legs Added\n";
  }
 
}
 
class ComplexRobot extends Robot {
 
  protected function buildHead() {
    echo "Complex Robot Head Created\n";
  }
 
  protected function buildBody() {
    echo "Complex Robot Body Created\n";
  }
 
  protected function addArms() {
    echo "Complex Robot Arms Added\n";
  }
 
  protected function addLegs() {
    echo "Complex Robot Legs Added\n";
  }
 
}
 
$simpleRobot = new SimpleRobot();
$simpleRobot->buildRobot();
 
$complexRobot = new ComplexRobot();
$complexRobot->buildRobot();
```

Bu örnekte, Robot sınıfı, bir buildRobot() yöntemi içerir. Bu yöntem, robotun üretim sürecini tanımlar ve buildHead(),
buildBody(), addArms() ve addLegs() adımlarını sırayla çağırarak robotu oluşturur. Bu adımlar, alt sınıflar tarafından
özelleştirilebilir.

SimpleRobot ve ComplexRobot sınıfları, Robot sınıfını genişleterek kendi özelliklerini eklerler. Örneğin, SimpleRobot
sınıfı, buildHead(), buildBody(), addArms() ve addLegs() adımlarını uygularken, kendi özelliklerini ekleyebilir. Aynı
şekilde, ComplexRobot sınıfı da aynı adımları uygular ve özelliklerini ekler.

Çıktı şu şekilde olacaktır:

## Kod

```php
Simple Robot Head Created
Simple Robot Body Created
Simple Robot Arms Added
Simple Robot Legs Added
Complex Robot Head Created
Complex Robot Body Created
Complex Robot Arms Added
Complex Robot Legs Added
```

Bu çıktıda, önce SimpleRobot ve ardından ComplexRobot sınıfının buildRobot() yöntemi çağrılır ve her iki durumda da
Robot şablonu kullanılarak robotlar oluşturulur.

Template Method Pattern, karmaşık algoritmaları daha modüler hale getirmek için kullanışlı bir desendir ve özellikle
kalıtım kullanarak davranışları özelleştirme ihtiyacı duyulan durumlarda kullanılabilir.