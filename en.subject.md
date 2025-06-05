## Templated containers, iterators, algorithms

You will notice that, in this module, the exercises can be solved WITHOUT the standard
Containers and WITHOUT the standard Algorithms.

However, using them is precisely the goal of this Module.
You must use the STL — especially the Containers (vector/list/map/and so forth)
and the Algorithms (defined in header<algorithm>) — whenever they are appropriate.
Moreover, you should use them as much as you can.
Thus, do your best to apply them wherever it’s appropriate.

You can define your templates in the header files as usual. Or, if you want to, you
can write your template declarations in the header files and write their implementations
in .tpp files. In any case, the header files are mandatory while the .tpp files are optional.

# ex00: Easy find
Files to turn in:Makefile, main.cpp, easyfind.{h, hpp}
and optional file: easyfind.tpp
Forbidden functions:None

A first easy exercise is the way to start off on the right foot.

Write a function templateeasyfindthat accepts a typeT. It takes two parameters:
the first one is of typeT, and the second one is an integer.

AssumingTis a container of integers , this function has to find the first occurrence
of the second parameter in the first parameter.

If no occurrence is found, you can either throw an exception or return an error value
of your choice. If you need some inspiration, analyze how standard containers behave.

Of course, implement and turn in your own tests to ensure everything works as ex-
pected.

You don’t have to handle associative containers.

# ex01: Span
Files to turn in:Makefile, main.cpp, Span.{h, hpp}, Span.cpp
Forbidden functions:None

Develop a Span class that can store a maximum ofNintegers. Nis an unsigned int
variable and will be the only parameter passed to the constructor.

This class will have a member function calledaddNumber()to add a single number
to the Span. It will be used in order to fill it. Any attempt to add a new element if there
are alreadyNelements stored should throw an exception.

Next, implement two member functions:shortestSpan()andlongestSpan()

They will respectively find out the shortest span or the longest span (or distance, if
you prefer) between all the numbers stored, and return it. If there are no numbers stored,
or only one, no span can be found. Thus, throw an exception.

Of course, you will write your own tests, and they will be far more thorough than the
ones below. Test yourSpanwith at least 10,000 numbers. More would be even better.

Running this code:

int main()
{
Span sp = Span(5);
sp.addNumber(6);
sp.addNumber(3);
sp.addNumber(17);
sp.addNumber(9);
sp.addNumber(11);
std::cout << sp.shortestSpan() << std::endl;
std::cout << sp.longestSpan() << std::endl;
return 0;
}

Should output:

$> ./ex
2
14
$>

Last but not least, it would be wonderful to fill yourSpanusing a range of iterators.
Making thousands of calls toaddNumber()is so annoying. Implement a member function
to add multiple numbers to yourSpanin a single call.

If you don’t have a clue, study the Containers. Some member
functions take a range of iterators in order to add a sequence of
elements to the container.

# ex02: Mutated abomination
Files to turn in:Makefile, main.cpp, MutantStack.{h, hpp}
and optional file: MutantStack.tpp
Forbidden functions:None

Now, it’s time to move on to more serious things. Let’s develop something weird.

Thestd::stackcontainer is very nice. Unfortunately, it is one of the only STL Con-
tainers that is NOT iterable. That’s too bad.

But why would we accept this? Especially if we can take the liberty of butchering the
original stack to create missing features.

To repair this injustice, you have to make thestd::stackcontainer iterable.

Write a MutantStack class. It will be implemented in terms of astd::stack.
It will offer all its member functions, plus an additional feature: iterators.

Of course, you will write and turn in your own tests to ensure everything works as
expected.

Find a test example below.

int main()
{
MutantStack< int > mstack;
mstack.push(5);
mstack.push(17);
std::cout << mstack.top() << std::endl;
mstack.pop();
std::cout << mstack.size() << std::endl;
mstack.push(3);
mstack.push(5);
mstack.push(737);
//[...]
mstack.push(0);
MutantStack< int >::iterator it = mstack.begin();
MutantStack< int >::iterator ite = mstack.end();
++it;
--it;
while (it != ite)
{
std::cout << *it << std::endl;
++it;
}
std::stack< int > s(mstack);
return 0;
}

If you run it a first time with your MutantStack, and a second time replacing the
MutantStack with, for example, astd::list, the two outputs should be the same. Of
course, when testing another container, update the code below with the corresponding
member functions (push()can becomepush_back()).