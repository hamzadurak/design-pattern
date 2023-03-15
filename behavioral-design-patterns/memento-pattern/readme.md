# 6.Memento Pattern (Anımsatıcı Deseni)

Nesnelerin iç durumlarını bir anımsatıcı aracılığıyla saklamak ve geri yüklemek için kullanılır. Bu, bir nesnenin iç
durumunu değiştirdikten sonra geri dönmek istediğinizde kullanışlıdır.

Memento Pattern, üç temel bileşenden oluşur: Originator (yaratıcı), Memento (anımsatıcı) ve Caretaker (bakıcı).

Originator, bir nesnenin iç durumunu temsil eder ve bir Memento oluşturabilir veya bir Memento'yu geri yükleyebilir.

Memento, bir Originator'un iç durumunun bir anlık görüntüsünü temsil eder ve bir Originator tarafından yaratılır ve geri
yüklenebilir.

Caretaker, Memento'ları saklar ve geri yükler.

## Kod

```php
// Originator
class Document {
    private $content;
    
    public function getContent() {
        return $this->content;
    }
    
    public function setContent($content) {
        $this->content = $content;
    }
    
    // Create memento
    public function createMemento() {
        return new Memento($this->content);
    }
    
    // Restore from memento
    public function restoreFromMemento(Memento $memento) {
        $this->content = $memento->getState();
    }
}

// Memento
class Memento {
    private $state;
    
    public function __construct($state) {
        $this->state = $state;
    }
    
    public function getState() {
        return $this->state;
    }
}

// Caretaker
class History {
    private $mementos = array();
    
    public function addMemento(Memento $memento) {
        $this->mementos[] = $memento;
    }
    
    public function getMemento($index) {
        return $this->mementos[$index];
    }
}

// Usage
$document = new Document();
$history = new History();

$document->setContent("This is the first version of the document.");
$history->addMemento($document->createMemento());

$document->setContent("This is the second version of the document.");
$history->addMemento($document->createMemento());

$document->setContent("This is the third version of the document.");
$history->addMemento($document->createMemento());

// Restore to second version
$document->restoreFromMemento($history->getMemento(1));
echo $document->getContent(); // Output: This is the second version of the document.
```

Bu örnekte, Document sınıfı Originator'ı temsil eder ve belgenin içeriğini temsil eden bir özellik içerir. Memento
sınıfı, belgenin içeriğinin bir anlık görüntüsünü temsil eder. History sınıfı, Memento'ları saklamak ve geri yüklemek
için bir Caretaker görevi görür.

Kullanım örneğinde, bir belge oluşturulur ve içeriği değiştirilir. Her değişiklik bir Memento oluşturarak History'ye
eklenilir. Ardından, üçüncü bir değişiklik yapılır ve belge yeniden kaydedilir. Son olarak, belgenin ikinci sürümü geri
yüklenir ve içerik ikinci sürümle aynı hale getirilir.

Bu örnek, Memento Pattern'in nasıl kullanılabileceğini göstermektedir. Bu desen, belirli bir nesnenin iç durumunu
saklamak ve geri yüklemek için kullanışlıdır. Bu özellikle, bir nesne üzerinde çalışırken yanlışlıkla yapılan bir
değişikliği geri almak istediğinizde faydalıdır.
