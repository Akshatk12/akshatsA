# akshatsA
So it will not work:
public interface Foo
{
 default boolean equals(Object o)
 {
 return false;
 }
}



nterface X
{
 static void foo()
 {
 System.out.println("foo");
 }
}
class Y implements X
{
}
public class Z 
{
 public static void main(String[] args)
 {
 X.foo();
 // Y.foo(); // won't compile
 }
}
// Expression Y.foo() will not compile because foo() is a static member 
// of interface X and not a static member of class Y

interface Operation {
int apply(int a, int b);
}
class Logic {
public static int operation(int a, int b, Operation operation) {
return operation.apply(a, b);
}
}
public class DemoBehaviour {
public static void main(String[] args) {
int sum = Logic.operation(2, 2, (int a, int b) -> a + b);
int mul = Logic.operation(2, 2, (int a, int b) -> a * b);
}
}

4
4


void method() {
 final int cnt = 16;
 Runnable r = new Runnable() {
 public void run() {
 System.out.println("count: " + cnt );
 }
 };
 Thread t = new Thread(r);
 t.start(); 
 cnt ++; // error: cnt is final
} 
 
Lambda expressions, too
------------------------------
 
 Runnable r = () -> { System.out.println("count: " + cnt ); }; 
 
 Thread t = new Thread(r);
 t.start(); 
 cnt ++; // error: cnt is implicitly final
}



List<Apple>grrenApples=Inventrory2.filterApples(list, (Apple a)-> "green".equals(a.getColor()));
(Apple a) -> a.getWeight() > 150
(Apple a) -> a.getWeight() < 80 ||"brown".equals(a.getColor())
Even Better use method reference
List<Apple>grrenApples=Inventrory2.filterApples(list, Inventrory2::isGreenApple);



@FunctionalInterface
public interface Consumer<T>{
void accept(T t);
}
public static<T> void forEach(List<T> list, Consumer<T> c){
for(T i:list){
c.accept(i);
}
}
forEach(Arrays.asList(1,2,3,5),(Integer i) -> sysout(i));

1235



List<Integer>list=Arrays.asList(4,5,6,7,4,5,88);
int sum=list.stream().reduce(0, (a,b)->a+b);
System.out.println(sum);
119


List<String>letter=Arrays.asList("a","b","c","d");
String concat="";
for(String temp:letter)
concat+=temp;
//java 8
String concat2=letter.stream().collect(Collectors.joining())
abcd

Note: stream should traversed once
-----------------------------------
List<String>list=..........;
Stream<String> s=list.stream();
Sysout(s.foreach(s->System.out::println());
Sysout(s.foreach(s->System.out::println());//////Will give an error


List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4);
	numbers.stream().filter(i -> i % 2 == 0).distinct().forEach(System.out::println);
2
4


class Foo {
private int a, b, c;
///
}
class Bar {
private int p, q;
///
}
public class DemoMapToObj {
static Function<Foo, Bar> chnager = new Function<Foo, Bar>() {
@Override
public Bar apply(Foo f) {
Bar bar = new Bar(f.getA(), f.getB());
return bar;
}
};
public static void main(String[] args) {
List<Foo> foos = Arrays.asList
(new Foo(1, 2, 3), new Foo(1, 2, 3), new Foo(1, 2, 3));
List<Bar> gettingBars = foos.stream().map(chnager)
.collect(Collectors.toList());
gettingBars.forEach(x-> System.out.println(x));
}
}

Bar [p=1, q=2]
Bar [p=1, q=2]
Bar [p=1, q=2]


What happens in this code?
-------------------------
final Stream<Integer>stream = Stream.of(1,2,3,4,5,6,7,8,9,10);
stream.flatMap();
=> It doesn't make sense to flatMap a Stream that's already flat, 
like the Stream<Integer> 
=> However, if you had a Stream<List<Integer>> then it would make sense and you could do this:
Stream<List<Integer>> integerListStream = Stream.of(
 Arrays.asList(1, 2), 
 Arrays.asList(3, 4), 
 Arrays.asList(5)
);
Stream<Integer> integerStream = integerListStream .flatMap(Collection::stream);
integerStream.forEach(System.out::println);
O/P: print 1 to 5



List<Integer> someNumbers = Arrays.asList(1, 2, 3, 4, 5);
Optional<Integer> firstSquareDivisibleByThree =someNumbers.stream()
.map(x -> x * x)
.filter(x -> x % 3 == 0)
.findFirst(); // 9


int sum = numbers.stream().reduce(0, (a, b) -> a + b); // if initial value is not written then compilation error occurs
int product = numbers.stream().reduce(1, (a, b) -> a * b);
reduce takes two arguments:
--------------------------
-> An initial value, here 0.
-> A BinaryOperator<T> to combine two elements and produce a new value; 
here we use lambda (a, b) -> a + b
Reduction in case of No initial value
-----------------------------------
Optional<Integer> sum = numbers.stream().reduce((a, b) -> (a + b));
Why does it return an Optional<Integer>? 
What happens if the case when the stream contains no elements?
=> The reduce operation can't return a sum because it doesn\92t have an initial value.
=> In that case result would be wrapped in an Optional object to indicate
 that the sum may be absent.



	List<Integer> result = Stream.of(2, 3, 4, 5,7,9,11)
			 .peek(x -> System.out.println("taking from stream: " + x))
			.map(x -> x + 17)
			 .peek(x -> System.out.println("after map: " + x))
			.filter(x -> x % 2 == 0)
			 .peek(x -> System.out.println("after filter: " + x))
			.limit(3)
			 .peek(x -> System.out.println("after limit: " + x))
			.collect(Collectors.toList());


taking from stream: 2
after map: 19
taking from stream: 3
after map: 20
after filter: 20
after limit: 20
taking from stream: 4
after map: 21
taking from stream: 5
after map: 22
after filter: 22
after limit: 22
taking from stream: 7
after map: 24
after filter: 24
after limit: 24



class StringConcatenator {
public static String result = "";
public static void concatStr(String str) {
result = result + " " + str;
}
}
Serial execution:
String words[] = "the quick brown fox jumps over the lazy dog".split(" ");
Arrays.stream(words).forEach(StringConcatenator::concatStr);
System.out.println(StringConcatenator.result);

the quick brown fox jumps over the lazy dog

parallel execution:
Arrays.stream(words).parallel().forEach(StringConcatenator::concatStr);

random order: over jumps lazy dog the brown fox quick the

Problem?
--------
=> When the stream is parallel, the task is split into multiple 
sub-tasks and different threads execute it.
=> The calls to forEach(StringConcatenator::concatStr) now access the globally
 accessible variable result in StringConcatenator class. 
=> Hence this program suffers from a race condition problem
Solution:
---------
=> get rid of modifying the global state and keep the
reduction localized
=> We can use the reduce() method 
Correct way:
-----------
String words[] = "the quick brown fox jumps over the lazy dog".split(" ");
Optional<String> originalString =(Arrays.stream(words).parallel().reduce((a, b) -> a + " " + b));
System.out.println(originalString.get());

the quick brown fox jumps over the lazy dog

List<String> list=IntStream
.rangeClosed(0, 50)
.filter(i-> i%5==0)
.mapToObj(i-> String.valueOf(i/5))
.collect(Collectors.toList());
System.out.println(list);


[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]




List<String>peek=new ArrayList<String>();
List<String> list=IntStream
.range(0, 50)
.parallel()
.filter(i-> i%5==0)
.mapToObj(i-> String.valueOf(i/5))
.peek(s->peek.add(s))//multiple thread adding to list!
.collect(Collectors.toList());
System.out.println(list);
System.out.println("-----processing -------------");
System.out.println(peek);
ArrayIndexOutOfBoundException: 
non thread ds added and manipulated ..so missing info, null etc 
Change to synch collection : List<String>peek=Collections.synchronizedList(new ArrayList<String>());
Note: order in which data is processed in paralled stream (by multiple threads )can not predictable ....
O/P: resembly of result is not based on processing order but on postion ...(encounter order




List<String> strin = Arrays.asList("one", "two", "three","four",
			 "five", "six", "seven", "eight", "nine", "ten");
			
			System.out.println(strin.stream().map(s-> "{"+s+"}").reduce("", (s1, s2)-> s1+s2));


{one}{two}{three}{four}{five}{six}{seven}{eight}{nine}{ten}


 List<String> strings = Arrays.asList("one", "two", "three","four",
			 "five", "six", "seven", "eight", "nine", "ten");
			
	 System.out.println(strings.stream()
			 .map(string -> new StringBuilder("{" + string + "}"))
			// .parallel()
			 .reduce(new StringBuilder(), (s1, s2) -> s1.append(s2)));

{one}{two}{three}{four}{five}{six}{seven}{eight}{nine}{ten}



System.out.println(strings.stream()
.map(string -> new StringBuilder("{" + string + "}"))
.parallel()
.reduce(new StringBuilder(), (s1, s2) -> s1.append(s2)));

Arrayindexoutofbound at runtime ya fir bekar result


	 List<String> strings = Arrays.asList("a", "b", "c", "d",
			"e", "f", "g", "h", "i", "j");
	 System.out.println(strings.stream().parallel().reduce("", (x,y)->y+x+y));


jjiijjhhjjiijjggffggjjiijjhhjjiijjeeddeecceeddeebbaabbeeddeecceeddeejjiijjhhjjiijjggffggjjiijjhhjjiijj




	=> find the name of emp whose woring on an project?
	-------------------------------------------------------
	select ename 
	from emp
	where eid in(select distinct (eid) from project);

	=> find the details of emp working on at least one project
	---------------------------------------------------------
	select * 
	from emp
	where eid exists( select eid
			  from project
			  where emp.eid=project.eid);



select id, salary 
from emp1 e1 where n-1=
	(select count(distinct salary)
	from emp1 e2 
	where e2.salary> e1.salary);




Find details of all dept where any employee works

Joins:
------
select distinct dept1.did, dept1.dname 
from dept1, employee1 
where dept1.did=employee1


Nested quaries
--------------
select * from dept1 
where did in (select did_fk from employee1);


Correlated quaries
-----------------
select * from dept1 
where exists (
	select did_fk from 
	employee1 
	where dept1.did=employee1.did_fk);




public interface Foo
	{
  	 	default boolean equals(Object o)
   	 	{
      		return false;
   		}
	}
A) Code will not compile 
B) Code with compile
C) Code compile but run time error
D) none of these

a












 Which one of the following abstract methods does not take any argument but
returns a value?
A.The accept() method in java.util.function.Consumer<T> interface
B.The get() method in java.util.function.Supplier<T> interface
C.The test() method in java.util.function.Predicate<T> interface
D.The apply() method in java.util.function.Function<T, R> interface


b









 Choose the best option based on this program:
import java.util.*;
 
class Sort {
public static void main(String []args) {
List<String> strings = Arrays.asList("eeny ", "meeny ", "miny ", "mo ");
Collections.sort(strings, (str1, str2) -> str2.compareTo(str1));
strings.forEach(string -> System.out.print(string));
}
}
A.	 Compiler error: improper lambda function definition
B.	This program prints: eeny meeny miny mo
C.	This program prints: mo miny meeny eeny
D.	This program will compile fine, and when run, will crash by throwing a runtime
exception.

c



Consider code snippet :

class Foo{
 void method() {
          int  cnt = 16;
        Runnable r = new Runnable() {
            public void run() {
                System.out.println("count: " +  cnt );
            }
        };
        Thread t = new Thread(r);
        t.start(); 
         cnt ++;  
} 
}
 A. Code will not compile 
B. Code with compile
C. Code compile but run time error
D. none of these

a



Consider code snippet, what would be the output?
class Foo{
 int i=55;
 void method() {
         int i=77;
        Runnable r = () ->{
                System.out.println("value of i: " +  this.i );
            };
       
        Thread t = new Thread(r);
        t.start(); 

} 
}

E) Code will not compile 
F) value of i=77
G) value of i=55
H) none of these


g



Behavior parameterization is
1. passing code to methods  arguments
2. passing object to method arguments
3. passing both code and objects to method arguments
4. none of these



1



Consider code snippet, what would be the output?

List<String>list=Arrays.asList(“java”,”is”,”fun”);
Stream<String> s=list.stream();
Sysout(s.foreach(s->System.out::println());
Sysout(s.foreach(s->System.out::println());

A. Code will not compile 
B. java is fun statement is printed twice
C. java is fun statement is printed once only
D. Code fails at run time

d


Optimizations applied by java while evaluating stream in java 8?
A. short-circuiting
B. loop fusion
C. lazy Evaluation
D. All of these

d

In java 8, R apply(T t) is a method of-
a.Function
b.Process
c.Predicate
d.None

a



What is Predicate in Java 8 -
a.method
b.class
c.Interface
d.Framework

c



Which method can be used to check null on an Optional variable in Java 8
a.isPresent()
b.isNullable()
c.isPresentable()
d.isNotNull()


a





We need to override which Predicate method in Java 8 -
a.predict(T t)
b.predictable(T t)
c.testable(T t)
d.test(T t)


d









