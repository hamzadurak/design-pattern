# 2.Command Pattern (Komut Deseni)

Kodun ana işlevselliğini komut nesneleri olarak soyutlayarak uygulamanın esnekliğini arttırır. Bu desen, bir komutu bir nesne olarak temsil ederek, bu nesneyi bir veri yapısında saklayarak, uygulamanın diğer bölümlerinin komutu çalıştırmak için ihtiyaç duydukları tüm bilgileri içeren bir arabirim sağlar.

Bu desenin avantajı, uygulama mantığını kolaylaştırarak ve esnekliği arttırarak kod tekrarını azaltmaktır. Bu desen sayesinde, komutların bir listesi kolayca oluşturulabilir ve saklanabilir. Bu liste, geri alma işlemleri gibi daha karmaşık işlemler için kullanılabilir.

## Kod

```php
// Command interface
interface Command {
    public function execute();
}

// Receiver class
class Light {
    public function turnOn() {
        echo "Light is on.\n";
    }

    public function turnOff() {
        echo "Light is off.\n";
    }
}

// Concrete command class
class TurnOnCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->turnOn();
    }
}

// Concrete command class
class TurnOffCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->turnOff();
    }
}

// Invoker class
class RemoteControl {
    private $onCommand;
    private $offCommand;

    public function setOnCommand(Command $command) {
        $this->onCommand = $command;
    }

    public function setOffCommand(Command $command) {
        $this->offCommand = $command;
    }

    public function pressOnButton() {
        $this->onCommand->execute();
    }

    public function pressOffButton() {
        $this->offCommand->execute();
    }
}

// Client code
$light = new Light();

$turnOnCommand = new TurnOnCommand($light);
$turnOffCommand = new TurnOffCommand($light);

$remoteControl = new RemoteControl();
$remoteControl->setOnCommand($turnOnCommand);
$remoteControl->setOffCommand($turnOffCommand);

$remoteControl->pressOnButton(); // Light is on.
$remoteControl->pressOffButton(); // Light is off.
```

Bu örnekte, Command arayüzü, Light sınıfı, TurnOnCommand ve TurnOffCommand beton komutları, RemoteControl etki çağıran sınıf ve Client kodu yer almaktadır. TurnOnCommand ve TurnOffCommand sınıfları, Light sınıfı üzerinde belirli eylemleri gerçekleştiren execute() yöntemlerini uygular. RemoteControl sınıfı, onCommand ve offCommand özellikleri ile Command nesnelerini saklar. pressOnButton() ve pressOffButton() yöntemleri, Command nesnelerinin execute() yöntemlerini çağırmak için kullanılır.

Client kodu, önce Light nesnesini oluşturur ve sonra TurnOnCommand ve TurnOffCommand nesnelerini bu nesneye parametre olarak verir. Daha sonra, RemoteControl nesnesi oluşturulur ve setOnCommand() ve setOffCommand() yöntemleri, TurnOnCommand ve TurnOffCommand nesnelerini saklar. Son olarak, pressOnButton() ve pressOffButton() yöntemleri, RemoteControl nesnesinde saklanan Command nesnelerinin execute() yöntemlerini çağırır.

Bu örnek, Command desenini kullanarak bir RemoteControl nesnesi oluşturur ve bu nesne üzerinden Light nesnesini kontrol eder. TurnOnCommand ve TurnOffCommand komutları, Light nesnesini açma ve kapatma eylemlerini gerçekleştirir ve RemoteControl nesnesi, bu komutları pressOnButton() ve pressOffButton() yöntemleri aracılığıyla çalıştırır.