# 2.Builder Pattern (Oluşturucu Deseni)

Builder Pattern (Oluşturucu Deseni), nesne yaratma sürecini sınıflandırarak ve yapılandırarak nesnelerin karmaşık oluşturma süreçlerini basitleştirmek ve yönetmek için kullanılan bir tasarım desenidir. Bu desen, özellikle büyük nesnelerin veya nesne ağaçlarının oluşturulmasında faydalıdır.

Builder Pattern genellikle üç temel bileşenle oluşturulur:

1.Product (Ürün): Oluşturulacak nesne veya nesne ağacı.

2.Builder: Ürünün oluşturulması için kullanılacak arayüzü sağlayan sınıf. Bu arayüz genellikle ürünün özelliklerini belirleyen ve ayarlayan yöntemler içerir.

3.Director: Builder'ı kullanarak nesne oluşturma işlemini yöneten sınıf. Bu sınıf, ürünün oluşturulmasını ve yapılandırılmasını belirleyen yönergeleri sağlar.

## Kod

```php
class House
{
    private $walls;
    private $roof;
    private $windows;
    
    public function setWalls($walls)
    {
        $this->walls = $walls;
    }
    
    public function setRoof($roof)
    {
        $this->roof = $roof;
    }
    
    public function setWindows($windows)
    {
        $this->windows = $windows;
    }
}

interface HouseBuilder
{
    public function buildWalls();
    public function buildRoof();
    public function buildWindows();
    public function getHouse();
}

class BasicHouseBuilder implements HouseBuilder
{
    private $house;
    
    public function __construct()
    {
        $this->house = new House();
    }
    
    public function buildWalls()
    {
        $this->house->setWalls("basic walls");
    }
    
    public function buildRoof()
    {
        $this->house->setRoof("basic roof");
    }
    
    public function buildWindows()
    {
        $this->house->setWindows("basic windows");
    }
    
    public function getHouse()
    {
        return $this->house;
    }
}

class HouseDirector
{
    private $builder;
    
    public function __construct(HouseBuilder $builder)
    {
        $this->builder = $builder;
    }
    
    public function buildHouse()
    {
        $this->builder->buildWalls();
        $this->builder->buildRoof();
        $this->builder->buildWindows();
        
        return $this->builder->getHouse();
    }
}

// Kullanım
$basicHouseBuilder = new BasicHouseBuilder();
$houseDirector = new HouseDirector($basicHouseBuilder);
$house = $houseDirector->buildHouse();

```

Bu örnekte, "House" adlı bir "Product" (Ürün) sınıfı oluşturulmuştur. Ardından "HouseBuilder" adlı bir arayüz belirlenmiştir. "BasicHouseBuilder" adlı bir "Builder" sınıfı, "HouseBuilder" arayüzünü uygular ve "HouseDirector" adlı bir "Director" sınıfı, "Builder" nesnesi ile birlikte "House" nesnesinin oluşturulmasını yönetir.

Kullanıcı, "BasicHouseBuilder" sınıfını kullanarak bir "House" nesnesi oluşturabilir. "HouseDirector" sınıfı, "Builder" nesnesini kullanarak "House" nesnesinin oluşturulmasını yönetir. Bu sayede, "House" nesnesinin oluşturulması için gerekli olan süreç basitleştirilir ve yönetilir.

Bu örnekte, "BasicHouseBuilder" sınıfı, sadece temel bir ev oluşturabilir. Bu sınıfı, daha karmaşık evlerin oluşturulması için genişletebilirsiniz. Örneğin, "LuxuryHouseBuilder" adlı bir sınıf oluşturarak, lüks bir ev oluşturabilirsiniz.

Builder Pattern, nesne oluşturma sürecindeki karmaşıklığı azaltır ve yönetilebilir hale getirir. Bu desen, özellikle büyük nesnelerin veya nesne ağaçlarının oluşturulması için faydalıdır.
