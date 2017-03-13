![Design Patterns For Humans](https://cloud.githubusercontent.com/assets/11269635/23065273/1b7e5938-f515-11e6-8dd3-d0d58de6bb9a.png)

***
<p align="center">
🎉 디자인 패턴 초간단 설명! 🎉
</p>
<p align="center">
생각을 쉽게 흔들 수 있는 주제. 가능한 <i>가장 단순한</i> 설명으로 당신의(그리고 아마도 나의) 뇌리에 깊숙히 박히도록 노력할 것입니다.
</p>
***

읽기에 앞서
=================

오역이 있을 수 있으며, 번역이 힘든 부분은 의역을 했습니다 만약 오타나 오역으로 인해 수정이 필요한 부분이나 이해가 어려운 내용이 있다면 [Issue](https://github.com/classtinginc/design-patterns-for-humans-ko/issues)에 글 남겨주세요

🚀 소개(Introduction)
=================

디자인 패턴은 되풀이되는 문제에 대한 해결책 입니다. **특정 문제를 해결하는 방법에 대한 지침**. 클래스나 패키지 또는 라이브러리 같이 응용프로그램에 연결하여 저절로 해결되는 것을 말하는 것이 아닙니다. 이는 특정 상황에서 발생하는 특정 문제를 해결하는 방법에 대한 지침입니다  

> 되풀이 되는 문제에 대한 디자인 패턴 해결책; 특정 문제를 해결하는 방법에 대한 지침

위키피디아는 다음과 같이 기술합니다

> 소프트웨어 공학에서 소프트웨어 디자인 패턴은 주어진 상황에서 공통적으로 발생하는 문제에 대한 일반적으로 재사용 가능한 해결법을 의미합니다. 소프트웨어 디자인 패턴은 소스나 기계어로 곧바로 변환 될 수 있는 완성된 디자인은 아닙니다. 그것은 문제를 해결 하기 위해 여러 상황에서 사용될 수 있는 설명 또는 템플릿입니다 

⚠️ 주의(Be Careful)
-----------------
- 디자인 패턴은 모든 문제에 대한 특효약이 아닙니다 
- 강요하지 마세요. 안좋은 일이 발생할 수 있습니다. 디자인 패턴은 문제를 **해결**하기 위한 솔루션이지 문제를 **찾기** 위한 해결책이 아님을 염두에 두세요. 그러므로 너무 오래 생각하지 마세요
- 올바른 방법으로 제대로 사용한다면, 구원자가 될 수 있을 겁니다. 그렇지 않으면 코드를 엉망으로 만드는 결과를 초래 할 수 있습니다

디자인 패턴의 유형(Types of Design Patterns)
-----------------

* [생성(Creational)](#creational-design-patterns)
* [구조(Structural)](#structural-design-patterns)
* [행동(Behavioral)](#behavioral-design-patterns)


생성 디자인 패턴(Creational Design Patterns)
========================================

쉽게 말해
> 생성 패턴은 객체 또는 관련 객체의 그룹을 어떻게 인스턴스화하는지에 초점을 맞춥니다.

위키피디아에서는
> 소프트웨어 공학에서 생성 디자인 패턴은 객체 생성 메커니즘을 다루는 디자인 패턴으로, 상황에 적합한 방식으로 객체를 생성하려 합니다. 객체 생성의 기본 형태는 설계 문제 또는 설계의 복잡성을 증가시킬 수 있습니다. 생성 디자인 패턴은 어떻게든 객체 생성을 제어함으로써 이러한 문제를 해결합니다.
 
 * [단순 팩토리(Simple Factory)](#-simple-factory)
 * [팩토리 메소드(Factory Method)](#-factory-method)
 * [추상 팩토리(Abstract Factory)](#-abstract-factory)
 * [빌더(Builder)](#-builder)
 * [프로토타입(Prototype)](#-prototype)
 * [싱글톤(Singleton)](#-singleton)
 
🏠 단순 팩토리(Simple Factory)
--------------
실세계 예제
> 자, 당신이 집을 짓는 중에 문이 필요하다고 생각해 봅시다. 당신이 문이 필요할 때마다 목수 옷을 입고 문을 손수 만들어야 한다면, 집안은 엉망진창일 것입니다. 대신, 공장에서 만들어진 문을 가져올 수 있습니다.

쉽게 말해
> 단순 팩토리는 클라이언트에게 인스턴스 생성 로직을 노출시키지 않고 단순히 클라이언트 인스턴스를 생성합니다

위키피디아에서는
> 객체 지향 프로그래밍(OOP)에서 팩토리는 다른 객체를 생성하기 위한 또다른 객체입니다. 공식적으로 팩토리는 "new"로 가정되는 메서드 호출을 통해 다양한 프로토타입 또는 클래스의 객체를 반환하는 함수 또는 메서드입니다. 

**프로그램 예제**

우선, Door 인터페이스와 Door의 구현체가 있다고 생각해 봅시다.

```php
interface Door {
    public function getWidth() : float;
    public function getHeight() : float;
}

class WoodenDoor implements Door {
    protected $width;
    protected $height;

    public function __construct(float $width, float $height) {
        $this->width = $width;
        $this->height = $height;
    }
    
    public function getWidth() : float {
        return $this->width;
    }
    
    public function getHeight() : float {
        return $this->height;
    }
}
```

그리고 나서, Door을 생성 후 리턴하는 DoorFactory를 추가합니다.

```php
class DoorFactory {
   public static function makeDoor($width, $height) : Door {
       return new WoodenDoor($width, $height);
   }
}
```

이제 다음과 같이 사용될 수 있습니다.

```php
$door = DoorFactory::makeDoor(100, 200);
echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();
```

**언제 사용해야 할까요?**

객체를 생성할 때 단지 몇개의 할당 뿐 아니라 일부 로직 또한 수반되기에, 모든 곳에서 동일한 코드를 반복하는 대신에 전용 팩토리에 그러한 것들을 넣는것이 더 좋습니다.


🏭 팩토리 메서드(Factory Method)
----------------------------

실세계 예시
> 고용 관리자의 경우를 생각해봅시다. 한 사람이 각 포지션을 모두 인터뷰하는 것은 불가능할 것입니다. 채용 공고를 바탕으로, 인터뷰 단계를 결정하고 각 단계별로 다른 사람에게 위임해야 합니다 

쉽게 말해
> 생성 로직을 하위 클래스에 위임하는 방법을 제공합니다.

위키피디아에서는
> 클래스 기반 프로그래밍에서는, 팩토리 메서드 패턴은 생성될 객체의 정확한 클래스를 지정하지 않고 객체 생성을 처리하는 팩토리 메서드를 사용하는 생성 패턴입니다. 이는 생성자를 호출하는 대신에 팩토리 메서드(인터페이스에 명세되어 하위 클래스에서 구현되거나 기본 클래스에 구현되며, 선택적으로 파생 클래스에서 대체되기도 하는)호출로 객체를 생성하여 수행됩니다.
 
 **프로그램 예제**

위의 채용 관리자 예제를 다시 봅시다. 우선, 우리에게는 Interviewer 인터페이스와 그에 대한 몇 개의 구현체가 있습니다. 
 
```php
interface Interviewer {
    public function askQuestions();
}

class Developer implements Interviewer {
    public function askQuestions() {
        echo 'Asking about design patterns!';
    }
}

class CommunityExecutive implements Interviewer {
    public function askQuestions() {
        echo 'Asking about community building';
    }
}
```

이제 `HiringManager`를 만들어 봅시다

```php
abstract class HiringManager {
    
    // Factory method
    abstract public function makeInterviewer() : Interviewer;
    
    public function takeInterview() {
        $interviewer = $this->makeInterviewer();
        $interviewer->askQuestions();
    }
}
```

이제 `HiringManager`를 상속받아 필요한 면접관을 제공 할 수 있습니다

```php
class DevelopmentManager extends HiringManager {
    public function makeInterviewer() : Interviewer {
        return new Developer();
    }
}

class MarketingManager extends HiringManager {
    public function makeInterviewer() : Interviewer {
        return new CommunityExecutive();
    }
}
```

그리고 이제 다음과 같이 사용될 수 있습니다

```php
$devManager = new DevelopmentManager();
$devManager->takeInterview(); // Output: Asking about design patterns

$marketingManager = new MarketingManager();
$marketingManager->takeInterview(); // Output: Asking about community building.
```

**언제 사용해야 할까요?**

클래스에 generic processing을 할 때 필요한 하위 클래스가 실행 중에 동적으로 결정되는 경우에 유용합니다. 다른말로 표현하면, 클라이언트가 필요한 하위 클래스를 정확히 알 수 없는 경우입니다.

🔨 추상 팩토리(Abstract Factory)
----------------

실세계 예시
> 단순 팩토리의 문 예제를 확장해봅시다. 당신은 필요하다면 나무문, 철문, PVC 문을 각각 나무문 가게, 철문 가게, PVC 가게로부터 구할 수 있습니다. 게다가 나무문을 위해선 목수, 철문을 위해서는 용접공 등 문을 설치할 서로 다른 종류의 전문기사들이 필요 할지 모릅니다. 이제 나무문은 목수, 철문은 용접공 등 문 사이에 어떤 의존성이 있음을 알 수 있습니다. 

쉽게 말해
> 팩토리들의 팩토리입니다. 개개인이 아니라 관련/종속 팩토리들을 그들의 구체적인 클래스를 지정하지 않고 함께 그룹화 하는 팩토리입니다. 
  
위키피디아에서는
> 추상 팩토리 패턴은 구체적인 클래스를 명세 없이 공통 주제를 가진 개개의 팩토리들의 그룹을 캡슐화하는 방법을 제공합니다.

**프로그램 예제**

위의 문 예제를 프로그램화 해봅시다. 우선 우리에게는 `Door` 인터페이스와 그것의 구현체가 몇개 있습니다.

```php
interface Door {
    public function getDescription();
}

class WoodenDoor implements Door {
    public function getDescription() {
        echo 'I am a wooden door';
    }
}

class IronDoor implements Door {
    public function getDescription() {
        echo 'I am an iron door';
    }
}
```
그런 다음 각 문 유형에 맞는 설치 전문가가 있습니다

```php
interface DoorFittingExpert {
    public function getDescription();
}

class Welder implements DoorFittingExpert {
    public function getDescription() {
        echo 'I can only fit iron doors';
    }
}

class Carpenter implements DoorFittingExpert {
    public function getDescription() {
        echo 'I can only fit wooden doors';
    }
}
```

이제 관련된 객체의 패밀리를 만들 수 있는 추상 팩토리가 있습니다. 즉, 나무문 팩토리는 나무문과 나무문 설치 전문가를 생성할 수 있고, 철문 팩토리는 철문과 철문 설치 전문가를 생성할 수 있습니다.

```php
interface DoorFactory {
    public function makeDoor() : Door;
    public function makeFittingExpert() : DoorFittingExpert;
}

// Wooden factory to return carpenter and wooden door
class WoodenDoorFactory implements DoorFactory {
    public function makeDoor() : Door {
        return new WoodenDoor();
    }

    public function makeFittingExpert() : DoorFittingExpert{
        return new Carpenter();
    }
}

// Iron door factory to get iron door and the relevant fitting expert
class IronDoorFactory implements DoorFactory {
    public function makeDoor() : Door {
        return new IronDoor();
    }

    public function makeFittingExpert() : DoorFittingExpert{
        return new Welder();
    }
}
```
그리고 나서 다음과 같이 활용될 수 있습니다

```php
$woodenFactory = new WoodenDoorFactory();

$door = $woodenFactory->makeDoor();
$expert = $woodenFactory->makeFittingExpert();

$door->getDescription();  // Output: I am a wooden door
$expert->getDescription(); // Output: I can only fit wooden doors

// Same for Iron Factory
$ironFactory = new IronDoorFactory();

$door = $ironFactory->makeDoor();
$expert = $ironFactory->makeFittingExpert();

$door->getDescription();  // Output: I am an iron door
$expert->getDescription(); // Output: I can only fit iron doors
```

이제 나무문 팩토리는 `목수`와 `나무문`을, 철문 팩토리는 `철문`과 `용접공`을 캡슐화함을 볼 수 있습니다. 그래서 우리는 각 생성된 문에 적합한 설치 전문가를 얻게 됩니다.

**언제 사용해야 할까요?**

단순하지 않은 생성 로직이 포함된 상호 의존성이 있을 때 사용합니다.

👷 빌더(Builder)
--------------------------------------------
실세계 예시
> 당신이 Hardee's에서 "Big Hardee"와 같은 특정 딜을 주문하였고, 그들은 *어떤 질문*없이 그것을 당신에게 넘겨줬다고 가정해보자. 이것은 단순 팩토리의 예제입니다. 하지만 생성 로직이 더 많은 단계들을 포함해야 하는 경우들도 있습니다. 예를 들어, 당신의 요구에 맞춰진 Subway 딜을 원할 경우, 당신은 어떤 빵을 원하는지, 어떤 종류의 소스를 좋아하는지, 어떤 치즈를 넣을지 등과 같은 당신만의 버거를 어떤식으로 만들지에 대한 몇개의 선택권이 있습니다. 이러한 경우에 빌더 패턴이 해결책이 될 수 있습니다.

쉽게 말해
> 생성자 오염을 피하면서 다양한 형태의 객체를 생성할 수 있도록 합니다. 여러 가지 종류의 객체가 필요할 때 유용합니다. 또는 객체 생성에 여러 단계가 포함되어 있을 때 사용됩니다.

위키피디아에서는
> 빌더 패턴은 telescoping constructor anti-pattern 에 대한 해결책을 제공하는 객체 생성 소프트웨어 디자인 패턴입니다.

telescoping constructor anti-pattern이 무엇인지 조금 더 봅시다. 한 지점 또는 다른 지점에서 우리 모두는 아래와 같은 생성자를 본적이 있습니다.
 
```php
public function __construct($size, $cheese = true, $pepperoni = true, $tomato = false, $lettuce = true) {
}
```

보시다시피 생성자의 매개변수의 수는 쉽게 많아 질 수 있고, 이로 인해 매개변수들의 배열을 이해하기 어렵게 합니다. 더우기 당신이 미래에 더 많은 옵션을 추가하고자 한다면, 이 매개변수 리스트는 계속해서 증가 할 것입니다. 이러한 현상을 telescoping constructor anti-pattern 이라 합니다.

**프로그램 예제**

정상적인 대안은 빌더 패턴을 사용하는 것입니다. 우선 우리가 만들고 싶은 햄버거가 있습니다.

```php
class Burger {
    protected $size;

    protected $cheese = false;
    protected $pepperoni = false;
    protected $lettuce = false;
    protected $tomato = false;
    
    public function __construct(BurgerBuilder $builder) {
        $this->size = $builder->size;
        $this->cheese = $builder->cheese;
        $this->pepperoni = $builder->pepperoni;
        $this->lettuce = $builder->lettuce;
        $this->tomato = $builder->tomato;
    }
}
```

이제 다음과 같이 빌더가 있습니다.

```php
class BurgerBuilder {
    public $size;

    public $cheese = false;
    public $pepperoni = false;
    public $lettuce = false;
    public $tomato = false;

    public function __construct(int $size) {
        $this->size = $size;
    }
    
    public function addPepperoni() {
        $this->pepperoni = true;
        return $this;
    }
    
    public function addLettuce() {
        $this->lettuce = true;
        return $this;
    }
    
    public function addCheese() {
        $this->cheese = true;
        return $this;
    }
    
    public function addTomato() {
        $this->tomato = true;
        return $this;
    }
    
    public function build() : Burger {
        return new Burger($this);
    }
}
```
그런 후 다음과 같이 사용될 수 있습니다.

```php
$burger = (new BurgerBuilder(14))
                    ->addPepperoni()
                    ->addLettuce()
                    ->addTomato()
                    ->build();
```

**언제 사용할까요?**

몇가지 형태의 객체가 있을 수 있을 때와 생성자 텔레스코핑을 피하고자 할 때 사용합니다. 팩토리 패턴과 다른점은 팩토리 패턴은 생성이 한 단계일 때 사용되는 반면에 빌더 패턴은 생성이 다중 단계 프로세스일 때 사용됩니다.

🐑 프로토타입(Prototype)
------------
실세계 예시
> 돌리를 기억하세요? 복제된 양! 자세한건 모르더라도, 여기서 요점은 복제에 관한 것이라는 겁니다.

쉽게 말해
> 복제를 통해 기존 객체를 기반으로 객체를 생성하는 것입니다.

위키피디아에서는
> 프로토타입 패턴은 소프트웨어 개발의 생성 디자인 패턴입니다. 생성할 객체의 유형이 새 객체를 만들기 위해 복제될 프로토타입 인스턴스에 의해 결정될 때 사용됩니다.

요컨대, 프로토타입 패턴은 객체를 처음부터 생성하고 설정하는 골치아픈 문제를 겪는 대신에 기존 객체의 사본을 생성하게 하고 당신의 필요에 맞게 변경하게 합니다.

**프로그램 예제**

PHP에서는 `clone`을 써서 쉽게 할 수 있습니다
  
```php
class Sheep {
    protected $name;
    protected $category;

    public function __construct(string $name, string $category = 'Mountain Sheep') {
        $this->name = $name;
        $this->category = $category;
    }
    
    public function setName(string $name) {
        $this->name = $name;
    }

    public function getName() {
        return $this->name;
    }

    public function setCategory(string $category) {
        $this->category = $category;
    }

    public function getCategory() {
        return $this->category;
    }
}
```

아래와 같이 복제될 수 있습니다

```php
$original = new Sheep('Jolly');
echo $original->getName(); // Jolly
echo $original->getCategory(); // Mountain Sheep

// Clone and modify what is required
$cloned = clone $original;
$cloned->setName('Dolly');
echo $cloned->getName(); // Dolly
echo $cloned->getCategory(); // Mountain sheep
```

또한 매직 메소드인 `__clone`을 사용하여 복제동작을 수정할 수 있습니다. 

**언제 사용할까요?**

기존 객체와 유사한 객체가 필요하거나 복제 작업에 비해 생성의 비용이 더 높을 때 사용합니다.

💍 싱글톤(Singleton)
------------
실세계 예시
> 한 국가에는 한명의 대통령만 있을 수 있습니다. 임무가 있을 때마다 동일한 대통령이 행동에 나섭니다. 여기서 대통령은 싱글톤입니다.

쉽게 말해
> 특정 클래스의 객체가 하나만 생성되도록 합니다

위키피디아 에서는
> 소프트웨어 공학에서 싱글톤 패턴이란, 클래스의 인스턴스화를 하나의 객체로 제한하는 소프트웨어 디자인 패턴입니다. 이는 시스템을 통틀어 작업을 조정하는데 정확히 하나의 객체만 필요할 때 유용합니다

싱글톤 패턴은 사실 anti-pattern으로 간주되며 과도한 사용은 피해야 합니다. 꼭 나쁜것은 아니며 유효한 use-case가 있을 수 있지만 당신의 어플리케이션 전역 상태를 드러내고 한곳에서 그것을 변경하면 다른 곳에 영향을 미칠 수 있으며, 디버깅하기 어렵게 하는 요인이 되기에 조심해서 사용되어야 합니다. 또 다른 안좋은 점은 코드를 단단히 결합시키는 데다가 싱글톤의 가짜(mock)를 만드는 것은 어렵습니다.

**프로그램 예제**

싱글톤을 생성하기 위해서는 생성자를 private으로 만들고, 복제를 비활성화 하고, 확장을 비활성화하고 인스턴스를 저장할 정적 변수를 생성합니다. 

```php
final class President {
    private static $instance;

    private function __construct() {
        // Hide the constructor
    }
    
    public static function getInstance() : President {
        if (!self::$instance) {
            self::$instance = new self();
        }
        
        return self::$instance;
    }
    
    private function __clone() {
        // Disable cloning
    }
}
```

이제 다음과 같이 사용하면 됩니다.

```php
$president1 = President::getInstance();
$president2 = President::getInstance();

var_dump($president1 === $president2); // true
```

Structural Design Patterns
==========================
In plain words
> Structural patterns are mostly concerned with object composition or in other words how the entities can use each other. Or yet another explanation would be, they help in answering "How to build a software component?"

Wikipedia says
> In software engineering, structural design patterns are design patterns that ease the design by identifying a simple way to realize relationships between entities.
  
 * [Adapter](#-adapter)
 * [Bridge](#-bridge)
 * [Composite](#-composite)
 * [Decorator](#-decorator)
 * [Facade](#-facade)
 * [Flyweight](#-flyweight)
 * [Proxy](#-proxy)

🔌 Adapter
-------
Real world example
> Consider that you have some pictures in your memory card and you need to transfer them to your computer. In order to transfer them you need some kind of adapter that is compatible with your computer ports so that you can attach memory card to your computer. In this case card reader is an adapter.
> Another example would be the famous power adapter; a three legged plug can't be connected to a two pronged outlet, it needs to use a power adapter that makes it compatible with the two pronged outlet.
> Yet another example would be a translator translating words spoken by one person to another

In plain words
> Adapter pattern lets you wrap an otherwise incompatible object in an adapter to make it compatible with another class.

Wikipedia says
> In software engineering, the adapter pattern is a software design pattern that allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

**Programmatic Example**

Consider a game where there is a hunter and he hunts lions.

First we have an interface `Lion` that all types of lions have to implement

```php
interface Lion {
    public function roar();
}

class AfricanLion implements Lion {
    public function roar() {}
}

class AsianLion implements Lion {
    public function roar() {}
}
```
And hunter expects any implementation of `Lion` interface to hunt.
```php
class Hunter {
    public function hunt(Lion $lion) {
    }
}
```

Now let's say we have to add a `WildDog` in our game so that hunter can hunt that also. But we can't do that directly because dog has a different interface. To make it compatible for our hunter, we will have to create an adapter that is compatible
 
```php
// This needs to be added to the game
class WildDog {
    public function bark() {}
}

// Adapter around wild dog to make it compatible with our game
class WildDogAdapter implements Lion {
    protected $dog;

    public function __construct(WildDog $dog) {
        $this->dog = $dog;
    }
    
    public function roar() {
        $this->dog->bark();
    }
}
```
And now the `WildDog` can be used in our game using `WildDogAdapter`.

```php
$wildDog = new WildDog();
$wildDogAdapter = new WildDogAdapter($wildDog);

$hunter = new Hunter();
$hunter->hunt($wildDogAdapter);
```

🚡 Bridge
------
Real world example
> Consider you have a website with different pages and you are supposed to allow the user to change the theme. What would you do? Create multiple copies of each of the pages for each of the themes or would you just create separate theme and load them based on the user's preferences? Bridge pattern allows you to do the second i.e.

![With and without the bridge pattern](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)

In Plain Words
> Bridge pattern is about preferring composition over inheritance. Implementation details are pushed from a hierarchy to another object with a separate hierarchy.

Wikipedia says
> The bridge pattern is a design pattern used in software engineering that is meant to "decouple an abstraction from its implementation so that the two can vary independently"

**Programmatic Example**

Translating our WebPage example from above. Here we have the `WebPage` hierarchy

```php
interface WebPage {
    public function __construct(Theme $theme);
    public function getContent();
}

class About implements WebPage {
    protected $theme;
    
    public function __construct(Theme $theme) {
        $this->theme = $theme;
    }
    
    public function getContent() {
        return "About page in " . $this->theme->getColor();
    }
}

class Careers implements WebPage {
   protected $theme;
   
   public function __construct(Theme $theme) {
       $this->theme = $theme;
   }
   
   public function getContent() {
       return "Careers page in " . $this->theme->getColor();
   } 
}
```
And the separate theme hierarchy
```php
interface Theme {
    public function getColor();
}

class DarkTheme implements Theme {
    public function getColor() {
        return 'Dark Black';
    }
}
class LightTheme implements Theme {
    public function getColor() {
        return 'Off white';
    }
}
class AquaTheme implements Theme {
    public function getColor() {
        return 'Light blue';
    }
}
```
And both the hierarchies
```php
$darkTheme = new DarkTheme();

$about = new About($darkTheme);
$careers = new Careers($darkTheme);

echo $about->getContent(); // "About page in Dark Black";
echo $careers->getContent(); // "Careers page in Dark Black";
```

🌿 Composite
-----------------

Real world example
> Every organization is composed of employees. Each of the employees has same features i.e. has a salary, has some responsibilities, may or may not report to someone, may or may not have some subordinates etc.

In plain words
> Composite pattern lets clients to treat the individual objects in a uniform manner.

Wikipedia says
> In software engineering, the composite pattern is a partitioning design pattern. The composite pattern describes that a group of objects is to be treated in the same way as a single instance of an object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies. Implementing the composite pattern lets clients treat individual objects and compositions uniformly.

**Programmatic Example**

Taking our employees example from above. Here we have different employee types

```php

interface Employee {
    public function __construct(string $name, float $salary);
    public function getName() : string;
    public function setSalary(float $salary);
    public function getSalary() : float;
    public function getRoles()  : array;
}

class Developer implements Employee {

    protected $salary;
    protected $name;

    public function __construct(string $name, float $salary) {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName() : string {
        return $this->name;
    }

    public function setSalary(float $salary) {
        $this->salary = $salary;
    }

    public function getSalary() : float {
        return $this->salary;
    }

    public function getRoles() : array {
        return $this->roles;
    }
}

class Designer implements Employee {

    protected $salary;
    protected $name;

    public function __construct(string $name, float $salary) {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName() : string {
        return $this->name;
    }

    public function setSalary(float $salary) {
        $this->salary = $salary;
    }

    public function getSalary() : float {
        return $this->salary;
    }

    public function getRoles() : array {
        return $this->roles;
    }
}
```

Then we have an organization which consists of several different types of employees

```php
class Organization {
    
    protected $employees;

    public function addEmployee(Employee $employee) {
        $this->employees[] = $employee;
    }

    public function getNetSalaries() : float {
        $netSalary = 0;

        foreach ($this->employees as $employee) {
            $netSalary += $employee->getSalary();
        }

        return $netSalary;
    }
}
```

And then it can be used as

```php
// Prepare the employees
$john = new Developer('John Doe', 12000);
$jane = new Designer('Jane', 10000);

// Add them to organization
$organization = new Organization();
$organization->addEmployee($john);
$organization->addEmployee($jane);

echo "Net salaries: " . $organization->getNetSalaries(); // Net Salaries: 22000
```

☕ Decorator
-------------

Real world example

> Imagine you run a car service shop offering multiple services. Now how do you calculate the bill to be charged? You pick one service and dynamically keep adding to it the prices for the provided services till you get the final cost. Here each type of service is a decorator.

In plain words
> Decorator pattern lets you dynamically change the behavior of an object at run time by wrapping them in an object of a decorator class.

Wikipedia says
> In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern.

**Programmatic Example**

Lets take coffee for example. First of all we have a simple coffee implementing the coffee interface

```php
interface Coffee {
    public function getCost();
    public function getDescription();
}

class SimpleCoffee implements Coffee {

    public function getCost() {
        return 10;
    }

    public function getDescription() {
        return 'Simple coffee';
    }
}
```
We want to make the code extensible to allow options to modify it if required. Lets make some add-ons (decorators)
```php
class MilkCoffee implements Coffee {
    
    protected $coffee;

    public function __construct(Coffee $coffee) {
        $this->coffee = $coffee;
    }

    public function getCost() {
        return $this->coffee->getCost() + 2;
    }

    public function getDescription() {
        return $this->coffee->getDescription() . ', milk';
    }
}

class WhipCoffee implements Coffee {

    protected $coffee;

    public function __construct(Coffee $coffee) {
        $this->coffee = $coffee;
    }

    public function getCost() {
        return $this->coffee->getCost() + 5;
    }

    public function getDescription() {
        return $this->coffee->getDescription() . ', whip';
    }
}

class VanillaCoffee implements Coffee {

    protected $coffee;

    public function __construct(Coffee $coffee) {
        $this->coffee = $coffee;
    }

    public function getCost() {
        return $this->coffee->getCost() + 3;
    }

    public function getDescription() {
        return $this->coffee->getDescription() . ', vanilla';
    }
}

```

Lets make a coffee now

```php
$someCoffee = new SimpleCoffee();
echo $someCoffee->getCost(); // 10
echo $someCoffee->getDescription(); // Simple Coffee

$someCoffee = new MilkCoffee($someCoffee);
echo $someCoffee->getCost(); // 12
echo $someCoffee->getDescription(); // Simple Coffee, milk

$someCoffee = new WhipCoffee($someCoffee);
echo $someCoffee->getCost(); // 17
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip

$someCoffee = new VanillaCoffee($someCoffee);
echo $someCoffee->getCost(); // 20
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip, vanilla
```

📦 Facade
----------------

Real world example
> How do you turn on the computer? "Hit the power button" you say! That is what you believe because you are using a simple interface that computer provides on the outside, internally it has to do a lot of stuff to make it happen. This simple interface to the complex subsystem is a facade.

In plain words
> Facade pattern provides a simplified interface to a complex subsystem.

Wikipedia says
> A facade is an object that provides a simplified interface to a larger body of code, such as a class library.

**Programmatic Example**
Taking our computer example from above. Here we have the computer class

```php
class Computer {

    public function getElectricShock() {
        echo "Ouch!";
    }

    public function makeSound() {
        echo "Beep beep!";
    }

    public function showLoadingScreen() {
        echo "Loading..";
    }

    public function bam() {
        echo "Ready to be used!";
    }

    public function closeEverything() {
        echo "Bup bup bup buzzzz!";
    }

    public function sooth() {
        echo "Zzzzz";
    }

    public function pullCurrent() {
        echo "Haaah!";
    }
}
```
Here we have the facade
```php
class ComputerFacade
{
    protected $computer;

    public function __construct(Computer $computer) {
        $this->computer = $computer;
    }

    public function turnOn() {
        $this->computer->getElectricShock();
        $this->computer->makeSound();
        $this->computer->showLoadingScreen();
        $this->computer->bam();
    }

    public function turnOff() {
        $this->computer->closeEverything();
        $this->computer->pullCurrent();
        $this->computer->sooth();
    }
}
```
Now to use the facade
```php
$computer = new ComputerFacade(new Computer());
$computer->turnOn(); // Ouch! Beep beep! Loading.. Ready to be used!
$computer->turnOff(); // Bup bup buzzz! Haah! Zzzzz
```

🍃 Flyweight
---------

Real world example
> Did you ever have fresh tea from some stall? They often make more than one cup that you demanded and save the rest for any other customer so to save the resources e.g. gas etc. Flyweight pattern is all about that i.e. sharing.

In plain words
> It is used to minimize memory usage or computational expenses by sharing as much as possible with similar objects.

Wikipedia says
> In computer programming, flyweight is a software design pattern. A flyweight is an object that minimizes memory use by sharing as much data as possible with other similar objects; it is a way to use objects in large numbers when a simple repeated representation would use an unacceptable amount of memory.

**Programmatic example**
Translating our tea example from above. First of all we have tea types and tea maker

```php
// Anything that will be cached is flyweight. 
// Types of tea here will be flyweights.
class KarakTea {
}

// Acts as a factory and saves the tea
class TeaMaker {
    protected $availableTea = [];

    public function make($preference) {
        if (empty($this->availableTea[$preference])) {
            $this->availableTea[$preference] = new KarakTea();
        }

        return $this->availableTea[$preference];
    }
}
```

Then we have the `TeaShop` which takes orders and serves them

```php
class TeaShop {
    
    protected $orders;
    protected $teaMaker;

    public function __construct(TeaMaker $teaMaker) {
        $this->teaMaker = $teaMaker;
    }

    public function takeOrder(string $teaType, int $table) {
        $this->orders[$table] = $this->teaMaker->make($teaType);
    }

    public function serve() {
        foreach($this->orders as $table => $tea) {
            echo "Serving tea to table# " . $table;
        }
    }
}
```
And it can be used as below

```php
$teaMaker = new TeaMaker();
$shop = new TeaShop($teaMaker);

$shop->takeOrder('less sugar', 1);
$shop->takeOrder('more milk', 2);
$shop->takeOrder('without sugar', 5);

$shop->serve();
// Serving tea to table# 1
// Serving tea to table# 2
// Serving tea to table# 5
```

🎱 Proxy
-------------------
Real world example
> Have you ever used an access card to go through a door? There are multiple options to open that door i.e. it can be opened either using access card or by pressing a button that bypasses the security. The door's main functionality is to open but there is a proxy added on top of it to add some functionality. Let me better explain it using the code example below.

In plain words
> Using the proxy pattern, a class represents the functionality of another class.

Wikipedia says
> A proxy, in its most general form, is a class functioning as an interface to something else. A proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked.

**Programmatic Example**
Taking our security door example from above. Firstly we have the door interface and an implementation of door

```php
interface Door {
    public function open();
    public function close();
}

class LabDoor implements Door {
    public function open() {
        echo "Opening lab door";
    }

    public function close() {
        echo "Closing the lab door";
    }
}
```
Then we have a proxy to secure any doors that we want
```php
class Security {
    protected $door;

    public function __construct(Door $door) {
        $this->door = $door;
    }

    public function open($password) {
        if ($this->authenticate($password)) {
            $this->door->open();
        } else {
        	echo "Big no! It ain't possible.";
        }
    }

    public function authenticate($password) {
        return $password === '$ecr@t';
    }

    public function close() {
        $this->door->close();
    }
}
```
And here is how it can be used
```php
$door = new Security(new LabDoor());
$door->open('invalid'); // Big no! It ain't possible.

$door->open('$ecr@t'); // Opening lab door
$door->close(); // Closing lab door
```
Yet another example would be some sort of data-mapper implementation. For example, I recently made an ODM (Object Data Mapper) for MongoDB using this pattern where I wrote a proxy around mongo classes while utilizing the magic method `__call()`. All the method calls were proxied to the original mongo class and result retrieved was returned as it is but in case of `find` or `findOne` data was mapped to the required class objects and the object was returned instead of `Cursor`.

Behavioral Design Patterns
==========================

In plain words
> It is concerned with assignment of responsibilities between the objects. What makes them different from structural patterns is they don't just specify the structure but also outline the patterns for message passing/communication between them. Or in other words, they assist in answering "How to run a behavior in software component?"

Wikipedia says
> In software engineering, behavioral design patterns are design patterns that identify common communication patterns between objects and realize these patterns. By doing so, these patterns increase flexibility in carrying out this communication.

* [Chain of Responsibility](#-chain-of-responsibility)
* [Command](#-command)
* [Iterator](#-iterator)
* [Mediator](#-mediator)
* [Memento](#-memento)
* [Observer](#-observer)
* [Visitor](#-visitor)
* [Strategy](#-strategy)
* [State](#-state)
* [Template Method](#-template-method)

🔗 Chain of Responsibility
-----------------------

Real world example
> For example, you have three payment methods (`A`, `B` and `C`) setup in your account; each having a different amount in it. `A` has 100 USD, `B` has 300 USD and `C` having 1000 USD and the preference for payments is chosen as `A` then `B` then `C`. You try to purchase something that is worth 210 USD. Using Chain of Responsibility, first of all account `A` will be checked if it can make the purchase, if yes purchase will be made and the chain will be broken. If not, request will move forward to account `B` checking for amount if yes chain will be broken otherwise the request will keep forwarding till it finds the suitable handler. Here `A`, `B` and `C` are links of the chain and the whole phenomenon is Chain of Responsibility.

In plain words
> It helps building a chain of objects. Request enters from one end and keeps going from object to object till it finds the suitable handler.

Wikipedia says
> In object-oriented design, the chain-of-responsibility pattern is a design pattern consisting of a source of command objects and a series of processing objects. Each processing object contains logic that defines the types of command objects that it can handle; the rest are passed to the next processing object in the chain.

**Programmatic Example**

Translating our account example above. First of all we have a base account having the logic for chaining the accounts together and some accounts

```php
abstract class Account {
    protected $successor;
    protected $balance;

    public function setNext(Account $account) {
        $this->successor = $account;
    }
    
    public function pay(float $amountToPay) {
        if ($this->canPay($amountToPay)) {
            echo sprintf('Paid %s using %s' . PHP_EOL, $amount, get_called_class());
        } else if ($this->successor) {
            echo sprintf('Cannot pay using %s. Proceeding ..' . PHP_EOL, get_called_class());
            $this->successor->pay($amountToPay);
        } else {
            throw Exception('None of the accounts have enough balance');
        }
    }
    
    public function canPay($amount) : bool {
        return $this->balance <= $amount;
    }
}

class Bank extends Account {
    protected $balance;

    public function __construct(float $balance) {
        $this->$balance = $balance;
    }
}

class Paypal extends Account {
    protected $balance;

    public function __construct(float $balance) {
        $this->$balance = $balance;
    }
}

class Bitcoin extends Account {
    protected $balance;

    public function __construct(float $balance) {
        $this->$balance = $balance;
    }
}
```

Now let's prepare the chain using the links defined above (i.e. Bank, Paypal, Bitcoin)

```php
// Let's prepare a chain like below
//      $bank->$paypal->$bitcoin
//
// First priority bank
//      If bank can't pay then paypal
//      If paypal can't pay then bit coin

$bank = new Bank(100);          // Bank with balance 100
$paypal = new Paypal(200);      // Paypal with balance 200
$bitcoin = new Bitcoin(300);    // Bitcoin with balance 300

$bank->setNext($paypal);
$paypal->setNext($bitcoin);

// Let's try to pay using the first priority i.e. bank
$bank->pay(259);

// Output will be
// ==============
// Cannot pay using bank. Proceeding ..
// Cannot pay using paypal. Proceeding ..: 
// Paid 259 using Bitcoin!
```

👮 Command
-------

Real world example
> A generic example would be you ordering a food at restaurant. You (i.e. `Client`) ask the waiter (i.e. `Invoker`) to bring some food (i.e. `Command`) and waiter simply forwards the request to Chef (i.e. `Receiver`) who has the knowledge of what and how to cook. 
> Another example would be you (i.e. `Client`) switching on (i.e. `Command`) the television (i.e. `Receiver`) using a remote control (`Invoker`).

In plain words
> Allows you to encapsulate actions in objects. The key idea behind this pattern is to provide the means to decouple client from receiver.

Wikipedia says
> In object-oriented programming, the command pattern is a behavioral design pattern in which an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

**Programmatic Example**

First of all we have the receiver that has the implementation of every action that could be performed
```php
// Receiver
class Bulb {
    public function turnOn() {
        echo "Bulb has been lit";
    }
    
    public function turnOff() {
        echo "Darkness!";
    }
}
```
then we have an interface that each of the commands are going to implement and then we have a set of commands
```php
interface Command {
    public function execute();
    public function undo();
    public function redo();
}

// Command
class TurnOn implements Command {
    protected $bulb;
    
    public function __construct(Bulb $bulb) {
        $this->bulb = $bulb;
    }
    
    public function execute() {
        $this->bulb->turnOn();
    }
    
    public function undo() {
        $this->bulb->turnOff();
    }
    
    public function redo() {
        $this->execute();
    }
}

class TurnOff implements Command {
    protected $bulb;
    
    public function __construct(Bulb $bulb) {
        $this->bulb = $bulb;
    }
    
    public function execute() {
        $this->bulb->turnOff();
    }
    
    public function undo() {
        $this->bulb->turnOn();
    }
    
    public function redo() {
        $this->execute();
    }
}
```
Then we have an `Invoker` with whom the client will interact to process any commands
```php
// Invoker
class RemoteControl {
    
    public function submit(Command $command) {
        $command->execute();
    }
}
```
Finally let's see how we can use it in our client
```php
$bulb = new Bulb();

$turnOn = new TurnOnCommand($bulb);
$turnOff = new TurnOffCommand($bulb);

$remote = new RemoteControl();
$remoteControl->submit($turnOn); // Bulb has been lit!
$remoteControl->submit($turnOff); // Darkness!
```

Command pattern can also be used to implement a transaction based system. Where you keep maintaining the history of commands as soon as you execute them. If the final command is successfully executed, all good otherwise just iterate through the history and keep executing the `undo` on all the executed commands. 

➿ Iterator
--------

Real world example
> An old radio set will be a good example of iterator, where user could start at some channel and then use next or previous buttons to go through the respective channels. Or take an example of MP3 player or a TV set where you could press the next and previous buttons to go through the consecutive channels or in other words they all provide an interface to iterate through the respective channels, songs or radio stations.  

In plain words
> It presents a way to access the elements of an object without exposing the underlying presentation.

Wikipedia says
> In object-oriented programming, the iterator pattern is a design pattern in which an iterator is used to traverse a container and access the container's elements. The iterator pattern decouples algorithms from containers; in some cases, algorithms are necessarily container-specific and thus cannot be decoupled.

**Programmatic example**
In PHP it is quite easy to implement using SPL (Standard PHP Library). Translating our radio stations example from above. First of all we have `RadioStation`

```php
class RadioStation {
    protected $frequency;

    public function __construct(float $frequency) {
        $this->frequency = $frequency;    
    }
    
    public function getFrequency() : float {
        return $this->frequency;
    }
}
```
Then we have our iterator

```php
use Countable;
use Iterator;

class StationList implements Countable, Iterator {
    /** @var RadioStation[] $stations */
    protected $stations = [];
    
    /** @var int $counter */
    protected $counter;
    
    public function addStation(RadioStation $station) {
        $this->stations[] = $station;
    }
    
    public function removeStation(RadioStation $toRemove) {
        $toRemoveFrequency = $toRemove->getFrequency();
        $this->stations = array_filter($this->stations, function (RadioStation $station) use ($toRemoveFrequency) {
            return $station->getFrequency() !== $toRemoveFrequency;
        });
    }
    
    public function count() : int {
        return count($this->stations);
    }
    
    public function current() : RadioStation {
        return $this->stations[$this->counter];
    }
    
    public function key() {
        return $this->counter;
    }
    
    public function next() {
        $this->counter++;
    }
    
    public function rewind() {
        $this->counter = 0;
    }
    
    public function valid(): bool
    {
        return isset($this->stations[$this->counter]);
    }
}
```
And then it can be used as
```php
$stationList = new StationList();

$stationList->addStation(new Station(89));
$stationList->addStation(new Station(101));
$stationList->addStation(new Station(102));
$stationList->addStation(new Station(103.2));

foreach($stationList as $station) {
    echo $station->getFrequency() . PHP_EOL;
}

$stationList->removeStation(new Station(89)); // Will remove station 89
```

👽 Mediator
========

Real world example
> A general example would be when you talk to someone on your mobile phone, there is a network provider sitting between you and them and your conversation goes through it instead of being directly sent. In this case network provider is mediator. 

In plain words
> Mediator pattern adds a third party object (called mediator) to control the interaction between two objects (called colleagues). It helps reduce the coupling between the classes communicating with each other. Because now they don't need to have the knowledge of each other's implementation. 

Wikipedia says
> In software engineering, the mediator pattern defines an object that encapsulates how a set of objects interact. This pattern is considered to be a behavioral pattern due to the way it can alter the program's running behavior.

**Programmatic Example**

Here is the simplest example of a chat room (i.e. mediator) with users (i.e. colleagues) sending messages to each other. 

First of all, we have the mediator i.e. the chat room 

```php
// Mediator
class ChatRoom implements ChatRoomMediator {
    public function showMessage(User $user, string $message) {
        $time = date('M d, y H:i');
        $sender = $user->getName();

        echo $time . '[' . $sender . ']:' . $message;
    }
}
```

Then we have our users i.e. colleagues
```php
class User {
    protected $name;
    protected $chatMediator;

    public function __construct(string $name, ChatRoomMediator $chatMediator) {
        $this->name = $name;
        $this->chatMediator = $chatMediator;
    }
    
    public function getName() {
        return $this->name;
    }
    
    public function send($message) {
        $this->chatMediator->showMessage($this, $message);
    }
}
```
And the usage
```php
$mediator = new ChatRoom();

$john = new User('John Doe', $mediator);
$jane = new User('Jane Doe', $mediator);

$john->send('Hi there!');
$jane->send('Hey!');

// Output will be
// Feb 14, 10:58 [John]: Hi there!
// Feb 14, 10:58 [Jane]: Hey!
```

💾 Memento
-------
Real world example
> Take the example of calculator (i.e. originator), where whenever you perform some calculation the last calculation is saved in memory (i.e. memento) so that you can get back to it and maybe get it restored using some action buttons (i.e. caretaker). 

In plain words
> Memento pattern is about capturing and storing the current state of an object in a manner that it can be restored later on in a smooth manner.

Wikipedia says
> The memento pattern is a software design pattern that provides the ability to restore an object to its previous state (undo via rollback).

Usually useful when you need to provide some sort of undo functionality.

**Programmatic Example**

Lets take an example of text editor which keeps saving the state from time to time and that you can restore if you want.

First of all we have our memento object that will be able to hold the editor state

```php
class EditorMemento {
    protected $content;
    
    public function __construct(string $content) {
        $this->content = $content;
    }
    
    public function getContent() {
        return $this->content;
    }
}
```

Then we have our editor i.e. originator that is going to use memento object

```php
class Editor {
    protected $content = '';
    
    public function type(string $words) {
        $this->content = $this->content . ' ' . $words;
    }
    
    public function getContent() {
        return $this->content;
    }
    
    public function save() {
        return new EditorMemento($this->content);
    }
    
    public function restore(EditorMemento $memento) {
        $this->content = $memento->getContent();
    }
}
```

And then it can be used as 

```php
$editor = new Editor();

// Type some stuff
$editor->type('This is the first sentence.');
$editor->type('This is second.');

// Save the state to restore to : This is the first sentence. This is second.
$saved = $editor->save();

// Type some more
$editor->type('And this is third.');

// Output: Content before Saving
echo $editor->getContent(); // This is the first sentence. This is second. And this is third.

// Restoring to last saved state
$editor->restore($saved);

$editor->getContent(); // This is the first sentence. This is second.
```

😎 Observer
--------
Real world example
> A good example would be the job seekers where they subscribe to some job posting site and they are notified whenever there is a matching job opportunity.   

In plain words
> Defines a dependency between objects so that whenever an object changes its state, all its dependents are notified.

Wikipedia says
> The observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.

**Programmatic example**

Translating our example from above. First of all we have job seekers that need to be notified for a job posting
```php
class JobPost {
    protected $title;
    
    public function __construct(string $title) {
        $this->title = $title;
    }
    
    public function getTitle() {
        return $this->title;
    }
}

class JobSeeker implements Observer {
    protected $name;

    public function __construct(string $name) {
        $this->name = $name;
    }

    public function onJobPosted(JobPost $job) {
        // Do something with the job posting
        echo 'Hi ' . $this->name . '! New job posted: '. $job->getTitle();
    }
}
```
Then we have our job postings to which the job seekers will subscribe
```php
class JobPostings implements Observable {
    protected $observers = [];
    
    protected function notify(JobPost $jobPosting) {
        foreach ($this->observers as $observer) {
            $observer->onJobPosted($jobPosting);
        }
    }
    
    public function attach(Observer $observer) {
        $this->observers[] = $observer;
    }
    
    public function addJob(JobPost $jobPosting) {
        $this->notify($jobPosting);
    }
}
```
Then it can be used as
```php
// Create subscribers
$johnDoe = new JobSeeker('John Doe');
$janeDoe = new JobSeeker('Jane Doe');
$kaneDoe = new JobSeeker('Kane Doe');

// Create publisher and attach subscribers
$jobPostings = new JobPostings();
$jobPostings->attach($johnDoe);
$jobPostings->attach($janeDoe);

// Add a new job and see if subscribers get notified
$jobPostings->addJob(new JobPost('Software Engineer'));

// Output
// Hi John Doe! New job posted: Software Engineer
// Hi Jane Doe! New job posted: Software Engineer
```

🏃 Visitor
-------
Real world example
> Consider someone visiting Dubai. They just need a way (i.e. visa) to enter Dubai. After arrival, they can come and visit any place in Dubai on their own without having to ask for permission or to do some leg work in order to visit any place here; just let them know of a place and they can visit it. Visitor pattern lets you do just that, it helps you add places to visit so that they can visit as much as they can without having to do any legwork.

In plain words
> Visitor pattern lets you add further operations to objects without having to modify them.
    
Wikipedia says
> In object-oriented programming and software engineering, the visitor design pattern is a way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existing object structures without modifying those structures. It is one way to follow the open/closed principle.

**Programmatic example**

Let's take an example of a zoo simulation where we have several different kinds of animals and we have to make them Sound. Let's translate this using visitor pattern 

```php
// Visitee
interface Animal {
    public function accept(AnimalOperation $operation);
}

// Visitor
interface AnimalOperation {
    public function visitMonkey(Monkey $monkey);
    public function visitLion(Lion $lion);
    public function visitDolphin(Dolphin $dolphin);
}
```
Then we have our implementations for the animals
```php
class Monkey implements Animal {
    
    public function shout() {
        echo 'Ooh oo aa aa!';
    }

    public function accept(AnimalOperation $operation) {
        $operation->visitMonkey($this);
    }
}

class Lion implements Animal {
    public function roar() {
        echo 'Roaaar!';
    }
    
    public function accept(AnimalOperation $operation) {
        $operation->visitLion($this);
    }
}

class Dolphin implements Animal {
    public function speak() {
        echo 'Tuut tuttu tuutt!';
    }
    
    public function accept(AnimalOperation $operation) {
        $operation->visitDolphin($this);
    }
}
```
Let's implement our visitor
```php
class Speak implements AnimalOperation {
    public function visitMonkey(Monkey $monkey) {
        $monkey->shout();
    }
    
    public function visitLion(Lion $lion) {
        $lion->roar();
    }
    
    public function visitDolphin(Dolphin $dolphin) {
        $dolphin->speak();
    }
}
```

And then it can be used as
```php
$monkey = new Monkey();
$lion = new Lion();
$dolphin = new Dolphin();

$speak = new Speak();

$monkey->accept($speak);    // Ooh oo aa aa!    
$lion->accept($speak);      // Roaaar!
$dolphin->accept($speak);   // Tuut tutt tuutt!
```
We could have done this simply by having a inheritance hierarchy for the animals but then we would have to modify the animals whenever we would have to add new actions to animals. But now we will not have to change them. For example, let's say we are asked to add the jump behavior to the animals, we can simply add that by creating a new visitor i.e.

```php
class Jump implements AnimalOperation {
    public function visitMonkey(Monkey $monkey) {
        echo 'Jumped 20 feet high! on to the tree!';
    }
    
    public function visitLion(Lion $lion) {
        echo 'Jumped 7 feet! Back on the ground!';
    }
    
    public function visitDolphin(Dolphin $dolphin) {
        echo 'Walked on water a little and disappeared';
    }
}
```
And for the usage
```php
$jump = new Jump();

$monkey->accept($speak);   // Ooh oo aa aa!
$monkey->accept($jump);    // Jumped 20 feet high! on to the tree!

$lion->accept($speak);     // Roaaar!
$lion->accept($jump);      // Jumped 7 feet! Back on the ground! 

$dolphin->accept($speak);  // Tuut tutt tuutt! 
$dolphin->accept($jump);   // Walked on water a little and disappeared
```

💡 Strategy
--------

Real world example
> Consider the example of sorting, we implemented bubble sort but the data started to grow and bubble sort started getting very slow. In order to tackle this we implemented Quick sort. But now although the quick sort algorithm was doing better for large datasets, it was very slow for smaller datasets. In order to handle this we implemented a strategy where for small datasets, bubble sort will be used and for larger, quick sort.

In plain words
> Strategy pattern allows you to switch the algorithm or strategy based upon the situation.

Wikipedia says
> In computer programming, the strategy pattern (also known as the policy pattern) is a behavioural software design pattern that enables an algorithm's behavior to be selected at runtime.
 
**Programmatic example**

Translating our example from above. First of all we have our strategy interface and different strategy implementations

```php
interface SortStrategy {
    public function sort(array $dataset) : array; 
}

class BubbleSortStrategy implements SortStrategy {
    public function sort(array $dataset) : array {
        echo "Sorting using bubble sort";
         
        // Do sorting
        return $dataset;
    }
} 

class QuickSortStrategy implements SortStrategy {
    public function sort(array $dataset) : array {
        echo "Sorting using quick sort";
        
        // Do sorting
        return $dataset;
    }
}
```
 
And then we have our client that is going to use any strategy
```php
class Sorter {
    protected $sorter;
    
    public function __construct(SortStrategy $sorter) {
        $this->sorter = $sorter;
    }
    
    public function sort(array $dataset) : array {
        return $this->sorter->sort($dataset);
    }
}
```
And it can be used as
```php
$dataset = [1, 5, 4, 3, 2, 8];

$sorter = new Sorter(new BubbleSortStrategy());
$sorter->sort($dataset); // Output : Sorting using bubble sort

$sorter = new Sorter(new QuickSortStrategy());
$sorter->sort($dataset); // Output : Sorting using quick sort
```

💢 State
-----
Real world example
> Imagine you are using some drawing application, you choose the paint brush to draw. Now the brush changes its behavior based on the selected color i.e. if you have chosen red color it will draw in red, if blue then it will be in blue etc.  

In plain words
> It lets you change the behavior of a class when the state changes.

Wikipedia says
> The state pattern is a behavioral software design pattern that implements a state machine in an object-oriented way. With the state pattern, a state machine is implemented by implementing each individual state as a derived class of the state pattern interface, and implementing state transitions by invoking methods defined by the pattern's superclass.
> The state pattern can be interpreted as a strategy pattern which is able to switch the current strategy through invocations of methods defined in the pattern's interface.

**Programmatic example**

Let's take an example of text editor, it lets you change the state of text that is typed i.e. if you have selected bold, it starts writing in bold, if italic then in italics etc.

First of all we have our state interface and some state implementations

```php
interface WritingState {
    public function write(string $words);
}

class UpperCase implements WritingState {
    public function write(string $words) {
        echo strtoupper($words); 
    }
} 

class LowerCase implements WritingState {
    public function write(string $words) {
        echo strtolower($words); 
    }
}

class Default implements WritingState {
    public function write(string $words) {
        echo $words;
    }
}
```
Then we have our editor
```php
class TextEditor {
    protected $state;
    
    public function __construct(WritingState $state) {
        $this->state = $state;
    }
    
    public function setState(WritingState $state) {
        $this->state = $state;
    }
    
    public function type(string $words) {
        $this->state->write($words);
    }
}
```
And then it can be used as
```php
$editor = new TextEditor(new Default());

$editor->type('First line');

$editor->setState(new UpperCaseState());

$editor->type('Second line');
$editor->type('Third line');

$editor->setState(new LowerCaseState());

$editor->type('Fourth line');
$editor->type('Fifth line');

// Output:
// First line
// SECOND LINE
// THIRD LINE
// fourth line
// fifth line
```

📒 Template Method
---------------

Real world example
> Suppose we are getting some house built. The steps for building might look like 
> - Prepare the base of house
> - Build the walls
> - Add roof
> - Add other floors
> The order of these steps could never be changed i.e. you can't build the roof before building the walls etc but each of the steps could be modified for example walls can be made of wood or polyester or stone.
  
In plain words
> Template method defines the skeleton of how a certain algorithm could be performed, but defers the implementation of those steps to the children classes.
 
Wikipedia says
> In software engineering, the template method pattern is a behavioral design pattern that defines the program skeleton of an algorithm in an operation, deferring some steps to subclasses. It lets one redefine certain steps of an algorithm without changing the algorithm's structure.

**Programmatic Example**

Imagine we have a build tool that helps us test, lint, build, generate build reports (i.e. code coverage reports, linting report etc) and deploy our app on the test server.

First of all we have our base class that specifies the skeleton for the build algorithm
```php
abstract class Builder {
    
    // Template method 
    public final function build() {
        $this->test();
        $this->lint();
        $this->assemble();
        $this->deploy();
    }
    
    public abstract function test();
    public abstract function lint();
    public abstract function build();
    public abstract function deploy();
}
```

Then we can have our implementations

```php
class AndroidBuilder extends Builder {
    public function test() {
        echo 'Running android tests';
    }
    
    public function lint() {
        echo 'Linting the android code';
    }
    
    public function assemble() {
        echo 'Assembling the android build';
    }
    
    public function deploy() {
        echo 'Deploying android build to server';
    }
}

class IosBuilder extends Builder {
    public function test() {
        echo 'Running ios tests';
    }
    
    public function lint() {
        echo 'Linting the ios code';
    }
    
    public function assemble() {
        echo 'Assembling the ios build';
    }
    
    public function deploy() {
        echo 'Deploying ios build to server';
    }
}
```
And then it can be used as

```php
$androidBuilder = new AndroidBuilder();
$androidBuilder->build();

// Output:
// Running android tests
// Linting the android code
// Assembling the android build
// Deploying android build to server

$iosBuilder = new IosBuilder();
$iosBuilder->build();

// Output:
// Running ios tests
// Linting the ios code
// Assembling the ios build
// Deploying ios build to server
```

## 🚦 Wrap Up Folks

And that about wraps it up. I will continue to improve this, so you might want to watch/star this repository to revisit. Also, I have plans on writing the same about the architectural patterns, stay tuned for it.

## 👬 Contribution

- Report issues
- Open pull request with improvements
- Spread the word
- Reach out to me directly at kamranahmed.se@gmail.com or [@kamranahmedse](http://twitter.com/kamranahmedse)

## License
MIT © [Kamran Ahmed](http://kamranahmed.info)
