# 6.Bridge Pattern (Köprü Deseni)

Bir nesne yapısını diğerinden ayrı tutmak için kullanılan bir yapısal desendir. Bu desen, soyutlama ve gerçekleştirme arasındaki ilişkiyi ayrıştırır ve bunları birbirinden bağımsız hale getirir. Bu, bir sınıfın birden fazla farklı özellikle davranabilmesine olanak tanır ve bu özelliklerin müşteri kodu üzerindeki etkilerinin azaltılmasına yardımcı olur.

Bir köprü deseni uygulamak için, öncelikle soyutlama ve gerçekleştirme sınıflarını tanımlamalısınız. Ardından, bir arayüz veya soyut bir sınıf kullanarak bu iki sınıf arasındaki bağımlılığı azaltın. Son olarak, müşteri kodu, soyutlama sınıfını kullanarak gerçekleştirme sınıfı örneklerine erişir.

Aşağıda, PHP ile basit bir köprü deseni örneği verilmiştir. Bu örnekte, bir çizici (Renderer) soyutlaması ve iki farklı gerçekleştirme sınıfı (HTMLRenderer ve JSONRenderer) tanımlanır. Ardından, bu sınıflar arasındaki köprü, soyutlama sınıfının özelliklerini kullanarak gerçekleştirme sınıflarına erişir.

## Kod

```php
<?php

// Soyutlama sınıfı
abstract class Renderer {
    protected $data;
    
    public function __construct($data) {
        $this->data = $data;
    }
    
    abstract public function render();
}

// HTML çizici sınıfı
class HTMLRenderer extends Renderer {
    public function render() {
        $output = "<ul>";
        foreach ($this->data as $item) {
            $output .= "<li>{$item}</li>";
        }
        $output .= "</ul>";
        return $output;
    }
}

// JSON çizici sınıfı
class JSONRenderer extends Renderer {
    public function render() {
        return json_encode($this->data);
    }
}

// Köprü sınıfı
class Bridge {
    protected $renderer;
    
    public function __construct(Renderer $renderer) {
        $this->renderer = $renderer;
    }
    
    abstract public function render();
}

// HTML köprü sınıfı
class HTMLBridge extends Bridge {
    public function render() {
        return $this->renderer->render();
    }
}

// JSON köprü sınıfı
class JSONBridge extends Bridge {
    public function render() {
        return $this->renderer->render();
    }
}

// Kullanım
$data = array("apple", "banana", "orange");

$htmlRenderer = new HTMLRenderer($data);
$htmlBridge = new HTMLBridge($htmlRenderer);
$htmlOutput = $htmlBridge->render();
echo $htmlOutput;

$jsonRenderer = new JSONRenderer($data);
$jsonBridge = new JSONBridge($jsonRenderer);
$jsonOutput = $jsonBridge->render();
echo $jsonOutput;
?>
```

Bu örnekte, soyutlama sınıfı Renderer, HTMLRenderer ve JSONRenderer adlı iki gerçekleştirme sınıfı tarafından uygulanır. Köprü sınıfı Bridge, Renderer nesnesi üzerinden gerçekleştirme sınıflarına erişim sağlar. HTMLBridge ve JSONBridge sınıfları, ilgili gerçekleştirme sınıflarına erişmek için Bridge sınıfını genişletir.

Kullanım örneğinde, önce HTMLRenderer ve HTMLBridge nesneleri oluşturulur ve render() yöntemi çağrılır. Ardından, aynı işlem JSONRenderer ve JSONBridge nesneleri için yapılır. Sonuçlar, echo ifadesi kullanılarak yazdırılır.

Bu örnekte, köprü deseni, müşteri kodunda gerçekleştirme sınıflarının oluşturulmasını ve yönetilmesini önemli ölçüde azaltır. Müşteri kodu, soyutlama sınıfı olan Renderer üzerinden gerçekleştirme sınıflarına erişir, ancak gerçekleştirme sınıflarının ayrıntılarından habersizdir. Bu, daha modüler ve esnek bir kod yapısı oluşturmanıza olanak tanır.
