# 3.Factory Method Pattern (Fabrika Metodu Deseni)

Bir nesne yaratma tasarım kalıbıdır ve bir nesne yaratma işlemini alt sınıflara bırakarak ana sınıfı soyutlamaya dayanır. Bu kalıp, bir nesnenin oluşturulması için gereken adımların tanımlandığı bir arayüz veya soyut sınıf sağlar ve alt sınıflar, bu adımları uygulayarak nesne oluştururlar.

Factory Method Pattern, bir arayüz veya soyut sınıf kullanarak nesne yaratmayı sağlar ve alt sınıfları bu arayüzü veya soyut sınıfı uygulayarak kendi nesnelerini oluşturmaya zorlar. Bu sayede, ana sınıfın alt sınıflar hakkında bilgi sahibi olması gerekmez ve alt sınıflar kendi nesnelerini yarattıkları sürece herhangi bir şekilde değiştirilebilirler.

## Kod

```php
// Soyut sınıf veya arayüz tanımlanması
abstract class Creator {
    abstract public function factoryMethod(): Product;
    public function someOperation(): string {
        $product = $this->factoryMethod();
        $result = "Creator: The same creator's code has just worked with " . $product->operation();
        return $result;
    }
}

// Ürün sınıfı tanımlanması
interface Product {
    public function operation(): string;
}

// İlk alt sınıf tanımlanması
class ConcreteCreator1 extends Creator {
    public function factoryMethod(): Product {
        return new ConcreteProduct1();
    }
}

// İkinci alt sınıf tanımlanması
class ConcreteCreator2 extends Creator {
    public function factoryMethod(): Product {
        return new ConcreteProduct2();
    }
}

// İlk ürün sınıfı tanımlanması
class ConcreteProduct1 implements Product {
    public function operation(): string {
        return "{Result of the ConcreteProduct1}";
    }
}

// İkinci ürün sınıfı tanımlanması
class ConcreteProduct2 implements Product {
    public function operation(): string {
        return "{Result of the ConcreteProduct2}";
    }
}

// Kullanım
function clientCode(Creator $creator) {
    echo "Client: I'm not aware of the creator's class, but it still works.<br>"
        . $creator->someOperation() . "<br>";
}

// İlk yaratıcı nesne örneği oluşturulması ve kullanımı
echo "App: Launched with the ConcreteCreator1.<br>";
clientCode(new ConcreteCreator1());
echo "<br>";

// İkinci yaratıcı nesne örneği oluşturulması ve kullanımı
echo "App: Launched with the ConcreteCreator2.<br>";
clientCode(new ConcreteCreator2());
echo "<br>";
```

Bu örnekte, Creator soyut sınıfı veya arayüzü, Product arayüzü ve ConcreteProduct1 ve ConcreteProduct2 gibi iki ürün sınıfı tanımlanmıştır. Creator sınıfı, factoryMethod adında bir soyut metoda sahip eder ve alt sınıfların bu metodu uygulamasını zorlar. someOperation adında bir metoda sahip olması, ürünün bir örneğini oluşturmak için factoryMethod metodunu çağırır ve ardından bu örneği kullanarak bir işlem gerçekleştirir.

ConcreteCreator1 ve ConcreteCreator2 alt sınıfları, factoryMethod metodunu uygular ve sırasıyla ConcreteProduct1 ve ConcreteProduct2 sınıflarından bir örnek döndürür.

Son olarak, clientCode fonksiyonu, bir Creator nesnesi alır ve someOperation metodunu çağırarak örnek bir ürün oluşturur ve sonucu ekrana yazdırır. Bu fonksiyon, ana sınıfın alt sınıflarından herhangi birinin kullanılmasına izin verir ve ürünün nasıl oluşturulduğu hakkında bilgi sahibi olmadan çalışabilir.

Yukarıdaki örnekte, ConcreteCreator1 ve ConcreteCreator2 alt sınıfları, ConcreteProduct1 ve ConcreteProduct2 ürünlerini oluşturur. Ancak, yeni bir ürün eklemek istediğimizde, yalnızca yeni bir ürün sınıfı tanımlamamız ve bir yaratıcı sınıfı oluşturmamız yeterlidir. Bu şekilde, uygulamamızı değiştirmeden yeni bir ürün ekleyebiliriz.

Özetle, Factory Method Pattern, bir nesne yaratma işlemini soyutlamaya ve alt sınıflara bırakmaya dayanır. Bu kalıp, ana sınıfın alt sınıflar hakkında bilgi sahibi olmadan çalışmasına izin verir ve yeni ürünler eklemeyi kolaylaştırır.
