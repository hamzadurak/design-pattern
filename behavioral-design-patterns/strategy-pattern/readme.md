# 9.Strategy Pattern (Strateji Deseni)

Davranışsal bir tasarım desenidir. Bu desen, belirli bir işi yapmak için birden fazla yöntem veya algoritma sunan bir nesne ailesi yaratmayı amaçlar. Bu sayede, kullanıcının işlemlerini farklı algoritmalarla yapmasına olanak sağlar.

Bu desen, bir arayüz veya soyut sınıf yoluyla belirli bir davranışı tanımlayan bir yapı oluşturarak başlar. Daha sonra, bu arayüzü veya sınıfı uygulayan ve belirli bir algoritma setiyle çalışan farklı sınıflar yaratılır. Bu sınıflar, uygulama sırasında belirli bir stratejiyi seçmek için kullanılır.

## Kod

```php
interface ShippingStrategy {
  public function calculateFee($weight);
}

class FedExShipping implements ShippingStrategy {
  public function calculateFee($weight) {
    // FedEx'in hesaplama algoritmasını kullanarak nakliye ücretini hesaplar
  }
}

class UPSShipping implements ShippingStrategy {
  public function calculateFee($weight) {
    // UPS'nin hesaplama algoritmasını kullanarak nakliye ücretini hesaplar
  }
}

class ShippingCalculator {
  private $strategy;

  public function __construct(ShippingStrategy $strategy) {
    $this->strategy = $strategy;
  }

  public function calculateShippingFee($weight) {
    return $this->strategy->calculateFee($weight);
  }
}

// Kullanım
$fedex = new FedExShipping();
$shippingCalculator = new ShippingCalculator($fedex);
$fee = $shippingCalculator->calculateShippingFee(10);

$ups = new UPSShipping();
$shippingCalculator = new ShippingCalculator($ups);
$fee = $shippingCalculator->calculateShippingFee(10);
```

Yukarıdaki örnekte, ShippingStrategy arayüzü, nakliye ücreti hesaplama işlemini tanımlayan bir yöntem içerir. FedExShipping ve UPSShipping sınıfları, bu arayüzü uygular ve kendi nakliye ücreti hesaplama algoritmalarını içerir.

ShippingCalculator sınıfı, seçilen nakliye stratejisi ile birlikte çalışan bir sınıftır. Bu sınıf, belirli bir nakliye ağırlığı için nakliye ücretini hesaplamak için seçilen stratejinin hesaplama yöntemini kullanır.

Kullanım örneğinde, önce FedExShipping sınıfı kullanılarak bir ShippingCalculator örneği oluşturulur. Daha sonra, bu örnekle calculateShippingFee() yöntemi çağrılır ve sonuç olarak hesaplanan nakliye ücreti döndürülür. Son olarak, aynı işlem UPSShipping sınıfı kullanılarak tekrarlanır.

Bu örnekte, ShippingStrategy arayüzü, herhangi bir nakliye firmasının uygulayabileceği farklı nakliye ücreti hesaplama algoritmalarını destekler. Bu sayede, uygulama sırasında kullanıcılar farklı nakliye firmalarının hesaplama algoritmalarını seçebilirler. ShippingCalculator sınıfı, seçilen nakliye stratejisiyle birlikte çalışarak, kullanıcının belirlediği ağırlık için doğru nakliye ücretini hesaplar.

Bu desen, kodun yeniden kullanılabilirliğini artırır ve bakımı kolaylaştırır. Yeni bir nakliye firması eklemek istendiğinde, yalnızca ShippingStrategy arayüzünü uygulayan yeni bir sınıf oluşturmak yeterlidir.

Bu desen ayrıca, benzer ancak farklı işlemler yapmak için birden fazla kod parçası yazmak yerine, farklı stratejilerin aynı arayüzü kullanarak kullanılmasını sağlar. Bu sayede, kodun karmaşıklığı azaltılır ve daha modüler bir yapı oluşturulur.