# 5.Mediator Pattern (Aracı Deseni)

Nesneler arasındaki etkileşimi sınırlayan bir aracı tasarım desenidir. Bu desen, birçok nesnenin birbirleriyle doğrudan
etkileşimde bulunmak yerine bir aracı nesne tarafından yönetildiği durumlarda kullanılabilir. Bu, nesneler arasındaki
sıkı bağımlılıkları azaltır ve daha esnek bir tasarım sunar.

Mediator Pattern, bir Mediator arayüzü, bu arayüzü uygulayan bir ConcreteMediator sınıfı ve bu sınıfın yönettiği
ConcreteColleague sınıflarından oluşur.

Mediator arayüzü, ConcreteMediator sınıfının yönettiği ConcreteColleague sınıflarına gönderilecek olan mesajların
tanımlanması için kullanılır. ConcreteMediator sınıfı, bu mesajları alır ve doğru ConcreteColleague sınıfına iletmek
için gereken tüm işlemleri gerçekleştirir.

## Kod

```php
<?php
// Mediator arayüzü
interface Mediator {
    public function sendMessage(string $message, Colleague $colleague);
}

// ConcreteMediator sınıfı
class ChatRoom implements Mediator {
    private $colleagues = [];

    public function addColleague(Colleague $colleague) {
        $this->colleagues[] = $colleague;
    }

    public function sendMessage(string $message, Colleague $colleague) {
        foreach ($this->colleagues as $c) {
            if ($c != $colleague) {
                $c->receiveMessage($message);
            }
        }
    }
}

// ConcreteColleague sınıfı
class User implements Colleague {
    private $name;
    private $mediator;

    public function __construct(string $name, Mediator $mediator) {
        $this->name = $name;
        $this->mediator = $mediator;
    }

    public function send(string $message) {
        $this->mediator->sendMessage($message, $this);
    }

    public function receiveMessage(string $message) {
        echo $this->name . " received message: " . $message . "\n";
    }
}

// Colleague arayüzü
interface Colleague {
    public function receiveMessage(string $message);
}

// Kullanımı
$mediator = new ChatRoom();

$user1 = new User("Alice", $mediator);
$user2 = new User("Bob", $mediator);
$user3 = new User("Charlie", $mediator);

$mediator->addColleague($user1);
$mediator->addColleague($user2);
$mediator->addColleague($user3);

$user1->send("Hello, everyone!");
$user2->send("Hey Alice!");
$user3->send("What's up, guys?");

// Output:
// Bob received message: Hello, everyone!
// Charlie received message: Hello, everyone!
// Alice received message: Hey Alice!
// Charlie received message: Hey Alice!
// Alice received message: What's up, guys?
// Bob received message: What's up, guys?
?>
```

Bu örnekte, ChatRoom sınıfı Mediator arayüzünü uygular ve ConcreteColleague sınıfları olan User sınıflarını yöneten
ChatRoom sınıfı, addColleague() yöntemiyle ConcreteColleague sınıflarını ekler ve sendMessage() yöntemiyle mesajları
alır ve doğru ConcreteColleague sınıfına iletir.

User sınıfı, Colleague arayüzünü uygular ve send() yöntemiyle mesajları Mediator arayüzüne gönderir. receiveMessage()
yöntemi ise Mediator arayüzü tarafından çağrılır ve mesajı alır.

Bu örnekte, Alice, Bob ve Charlie isimli üç kullanıcı var ve birbirleriyle iletişim kurmak için Mediator aracılığıyla
mesajlar gönderiyorlar. Mediator olarak ChatRoom kullanılır ve bu sınıf ConcreteColleague sınıflarını yönetir.

Örnekteki çıktıda, her kullanıcının diğer kullanıcılardan aldığı mesajlar görülebilir. Örneğin, Bob'un "Hello,
everyone!" mesajını aldığı ve Charlie'nin "Hey Alice!" mesajını aldığı görülebilir.

Bu örnekte Mediator Pattern, ConcreteColleague sınıfları arasındaki doğrudan etkileşimi azaltarak daha esnek bir tasarım
sunar. Ayrıca yeni ConcreteColleague sınıflarının kolayca eklenebilmesine de olanak tanır.