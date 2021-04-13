---
layout: post
title: "Working with legacy code"
date: 2021-04-13 12:00:00 +0000
categories: legacy
---
## What is legacy code?
There is some debate about what exactly constitutes “legacy code”, but it is generally older code which is difficult to maintain. We expand below on what makes code difficult to maintain and suggest a general approach to improving it.

## What makes code difficult to maintain? 
There are many articles written about software best practices and how to make code easier to maintain.  Example features of legacy code include:
- “Brittleness” - tiny modifications can have a disastrous impact in totally unexpected places. 
- A history of taking shortcuts and quick fixes 
- A lack of modern tools (e.g. testing frameworks, containerisation, CI) 
- Low test coverage or low-quality tests 
- Poor, incomplete or out-of-date documentation 
- A lack of modularity and poorly-defined interfaces 
- Code that is hard or impossible to understand 

## Why work on legacy code?
There are a number of reasons why you might want to work on legacy code, for example, if you need to fix a bug, run the software on a different computer (or updated operating system), add a new feature, or integrate it into newer code. Sometimes, you can save time and effort by reusing legacy code. (Sometimes it is better to rewrite it from scratch!)

## What approach to take?
Sometimes, in preparation for future work, you can justify (and get funding/support for) putting in a significant focussed effort to make code more maintainable without providing other value at the same time.  This could be justified from the perspective of saving time in the long run, or reducing risk.  However, often a large effort to clean up the entire code is not possible, and instead you must work to improve the code with small incremental improvements over time. 

The “boy scout principle” (“Always leave the campground cleaner than you found it.”) is one approach that often works well.  This continuous improvement method can be a sustainable approach to improving a codebase over time, without the same need to justify how you are spending your time to others.  It does require buy-in from everyone who might modify the code, and it is worthwhile putting in significant time and effort to get that. 

It is often worth treating some parts of the code as “black boxes” that don't need to be understood or modified. This can allow the areas of most benefit to be focussed on first, avoiding rabbit-holes of refactoring for little or no gain. 

This is a roughly ordered list of things you might do: 
1. Decide on the aim and the scope of the work
2. Ensure the code is under version control (e.g. git)
3. Find out how the code is being used, and start updating the documentation, which may be incomplete, poorly written and/or out-of-date 
4. Start trying to understand the relevant code
   1. Continuing to improve documentation, and maybe adding comments to the code. (It may not be worth thoroughly commenting code – time might be better spent adding tests: “comments that compile”.) 
   2. Some parts of the code may not be relevant to the changes you need to make, and it can be helpful to treat some parts as an untouched black box.
   3. Review how bad the code is, and if the planned change is feasible!
5. Ensure you have a reasonable development environment – For example, if the software can only run in one folder which is in the old developer’s personal workspace, then you might want to consider updating the build system
6. Ensure you have sufficient test coverage of any code that you will be modifying
   1. “sufficient” is often hard to define.  One “percentage covered” value for the whole codebase can be unhelpful.  The quality of the tests and functionality covered are both important.
   2. Test coverage visualization tools can be helpful 
   3. You want automated tests, ideally in CI
   4. When adding new tests, find users of the code, and consider their use cases. (Existing functionality is not always captured in tests, and can be difficult to discover.)
   5. When tests fail, don’t assume that the test is correct.
   6. (Also, linters and other static analysis tools can be helpful)
   7. (How to test software is a big area – we’re not going to go into too much detail here)
7. Refactor code to prepare for modification, and help to understand it 
   1. Refactoring is changing the structure of the code without changing its result 
   2. Particularly simplifying the code (and reducing the size of the codebase) 
   3. Untangling spaghetti code, and break it up into more manageable pieces 
   4. Aiming to remove global state so that functions can be idempotent and are easier to test
   5. Using modern good software engineering practices
   6. Making changes incrementally
8. (and then eventually) Make the required change (following good software engineering practices) 
   
As part of using modern good software engineering practices, if you are not going to be the only person ever modifying this codebase, then you should consider adopting shared practices, such as enforcing a review of every merge request, and working to an agreed coding standard.