# 5.Proxy Pattern (Vekil Deseni)

Bir nesneyi temsil eden bir vekil nesne oluşturarak bir nesne yerine kullanılır. Vekil nesne, özgün nesnenin yönetimini üstlenir ve onun yerine istemci tarafından kullanılır. Bu, özgün nesneyi doğrudan kullanmaktan daha uygun olabilir, örneğin, özgün nesne yüksek maliyetli olabilir, uzak bir sunucuda bulunabilir veya güvenlik nedenleriyle korunabilir.

Proxy Pattern, iki ana bileşen içerir: Özgün Nesne ve Vekil Nesne. İstemci, Vekil Nesne'ye erişim sağlar ve Vekil Nesne, istemci tarafından istenen işlemleri gerçekleştirmek için Özgün Nesne'ye yönlendirir.

## Kod

```php
interface Image
{
    public function displayImage(): void;
}

class RealImage implements Image
{
    private string $filename;

    public function __construct(string $filename)
    {
        $this->filename = $filename;
        $this->loadFromDisk();
    }

    private function loadFromDisk(): void
    {
        echo "Loading {$this->filename} from disk." . PHP_EOL;
    }

    public function displayImage(): void
    {
        echo "Displaying {$this->filename}." . PHP_EOL;
    }
}

class ProxyImage implements Image
{
    private ?RealImage $realImage = null;
    private string $filename;

    public function __construct(string $filename)
    {
        $this->filename = $filename;
    }

    public function displayImage(): void
    {
        if ($this->realImage === null) {
            $this->realImage = new RealImage($this->filename);
        }
        $this->realImage->displayImage();
    }
}

$image1 = new ProxyImage("image1.jpg");
$image2 = new ProxyImage("image2.jpg");

// the images will be loaded from disk only when necessary
$image1->displayImage(); // Loading image1.jpg from disk. Displaying image1.jpg.
$image1->displayImage(); // Displaying image1.jpg.
$image2->displayImage(); // Loading image2.jpg from disk. Displaying image2.jpg.
$image2->displayImage(); // Displaying image2.jpg.
```

Bu örnekte, RealImage sınıfı özgün nesnedir ve ProxyImage sınıfı vekil nesnedir. RealImage sınıfı, gerçek resim dosyasını yükler ve görüntüleme işlemini gerçekleştirir. ProxyImage sınıfı, gerçek resim dosyasının yüklenmesini geciktirir ve gerektiğinde RealImage sınıfını kullanarak görüntüleme işlemini gerçekleştirir. Bu, resim dosyalarının yalnızca ihtiyaç duyulduğunda yüklenmesini sağlar ve gereksiz yere kaynak kullanımını önler.