Assignment 5
=========
# Team Members:
- Jason Michaeloff
- Mason 


# Expected Data Structures 150 words
One approach I think of is to have a bunch of Markers, these would be entries in a Dict that maps int -> int. The first int will be the ID and the next would be the number of lines it represents. We also have a set representing called marker IDs and a function that takes a Marker ID, checks if it is in the called set, and adds the respective lines of code to a total if it isn't (and ignores it if the Marker has been reached before). Then, our program combs through the codebase and adds the Markers to the Dict (assingn an ID and count the respective lines of code) + writes a line of code: our function call with the appropriate ID as a paramater, at every deviation in the execution flow. For instance, an "if elif else" statement would recieve 3 markers, one for each branch of exeuction. This way, we can count the total of lines in the program by totalling up the values of the Dict, and then we have our total due to our function. We can compare the numbers to get the percentage of total lines called, without worrying about the total getting messed up, if say, one test case calls one function 1000000 times (only first exec adds the lines to the total).


# Initial Code Examination 200 words
The provided coveragepy program code measures which lines in a Python program run during testing, with two major parts. One part runs and manages all the tests, the other analyzes the code to figure out which lines can run.

For the test-running function of the code, an environment is set up, the method for tracing execution (differing python cores) is prepared, and coverage measurement starts before running pytest. It also works with environment vars, files, and objects to store execution data to save the collected results of tracked subprocesses and figure out exceptions and elements to ignore.

The analysis function focuses on bytecode, using mainly dictionaries and line numbers. It walks through compiled code objects, including nested functions. It gathers line numbers, from metadata I think, and makes the bytcode position to source line mappings. The core data it's working with is primarily dictionaries like the byte offset-to-line mapping, code objects, and line-number collections.

Overall, we were partially wrong with our hypothesis of inserting markers into source code. Instead of relying on that coverage.py focuses on Python built-in tracing and bytcode information to record the lines that execute, comparing that to a thorough identification of the program's total lines.


# Detailed Code Examination 300 words
We focused on the class PyTracer, since that is the focus of coverage.py collecting data for execution. The most significant data structure in the file is self.data, more or less a dictionary with keys by file names, so each value contains the executed lines or sometimes branches. This stores the raw coverage results, and is passed into the tracer after a lot of updating in execution.

Another interesting use of data structures is the self.data_stack, which is a list kind of converted into a stack. It appear to be a series of tuples with the file trace data and name, line number previously executed, and new context started, which is basically the call stacks we discussed in lecture.

For each function call event == 'call', the tracer will push the current state to data_stack. When there is a return or othwise exiting tracing the previous state is popped off, making sure tracking nested functions works.

Meanwhile, the _trace method is constantly called by the setup system for tracing; this sys.settrace checks each even to decide whether the file should be traced. If it should be, the executed line is recorded in self.data and sets make sure that there are no repeats in lines stored. Overall a dictionary and stack are the primary data structures focused on to accurately measure coverage.


# Summary 150 words
Coverage.py has descriptive naming, thorough comments, and functions that are easy to understand without extra docs. Functionality is split into many files and modules. Type hints are used extensively, as in our CSC202 class. Also similar to our class, the functions have purpose statements (just under the headers). If I had to maintain this code, the onboarding cost would be relatively smooth thanks to its self-documenting style. My code, on the other hand (aside from the code for this class) is typically much less consistent on type hints and comments. For instance, sqldata.py's CoverageData class contains 80 lines of documentation comments right at the top. Would I do this to my own code? Probably not, though I see the value of it for a polished and easy to understand program. The CONTRIBBUTORS.txt file lists hundreds of names, so this project had to be good for collaborating.