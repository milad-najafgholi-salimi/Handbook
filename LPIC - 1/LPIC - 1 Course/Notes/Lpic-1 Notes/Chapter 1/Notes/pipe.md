With the pipe, you can redirect `STDOUT`, `STDIN`, and `STDERR` between multiple commands all on one command line. Now that is powerful redirection.
The syntax for pipe redirection shows that the first command, COMMAND1, is executed. Its `STDOUT` is redirected as `STDIN` into the second command, COMMAND2. Also, you can pipe more commands together than just two. Keep in mind that any command in the pipeline has its `STDOUT` redirected as `STDIN` to the next command in the pipeline.

![pic-71](Pics/71.png)

