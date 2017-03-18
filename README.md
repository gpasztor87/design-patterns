# Design-patterns

Singleton pattern
------------

A singleton desing pattern egy olyan tervezési minta, amely egy objektumra korlátozza egy osztály létrehozható példányainak a számát.
Gyakran előfordul, hogy egy osztályt úgy kell megírni, hogy egyetlen példány lehet belőle. Az objektumorientált paradigmából jól ismert, hogy egy osztályból példányt a konstruktorán keresztül lehet készíteni.

Ha van publikus konstruktor az osztályban, akkor akárhány példány készíthető belőle.
Tehát publikus konstruktora nem lehet a singletonnak.
Viszont ha nincs konstruktor, akkor nem hozható létre a példány, amin keresztül meghívhatjuk a metódusait. A megoldást az osztályszintű (statikus) metódusok jelentik. Ezeket akkor is meg lehet hívni, ha nincs példány.

A singletonnak van egy olyan osztályszintű metódusa, amely minden hívójának ugyanazt az objektumot adja vissza. Ennek a neve konvenció szerint `getInstance` szokott lenni.

Természetesen ezt a példányt is létre kell hozni. Ehhez egy privát konstruktort kell készíteni, amit a `getInstance` metódus meghívhat.

**Pédakód**

```php

final class President
{
    private static $instance;

    private function __construct()
    {
        // Hide the constructor
    }

    public static function getInstance(): President
    {
        if (!self::$instance) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    private function __clone()
    {
        // Disable cloning
    }

    private function __wakeup()
    {
        // Disable unserialize
    }
}
```

Hívása a következőképp történik:
```php
$president1 = President::getInstance();
$president2 = President::getInstance();

var_dump($president1 === $president2); // true

```

