# 1.Chain of Responsibility Pattern (Sorumluluk Zinciri Deseni)

Bir istek veya işlemi işleyebilecek farklı nesneler arasında bir zincir oluşturur. Her nesne, istek veya işlemin kendisine uygun olup olmadığını kontrol eder ve işleyebileceği durumda işlemi gerçekleştirir. Aksi takdirde, istek veya işlem bir sonraki nesneye aktarılır ve zincirdeki bir sonraki nesne aynı işlemi gerçekleştirmeye çalışır. Bu şekilde zincirin sonuna kadar ilerlenir ve işlem, uygun bir nesne tarafından işlenene kadar zincir boyunca devam eder.

Bu desen, özellikle birden fazla nesnenin birbirleriyle sıkı bağlantı içinde olmasını önlemek için faydalıdır. Her nesne sadece kendi işlevselliğine odaklanır ve zincirdeki bir sonraki nesneyle iletişim kurarak işlemi devam ettirir.

## Kod

```php
<?php

abstract class Logger {
    protected $nextLogger;
    
    public function setNextLogger(Logger $nextLogger) {
        $this->nextLogger = $nextLogger;
    }
    
    public function logMessage($level, $message) {
        if ($this->canHandleMessage($level)) {
            $this->writeMessage($message);
        } else if ($this->nextLogger != null) {
            $this->nextLogger->logMessage($level, $message);
        }
    }
    
    protected abstract function canHandleMessage($level);
    protected abstract function writeMessage($message);
}

class ConsoleLogger extends Logger {
    protected function canHandleMessage($level) {
        return $level == 'Console';
    }
    
    protected function writeMessage($message) {
        echo "ConsoleLogger: " . $message . "\n";
    }
}

class FileLogger extends Logger {
    protected function canHandleMessage($level) {
        return $level == 'File';
    }
    
    protected function writeMessage($message) {
        echo "FileLogger: " . $message . "\n";
    }
}

class ErrorLogger extends Logger {
    protected function canHandleMessage($level) {
        return $level == 'Error';
    }
    
    protected function writeMessage($message) {
        echo "ErrorLogger: " . $message . "\n";
    }
}

// Logger zincirinin oluşturulması
$consoleLogger = new ConsoleLogger();
$fileLogger = new FileLogger();
$errorLogger = new ErrorLogger();

$consoleLogger->setNextLogger($fileLogger);
$fileLogger->setNextLogger($errorLogger);

// İşlemi gerçekleştirmek için zincirin başındaki Logger kullanılır
$consoleLogger->logMessage('Console', 'This message will be logged in console.');
$consoleLogger->logMessage('File', 'This message will be logged in file.');
$consoleLogger->logMessage('Error', 'This message will be logged in error log.');

?>
```

Bu örnekte, Logger soyut sınıfı, zincirdeki nesneler arasındaki temel işlevleri içerir. ConsoleLogger, FileLogger ve ErrorLogger sınıfları, her biri zincirdeki bir sonraki nesneyi ayarlamak için setNextLogger yöntemini uygular. canHandleMessage yöntemi, her Logger nesnesinin hangi tür mesajları işleyebileceğini belirlerken, writeMessage yöntemi, Logger nesnesinin mesajı nasıl işleyeceğini belirler.

Son olarak, zincirin oluşturulması ve işlemin gerçekleştirilmesi için örnek bir kod yazılmıştır. Zincir, ConsoleLogger, FileLogger ve ErrorLogger nesneleri tarafından oluşturulur ve zincirin başındaki ConsoleLogger nesnesi kullanılarak logMessage yöntemi çağrılır.

Örnekte, eğer mesaj 'Console' ise ConsoleLogger nesnesi tarafından işlenecek, 'File' ise FileLogger nesnesi tarafından, 'Error' ise ErrorLogger nesnesi tarafından işlenecektir. Zincir boyunca ilerlenirken, her Logger nesnesi canHandleMessage yöntemini kullanarak mesajın kendi işlevselliğine uygun olup olmadığını kontrol eder. Eğer uygun değilse, mesaj zincirdeki bir sonraki Logger nesnesine aktarılır.

Bu örnek, PHP dilinde Chain of Responsibility Pattern kullanımını açıklamak için basit bir şekilde tasarlanmıştır. Gerçek hayatta daha karmaşık senaryolarda, zincirdeki nesneler arasında daha fazla bağımlılık olabilir ve zincirin oluşturulması daha karmaşık hale gelebilir. Ancak, bu desen, bu tür senaryolarda bile faydalıdır ve kodun yeniden kullanılabilirliğini ve esnekliğini artırabilir.