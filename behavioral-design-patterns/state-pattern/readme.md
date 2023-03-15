# 8.State Pattern (Durum Deseni)

Bir nesnenin durumunun değişmesi durumunda farklı davranışlar sergilemesini sağlayan bir tasarım desenidir. Bu desen, durum makinesi kavramına dayanır ve nesnenin belirli bir durumda olup olmadığını ve o durumda nasıl davranması gerektiğini belirler.

Bu desenin amacı, nesnenin durumuna bağlı olarak kod tekrarını azaltmak ve kodun daha okunaklı ve sürdürülebilir olmasını sağlamaktır.

Örneğin, bir siparişin durumu "Onay Bekliyor", "Hazırlanıyor", "Kargoya Verildi" ve "Teslim Edildi" gibi farklı durumlarda olabilir. Her durumda, siparişin müşteriye sunulan farklı seçenekleri ve davranışları vardır. Bu durumda State Pattern kullanarak, sipariş nesnesinin durumunu belirleyen bir sınıf tanımlayabiliriz ve her durum için farklı davranışlar belirleyebiliriz.

Aşağıda, PHP ile bir örnek gösterilecektir. Bu örnekte, "Context" adında bir sınıfımız ve "State" adında bir soyut sınıfımız var. "State" sınıfından türetilen "ConcreteStateA" ve "ConcreteStateB" sınıfları, "Context" nesnesinin durumuna bağlı olarak farklı davranışlar sergilerler.

## Kod

```php
<?php
interface State {
    public function handle(): void;
}

class ConcreteStateA implements State {
    public function handle(): void {
        echo "ConcreteStateA handle method is called.";
    }
}

class ConcreteStateB implements State {
    public function handle(): void {
        echo "ConcreteStateB handle method is called.";
    }
}

class Context {
    private $state;

    public function __construct(State $state) {
        $this->state = $state;
    }

    public function setState(State $state): void {
        $this->state = $state;
    }

    public function getState(): State {
        return $this->state;
    }

    public function request(): void {
        $this->state->handle();
    }
}

// Kullanım örneği
$context = new Context(new ConcreteStateA());
$context->request(); // "ConcreteStateA handle method is called."

$context->setState(new ConcreteStateB());
$context->request(); // "ConcreteStateB handle method is called."
```

Bu örnekte, "ConcreteStateA" ve "ConcreteStateB" sınıfları, "State" arayüzünden türetilmiştir ve her bir sınıfın kendi "handle" metodu vardır. "Context" sınıfı, şu anki durumu tutmak için bir "state" değişkeni içerir ve "request" metodu, mevcut durumun "handle" metodunu çağırır. Durum değiştirildiğinde, "setState" metodu kullanılır.

Örnekte, Context sınıfı State arayüzünü uygular ve ConcreteStateA ve ConcreteStateB sınıfları bu arayüzden türetilir. Bu sayede, Context sınıfı herhangi bir durum sınıfı nesnesini kabul edebilir ve o duruma özgü davranışı çağırabilir.

Context sınıfı, setState metodu ile durumu değiştirebilir ve bu değişiklik, sonraki request çağrısında etkisini gösterir. Bu sayede, Context sınıfı, farklı durumlara geçiş yapabilir ve her durumda farklı davranışlar sergileyebilir.

State Pattern, durum makinelerinin karmaşık durumlarını ve geçişlerini yönetmek için ideal bir tasarım desenidir. Bu desen, kod tekrarını azaltır, kodun daha okunaklı ve sürdürülebilir olmasını sağlar ve nesnelerin davranışlarını dinamik olarak değiştirebilir hale getirir.