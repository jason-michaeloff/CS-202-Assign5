Assignment 5
=========
# Team Members:
- Jason Michaeloff
- Mason 

# Expected Data Structures 150 words
One approach I think of is to have a bunch of Markers, these would be entries in a Dict that maps int -> int. The first int will be the ID and the next would be the number of lines it represents. We also have a set representing called marker IDs and a function that takes a Marker ID, checks if it is in the called set, and adds the respective lines of code to a total if it isn't (and ignores it if the Marker has been reached before). Then, our program combs through the codebase and adds the Markers to the Dict (assingn an ID and count the respective lines of code) + writes a line of code: our function call with the appropriate ID as a paramater, at every deviation in the execution flow. For instance, an "if elif else" statement would recieve 3 markers, one for each branch of exeuction. This way, we can count the total of lines in the program by totalling up the values of the Dict, and then we have our total due to our function. We can compare the numbers to get the percentage of total lines called, without worrying about the total getting messed up, if say, one test case calls one function 1000000 times (only first exec adds the lines to the total).

# Initial Code Examination 200 words
Appears to run as _.

# Detailed Code Examination 300 words
Placeholder text.

# Summary 150 words
Placeholder text.