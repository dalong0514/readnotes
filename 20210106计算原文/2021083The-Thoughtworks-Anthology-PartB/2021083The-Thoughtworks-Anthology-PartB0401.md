# 0401. Functional Programming Techniques in Object-Oriented Languages

by Marc Needham

Functional programming languages have grown in popularity over the past few years, which has popularized some useful programming techniques that we can use even if our language of choice is predominantly object-oriented.

While the ideas behind functional programming have become popular only in the past couple of years, the underlying platform features that allow us to program in a functional way in C# have been built into the CLR since around 2005.

The C# language has evolved since then to the point where we can write code in C# that looks quite similar to that which could be written in F# — Microsoft’s functional programming language that has recently been made a first-class language for Visual Studio.

The functional programming ideas 1 themselves have been around for at least half a century.

In this essay, we’ll demonstrate these techniques with examples in C# and Ruby, although the ideas presented are also applicable in other similar languages such as Scala and Java.

4.1 Collections

When it comes to understanding how a functional approach to problem solving can be used, one of the first things to consider is the way that we view collections.

The Transformational Mind-Set

The most interesting mental paradigm switch when learning how to program in a functional way is how you deal with collections.

With an imperative approach, you think about each item in the collection individually, and you typically use a for each loop when working with that collection.

If we take a functional approach to solving problems with collections, our approach becomes much more about viewing the collection as a wholesomething that Patrick Logan refers to as a transformational mind-set.2 

We look at the original collection that we have and then visualize how we want it to look once we’ve transformed it, before working out which functions we need to apply to the collection to get it into that state.

Original -> () -> () -> () -> Final

It closely resembles the pipes and filters architecture where the data moves through a pipe, and the filters are represented by the different functions that can be applied to that data.

Our approach to dealing with collections in this way is possible by using what Bill Six calls functional collection patterns.3 

There are three main categories of operations on collections.

Map

The map pattern applies a function to each element in the collection and returns a new collection with the results of each function application (see Figure 1, The Map Function, on page 73). Therefore, if we want to get the first names of a group of people, we would write the following code:

var names = people.Select(person => person.FirstName)

rather than the following imperative equivalent:

2. http://www.markhneedham.com/blog/2010/01/20/functional-collectional-parameters-some-thoughts/#comment30627

3. http://www.ugrad.cs.jhu.edu/~wsix/collections.pdf

Filter

The filter pattern applies a predicate to each element in the collection and returns a new collection containing the elements that returned true for the predicate provided.

If we want to get only the people older than twenty-one years old, we would write the following code:

var peopleOlderThan21 = people.Where(person => person.Age > 21);

which is again simpler to read than the following imperative equivalent:

Reduce

The reduce pattern converts a collection to a single value by combining each element in turn via a user-supplied function.

If we want to get the ages of a group of people, we would write the following code:

var sumOfAges = people.Aggregate(0, (sum, person) => sum + person.Age);

as compared to this:

var sumOfAges = 0 foreach(var person : people) { sumOfAges += person.Age; }

Embracing Collections

Once we get into the habit of applying functions to collections, we start to see more opportunities to use a collection where before we might have used a different approach.

Quite frequently I’ve noticed that we end up with code that more closely describes the problem we’re trying to solve.

To take a simple example, if we wanted to get a person’s full name, we might write the following code:

which works fine, but we could write it like this instead:

public class Person { public string FullName() { return String.Join(" ", new[] { firstName, middleName, lastName }); } }

In this case, it doesn’t make a lot of difference, and there’s not that much repetition in the original version. However, as we end up doing the same operation to more and more values, it starts to make more sense to use a collection to solve the problem.

A fairly common problem I’ve come across is comparing two values against each other and then returning the smaller value. The typical way to do that would be as follows:

public class PriceCalculator { public double GetLowestPrice(double originalPrice, double salePrice) { var discountedPrice = ApplyDiscountTo(originalPrice); return salePrice > discountedPrice ? discountedPrice : salePrice; } }

But instead we could write it like this:

The second version is arguably easier to understand because the code reads as return the minimum of discountedPrice and salePrice, which perfectly describes what we want to do.

Don’t Forget to Encapsulate

One unfortunate side effect of the introduction of the LINQ library and the consequent ease with which we can now work with collections is that we tend to end up with collections being passed around more than we would have previously.

While this isn’t a problem in itself, what we’ve seen happen is that we’ll get a lot of repetition of operations on these collections that could have been encapsulated behind a method on the object that the collection is defined on. The other problem with passing around collections is that we can do anything we want with that collection elsewhere in the code.

We worked on a project where it became increasingly difficult to understand how certain items had ended up in a collection because you could add and remove any items from the collection from multiple places in the code.

Most of the time, it’s unlikely that the domain concept we’re trying to model with a collection actually has all the operations available on the C# collection APIs. LINQ typically gets the blame when these problems occur, but it’s more a case of it being used in the wrong place.

The following is a typical example of passing around a collection:

company.Employees.Select(employee => employee.Salary).Sum()

We could easily end up with the calculation of the employees’ salaries being done in more than one place, and our problem would be increased if we added more logic into the calculation.

It’s relatively easy to push this code onto the Company class.

Sometimes it makes sense to go further than this and create a wrapper around a collection.

For example, we might end up with a Division that also needs to provide the TotalSalary of its employees.

We can create an Employees class and push the logic onto that.

public class Employees {

private List<Employee> employees; public int TotalSalary {

get

{

return employees.Select(employee => employee.Salary).Sum();

} }

}

We’ve frequently seen a lot of resistance to the idea of creating classes like this, but if we start to have more logic on collections, then it can be quite a good move.

Lazy Evaluation

JavaScript sees extensive usage of its language. One problem that we can very easily run into when using iterators is evaluating the same bit of code multiple times.

For example, we might have the following code reading a list of names from a file:

which is then referenced from our PersonRepository.

public class PersonRepository {

private FileReader fileReader; IEnumerable<Person> GetPeople() { return fileReader.ReadNamesFromFile("names.txt") .Select(name => new Person(name)); }

}

It’s used elsewhere in our code like so:

var people = personRepository.GetPeople(); foreach(var person in people) { Console.WriteLine(person.Name); }

Console.WriteLine("Total number of people: " + person.Count());

The file actually ends up being read twice — once when printing out each of the names and then once when printing out the total number of people because the ReadNamesFromFile() method is lazy evaluated.

We can get around that by forcing eager evaluation.

4.2 First-Class and Higher-Order Functions

A higher-order function is one that takes in another function or returns a function as a result. We’ve seen plenty of examples of the former in the previous section.

Functions (lambda expressions) are first-class citizens in C#; we can use them in any place where we can use any other language entity. In fact, they are converted into delegates by the compiler and are merely syntactic sugar available to the developer at design time.

One thing the lambda syntax does give us is the ability to pass around functions much more easily.

The only thing we need to be careful with when passing around functions is ensuring that we’ll still be able to understand the code when we come back to it later. It’s very easy to write code that is completely incomprehensible when we start to make heavy use of the Func() and Action() delegates. One way to save ourselves some of the pain is to create named delegates to describe what the function actually does.

For example, if we were passing around the following function:

public class PremiumCalculator { public Money CalculatePremium(Func<Customer, DateTime, Money> calculation) { // calculate the premium } }

then we could replace each use of that function with the following delegate:

public delegate Money PremiumCalculation(Customer record, DateTime effectiveDate);

and then change the CalculatePremium() method to take in the delegate, like so:

public class PremiumCalculator { public Money CalculatePremium(PremiumCalculation calculation) { // calculate the premium } }

It’s not a match for match replacement, so we can’t move the code across to this solution incrementally — we’ll now have to go and change all the places that we were passing in a function to pass in the delegate instead.

Simplifying Gang of Four Patterns

One of the nice side effects of being able to pass around functions is that we’re able to massively reduce the amount of code that we need to write in order to implement some of the patterns from Design Patterns: Elements of Reusable Object-Oriented Software [GHJV95].

On a recent project, we wanted to find a generic way of caching the results of any request to around twenty to thirty web services that we were able to do with the following code, a variation of the Decorator pattern:4 

public class ServiceCache<TService> {

protected readonly TService service; private readonly ServiceCache cache; public ServiceCache(TService service, ServiceCache cache) { this.service = service; this.cache = cache; } protected TResp FromCacheOrService<TReq, TResp>(Func<TResp> service, TReq req) { var cached = cache.RetrieveIfExists(typeof(TService), typeof(TResp), req); if (cached == null) { cached = service(); cache.Add(typeof(TService), req, cached); } return (TResp) cached;

}

}

Since we’re able to pass a function to the FromCacheOrService() method, we do not need to add an abstract method to ServiceCache that each cached service would need to implement.

We can then use ServiceCache like so:

4.3 Minimizing State

One of the other key ideas behind functional programming is that of avoiding mutable state in our applications.

This is done by creating values rather than variables. In functional programming languages, you typically wouldn’t be able to change a value once it has been created; in other words, values are immutable.

It’s difficult and somewhat nonidiomatic to write code that is completely immutable in object-oriented languages, but we can still make our programs easier to understand by mutating state less frequently.

For example, hashes in Ruby are typically built like this:

delivery_costs = {} [:standard, :next_day, :same_day].each do |type| cost = DeliveryService.calculate_delivery_cost(delivery_address, type)

delivery_costs[type] = "%.2f" % cost

end

In this version of the code, we’re creating a variable called delivery_costs and then mutating it inside the each loop.

In this case, there’s probably not much problem with that, but if the definition of delivery_costs ends up moving away from the place where it’s actually populated, then we can end up quite confused about the state of the variable.

We could encapsulate that mutation with the following code, which uses the reduce() method:

delivery_costs = [:standard, :next_day, :same_day].reduce({}) do |result, type|

cost = DeliveryService.calculate_delivery_cost(delivery_address, type)

result[type] = "%.2f" % cost

result end

We could still go on and mutate delivery_costs elsewhere in the code if we wanted, but at least the initial creation and population process doesn’t involve mutation of that variable.

Another way that we can help reduce state in our applications is by performing calculations only when we actually need the result 5 rather than doing so ahead of time and storing the result in a field.

I’ve come across the following style of code fairly frequently:

We don’t actually need to know the monthlyPayment or the yearlyPayment unless the user of PaymentService makes a call to the appropriate methods.

We’ve also unnecessarily created state in the PaymentService class.

Instead of doing that, we can store the externalService and then calculate the payment values when needed.

One argument against transforming the code like this is that we might end up making more calls to ExternalService, but if we do get to the stage where that’s a problem, we can deal with it then.

4.4 Other Ideas

The following are a few other ideas.

Continuation Passing Style

Now we can start to use things like Continuation Passing Style (CPS), where we pass the rest of the computation as a function.

A simple example of CPS would be the following identity function:

static void Identity<T>(T value, Action<T> k) { k(value); }

which we might use like so:

Identity("foo", s => Console.WriteLine(s));

Here we’ve passed the remaining computation — in this case, just a print statement — to the Identity() function, which passes control of the program to that function.

In a more interesting example, 6 I converted the following controller code to follow CPS:

using an idea I’ve seen in jQuery code where you pass success and failure functions as callbacks to other functions.

The common theme in this code seemed to be that there were both success and failure paths for the code to follow depending on the result of a function, so I passed in both success and failure continuations.

I quite like that the try/catch block is no longer in the main() method, and the different things that are happening in this code now seem grouped together more than they were before.

In general, though, the way I read the code doesn’t seem that different.

Instead of following the flow of logic in the code from top to bottom, we just need to follow it from left to right, and since that’s not as natural, the code is more complicated than it was before.

4.5 Wrapping Up

One of the hazards of using an object-oriented language every day is that it seeps into your thinking. Embracing different paradigms allows you to see problems differently. I illustrated that many on-the-fly concatenations are really just list transformations; thinking about them in that way allows us to treat them more as first-class citizens. Think of collections as transformations, and you might find that you are solving a broader problem than you thought or, better yet, someone has already solved it for you.

You can also use these techniques to simplify design patterns. I showed how using different building blocks such as higher-order functions allows you to think about problems and their solutions differently. Learning any new programming paradigm is useful because it broadens your palette of approaches. Functional programming offers a lot of innovative ways to solve old problems.