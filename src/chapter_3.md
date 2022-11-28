# Compilation Stages

We know the term "compiling" basically that means converting human readable code
to machine generated code for the system to understand.Let's dive a bit deep 
into stages of compilation

So there are four basic stages of compilation which can be further bifurcated
to different complex stages. but for a high level understanding let's keep it
four.

PREPROCESSING - - - - > COMPILATION - - - - > ASSEMBLY - - - - > LINKING


1) PREPROCESSING :- It's a stage where all the contents of the header files gets
                    pasted into the source files and creates and intermediatery
                    file .we can easily confirm this by executing the following
                    command ``` gcc -E test.c ```

2) COMPILATION   :- This stage converts the preprocessed file into an assembly
                    generated file which contains the assembly code. you can 
                    check it out using ``` gcc -S test.c ```

3) ASSEMBLY     :- This stages is responsible to convert the assembly code into
                   the corresponding object code (non human readable code) . you can see
                   this by the following command ``` gcc -c test.c ```

4) LINKER       :- The linker takes one or more object code files and converts into 
                   a single executable file. we can see this using ``` gcc -c test.c
                   after this loader comes into the scenario which loads the program
                   into the memory




