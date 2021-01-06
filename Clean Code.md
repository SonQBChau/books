# Clean Code A Handbook of Agile Software Craftmanship

A very popular book for software developer. My biggest complaint is the book examples are written in Java,  which is my least used language. Nevertheless, most of the princicles can be applied in general, but still, for some specific sections, I wished it was not Java. 

Anyway, here are the highlights I have from reading this book.



**The Rough Draft**

> Most freshman programmers (like most grade-schoolers) don’t follow this advice particularly well. They believe that the primary goal is to get the program working. Once it’s “working,” they move on to the next task, leaving the “working” program in whatever state they finally got it to “work.” Most seasoned programmers know that this is professional suicide.

(Page 232). 


This is an exellent advice. Refactor after we get the code running is step we mostly ignore and procrastinate until we get spaghetti or abomination code. Also, this is a chance for us to re-asset our logic or we will forget it latter. 

>One of the best ways to ruin a program is to make massive changes to its structure in the name of improvement. Some programs never recover from such “improvements.” The problem is that it’s very hard to get the program working the same way it worked before the “improvement.”

(Page 243). 

This is true. So how do we fix this? Luckily, the author offer the solution

>To avoid this, I use the discipline of Test-Driven Development (TDD). One of the central doctrines of this approach is to keep the system running at all times. In other words, using TDD, I am not allowed to make a change to the system that breaks that system. Every change I make must keep the system working as it worked before.

(Page 244). 

I know that I should write more tests. However, my argument here is that without proper defined requirements, changing the approach would have to change the test case also. That would leave me 2 places to fix, one in my development code and one in my test code. Maybe the way I write my test code is wrong. Anyway, this is a good point to work on my testing habit


## Chapter 17: Smells and Heuristics
### Comments
**Inappropriate Information**
> In general, meta-data such as authors, lastmodified-date, SPR number, and so on should not appear in comments. Comments should be reserved for technical notes about the code and design.

**Obsolete Comment**
>A comment that has gotten old, irrelevant, and incorrect is obsolete. Get rid of it as quickly as possible. 

**Redundant Comment**
>A comment is redundant if it describes something that adequately describes itself. For example: 

    i++; // increment i 

>Another example is a Javadoc that says nothing more than (or even less than) the function signature: 

    /** 
     * @param sellRequest 
     * @return 
     * @throws ManagedComponentException 
     * / 
    public SellResponse beginSellItem(SellRequest sellRequest) throws ManagedComponentException 

>Comments should say things that the code cannot say for itself.

**Poorly Written Comment**
>Don’t ramble. Don’t state the obvious. Be brief.


**Commented-Out Code**
>When you see commented-out code, delete it! Don’t worry, the source code control system still remembers it. If anyone really needs it, he or she can go back and check out a previous version. Don’t suffer commented-out code to survive.

### Functions  
**Too Many Arguments**
>Functions should have a small number of arguments. No argument is best, followed by one, two, and three. More than three is very questionable and should be avoided. 

**Output Arguments**

>Output arguments are counterintuitive. Readers expect arguments to be inputs, not outputs. If your function must change the state of something, have it change the state of the object it is called on.

**Flag Arguments**  
>Boolean arguments loudly declare that the function does more than one thing. They are confusing and should be eliminated.

**Dead Function**
>Methods that are never called should be discarded. Keeping dead code around is wasteful.

### General
**Incorrect Behavior at the Boundaries**

>It seems obvious to say that code should behave correctly. The problem is that we seldom realize just how complicated correct behavior is. Developers often write functions that they think will work, and then trust their intuition rather than going to the effort to prove that their code works in all the corner and boundary cases.
There is no replacement for due diligence. Every boundary condition, every corner case, every quirk and exception represents something that can confound an elegant and intuitive algorithm. Don’t rely on your intuition. Look for every boundary condition and write a test for it.

**Obscured Intent**

>We want code to be as expressive as possible. Run-on expressions, Hungarian notation, and magic numbers all obscure the author’s intent. For example, here is the overTimePay function as it might have appeared:

    public int m_otCalc() { 
	    return iThsWkd * iThsRte +
		    (int) Math.round(0.5 * iThsRte * 
		    Math.max(0, iThsWkd - 400)
    ); }

>Small and dense as this might appear, it’s also virtually impenetrable. It is worth taking the time to make the intent of our code visible to our readers.

**Function Names Should Say What They Do**

>Look at this code:

    Date newDate = date.add(5);

>Would you expect this to add five days to the date? Or is it weeks, or hours? Is the date instance changed or does the function just return a new Date without changing the old one? You can’t tell from the call what the function does.
>If the function adds five days to the date and changes the date, then it should be called *addDaysTo* or *increaseByDays*. If, on the other hand, the function returns a new date that is five days later but does not change the date instance, it should be called *daysLater* or *daysSince*.

**Understand the Algorithm**
>Often the best way to gain this knowledge and understanding is to refactor the function into something that is so clean and expressive that it is obvious how it works.

**Functions Should Do One Thing**
>It is often tempting to create functions that have multiple sections that perform a series of operations. Functions of this kind do more than one thing, and should be converted into many smaller functions, each of which does one thing. 
>For example:

    public void pay() {  
		for (Employee e : employees) {
			if (e.isPayday()) {  
				Money pay = e.calculatePay(); e.deliverPay(pay);
			} 
		}
	}
>This bit of code does three things. It loops over all the employees, checks to see whether each employee ought to be paid, and then pays the employee. This code would be better written as:

    public void pay() {  
	    for (Employee e : employees)
		    payIfNecessary(e); 
	}
    
    private void payIfNecessary(Employee e) { 
	    if (e.isPayday())
		    calculateAndDeliverPay(e); }
    
    private void calculateAndDeliverPay(Employee e) { 
	    Money pay = e.calculatePay(); 
	    e.deliverPay(pay);
    }

**Encapsulate Boundary Conditions**
>Boundary conditions are hard to keep track of. Put the processing for them in one place. Don’t let them leak all over the code. We don’t want swarms of +1s and -1s scattered hither and yon. Consider this simple example from FIT:

    if(level + 1 < tags.length) 
    {
	    parts = new Parse(body, tags, level + 1, offset + endTag);
	    body = null; 
	}

>Notice that level+1 appears twice. This is a boundary condition that should be encapsu- lated within a variable named something like nextLevel.

    int nextLevel = level + 1; if(nextLevel < tags.length) 
    {
	    parts = new Parse(body, tags, nextLevel, offset + endTag);
	    body = null; 
    }

**Keep Configurable Data at High Levels**
>If you have a constant such as a default or configuration value that is known and expected at a high level of abstraction, do not bury it in a low-level function. Expose it as an argu- ment to that low-level function called from the high-level function. Consider the following code from FitNesse:

    public static void main(String[] args) throws Exception {
	    Arguments arguments = parseCommandLine(args); ...
    }
    
    public class Arguments {
	    public static final String DEFAULT_PATH = ".";  
	    public static final String DEFAULT_ROOT = "FitNesseRoot"; 
	    public static final int DEFAULT_PORT = 80;  
	    public static final int DEFAULT_VERSION_DAYS = 14;  
	    ...
    }
>The command-line arguments are parsed in the very first executable line of FitNesse. The default values of those arguments are specified at the top of the Argument class. You don’t have to go looking in low levels of the system for statements like this one:

    if (arguments.port == 0) // use 80 by default

>The configuration constants reside at a very high level and are easy to change. They get passed down to the rest of the application. The lower levels of the application do not own the values of these constants.

**Avoid Transitive Navigation**
>In general we don’t want a single module to know much about its collaborators. More specifically, if A collaborates with B, and B collaborates with C, we don’t want modules that use A to know about C. (For example, we don’t want `a.getB().getC().doSomething();`.)
>
>Rather we want our immediate collaborators to offer all the services we need. We should not have to roam through the object graph of the system, hunting for the method we want to call. Rather we should simply be able to say: `myCollaborator.doSomething().`

**Choose Descriptive Names**
>Don’t be too quick to choose a name. Make sure the name is descriptive. Remember that meanings tend to drift as software evolves, so frequently reevaluate the appropriateness of the names you choose.
>Consider the code below:

    public int x() { 
	    int q = 0; 
	    int z = 0;
        for (int kk = 0; kk < 10; kk++) { 
    	    if (l[z] == 10)  
    	    {
	    	    q += 10 + (l[z + 1] + l[z + 2]);
	    	    z += 1; 
	    	}
    	    else if (l[z] + l[z + 1] == 10) 
    	    {
	    	    q += 10 + l[z + 2];
	    	    z += 2; 
	    	} 
	    	else 
	    	{
	    	    q += l[z] + l[z + 1];
	    	    z += 2; 
    	    }
    	  }
    	  return q; 
        }

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5NzUxNjk0NywxMjI5NjY1NDI0LC0xMT
kyMTIxMzAzLDg3MTcxMjk1MCw1OTY0NjA1NDksNTk0ODA3MTQ0
LC0zNzA0NTg0NjIsOTMxMDQ5ODY2LC01NDc2MTI5ODQsMTg4Mz
AxNTgzNiw4MzE4OTI4NTBdfQ==
-->