# 4.Prototype Pattern (Prototip Deseni)

Nesnelerin kopyalarının oluşturulması için bir tasarım desenidir. Bu desen, bir nesne örneğinin yapısını ve davranışını koruyarak yeni nesne örneklerinin üretilmesine olanak sağlar.

Bu desen, özellikle nesne oluşturma işleminin maliyetli olduğu durumlarda kullanışlıdır. Örneğin, bir nesnenin oluşturulması için birçok hesaplama veya dosya okuma işlemi gerekiyorsa, bu desen kullanılarak bir kez hesaplanan nesne örneği daha sonra kopyalanabilir.

PHP'de bir örnek oluşturmak için, öncelikle kopyalanacak nesnenin bir prototipini oluşturmamız gerekir. Ardından, yeni nesne örneklerini bu prototipe dayalı olarak oluşturabiliriz. Aşağıda örnek bir PHP kodu verilmiştir:

## Kod

```php
// Prototip nesne sınıfı
class Book {
    private $title;
    private $author;
    
    public function __construct($title, $author) {
        $this->title = $title;
        $this->author = $author;
    }
    
    public function getTitle() {
        return $this->title;
    }
    
    public function getAuthor() {
        return $this->author;
    }
    
    public function setTitle($title) {
        $this->title = $title;
    }
    
    public function setAuthor($author) {
        $this->author = $author;
    }
    
    // Prototip kopyalama işlemi
    public function clone() {
        return new Book($this->title, $this->author);
    }
}

// Prototip nesne örneği
$prototype = new Book("Design Patterns", "Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides");

// Yeni nesne örnekleri oluşturma
$book1 = $prototype->clone();
$book1->setTitle("PHP Design Patterns");
$book2 = $prototype->clone();
$book2->setTitle("Python Design Patterns");

// Yeni nesneleri kullanma
echo $book1->getTitle() . " by " . $book1->getAuthor() . "<br>"; // PHP Design Patterns by Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides
echo $book2->getTitle() . " by " . $book2->getAuthor() . "<br>"; // Python Design Patterns by Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides
```

Yukarıdaki örnekte, Book sınıfı prototip olarak kullanılmaktadır. Bu sınıfın clone metodu, mevcut nesne örneğinin bir kopyasını oluşturur. clone metodunu kullanarak, yeni nesne örnekleri oluşturulur ve daha sonra bu nesnelere özel özellikler atanır. Son olarak, yeni nesneler kullanılarak çıktı oluşturulur.