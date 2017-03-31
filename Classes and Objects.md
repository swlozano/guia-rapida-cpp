# Classes and Objects
## Declaring a Class
You declare a class using the keyword class followed by the name of the class, followed by a statement block {...} that encloses a set of member attributes and member functions within curly braces, and finally terminated by a semicolon ‘;’.

A class that models a human looks like the following (ignore syntactic short-comings for the moment):

```c++
class Human {
  // Member attributes: 
  string name;
  string dateOfBirth; 
  string placeOfBirth; 
  string gender;
  // Member functions:
  void Talk(string textToTalk); 
  void IntroduceSelf();
  ...
};
```

 You may often encounter the term method—these are essentially functions that are members of a class.
 
 ## An Object as an Instance of a Class
 A class is like a blueprint, and declaring a class alone has no effect on the execution of a program. The real-world avatar of a class at program execution time is an object. To use the features of a class, you typically create an instance of that class, called an object. You use that object to access its member methods and attributes.
 Creatinganobjectoftypeclass Humanissimilartocreatinganinstanceofanother
type, say double:
```c++
double pi= 3.1415; // a variable of type double
Human firstMan; // firstMan: an object of class Human
```
Alternatively,youwoulddynamicallycreateaninstanceofclass Humanusingnewas
you would for another type, say an int:
```c++
int* pointsToNum = new int; // an integer allocated dynamically
delete pointsToNum; // de-allocating memory when done using
Human* firstWoman = new Human(); // dynamically allocated Human delete firstWoman; // de-allocating memory
```

## Accessing Members Using the Dot Operator (.)

```c++
Human firstMan; // an instance i.e. object of Human
```
As the class declaration demonstrates, firstMan has attributes such as dateOfBirth
that can be accessed using the dot operator (.): 

```c++
firstMan.dateOfBirth = "1970";
```

If you have a pointer firstWoman to an instance of class Human, you can either use the pointer operator (->) to access members, or use the indirection operator (*) to reference the object following the dot operator.
```c++
Human* firstWoman = new Human(); 
(*firstWoman).IntroduceSelf();
```

A class name and member functions are declared in Pascal case, for example, IntroduceSelf(). Class member attributes are in camel case, for example, dateOfBirth.

## Accessing Members Using the Pointer Operator (->)

If an object has been instantiated on the free store using new or if you have a pointer to an object, then you use the pointer operator (->) to access the member attributes and functions:

```c++
Human* firstWoman = new Human(); 
firstWoman->dateOfBirth = "1970"; 
firstWoman->IntroduceSelf(); 
delete firstWoman;
```

## keyword public
```c++
#include <iostream>
#include <string>
using namespace std;

class Human
{
public:
   string name;
   int age;

   void IntroduceSelf()
   {
      cout << "I am " + name << " and am ";
      cout << age << " years old" << endl;
   }
};

int main()
{
   // An object of class Human with attribute name as "Adam"
   Human firstMan;
   firstMan.name = "Adam";
   firstMan.age = 30;

   // An object of class Human with attribute name as "Eve"
   Human firstWoman;
   firstWoman.name = "Eve";
   firstWoman.age = 28;
   
   firstMan.IntroduceSelf();
   firstWoman.IntroduceSelf();
}
```
## Keywords public and private
Information can be classified into at least two categories: data that we don’t mind the public knowing and data that is private.
C++ enables you to model class attributes and methods as public or private. Public class members can be used by anyone in possession of an object of the class. Private classmembers can be used only within the class (or its “friends”). C++ keywords public and private help you as the designer of a class decide what parts of a class can be invoked from outside it, for instance, from main(), and what cannot.

```c++
class Human {
  private:
  // Private member data: int age;
  string name;
  public:
  int GetAge()
  {
    return age;
  }
  void SetAge(int humansAge) {
    age = humansAge; 
   }
  // ...Other members and declarations 
};
```

## Abstraction of Data via Keyword private
C++ empowers you to decide what information remains unreachable to the outside world (that is, unavailable outside the class) via keyword private. At the same time, you have the possibility to allow controlled access to even information declared private via methods that you have declared as public. Thus your implementation of a class can abstract member information that classes and functions outside this class don’t need to have access to.

```c++
#include <iostream>
using namespace std;

class Human
{
private:
   // Private member data:
   int age;

public:
   void SetAge(int inputAge)
   {
      age = inputAge;
   }

   // Human lies about his / her age (if over 30)
   int GetAge()
   {
      if (age > 30)
         return (age - 2);
      else 
         return age;
   }
};

int main()
{
   Human firstMan;
   firstMan.SetAge(35);

   Human firstWoman;
   firstWoman.SetAge(22);

   cout << "Age of firstMan " << firstMan.GetAge() << endl;
   cout << "Age of firstWoman " << firstWoman.GetAge() << endl;

   return 0;
}
```
# Constructors
A constructor is a special function (or method) invoked during the instantiation of a class to construct an object. Just like functions, constructors can also be overloaded.
## Declaring and Implementing a Constructor
A constructor is a special function that takes the name of the class and returns no value. So,class Humanwouldhaveaconstructorthatisdeclaredlikethis:
```c++
class Human {
  public:
    Human(); // declaration of a constructor 
};
```
This constructor can be implemented either inline within the class or externally outside the class declaration. An implementation (also called definition) inside the class looks like this:

```c++
class Human {
public:
  Human() {
    // constructor code here 
    }
};
```

A variant enabling you to define the constructor outside the class’ declaration looks like this:

```c++
class Human {
public:
  Human(); // constructor declaration 
};
// constructor implementation (definition) 
Human::Human()
{
  // constructor code here
}
```
_:: is called the scope resolution operator. For example, Human::dateOfBirth is referring to variable dateOfBirth declared within the scope of class Human. ::dateOfBirth, on the other hand would refer to another variable dateOfBirth in a global scope._
## When and How to Use Constructors
A constructor is always invoked during object creation, when an instance of a class is constructed. This makes a constructor a perfect place for you to initialize class member variables such as integers, pointers, and so on to values you choose.

Using Constructors to Initialize Class Member Variables

```c++
#include <iostream>
#include <string>
using namespace std;

class Human
{
private:
   string name;
   int age;
   
public:
   Human() // constructor 
   {
      age = 1; // initialization
      cout << "Constructed an instance of class Human" << endl;
   }

   void SetName (string humansName)
   {
      name = humansName;
   }

   void SetAge(int humansAge)
   {
      age = humansAge;
   }

   void IntroduceSelf()
   {
      cout << "I am " + name << " and am ";
      cout << age << " years old" << endl;
   }
};

int main()
{
   Human firstWoman;
   firstWoman.SetName("Eve");
   firstWoman.SetAge (28);
   
   firstWoman.IntroduceSelf();
}
```

_A constructor that is invoked without arguments is called the default constructor. Programming a default constructor is optional._

## Overloading Constructors

Constructors can be overloaded just like functions.

```c++
class Human {
  public:
  Human() {
    // default constructor code here }
  Human(string humansName) {
    // overloaded constructor code here 
   }
};
```

## Constructor Parameters with Default Values

Just the same way as functions can have parameters with default values specified, so can constructors. 

```c++
class Human {
  private:
    string name; int age;
  public:
    // overloaded constructor (no default constructor) Human(string humansName, int humansAge = 25)
  {
    name = humansName;
    age = humansAge;
    cout  << "Overloaded constructor creates " << name; cout << " of age " << age << endl;
  }
  // ... other members 
 };
 ```
 
_Note that a default constructor is one that can be instantiated without arguments, and not necessarily one that doesn’t take parameters._

## Constructors with Initialization Lists

You have seen how useful constructors are in initializing member variables. Another way to initialize members is by using initialization lists. 
Thus, the initialization list is characterized by a colon (:) following the parameter declaration contained in parentheses (...), followed by an individual member variable and the value it is initialized to. 
Default Constructor That Accepts Parameters with Default Values to Set Members Using Initialization Lists

```c++
#include <iostream>
#include <string>
using namespace std;

class Human
{
private:
   int age;
   string name;

public:
   Human(string humansName = "Adam", int humansAge = 25)
        :name(humansName), age(humansAge)
   {
      cout << "Constructed a human called " << name;
      cout << ", " << age << " years old" << endl;
   }
};

int main()
{
   Human adam;
   Human eve("Eve", 18);

   return 0;
}
```

## Destructor
A destructor, like a constructor, is a special function, too. A constructor is invoked at object instantiation, and a destructor is automatically invoked when an object is destroyed.

## Declaring and Implementing a Destructor
The destructor looks like a function that takes the name of the class, yet has a tilde (~) precedingit.

```c++
class Human {
  ~Human(); // declaration of a destructor 
};
```

This destructor can either be implemented inline in the class or externally outside the class declaration. An implementation or definition inside the class looks like this:

```c++
class Human {
public:
~Human() {
  // destructor code here }
};
```

A variant enabling you to define the destructor outside the class’s declaration looks like this:

```c++
class Human {
  public:
    ~Human(); // destructor declaration 
};
// destructor definition (implementation) 
Human::~Human()
{
  // destructor code here 
}
```
 
As you can see, the declaration of the destructor differs from that of the constructor slightly in that this contains a tilde (~). The role of the destructor is, however, diametrically opposite to that of the constructor.

## When and How to Use a Destructor

A destructor is always invoked when an object of a class is destroyed when it goes out of scope or is deleted via delete. This property makes a destructor the ideal place to reset variables and release dynamically allocated memory and other resources.
Recommended the usage of std::string over a char* buffer, so that you don’t need to worry about managing memory allocation and timely deallocation yourself. std::string and other such utilities are nothing but classes themselves that make use of constructors and the destructor 

A Simple Class That Encapsulates a Character Buffer to Ensure 9 Deallocation via the Destructor

```c++
#include <iostream>
#include <string.h>
using namespace std;

class MyString
{
private:
   char* buffer;

public:
   MyString(const char* initString)  // constructor
   {
      if(initString != NULL)
      {
         buffer = new char [strlen(initString) + 1];
         strcpy(buffer, initString);
      }
      else 
         buffer = NULL;
   }

   ~MyString()
   {
      cout << "Invoking destructor, clearing up" << endl;
      if (buffer != NULL)
         delete [] buffer;
   }

   int GetLength() 
   {
      return strlen(buffer);
   }

   const char* GetString()
   {
	   return buffer;
   }
};

int main()
{
   MyString sayHello("Hello from String Class");
   cout << "String buffer in sayHello is " << sayHello.GetLength();
   cout << " characters long" << endl;

   cout << "Buffer contains: " << sayHello.GetString() << endl;
}
```

_A destructor cannot be overloaded. A class can have only one destructor. If you forget to implement a destructor, the compiler creates and invokes a dummy destructor, that is, an empty one (that does no cleanup of dynamically allocated memory)._





