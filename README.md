# llm-coding-analysis

## Overview 

This code evaluates the accuracy of LLMs in predicitng Python function outputs. The problems were taken from CRUXEval, and the models tested were **Gemini 2.0 Flash** and **DeepSeek R1**. 

## Results
### Gemini Performance 
- Total Problems Evaluated: 100
- Correct Predictions: 92
- Incorrect Predictions: 8

Note that for one problem, Gemini outputted the correct answer with incorrect formatting.

### DeepSeek Performance (on Gemini's Incorrect Cases)
- Total Problems Evaluated: 8
- Correct Predictions: 4
- Incorrect Predictions: 4

Since we are able to view DeepSeek's reasoning steps, we can understand why it got problems incorrect.

Problem 0: DeepSeek got the correct solution, but just formatted the answer wrong. 

Problem 1: DeepSeek gets to the `return [0]` line of code (which is the correct solution), but does not recognize that the return statement ends the execution of the function. Instead, DeepSeek continues after the return statement and outputs the incorrect solution of `0` at the end. In this case, DeepSeek fails the **Validity** criterion, as it made an invalid logical step. 

Problem 2: DeepSeek seems to be struggling with figuring out how Python behaves when we remove elements from a list we are iterating through. DeepSeek fails to realize that when we pop an element from the list, this causes elements to be skipped in our iteration. This seems like an issue with **Groundedness**, as DeepSeek is incorrect in its knowledge of Python's behavior. Note that it could also be the case that DeepSeek does know how Python should behave in this situation, but was unable to make the correct logical step from this information. 

Problem 3: DeepSeek has the correct reasoning until the last line of the code `return '+'.join(ls)`. It is able to figure out what the contents of `ls` should be, but it incorrectly determines the output of the join function. However, it seems to understand what `join` is supposed to do, so this is another **Validity** error. 

It seems that the biggest cause of incorrect answers for DeepSeek was making invalid logical steps. For all the problems, DeepSeek seemed to fully understand the query and the input function (which shows query groundedness). However, for problem 2, DeepSeek seemed not understand Python behavior, which is an error in evidence groundedness. For all problems, DeepSeek had fairly **Coherent** steps, as each step followed from the previous one, and its reasoning was easy to follow throughout. 

## Conclusion 
Overall, the reasoning LLMs performed very well on this dataset of problems. Out of 100 problems, Gemini only got 8 incorrect, and 1 was due to improper formating. Of these 8 problems, DeepSeek was able to get 4 of them correct. From analyzing DeepSeek's reasoning on the problems it got incorrect, it seems that the biggest issue it had was making invalid logical steps. 
