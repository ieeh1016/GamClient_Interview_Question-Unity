# Virtual(가상) vs Abstract(추상) vs Interface(인터페이스)

## 1. Virtual (가상 키워드)
virtual 키워드는 메서드, 속성, 인덱서 또는 이벤트 선언을 한정하는데 사용됩니다.
패상 클래스에서 필요에 따라서 재정의(override) 할 수 있지만, 필수적으로 재정의 할 필요는 없습니다.
virtual 한정자를 사용한 클래스는 완벽한 기능을 제공할 수 있습니다.

```
public class Animal
{   
	public virtual void Speak()  
	{        
		Console.WriteLine("Nothing!");   
	}
} 

public class Dog : Animal
{    
	public override void Speak()    
	{        
		Console.WriteLine("멍멍!");    
	}
} 
Dog temp = new Dog();
temp.Speak();//멍멍!

```

## 2. abstract (추상 키워드)
abstract 키워드를 사용하면 불완전하여 파생 클래스에서 구현해야하는 클래스 및 클래스 멤버를 만들수 있습니다.
추상클래스의 사용 목적은 여러개의 파생 클래스에서 공유할 기본 클래스의 공통적인 정의를 제공하는 것입니다.
추상클래스는 인스턴스화 할 수 없습니다.

```

public abstract class Animal
{    
	public abstract void Speak();    
} 

public class Dog : Animal
{    
	public override void Speak()    
	{        
		Console.WriteLine("멍멍!");    
	}
}   
Dog temp = new Dog();  
temp.Speak();//멍멍!


```


## 3. Interface (인터페이스)
인터페이스는 abstract와 비슷하지만 멤버필드(변수)를 사용할 수 없습니다. 대신에 프로퍼티는 사용이 가능합니다.
인터페이스는 보통 여러 클래스에 공통적인 변수를 추가하기 위해서 사용합니다.

```

public interface Animal
{    
	void Speak();     
	string Name    
	{        
		get;       
		set;    
	}  
} 
class Dog : Animal
{    
	private string name;     
	public void Speak()    
	{        
		Console.WriteLine(name + "->멍멍!");    
	}     
	
	public string Name    
	{        
		get       
		{            
			return name;       
		}        
		set        
		{            
			name = value;        
		}    
	}
} 
Dog temp = new Dog();
temp.Name = "흰둥이";
temp.Speak(); //흰둥이->멍멍!


```

### 4. 결론
-Vritual은 하나의 기능을 하는 완전한 클래스이며, 파생클래스에서 상속해서 추가적인 기능추가 및 virtual 한정자가 달린 것을 재정의해서 사용가능합니다.

-Abstract는 여러개의 파생 클래스에서 공유할 기본 클래스의 공통적인 정의만 하고 ,파생클래스에서 abstract 한정자가 달린 것을 모두 재정의(필수)해야 합니다.

-Interface에서도 abstract와 비슷하지만 멤버변수를 사용할 수 없습니다.  보통 abstract는 개념적으로 계층적인 구조에서 사용이 되며(동물이나 어떤 사물의 계층적인 구조가있을때) Interface는 서로다른 계층이나 타입이라도 같은기능을 추가하고 싶을때 사용합니다.(사람이나 기계가 말을하게(speak)하는 인터페이스를 추가할때)
