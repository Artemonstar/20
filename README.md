# 20
:Код представляет собой реализацию системы управления одеждой с использованием перечислений, интерфейсов и классов в Java.

Перечисление Size
- Содержит размеры одежды (XXS, XS, S, M, L) и соответствующие им размеры в евро.
- Метод getDescription возвращает "Детский размер" для XXS и "Взрослый размер" для остальных.

Интерфейсы
- MensClothing и WomensClothing имеют метод wear(), который будет реализован в классах одежды.

Абстрактный класс Clothing
- Имеет переменные для размера, цены и цвета.
- Конструктор и абстрактный метод displayInfo(), который нужно переопределить в наследниках.

Классы одежды (TShirt, Pants, Skirt, Tie)
- Каждый класс наследует Clothing и реализует интерфейсы для обозначения, к какому типу одежды он относится.
- Реализуют метод wear для вывода информации о том, что одежда надета, и переопределяют displayInfo для показа деталей.

Класс Atelier
- Содержит методы dressWoman и dressMan, которые принимают массив одежды и выводят информацию о соответствующей одежде на основе типа (женская или мужская).

Класс Main
- В main создается массив одежды, и затем производится вызов методов ателье для отображения информации о женской и мужской одежде. 

В целом, код организует информацию о разных типах одежды, их свойствах, а также действиях, которые могут быть выполнены с ними.:


enum Size {
    XXS(32), XS(34), S(36), M(38), L(40);

    private final int euroSize;

    Size(int euroSize) {
        this.euroSize = euroSize;
    }

    public String getDescription() {
        return this == XXS ? "Детский размер" : "Взрослый размер";
    }

    public int getEuroSize() {
        return euroSize;
    }
}

interface MensClothing {
    void wear();
}

interface WomensClothing {
    void wear();
}

abstract class Clothing {
    protected Size size;
    protected double price;
    protected String color;

    public Clothing(Size size, double price, String color) {
        this.size = size;
        this.price = price;
        this.color = color;
    }

    public abstract void displayInfo();
}

class TShirt extends Clothing implements MensClothing, WomensClothing {
    public TShirt(Size size, double price, String color) {
        super(size, price, color);
    }

    @Override
    public void wear() {
        System.out.println("Надел футболку");
    }

    @Override
    public void displayInfo() {
        System.out.println("Футболка: " + size + ", " + price + ", " + color);
    }
}

class Pants extends Clothing implements MensClothing, WomensClothing {
    public Pants(Size size, double price, String color) {
        super(size, price, color);
    }

    @Override
    public void wear() {
        System.out.println("Надел брюки");
    }

    @Override
    public void displayInfo() {
        System.out.println("Брюки: " + size + ", " + price + ", " + color);
    }
}

class Skirt extends Clothing implements WomensClothing {
    public Skirt(Size size, double price, String color) {
        super(size, price, color);
    }

    @Override
    public void wear() {
        System.out.println("Надела юбку");
    }

    @Override
    public void displayInfo() {
        System.out.println("Юбка: " + size + ", " + price + ", " + color);
    }
}

class Tie extends Clothing implements MensClothing {
    public Tie(Size size, double price, String color) {
        super(size, price, color);
    }

    @Override
    public void wear() {
        System.out.println("Надел галстук");
    }

    @Override
    public void displayInfo() {
        System.out.println("Галстук: " + size + ", " + price + ", " + color);
    }
}

class Atelier {
    public void dressWoman(Clothing[] clothingArray) {
        System.out.println("Женская одежда:");
        for (Clothing clothing : clothingArray) {
            if (clothing instanceof WomensClothing) {
                clothing.displayInfo();
            }
        }
    }

    public void dressMan(Clothing[] clothingArray) {
        System.out.println("Мужская одежда:");
        for (Clothing clothing : clothingArray) {
            if (clothing instanceof MensClothing) {
                clothing.displayInfo();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Clothing[] clothingArray = {
                new TShirt(Size.M, 19.99, "Красный"),
                new Pants(Size.L, 29.99, "Синий"),
                new Skirt(Size.S, 24.99, "Черный"),
                new Tie(Size.M, 14.99, "Зеленый")
        };

        Atelier atelier = new Atelier();
        atelier.dressWoman(clothingArray);
        atelier.dressMan(clothingArray);
    }
}
