# Abstract
Large Language Models showed significant potential in the Code Generation. However, Consistancy of the code is not reliable enough in General Code Generation. On top of that, Performance related code optimization is very important while Generating code. our Objective is to analyze our PerfCurator Performance related codes to setup LLM benchmarking for various individual tasks. An Ideal Model should be generating the performance level code on its own with the descriptions. those descriptions can be preserved to high level performance code on its own. any lack of in-consistancy while generating code or generating descriptions will create a in-consistancy. so we plan to evaluate LLMs self consistancy when they do tasks Programming language to Natural language and Natural language to programming language with focus of performance related code data. Our Focus is to Explain the self consistancy of the LLMs on performance level data in the PL to NL and NL to PL. then we designed a framework to create this self consistancy with our PerfCurator performance data to evaluate the LLMs. Our study is to consider the top Code Generation models to Evaluate the performance level Individual LLM Tasks with our LLM benchmarking. 

## Introduction

For Evaluating Code LLMs people using Existing benchmaking CodeXBleu, HumanEval and so on. But for Evaluating Performance level Generation of the code using LLM is yet to be Explored. It requires high quality performance data to set it up robust Evaluation design. Also Conventional LLM individual tasks with LLMs is Primarily focus on the 

1. Code Generation: we Generate Code Generation from the clear description. it is a NL to PL task.
2. Code Summarization: we generate Summary for the code. it is PL to NL task.

As from Paper "BEYOND ACCURACY: EVALUATING SELF-CONSISTENCY OF CODE LARGE LANGUAGE MODELS WITH IDENTITYCHAIN" they have mentioned evaluating these two tasks in isolation overlooks their symmetric nature. NL-to-PL and PL-to-NL Generation can be thought of as semantic-preserving translation and back-translation between the PL space and the NL space. Therefore, a trustworthy model should be able to correctly perform PL-to-NL Generation given programs generated by itself from previous NL-to-PL tasks. Similarly, it should correctly perform NL-to-PL Generation given natural language specifications generated by itself from previous PL-to-NL tasks.they call such a property “self-consistency”.

Here, Our Primary objective is to show the self consistancy of the LLMs using our Performance data. Our performance data is mined from Git Repository. these data is crafted by various authors in the Git repositories. Our data will have Code before, Code After, Commit message, Category of the performance issue and patch informations. we collected a lot of high level performance code and categorized them into APIMisuse, MemoryInefficiency, PoorConcurrencyControl, InefficientI/O, 
 NetworkBottlenecks, InefficientAlgorithm/Data-structure, Parallelization, Micro-architectural. so we want to evaluate the LLMs on these categories. 
 
 Our design for the Experimentation is we want to check the LLM how it preserves to Generate the Source code from it's own description. we start with code summarization (PL to NL) using a top 4 7B LLMs in the Hugggingface Code LLMs leaderboard. we have used CodeInterpreter 7B, Artigenz Coder 7B, CodeGwen 7B, NXCoder 7B. we provide code before,code after and commit message as a input. we crafted a prompt to focus on the Performance in-efficiency in the code and how they fixed it. from this we were able to generate quality description which talks about the performance issue and how it is optimized using these top LLMs. for Next step our Code Generation task ( NL to PL) we provide code before + descritoption to optimize the issue in the code before. finally, we augument the code before and after with the help of LLM to executable code then we execute them in a Python environment to check the performance. For Augumenting the inputs as a executable code,  we use GPT-4o. we select all the Augumented code Manually to filter High quality data points. which will be used for Executable Experiment.

so, Executable Experiment, we run the code for N iterations 5 times to make sure our code before run for more than 5s. Normally, our NL to PL stage, LLMs struggle to generate the Optimized code as some lack of information in the description causes LLM to be not consistent in those cases. we wanted to experiment these for our performance related Examples which is crafted by humans. 
