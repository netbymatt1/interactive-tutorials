Tutorial
--------

Dynamic allocation of memory is a very important subject in C. It allows building complex data structures such as linked lists. Allocating memory dynamically helps us to store data without initially knowing the size of the data in the time we wrote the program.

To allocate a chunk of memory dynamically, we need to have a pointer ready to store the location of the newly allocated memory. We can access memory that was allocated to us using that same pointer, and we can use that pointer to free the memory again, once we have finished using it.

Let's assume we want to dynamically allocate a person structure. The person is defined like this:

    typedef struct {
        char * name;
        int age;
    } person;

To allocate a new person in the `myperson` argument, we use the following syntax:

    person * myperson = (person *) malloc(sizeof(person));

This tells the compiler that we want to dynamically allocate just enough to hold a person struct in memory and then return a pointer of type `person` to the newly allocated data. The memory allocation function `malloc()` reserves the specified memory space. In this case, this is the size of `person` in bytes.

 The reason we write `(person *)` before the call to `malloc()` is that `malloc()` returns a "void pointer," which is a pointer that doesn't have a type. Writing `(person *)` in front of it is called *typecasting*, and changes the type of the pointer returned from `malloc()` to be `person`. However, it isn't strictly necessary to write it like this as C will implicitly convert the type of the returned pointer to that of the pointer it is assigned to (in this case, `myperson`) if you don't typecast it.

Note that `sizeof` is not an actual function, because the compiler interprets it and translates it to the actual memory size of the person struct.

To access the person's members, we can use the `->` notation:

    myperson->name = "John";
    myperson->age = 27;

After we are done using the dynamically allocated struct, we can release it using `free`:

    free(myperson);

Note that the free does not delete the `myperson` variable itself, it simply releases the data that it points to. The `myperson` variable will still point to somewhere in the memory - but after calling `free(myperson)` we are not allowed to access that area anymore. We must not use that pointer again until we allocate new data using it.

Exercise
--------

Use `malloc` to dynamically allocate a point structure.

Tutorial Code
-------------

    #include <stdio.h>
    #include <stdlib.h>

    typedef struct {
      int x;
      int y;
    } point;

    int main() {
      point * mypoint = NULL;

      /* Dynamically allocate a new point
         struct which mypoint points to here */

      mypoint->x = 10;
      mypoint->y =5 ;
      printf("mypoint coordinates: %d, %d\n", mypoint->x, mypoint->y);

      free(mypoint);
      return 0;
    }

Expected Output
---------------

    mypoint coordinates: 10, 5

Solution
--------

    #include <stdio.h>
    #include <stdlib.h>

    typedef struct {
      int x;
      int y;
    } point;

    int main() {
      point * mypoint;

      mypoint = (point *)malloc(sizeof(point));

      mypoint->x = 10;
      mypoint->y =5 ;
      printf("mypoint coordinates: %d, %d\n", mypoint->x, mypoint->y);

      free(mypoint);
      return 0;
    }
