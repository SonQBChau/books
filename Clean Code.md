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

> It is inappropriate for a comment to hold information better held in a different kind of system such as your source code control system, your issue tracking system, or any other record-keeping system. Change histories, for example, just clutter up source files with volumes of historical and uninteresting text. In general, meta-data such as authors, lastmodified-date, SPR number, and so on should not appear in comments. Comments should be reserved for technical notes about the code and design.

(Page 317). 

Obsolete Comment

(Page 317). 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMjE3NDczMzQsODMxODkyODUwXX0=
-->