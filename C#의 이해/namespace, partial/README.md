# namespace

C#에서의 가장 최소 단위는 객체(object)를 클래스라고 설명했다.

실행 함수(Main)을 사용하더라도 그 함수는 반드시 클래스에 포함되어야 한다.

즉, 함수 만을 사용할 수 없다.

그래서 우리가 프로그램을 다루다 보면 많은 라이브러리를 연결하고 많은 소스를 작성하게 된다.

그럴 경우, 클래스 명을 모두 다르게 작성할 수 있을까? 참고로 클래스는 오버로드(overload- 같은 이름의 다른 처리)가 적용되지 않는다.

같은 이름의 클래스를 작성하면 반드시 에러가 발생한다.
![image](https://user-images.githubusercontent.com/65186857/173243522-1bda01f4-f290-4d07-9f8b-69215f0926b3.png)

그렇다면 우리가 프로그램을 작성할 때는 그것을 조심하게 작성한다고 해도, 오픈 라이브러리를 연결해 쓸때, 그 라이브러리 안에 있는 클래스 명이 절대 중복되지 않을까? 아니다.
그럼 우리는 라이브러리를 연결해서 사용해야 하는데 클래스가 중복되어 실행되지 않을 수 있다.

그것을 방지하기 위해 namespace가 있다.

```

using System;
// Test1의 이름인 namespace
namespace Test1
{
  // Node 클래스
  class Node
  {
    // 콘솔 출력 함수
    public void Print()
    {
      // 콘솔 출력
      Console.WriteLine("Test1.Node");
    }
  }
}
// Test2의 이름인 namespace
namespace Test2
{
  // Node 클래스
  class Node
  {
    // 콘솔 출력 함수
    public void Print()
    {
      // 콘솔 출력
      Console.WriteLine("Test2.Node");
    }
  }
}
// Example의 이름인 namespace
namespace Example
{
  // 실행 함수가 있는 클래스
  class Program
  {
    // 실행 함수
    static void Main(string[] args)
    {
      // Test1의 namespace 안에 있는 Node 클래스
      var test1 = new Test1.Node();
      // 함수 실행
      test1.Print();
      // Test2의 namespace 안에 있는 Node 클래스
      var test2 = new Test2.Node();
      // 함수 실행
      test2.Print();
 
      // 아무 키나 누르시면 종료합니다.
      Console.WriteLine("Press any key...");
      Console.ReadLine();
    }
  }
}


```


namespace를 두개로 나누어서 class를 생성하면 같은 class 이름이라도 생성이 가능하다.

정확히는 Test1.Node 이름과 Test2.Node 이름이기 때문에 다른 이름이다.

이렇게 각자의 namespace를 유니크로 지정해 놓으면 다른 라이브러리와 클래스 이름이 충돌할 일이 줄어든다.


# Partial

partial class는 C# 2.0에 도입된 기능으로 클래스를 여러 파일에 정의할 수 있다.
클래스의 내용을 다른 파일로 분할할 수 있지만 논리적으로는 하나이다. 응용 프로그램이 컴파일될 때 분할된 파일이 결합되기 때문이다.

클래스를 여러 파일로 분할하려면 partial키워드를 사용하여 Partial Class로 정의한다.

## Partial Class 예제

다음 예제는 Partial Class를 구현하는 방법이다. Person.cs라는 클래스 파일을 프로젝트에 추가하고 아래 소스코드를 Person.cs클래스 파일에 붙여넣는다.

![image](https://user-images.githubusercontent.com/65186857/173243868-a1e96cd0-22a1-4e5f-8fe9-a552acf79a3f.png)

```

partial class Person
{
  // 필드
  private string _name;
  private int _age;

  // 프로퍼티
  public string Name
  {
    get { return _name; }
    set { _name = value; }
  }

  public int Age
  {
    get { return _age; }
    set { _age = value; }
  }

  // 메서드
  public void DisplayPersonInfo()
  {
    Console.WriteLine("Name: " + _name + " / Age: " + _age);
  }
}

```
Person 클래스는 partial 키워드로 정의되었으며, 2개의 private 필드, 2개의 public 프로퍼티, 1개의 public 메서드가 존재한다.
Main() 메서드가 존재하는 클래스 파일에서 Person클래스의 객체를 생성하고 필드에 값을 설정한다.


```

class Program
{
  static void Main(string[] args)
  {
    Person person = new Person();

    person.Name = "마이콜";
    person.Age = 20;

    person.DisplayPersonInfo();
  }
}

```

### 실행 결과
```
Name: 마이콜 / Age: 20
```

이제 Person 클래스의 필드, 프로퍼티, 메서드를 파일별로 관리하기 위해 세 개의 파일로 분할합니다.
다음은 필드를 관리하는 PartialPersonField.cs파일이다.

```
partial class Person
{
    // 필드
    private string _name;
    private int _age;
}
```

다음은 프로퍼티를 관리하는 PartialPersonProperty.cs  파일이다.
```
partial class Person
{
  // 프로퍼티
  public string Name
  {
    get { return _name; }
    set { _name = value; }
  }
  
  public int Age
  {
    get { return _age; }
    set { _age = value; }
  }
}
```

다음은 메서드를 관리하는 PartialPersonMethod.cs 파일이다.
```
partial class Person
{
  // 메서드
  public void DisplayPersonInfo()
  {
    Console.WriteLine("Name: " + _name + " / Age: " + _age);
  }
}
```

파일 분할 작업이 완료되었으므로 Person.cs 파일을 제거한다.
![image](https://user-images.githubusercontent.com/65186857/173244020-b9d1b76a-bb8a-4207-ab7c-11e1618be3b5.png)

##### 프로그램을 실행하면 실행 결과가 동일한 것을 확인할 수 있으며, 분할된 파일이 하나로 동작한다는 것을 알 수 있다.


### Partial Class 주의사항

#### 첫번째

분할된 파일은 모두 Partial 키워드를 사용해야 한다. 다음 예제처럼 특정 파일에서 partial 키워드를 작성하지 않으면 컴파일 에러가 발생한다.

```
partial class Person
{
}

partial class Person
{
}

// partial 키워드가 없으므로 컴파일 에러가 발생합니다.
class Person
{
}
```

#### 두번째

분할된 파일은 모두 동일한 접근 지정자를 가져야 한다. 다음 예제처럼 접근 지정자가 다른 경우 충돌이 발생한다.
```
public partial class Person
{
}

public partial class Person
{
}

// 접근 지정자가 다르므로 컴파일 에러가 발생합니다.
protected class Person
{
}
```

#### 세번째
C#은 다중 상속을 지원하지 않는다. 그러므로 Partial 클래스의 부모 클래스가 다른 경우 컴파일 에러가 발생한다.
```
public class A
{
}

public class B
{
}

public partial class Person : A
{
}

public partial class Person : B
{
```

#### 네번째
Partial 클래스는 다음 예제처럼 Partial 별로 인터페이스를 구현할 수 있다.
```
public interface A
{
  void showA();
}

public interface B
{
  void showB();
}

public partial class Person : A
{
  public void showA()
  {
    // showA() 메서드 구현
  }
}

public partial class Person : B
{
  public void showB()
  {
    // showB() 메서드 구현
  }
}
```

##### 정리
❗ Partial 키워드를 사용하여 클래스를 여러 파일로 분할할 수 있다.
❗ 큰 클래스를 여러 파일로 분할하여 여러 개발자가 동시에 작업할 수 있다.
❗ Partial 메서드는 C# 9.0 버전부터 사용할 수 있다.
