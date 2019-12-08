# FINAL ⇒ notes

Created: Dec 03, 2019 3:20 PM
Reviewed: No

## Module 1

- It should never be possible to change the state of the internal of an object from outside the class or without using the internal method of the class // avoid it
- ENUM type is immutable
- if you wanna return an array list but modification is not possible then use ⇒ `java.util.Collections.unmodifiableList(...)` \\ returning copy of collections
- **Object Diagrams :**
    - Represents and existing graph of objects , or classes instances.
- 

    enum type : 
    
    public enum Day . {
    	SUNDAY , MONDAY , ... 
    }
    
    ----ASSINGMENT---
    variable of type Day here :::
    Day varialbe = Day.SUNDAY ; 

- Creating shallow copy of `ArrayList<>`

    `List<Integer> newList = new ArrayList<>(oldList)`

---

---

## Module 2

[prmr/SoftwareDesign](https://github.com/prmr/SoftwareDesign/blob/master/modules/Module-02.md)

- Class implementing an **interface** is of subtype of that interface example `car implements 4 wheelers` than it means that car is of type `4 wheeler`
- For polymorphism to make sense in the context of a Java program it's important to remember that according to the rules of the Java type system it is possible to assign a value to a variable if the value is of the same type or a subtype of the type of the variable.
- Because the interface implementation relation defines a subtype relation , concrete classes declared to implement an interface can be assigned to variable declared to be of the interface type.
- **Polymorphism** provides quality features in software design :
    - **loose coupling**
    - **Extensibility**
- C**omparable** interface
    - type checking mechanism makes it possible for the compiler to detect that a `Stack<Card>` object cannot be passed to `Collections.sort` unless the `Card` class declares to implement `Comparable` interface
- **UML** class diagram represents a static, or compile time view of software system
    - represents how classes are defined and related to each other
- **Comparator**  interface
    - using this you change the comparison style during runtime for example if you want to compare two cards using Suit and then want to compare using Rank you can do that by implementing  comparator interface
    - has single method `Compare( Object T1 , Object T2 )` but takes two arguments instead of one
    - `Collection.sort( List , new SortByRankComparator())`
    - you have to create an external class that implementation comparator interface and has one method inside it [ `compare(...)` ]
    - @Override the method `Compare()`  in the class implementing the `Comparator<T>` interface
    - **Disadvantage** :
        - because it's an external class for comparison you won't have access to private method of the objects to be compared
        - `**solution**` :  when such situation arrises just declare the comparator class as **nested** class inside the **Object** class that you want to compare
        - Then you can use
            - `Collections.sort( List , new**Object**.SortByRankComparator())`
        - Another option is to use **Anonymous** **class**

            Collections.sort( List , new Comparator<T>()
            {
            		
            	// we are inside  of any anonymous class 
            	@Override 
            	public int compare( T Object1 , T Object2 ) 
            	{/*code for comparisoin of two objects*/}
            	});
            }

        - We can also use **Lambda Expressions**

            // ADD CODE HERE LATER

        - Using **Factory Method**
            - return a comparator of the desired type
- I**terator Design Pattern**
    - provides a way to access the elements of an aggregate object sequentially wihout exposing its underlying representation
    - has to implement  two methods

        [Iterator Design Pattern in Java](https://javadiscover.blogspot.com/2013/11/iterator-design-pattern-in-java.html)

            public class Nameofclass implements Iterbale<T> .. . 
            
            and then implement method 
            
            public Iterator<T> iterator() {... it will return instance of CustomIterable i.e. return new CustonIterable()
             ...}
            
            			now just make a nested class "CustomIteraotr"the implements Iterator<T>{ ..
            			
            			
            			
            			
            			provide the two implementations here >>> 
            			boolean hasNext() ;  i.e return true if eof not reached
            			Object next() ; i.e. return the next object in list

**difference between iterable() and iterator() is that iterable() implementation allows you to have custom definition of hasNext() next() method implementation**

**Both has to be used simultaneously**  

1. Implement Iterable interface along with its methods in the said Data Structure
2. Create an Iterator class which implements Iterator interface and corresponding methods.

Class that implements iterator<T> can  is  nested class

[Java Iterable vs Iterator tutorial and code](https://www.youtube.com/watch?v=PmX3H73bqKI)

- **Strategy Design Pattern**
    - A class behavior or its algorithm can be changed at run time.[behavior pattern]
    - Code receives a runtime instruction on which family of algorithm to use

    [Design Patterns - Strategy Pattern](https://www.tutorialspoint.com/design_pattern/strategy_pattern.htm)

    [Strategy Pattern | Set 2 (Implementation) - GeeksforGeeks](https://www.geeksforgeeks.org/strategy-pattern-set-2/)

    - e.g. can be used to change RPG game strategy during runtime for a player
        - `Strategy Interface` has one method that execute the algorithm uniquely for each concrete class that going to implement this interface to create a new algorithm
        - Examples in folder in eclipse
- **Interface Segregation Principle**
    - It states that : clients should not be forced to depend on interfaces they do not need .
    - ISP splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them.

    ---

## Module 3

[prmr/SoftwareDesign](https://github.com/prmr/SoftwareDesign/blob/master/modules/Module-03.md)

- **UML state Diagrams**
    - represents a dynamic or run-time view of a software system.
    - start state of the UML state diagrams defines the constructor for that object i.e. if the start of the state is described as empty for deck of card that means that constructor initializes an empty deck of card
    - Finally, this diagram does not include any end state. The end state model element is used to specify if an object must be in a certain state at the end of its lifetime (i.e., in Java, when it is garbage collected). In many designs, objects can end their life (stop being used) in any state, in which case the end state model element does not apply.
- **Object Identity**
    - location in memory space of the object defines the identity of the object
    - `==` returns true if two objects evaluates to same identity  : same memory location : same instance of class [ `Same HashMap`  ]
    - before `Overrding` the equal method for objects in the class it checks using `==` and therefore provides equality results of two objects based on their identity

        @Override
        public boolean equals(Object pObject)
        {
           if( pObject == null ) // As required by the specification
           {
              return false;
           }
           else if( pObject == this ) // Performance optimization
           {
              return true;
           }
           else if( pObject.getClass() != getClass()) // Ensures the objects are of the same runtime class
           {
              return false;
           }
           else // Actual comparison code. Assumes the downcast is safe.
           {
              return aRank == ((Card)pObject).aRank && ((Card)pObject).aSuit == aSuit;
           }
        }
        -----output ----
        card1.equals(card2) will return true
        where, card1 =  Rank.ACE , suit.CLUBS
        and,   card2 =  Rank.ACE , suit.CLUBS-

    - any class in java that overrides `equals` must also override `hashCode` so that the following constraint is respected: "If two objects are equal according to the `equals(Object)` method, then calling the hashCode method on each of the two objects must produce the same integer result."
    - When we have flyweight design pattern applied in the class than there is no need to use `equals` method because equality of object now can be obtained using `==` i.e. identity of two object
- **Anonymous class :**
    - READ THE MODULE /

- **Flyweight Design Pattern  || ONLY USE HASHMAP FOR THIS PART**
    - Improves memory usage because it prevent duplicate object creation
    - The Flyweight Pattern is provides a useful way to cleanly manage collections of low-level immutable objects. Although often use to address performance concerns, the Flyweight is also valuable to ensure the uniqueness of objects of a class.

    1. A private constructor for the Flyweight, so clients cannot control the creation of objects;
    2. A data structure that keeps a list of Flyweight instances, stored in a static field;  **static *flyweight store*** 
    3. A static factory method that returns the unique Flyweight object that corresponds to the input parameter.

    `Suit.values()` for Suit : ENUM :: returns an array containing all of the values of the enum in the order they are declared 

        -----------lazy approach 
        public class Card {
        //creating flyweight store
        private static final Card[][] CARDS =new Card[Suit.values().length][Rank.values().length];
        
        //get method 
        public static Card get(Rank pRank, Suit pSuit) {
        
        		//if object is not present in flyweight store then create a new one
        		if( CARDS[pSuit.ordinal()][pRank.ordinal()] == null ) {
        						CARDS[pSuit.ordinal()][pRank.ordinal()] = new Card(pRank, pSuit);
        			}
        		//else returning the object already present
        						return CARDS[pSuit.ordinal()][pRank.ordinal()]; 
        }

        private static final Card[][] CARDS = new Card[Suit.values().length][Rank.values().length]
        
        static {
        	for ( Suit suit : Suit.values() ){
        				 CARDS[suit.ordinal()] = new Card[Rank.values().length] ; 
        				for ( Rank rak : Rank.values())
        				{
        					CARDS[suit.ordinal()][rank.ordinal()] = new Card(rank, suit ) ; 
        				}
        			}
        }
        
        -- to grant access to cards to code outside the class 
        public static Card get ( Rank pRank , Suit pSuit)
        {
        	assert pRank !=null && pSuit != null ;
        	return CARDS[pSuit.ordinal()][pRank.ordinal()] ; //getting card from the fliweight store
        }

    - **Singleton Design Pattern**
        - Single instance of  any given class at any given point of time

        1. A private constructor for the Singleton, so clients cannot create duplicate objects; [this prevents instantiations of the class object again somewhere else : ]
        2. A static final field keeping a reference to the single instance of the singleton object.[  Global field ] 
        3. A static accessor method, usually called `instance()`, that returns the unique instance of the Singleton.

        you can also force the singleton property with a private constructor or enum type

         Stick to private constructor for exam :: 

        e.g. 

            //Singleton class :: i.e. the there is only once instance of this class saved in Global INSTANCE 
            //variable
            public class GameModel
            {
            	private static final GameModel INSTANCE = new GameModel() ; 
            	private GameModel(){//... implement the constructor}
            	public static GameModel instance() { return INSTANCE;}//accessor method for singleton instance
            }

        ![FINAL%20notes/Screen_Shot_2019-12-05_at_8.38.59_AM.png](FINAL%20notes/Screen_Shot_2019-12-05_at_8.38.59_AM.png)

        - **NULLABILITY :: READ NOTES FROM BOOK**

        Design a class in such a way that null references are not used at all 

        - to avoid that variables are not assigned NULL values we can use :
            - input validation  :: using if statements + throw an exception
            - Design by contract :: using assert statement

        you can assign joker card   a value called  `INAPPLICABLE` to enum types : Rank and Suit to tell that joker doesn't have Rank and Suit  ⇒ generates problems ⇒ solution : use **Optional Types**

        `Optional<T>`   library type 

        generic type act as an instance of type T  and which can be empty

        to make a value of type T optional for a variable , we declare this variable to be type `Optional<T>`

        `private Optional<Rank> aRank ;` 

        `private Optional<Suit> aSuit ;`

        so now represent absence of value we can use `**Optional.empty()**`

        e.g. 

            public class Card {
            	private Optional<Rank> aRank ;
            	private Optional<Suit> aSuit ; 
            //constructor
            	public Card(){
            	//assigning null equilvalent values
            		aRank.**Optional.empty()** ; 
            		aSuit.**Optional.empty()** ; 
            	}
            	public boolean isJoker(){
            		//returns true is value is present otherwise return false 
            		return !aRank.**isPresent()** ; 
            	}
            
            }
            

        but to create actual value for the variable of type `Optional<T>` we use `**Optional.of(value)**` Where `value ≠ NULL`

        Make sure you change the getter methods of the class which defines `Optional<T>` field to be return type of `Optional<T>` types

        e.g. `public  Optional<Rank> getRank(){...}`

         Calling get() on an empty instance of Optional will raise an exception immediately when the value is misused, as
        opposed to potentially propagating a null reference 

    ## Null Object Design Pattern

    - Avoids the use of `Optional<T>` types here [called unwrappers ]
    - relies on Polymorphism
    - uses special object to represent the null value  = `interface`
    - main idea of NULL object is to create one special object to represent the absent value and to test for absence **using a polymorphic method call**

    e.g.

        public interface CardSource {
        	//Using anonymous class for **NullCardSource** to create **NULL** object represent **NULL** values
        	//Empty object can refere to this object to represent **NULL** values :: simple idea :: 
        	public static CardSource NULL = new CardSource()
        																	{
        																	public boolean isEmpty() { return true ; } 
        																	public Card draw() { assert !isEmpty() ; return null ; }
        																	public boolean isNull() { return true  ; }
        																	
        																	};
        	public Card draw() ; 
        	public boolean isEmpty() ; 
        	//default method implementation
        	public default boolean isNull()
        		{return false ; }
        
        }
        --------------
        with this solution we don't need separate class called NullCardSource implements CardSource

    - with `final` keyword you can not change the state of fields of an object after is has been assigned to it
    - An important thing to keep in mind with the use of the final keyword, however, is that for reference types, the value stored in a variable is a reference to an object. So, although it is not possible to reassign a final field, it is certainly possible to change the state of the object referenced (if the object is mutable).
    - e.g. `private  final List<Card> aCards = new Arraylist<>() ;` can be changed but cannot be reference to another array list :: final doesn't make reference object I**mmutable** :: only makes reference final not values at any given index final

    ---

    - **Nested Class**
        - outer class instance is linked to inner class method ⇒ used to call outer class methods
            - `outerClassName.this.MethodNameInOuterClass()`
        - Static nested class are not linked to an outer instance
        - Nested inner class can access any private instance variable of outer class
        - we can't have static method in a nested class because an inner class is implicitly associated with an object of its outer class so it cannot define any static method for itself

            Important detail : how to instantiate the inner nested class

            To instantiate an inner class, you must first instantiate the outer class, then ,

            create the inner object within the outer object with this syntax

            `OuterClass.InnerClass innerObject = outerObject.new InnerClass()  ;` 

        - Inner class can be declared within a method of outer class
        - READ notes for this part
        - **if an inner is declared inside the method of outer class it cannot access it's outer methods variable unless they are declared final**
        - methods of inner class cannot be marked as private . protected , static and but can be marked as abstract and final but not both at the same time.

            public class Deck {
            public void shuffle() { ... }
            
            
            //this method creates the instance of the inner class and return that
            public Shuffler newShuffler() { return new Shuffler(); }
            
            
            //INNER CLASS
            public class Shuffler {
            								private int aNumberOfShuffles = 0; private Shuffler() {// constructor}
            
            								public void **shuffle**()
            								{ aNumberOfShuffles++; Deck.this.shuffle(); }
            
            								public int **getNumberOfShuffles**()
            								{ return aNumberOfShuffles; } }
            
            }// inner class ends
            
            -----------usage  in client file i..e main method-----------------------------------------
            //remember that outer class instance has to be instantiate before instantiating Inner class object
            Deck deck = new Deck() ; 
            //calls the method newShuffler() of the inner class  on the instance of Deck referred by variable deck
            //returning instance of inner class using newShuffler() method of outer class
            Shuffler shuffler  = deck.newShuffler() ; 
            shuffler.**shuffle() ; // calling shuffle method of inner clasls Shuffler**

        When to use : 

        - in case where your class B is used only by class A it's better to put class B as an inner class to Class A. :: improves encapsulation and readability of the code.

    ---

    - **Anonymous  class**
        - are declared without any name at all
        - we declare and instantiate them at the same time
        - they are used whenever you need to override the method of a class or an interface
        - **Object life cycle of anonymous class is independent of the object life cycle of the class it was defined in.**
        - you can pass inner class to methods e.g.
        - 

            obj.My_method(new Anonymous(){
            															public void doAnonymous() { ..}
            														}
            							);
            
            ///-------
            Is it valid  ?? :: 
            Class obj 
            {
            	public void My_method(Object pobj){
            				Object aobg = pobg ; 
            				aobg.doAnonymous() ; 
            		}
            
            }

            //interface 
            interface Message {
            	String greet(); 
            }
            
            ---------different file --------
            	//OUTER CLASS
            public class My_class{
            
            	//method which accepts the object of interface message 
            	public void displayMessage( Message m ) {
            	System.out.println( m.greet() + " , this is example of anonymous inner class as an argument  " )  ; 
            
            	}
            ------- MAIN METHOD -------------
            	public static void main(String args[] ) {
            		// Instantiating the class 
            		My_class obj = new  My_class() ; 
            	
            	//passing an anonymous inner class as an argument
            		obj.dispalyMessage( new Message() { //INNER CLASS BODY......
            
            												public String greet() {
            													return "hello " ; 
            												}	
            		}) ;  //end of method displayMessage invokecation
            
            	}
            }
            -------------output --- ---------------
            Hello , this is example of anonymous inner class as an argumet

        NOTE : 
        What does static word do in class ??  

        `static` members belong to class instead of a specific instance

        ⇒ means that only one instance of `static` filed exist. Even if you create a million instance of class that **single** static member is **shared** between all the instance

        technical  def : the static variable gets memory only once in the class area at the time of class loading ⇒ makes memory efficient codes

        Declaration of `enum`

            public class Test {
            	enum Color 
            	{RED, GREEN ,BLUE}
            }

        ---

        ---

        ## Module 4 : JUnit Testing

        - Idea :  the idea of unit testing is to test a very small part of the program in isolation ⇒ if test fails it's easy to look where to look for problems
        - **UUT**  : Unit Under Test
        - **Oracle :** value for comparison of output of a function
        - **JUnit**  in Java automates lot of testing

            public class AbsTest
            {
               @Test
               public void testAbsPositive()
               {
                  assertEquals(5,Math.abs(5));
               }
            	
               @Test
               public void testAbsNegative()
               {
                  assertEquals(5,Math.abs(-5));
               }
            	
               @Test
               public void testAbsMax()
               {
                  assertEquals(Integer.MAX_VALUE,Math.abs(Integer.MIN_VALUE));
               }
            }

        - Assert methods are different from the assert statement in Java. They are declared as static methods of the class `org.junit.Assert*` and all they do is basically verify a predicate and, if the predicate is not true, report a test failure
        - A Test Class various `@Test`  units together ⇒ all the tests are run in this class for a given project
        - **Test Fixtures**
            - In test classes that group multiple test methods, it will often be convenient to define a number of "default" objects or values to be used as receiver objects and/or oracles. This practice will avoid the duplication of setup code in each test method.
            - Baseline Objects used for testing are often referred to as test fixture and declared as a field to a test class
            - unit Test are not executed according to order
                - Unit test are independent of each other so they can be executed independently
                - This further implies that no test method should rely on the fixture being left in a given state by another test.
                - The workaround is to nominate a method of the test class to execute before any test method. In JUnit this method is nominated using te @Before annotation. Fixture initialization code should therefore be located in this method.

            `@Before` is executed before `@Test` annotated method

            when method doesn't work as it suppose to do it can  throw an  exception  and Test should be able to test if the method throws an exception on wrong input or not 

            solution ⇒ use `expected` property of the `@Test` annotation :

                @Test( expected = EmptyStackException.class)
                public void testPeekEmpty1()
                {
                	Stack<String> stack = new stack<>();  
                	stack.peek(); 
                }
                
                -----
                stack should throw an exception on peek() on empty stack  => Test passed
                JUnit will fail the test if the execution of the corresponding test methods completes
                without raising an exception of the specified type. 

        execute additional testing code after testing the exception behavior , 

            @Test
            public void testPeekEmpty2(){
            	Stack<String> stack = new Stack<>() ; 
            	try 
            	{
            	 stack.peek(); 
            	//after normal execution of stack.peek() and if it doens't raises the 
            	// exception it is forced to raise one by using fail() ; for test purpose
            		fail(); 
            	}
            	catch (EmptyStackException e ) 
            	{}
            }
            ----forces the test failure at the end---------

        This idiom is a bit convoluted, but does exactly what we want. If the UUT (the peek method here) is faulty in the sense that it does not raise an exception when it should, the program will keep executing normally and reach the following statement, which will force a test failure. If the UUT is (at least partially) correct in that it does raise the exception when it should, control-flow will immediately jump to the catch clause, thereby skipping the `fail();` statement. It is then possible to add additional code below the catch clause.

    - **Encapsulation and Unit Testing**
        - Code in the private methods should be tested indirectly through the execution of the accessible methods that call them
        - `private` access modifier is a tool to help us structure the project code , and tests can ignore it

    - **Reflection**
        - The ability to inspect the code in the system and see object types is not reflection, but rather Type Introspection. Reflection is then the ability to make modifications at runtime by making use of introspection.

        [What is reflection and why is it useful?](https://stackoverflow.com/questions/37628/what-is-reflection-and-why-is-it-useful)

        e.g. you need to know about object foo 

            -- foo is object we want to know about :: => reflection 
            Method method = foo.getClass().getMethod("MethodName" , null ) ; 
            method.invoke( foo , parameterForTheMethodCall) ; 
            --------------------
            /*if parameterForTheMethodCall = Null  => that no parameters are passed to method call*/

        in JAVA :: metaprogramming ⇒ reflection ⇒ ability to know about a object → what class it belongs to :: what methods it has  etc .. 

        `library` ⇒ `java.lang.Class`

        `package` ⇒ `java.lang.reflect`

        **Getting reference to an object that represents the Card class** 

        **Method 1 :** 

        if you know requested class during compile time

            ---Class of object is known during compile time
            ---In our case name of the class = Cards
            
            
            try {
            	Class<Card> **cardClass**  = (Class<Card>)Class.forName( **"Name of the Class"**);
            	
            }catch(ClassNotFoundExceptione e){...}
            [Here  **cardClass** will refere to the instance of the Class **"Name of the Class"**]
            
            ---------
            the call to Class.forName returns a reference to an instance of class Class
            that represents class Card, as illusstrated by diagram below.......

        if you don't know the name of the class at the runtime : **Using type wildcard  : placeholder for any type**

            public static void main(String args[])
            {
            	try 
            	{
            Class<?> theClass = Class.**forName**( args[0] ) ; 
            	} catch( ClassNotFoundException e) { e.printStackTrace() ;}
            
            	}

        **Method 2 :** 

        if you know requested class during compile time 

        Using **Class literals : ⇒ caveats : ⇒ you must know class during compile time**

            Class<**Card**> cardClass1 = **Card**.class ; 

        **Method 3 :** 

        Using `**getClass()`** ⇒ returns a valid reference to an instance of class 

        If an instance of an object is available, then the simplest way to get its `[Class](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)` is to invoke `[Object.getClass()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--)`. Of course, this only works for reference types which all inherit from `[Object](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`. Some examples follow.

        `Class c = "foo".getClass()` or `Class<?> c = foo.getClass()`

        - Printing all the methods of class  using **class `Method`**

                for ( Method method  : foo.class.**getDeclareMethods**())
                	{
                		System.out.println( method.**getName**()); 
                	}
                
                ----------------------------------------------------
                ----or if you want methods of cardClass1 object ---- 
                ----------------------------------------------------
                
                for ( Method method  : cardClass1.class.**getDeclareMethods**()) // returns array of methods
                	{
                		System.out.println( method.**getName**()); 
                	}

    - **Program Manipulation**
        - To change accessibility of methods, set filed values , create new instance of objects , and invoke methods

            Create a duplicate ace of clubs 

                try 
                {
                	Card card1 = Card.get(Rank.ACE, Suit.CLUBS) ;
                
                //obtains a reference to an instance of class Constructor that represents the            (private) constructor of class Card
                	Constructor<Card> cardConstructor = Card.class.getDeclaredConstructor(Rank.class, Suit.class)  ; 
                
                //changes the accessibility of the constructor effectively bypassing 
                //the private keyword in the code  so that you can access this constructor 
                //outside the scope of the class it was declared in 
                	cardConstructor.setAccessible(true) ;
                
                // calls newInstance on the Constructor object => makes a new instance of the  
                // declaring class of the constructor represented by the **Constructor** **instance**, 
                //as opposed to a new instance of class Constructor.
                
                // in simple words if constructor we are dealing with is of classs animals 
                //then this way we will create a new instance of animals :: onwer of the 
                //constructor
                
                // beacause constructor  of this class requires two parameters
                // we pass rank and suit types values to the newinstance call
                	Card card2 = cardConstructor.newInstance(Rank.ACE  ,Suit.CLUBS) ;
                	System.out.println( card1 == card2) ; 
                
                }catch ( ReflectiveOperationException e ) { e.printStackTrace() ; }
                
                

            `Constructor<**className**> **con** = **foo**.class.getDeclaredConstructor(parameters)` ⇒  get reference to an instance of class of Constructor

            `**con**.setAccessible(true)` ⇒bypassing the private keyword  ⇒ changing accessibility of constructor

            `**className** obj = **con**.newInstance(parameter)` ⇒ creating new instance of type **className**

            `foo.getDeclareMethods()`⇒ method returns an array of Method objects including public, protected, default (package) access, and private methods, of class foo

            - Use Class `Field`  to fields of a class
                - e.g. `Field **rankField** = Card.class.getDeclaredField("**aRank**")`

                Changing accessor ⇒`rankFiled.setAccessible(true)`

                setting field to different values ⇒ `rankFiled.set(  object , newFieldValues)`

                object = instance For Which You Want To Change The Field,

            **Some Basic Rules :** 

            - `@Before` ⇒ method execute before any Test
            - `@After` ⇒ method executes after every test  ⇒ free up the state of the object before going to execute another Test
            - Very Important Example

                pubic class TestFoundationPile 
                
                {
                	//creating three objects of type Card i.e. now we have three diffferent Card
                	private static final Card ACE_CLUBS = Card.get(Rank.ACE , Suit.CLUBS) ; 
                	private static final Card TWO_CLUBS = Card.get(Rank.TWO , Suit.CLUBS) ; 
                	private static final Card THREE_CLUBS = Card.get(Rank.THREE , Suit.CLUBS) ; 
                
                	private FoundationPile aPile ; 
                
                	@Before
                //	Before any test create a new instance [aPile] of type FoundationPile 
                //purpose of this is that different Test Units gets fresh object to Test with other wise if a Test leaves an objects in some state that is not compatible with the Testing Unit then whole purpose of independent testing is defeated
                	public void setUp(){ aPile = new FoundatonPile() ; }
                
                	@Test
                	public void testCanMoveTo_Empty() 
                	{
                		assertTrue(aPile.canMoveTo(ACE_CLUBS); 
                		aseertFalse(aPile.canMoveto(THREE_CLUBS) ; 
                	}//End of Test Unit #1
                
                	@Test
                	// before running this test @Before will be executed again and create a fresh instnace aPile of type FoundationPile
                	public void testCanMoveTo_NotEmptyAndSameSuit(){
                		//pushing  a card to the empty pile so that new pile is not empmty anymore
                		aPile.push(ACE_CLUBS) ; 
                		assertTrue(aPile.canMoveTo(TWO_CLUBS)); 
                		assertTrue(aPile.canMoveTo(THREE_CLUBS)) ; 
                	} // end Test Unit #2
                }

            **lets check if the foundationPile() throws an exception or not if peek() called on emptyPile()** 

            Method 1 : 

                @Test ( expected = EmptyStackException.class) 
                public void testpeek_empty()
                {
                	new FoundationPile().peek() ; 
                }
                ---- if peek() doesn't raise exception than the test will fail---- 

            Method 2 : 

                @Test 
                public void testpeek_empty()
                {
                	FoundationPile pile = new FoundationPile() ; //instead of this just use @Before annotation
                try 
                	{
                		pile.peek(); 
                		fail() ; //forces to fail if no exception is raised ; 
                	}
                catch ( EmtpyStackException e ) {...}
                assertTrue(pile.Empty()) ; 
                
                }

            - You can use helper function for testing  : ⇒ also test private methods you have to use metaprogramming ⇒ reflection ⇒ there has to create helper function  for testing private method
            - Use helper methods to `setAccessbile ⇒ True`

                public class TestFoundationPile 
                {
                	private FoundationPile aPile ; 
                	@Before
                	public void setUp() { aPile  = new FoundationPile ; }
                	private Optional<Card> getPreviousCard(Card pCard) 
                
                	{
                		try 
                		{
                			Method method = aPile.class.getDeclaredMethod("getPreviousCard" , Card.class); 
                			method.setAccessible(true); // main reason we needed helper method
                			return (Optional<Card>)method.invoke(aPile , pCard) ; 	
                		}
                		catch ( RelflectiveOperationException e ) 
                			{
                				 fail() ; 
                					return Optional.empty() ; 
                			}
                	}
                
                @Test 
                public void testGetPreviousCard_Empty(){
                		assertFalse(getPreviousCard(Card.get(Rank.ACE , Suit.CLUBS)).isPresent()); }
                
                }

    - **Coverage**
        - Statement Coverage
            - (number of statements executed ) / ( number of statements in the program )
        - Branch Coverage
            - ( number of branches executed) / (number of  branches in the program )
        - Path Coverage
            - ( number of paths executed ) / (number of paths in the program)

        ### Notes :

        Accumulated during practice 

        `assertEquals(Oracle , invoke method => returns something  = Oracles)` ⇒ Test passed

        else Test Fail

        - When you use catch statement while using metaprogramming makes sure to throw exception as `**Catch**(ReflectiveOperationException **e**){...}`
        - `method.getParameterCount()` ⇒ get the methods number of parameter in order to invoke it
        - `assertSame( orcal, function's return value)` ⇒ is it same as `assertEquals(...)` ?
        - 

        assertEquals: Asserts that two objects are **equal**.

        assertSame: Asserts that two objects refer to the **same object**.

        [Why assertEquals and assertSame in junit return the same result for two instances same class?](https://stackoverflow.com/questions/28451925/why-assertequals-and-assertsame-in-junit-return-the-same-result-for-two-instance)

        - checking if the method throws an exception or not using  **lambda** **Expressions**

            assertThrow( exceptionName.class , new Executable() {
            
            																		@Override 
            																		public void execute() throws Throwable 
            																		{  ..... invoke method here ... .}
            																		
            }); 

---

# Module 5 - composition

- Composing objects simply means that one object stores a reference to one or more other objects
- **Delegation :**
    - delegates some services to the object it contains
    - the composite class will contain methods to delegate the instruction to each object store in the `arraylist<objectType>`
- the composite should have a way to add instance of primitive type that it composes

### Decorator Design Pattern

- looks similar to composite design pattern ⇒ both aggregates primitive type objects you want to decorate
- decorator should implements primitive type so that it can be treated as primitive type and decorator can be decorated too
- it's a good idea to specify as `final` the field that stores a reference to the decorated object, and to initialize it in the constructor.

### Polymorphic object copying

**Copy constructor** 

    //copy constructor
    public Card( Card pCard)
    { Card cardCopy = new Card(pCard) ; }

we want to be able to make copies of objects without knowing the exact concrete types of the object ⇒ **cloning**

**steps :** 

- tag the class `Cloneable`
- Override `clone` method
- make is accessor public

    @Override 
    public Card clone() {
     Card clone = super.clone() ; // calling clone method  of super class
    //Card clone = (Card)super.clone() ;  // should we include wrapper ;
    }

it's a good idea to specify as final the field that stores a reference to the decorated object, and to initialize it in the constructor.

- makes shallow copy of all the instances fields
- when you want to copy deep copy i..e. copying the `aCards` arraylist within [filled `Card` type objects] you must perform a deep copy using loop

    class Deck implements Cloneable {
    	private static final List<Card> aCards = new ArrayList<>(); 
    .
    .
    .
    @Override
    public Deck clone()
    {
    	try 
    {
    				Deck lReturn = (Deck)super.clone(); 
    				lReturn.aCards = new ArrayList<>(); 
    				for ( Card card : aCards)  //here aCards is present in the class of Deck itself 
    							{
    								lReturn.aCards.add(card); 
    							}
    				return lReturn ; 
    }
    catch (CloneNotSupportedException e)
    { return null ; } 
    }
    
    .
    .
    .
    }

## Prototype Design Pattern

⇒ hides the complexity of making new instances from the client. The concept is to copy an existing object rather than creating a new instance from scratch 

the existing object acts as a prototype and contains the state of object

[Prototype](https://refactoring.guru/design-patterns/prototype)

⇒ reduces the need of creating multiple subclasses 

[Prototype Design Pattern Tutorial](https://www.youtube.com/watch?v=AFbZhRL0Uz8)

simple idea ⇒ client has access to pass the object to a factory method that will clone the object for you. ⇒  type has to be cloneable for that

**steps ~** 

- create an abstract class or interface that implements Cloneable  and then other concrete class either extends abstract class or implement the interface
- in case of abstract class define clone() method in it so extending class will inherit `@Overriden clone()`  method already
- in case of implementing interface all the type of the interface has to define `@Overriden clone()` method separately ⇒ might lead to code duplication
- and then create a separate class [**you can call is CloneFactory**] that has method getClone() or anything that simply returns clone of the object passed into this method which is of type same as the object you want copy
- the above video explains it pretty good

## Command Design Pattern

[Design Patterns - Command Pattern](https://www.tutorialspoint.com/design_pattern/command_pattern.htm)

- Use an entire object to represent a command
    - `command <<interface>>` ⇒ implemented by other concrete commands
    - interface contains single method `execute()` that has to be implemented by all the concrete command type :⇒ each execute in concrete command types will have different definition.  so client just have to  call method `execute` on an object of type `Command` and the implementation  of `execute` in the corresponding **concrete command** gets selected polymorphically

### Law of Demeter

- it's a design guideline that states that the code of a method should only access
    - the instance variables of its implicit parameter
    - the arguments passed to the method
    - any new object created within the method
    - ( if need be ) globally available objects

# Module 7 - Inheritance

- run type is specified by → `new`
- An object can always be assigned to a variable of any of its superclasses (  in addition to its implementing interfaces )
- `Animal sally = new Sheep()` ⇒ Animal is superclass and Sheep is base-class ⇒ **compile type | static type**  = Animal and **run type** ⇒ Sheep()
- in java runtime remains same throughout the life of the object
- `getClass()` always returns  **runtime** type of the object
- static type can be different of a variable in different time of code
- `instanceof` → is used to test whether the object is an instance of the specified type ( class or sublcass or interface)

Include **downcasting** 

[Java instanceof - javatpoint](https://www.javatpoint.com/downcasting-with-instanceof-operator)

- **DownCasting →  `Dog d = new Animal()`**  compile time error :: `Dog d =  (Dog) new Animal` ClassCastException at runtime
- but is you know that `Animal d = new Dog()` then  so  lets say d is passed to a method and we check  `if( a instanceof Dog)` returns true then

    **downcasting** is legal  `Dog d = (Dog)a ;`

- In Java, type members declared to be protected are only accessible within methods of the same class, classes in the same package, and subclasses in any package.
- ??cant we access private field of supeclass
    - A subclass does not inherit the private members of its parent class. However, if the superclass has public or protected methods for accessing its private fields, these can also be used by the subclass.
    - A **nested class** has access to all the private members of its enclosing class—both fields and methods. Therefore, a public or protected nested class inherited by a subclass has indirect access to all of the private members of the superclass.
- in java field of an object is initialized top down approach i.e. first fields of superclass is assigned then base-class
- in base class ⇒ **first instruction**  has to be  calling constructor of superclass
- first line of any constructor is the call to the super-constructor can be implicit. In the running example, declaring:
- 

    Class Empolyee
    {
    	private String aName = "Anondymous"; 
    	private int aSalary = 0 ; 
    	public int aSalary = 0 ; 
    	public Employee(String pName , int pSalary)
    	{
    		aName = pName ; 
    		aSalary = pSalary; 
    	}
    ...
    }
    
    Class Manager extends Employee 
    {
    	private int aBonus = 0 
    	public Manager(String pName , int pSalary , int pBonus)
    	{
    	super(pName , pSalary); 
    	aBonus  = pBonus ; 
    	}
    	
    }
    
    ---if argument passed to baseclass constructor didn't include any fields initialization of parent class then you can skip super() 
    call 
    This explicit call is now actually required, because declaring a non-default constructor 
    in Employee disables the automatic generation of a default constructor
    
    so this syntax is only valid when Employee doesn't have any constructor decalration of it's own
    public Manager(int pBonus)
       { // Automatically calls super() // a default parameter with no inputs to constructor
          aBonus = pBonus.

- By default, methods of a superclass are applicable to instances of a subclass
- **private** **fields** are inherited ⇒ you cannot use them in methods of base class
- **superclass** methods can be **Overriden** by redefining them in **base class** you don't even hav to use `@Override` keyword
- which function out of two to run ⇒  decided using run time type of the implicit parameter ⇒ **dynamic dispatch  or dynamic binding ⇒** Selection of an overriden method relies on **run time** information of object

lets say you have private field that is used in `getCompensation()` method and you want to add to  the definition in the base class by overriding it but you cannot use the private filed during overriding so you do this way : 

    class Manager extends Employee 
    {
       private int aBonus = ...;
       ...
       public int getCompensation() 
       {
          // Cannot be replaced with return getCompensation() + aBonus;
          return aSalary + aBonus; 
       }
    
    
    ---------
    
    public int getCompensation()
    {
    	return super.getCompensation() + aBonus ; 
    }

### Overloading

- selecting methods based on the type of the explicit parameters

### Abstract Class

- doesn't have to provide implementation of interface it implements  ⇒  implementations provided by classes that extend abstract class
- cannot be instantiated
- contains abstract method ⇒ method without implementation  ⇒ subclass provides implementation
- abstract class constructor can only be called from **constructor** of subclasses ⇒ there declare constructors of **abstract** **class** `**protected**`

### Template Method Design Pattern

- if some part of code is common to subclasses just move it up to superclass ⇒ so that the design can be reused by all the base class
- but sometime you need information of baseclass to implement that common method ⇒ which is not possible to obtain by superclass
- so superclass just provides the common code in superclass and methods unique to each sub class are implemented separately
- The method in the abstract superclass is the template method, it calls the concrete and abstract step methods
- **template** **method** should be declared `final` if you don't want the Algorithm to be changed by base classes

    declaring a method to be a final means that the method in subclasses cannot be overridden by subclasses. 

    do this when you want to prevent the method to be  overridden by other subclasses

- abstract methods in template method should be `protected` ⇒ so that client outside the class hierarchy  cannot make change

Note 

- when a class inherits a superclass ⇒ then base class becomes the subtype of that superclass
- to avoid major design flaws, inheritance should only be used for extending the behavior of superclasses. As such, it is incorrect to use inheritance to limit or restrict the behavior of the superclass, and/or to use inheritance when the subclass is not a proper subtype of the superclass.

### Liskov substitution principle

This intuition is captured by the [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle), which basically states that subclasses should not restrict what clients of the superclass can do with an instance. Specifically, this means that methods of the subclass:

- Cannot have stricter preconditions;
- Cannot have less strict post-conditions;
- Cannot take more specific types as parameters;
- Cannot make the method less accessible (e.g., public -> protected);
- Cannot throw more checked exceptions;
- Cannot have a less specific return type.

---

# Module 6 -

### Observer Design Pattern

- central idea  → store state of interest in specialized object
- The model can be used without observer
- add or remove observer at runtime
- Observer type have to implement call back function that model can invoke whenever there is change made in Model worth notifying to observers
- If There are more than one observer than just provide the loop to call the "callback" function on all of them
- `type << Observer>> void event2(data)` ⇒ callback function using **push data flow  method**  i.e. callback's parameters provide information about what changed,
- `type <<Observer>> void event3(Model)` +> callback function using **pull data flow method** i.e. callback provides a reference to the entire model ( or assumes the observers can obtain the reference)  but requires the model to determine what information to obtain.
- Observer can choose to get any information or change the values inside model if it wishes to act as an **controller**
- `notifyObserver()` method should be called automatically when the changes are made in model class

**NOTE : make sure to make the    `List<Observer>observerList = new ArrayList<>()`  iteratble**

    @Override
    	public void notifyObserver() {
    
    		for ( Iterator<Observer> it = observerList.iterator() ; it.hasNext();) 
    // if it.hasNext() doesn't return false  :: loop will keep running
    		{
    			Observer o = it.next() ; 
    			//push data-flow strategy 
    			o.update( runs, wickets, overs) ; 
    		}
    		
    	}

### Visitor Design Pattern

- Behavioral Design Pattern  ⇒ it is used when we have to perform an operation on a group of similar kind of objects  ⇒ or you can say that you have to inject a functionality to a type of objects without modifying the class
- A method called `Visit()` which  is implemented by the visitor and is called for every element in the data structure
- visitable classes providing `Accept()` methods that accept a visitor *⇒ every class that accepts visitors i.e. extra functionality to be added must implement a interface of type visitor  and implement method accept() that allows visitor to come and do there things in the class*
- you can also say the it's allows you to define external classes that can extend other classes without majorly editing them :: .. .just adding functionality to pre existing class ..

[Visitor Design Pattern](https://www.youtube.com/watch?v=pL4mOUDi54o)

NOTE :: make the class that has to visit of type `Visitor` and the class that allows visitor as `Visitable`

    public interface Visitable {
    accept( Visitor visitor) ; 
    
    }
    .
    .
    .
    public interface Visitor {
    	//each class that allows that allows visitor has to be handled in different way in concrete Visitor class 
    // so..   => numboer visit methods in interface = number of classes that allow visitor
    visit ( Class1 obj1) ; 
    visit ( Class2 obj2 ) ;
    .
    .
    .
    }