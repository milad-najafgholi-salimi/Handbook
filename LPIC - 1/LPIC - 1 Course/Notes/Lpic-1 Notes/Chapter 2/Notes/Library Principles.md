A system `library` is a collection of items, such as program functions. `Functions` are self-contained code modules that perform a specific task within an application, such as opening and reading a data file. 

The benefit of splitting functions into separate library files is that multiple applications that use the same functions can share the same library files. These files full of functions make it easier to distribute applications, but also make it more complicated to keep track of what library files are installed with which applications.

Linux supports two different flavors of libraries. One is *static libraries* (also called `statically linked libraries`) that are copied into an application when it is compiled. The other flavor is *shared libraries* (also called `dynamic libraries`) where the library functions are copied into memory and bound to the application when the program is launched. This is called `loading a library`.

![pic-27](Pics/27.png)

On Linux, like application packages, library files have naming conventions. A shared library file employs the following filename format:
`libLIBRARYNAME.so.VERSION`

Keep in mind that just as with packages, these are naming guidelines (similar to pirate codes) and not laws.
