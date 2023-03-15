# 7.Observer Pattern (Gözlemci Deseni)

Bir nesnenin durumundaki değişiklikleri takip eden bir grup nesne arasındaki bağımlılıkları yönetmek için kullanılan bir
yazılım tasarım desenidir. Bu desen, birçok durumda kullanılır; örneğin, bir nesnenin durumu değiştiğinde, diğer
nesnelere bu değişikliği iletmek veya bir nesnenin belirli bir durumu sağladığında, diğer nesnelerin kendilerini buna
göre güncellemesi gereken durumlarda kullanılır.

Observer Pattern, bir Subject (Özne) ve bir veya daha fazla Observer (Gözlemci) nesnesi arasındaki ilişkiyi tanımlar.
Subject nesnesi, durum değişikliği olduğunda Observer nesnelerine bilgi verir. Observer nesneleri, Subject nesnesindeki
durum değişikliğine göre kendilerini günceller.

PHP dilinde, Observer Pattern uygulamak için öncelikle Subject ve Observer arayüzlerini tanımlamanız gerekir. Ardından,
bu arayüzleri uygulayan sınıfları oluşturun.

Aşağıdaki örnek kod, bir Subject arayüzü tanımlar. Bu arayüzde, Observer nesnelerinin güncelleneceği notifyObservers()
yöntemi ve Subject nesnesinin durumunu ayarlamak için kullanılacak setState() yöntemi tanımlanmıştır:

## Kod

```php
interface Subject {
    public function setState($state);
    public function notifyObservers();
}
```

Ardından, Observer arayüzünü tanımlayabilirsiniz. Bu arayüzde, Observer nesnelerinin güncelleme alacağı update() yöntemi
tanımlanmıştır:

## Kod

```php
interface Observer {
    public function update($subject);
}
```

Son olarak, ConcreteSubject ve ConcreteObserver sınıflarını oluşturmanız gerekiyor. ConcreteSubject sınıfı, Subject
arayüzünü uygulayan bir sınıftır ve durum değişikliği olduğunda Observer nesnelerine bildirim gönderir. ConcreteObserver
sınıfı ise Observer arayüzünü uygulayan bir sınıftır ve güncelleme bildirimi alır.

Aşağıdaki örnek kod, ConcreteSubject sınıfını tanımlar. Bu sınıf, setState() yöntemini uygular ve durum değişikliği
olduğunda notifyObservers() yöntemini kullanarak Observer nesnelerine bildirim gönderir:

## Kod

```php
class ConcreteSubject implements Subject {
    private $state;
    private $observers = array();

    public function setState($state) {
        $this->state = $state;
        $this->notifyObservers();
    }

    public function notifyObservers() {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }

    public function attach($observer) {
        $this->observers[] = $observer;
    }
}
```

Aşağıdaki örnek kod, ConcreteObserver sınıfını gösterir. Bu sınıf, Observer arayüzünü uygular ve update() yöntemini
kullanarak güncelleme bildirimi alır:

## Kod

```php
class ConcreteObserver implements Observer {
    private $state;

    public function update($subject) {
        $this->state = $subject->getState();
    }
}
```

Bu örnekte, ConcreteObserver sınıfı sadece Subject nesnesinin durumunu kendi durumuna eşitliyor. Ancak gerçek bir
senaryoda, ConcreteObserver sınıfı durum değişikliğine göre kendini güncelleyebilir.

Son olarak, ConcreteSubject nesnesi oluşturulur ve ConcreteObserver nesnesi bu nesneye bağlanır:

## Kod

```php
$subject = new ConcreteSubject();
$observer = new ConcreteObserver();
$subject->attach($observer);
```

Daha sonra, Subject nesnesinin durumu değiştirilir ve Observer nesnesi bu değişikliği alır:

## Kod

```php
$subject->setState("new state");
```

Bu örnekte, Observer Pattern kullanarak bir nesne grubu arasında durum değişiklikleri yönetilir. Durum değişikliği
olduğunda, ConcreteSubject nesnesi notifyObservers() yöntemini kullanarak Observer nesnelerine bildirim gönderir.
ConcreteObserver nesnesi, güncelleme bildirimi aldığında kendini günceller veya işlemlerini gerçekleştirir. Bu desen,
nesneler arasındaki bağımlılıkları yönetmek için kullanışlıdır ve dinamik olarak değişen sistemlerde kullanılabilecek
esnek bir yapı sunar.