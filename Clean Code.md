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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NjI4ODU4NDQsOTMxMDQ5ODY2LC01ND
c2MTI5ODQsMTg4MzAxNTgzNiw4MzE4OTI4NTBdfQ==
-->