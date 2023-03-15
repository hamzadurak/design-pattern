# 4.Iterator Pattern (Yineleyici Deseni)

Nesne koleksiyonlarının elemanlarına erişim sağlamak için bir arabirim sağlayan bir tasarım desenidir. Bu desen, nesne koleksiyonlarına genel bir arayüz sağlar ve bu arayüz üzerinden koleksiyondaki elemanlar üzerinde gezinme işlemi gerçekleştirilir. Bu sayede, farklı türdeki koleksiyonlar için aynı arayüz kullanılabildiği gibi, gezinme işlemi de herhangi bir değişikliğe gerek kalmadan farklı şekillerde gerçekleştirilebilir.

## Kod

```php
// Iterator arayüzü, koleksiyon üzerinde gezinme için gerekli olan yöntemleri tanımlar
interface Iterator {
    public function hasNext();
    public function next();
}

// Koleksiyon sınıfı, elemanlarını depolar ve Iterator arayüzünü uygular
class Collection implements IteratorAggregate {
    private $items = array();

    public function addItem($item) {
        $this->items[] = $item;
    }

    public function getIterator(): Iterator {
        return new CollectionIterator($this->items);
    }
}

// Iterator sınıfı, koleksiyondaki elemanlar üzerinde gezinme işlemini gerçekleştirir
class CollectionIterator implements Iterator {
    private $items = array();
    private $index = 0;

    public function __construct($items) {
        $this->items = $items;
    }

    public function hasNext() {
        return isset($this->items[$this->index]);
    }

    public function next() {
        $item = $this->items[$this->index];
        $this->index++;
        return $item;
    }
}

// Koleksiyon nesnesi oluşturma
$collection = new Collection();
$collection->addItem('item 1');
$collection->addItem('item 2');
$collection->addItem('item 3');

// Koleksiyondaki elemanlara erişim
$iterator = $collection->getIterator();
while ($iterator->hasNext()) {
    echo $iterator->next() . "\n";
}
```

Bu örnekte, Iterator arayüzü, hasNext() ve next() yöntemlerini tanımlar. Collection sınıfı, elemanlarını depolamak için bir dizi kullanır ve getIterator() yöntemiyle Iterator nesnesini döndürür. CollectionIterator sınıfı, Iterator arayüzünü uygular ve koleksiyondaki elemanları üzerinde gezinme işlemini gerçekleştirir. Koleksiyon nesnesi oluşturulduktan sonra, getIterator() yöntemi kullanılarak Iterator nesnesi elde edilir ve hasNext() ve next() yöntemleri kullanılarak koleksiyondaki elemanlara erişilir.

Bu örnekte, $collection nesnesi oluşturulduktan sonra, addItem() yöntemi kullanılarak koleksiyona elemanlar eklenir. Daha sonra, getIterator() yöntemi kullanılarak bir Iterator nesnesi elde edilir ve while döngüsü içinde hasNext() ve next() yöntemleri kullanılarak koleksiyondaki elemanlar gezilir ve ekrana yazdırılır.

Iterator Pattern, farklı türdeki koleksiyonlar için kullanılabilen genel bir arayüz sağlar ve koleksiyondaki elemanlara erişim işlemlerini kolaylaştırır. Ayrıca, koleksiyonda herhangi bir değişiklik yapılmadan gezinme işleminin farklı şekillerde gerçekleştirilmesine olanak tanır.