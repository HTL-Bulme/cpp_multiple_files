# Working with Multiple Files - Build Systems


## Calculate Total Resistance

Implement a `struct Circuit` that stores the resistances of three different
resistors and a `bool` indicating whether the three resistors are in series or
parallel. Declare `struct Circuit` in `circuit.h`. Store the resistances using
double precision floating point numbers.
Create the following files: `circuit.c`, `circuit.h`, `main.c`, `ui.c`, `ui.h`
and implement the functions below.


```cpp
/* circuit.h, circuit.c */
// return the total resistance of the circuit
double calc_circuit_resistance(const Circuit& c);


/* ui.h, ui.c */
// read the resistances from stdin
// also ask the user whether a parallel or series connection is used
// return a new circuit struct containing the above data
Circuit read_circuit();
// print a visual representation of the struct; this can be something like
// -[220Ω]-[330Ω]-[220Ω]- and
//
//  ┌[220Ω]┐
// ─┼[330Ω]┼─
//  └[220Ω]┘
void draw_circuit(const Circuit& c);
// print the values of the resistors, whether a parallel or series connection
// is used and the total resistance
void print_circuit(const Circuit& c);


/* main.c */
// create at least two different circuits (one parallel and one serial)
// and use both draw_circuit(.) and print_circuit(.) on each of them
int main();
```

Declare all functions in the corresponding header files and include the header
files wherever needed.
Make sure to use `#include` guards in each of the header files.

For now, compile and test this task manually from the commandline.


## Inventory Management System

Your employer stores many different electric components (resistors, capacitors,
...). It is your duty to create an in-memory database to keep track of these
components. Create the following files to contain your program:
`inventory.{c,h}`, `interface.{c,h}`. Use the existing `main.c` and extend
`main(.)` to use your new code.

In `inventory.h` define a `struct Item`. Each `Item` stores

* 80 characters for the component type (resistor, capacitor, ...)
* unsigned holding the quantity of devices available
* double holding the value (resistance, capacity, ...)
* 20 characters for the unit (Ω, MΩ, µF, ...)

Create the following functions: 

```cpp
/* inventory.h, inventory.c */
// Return the total number of resistors in the inventory.
// Eg. there are 100 resistors with 330 ohm, 50 with 5600 ohm and 10 with
// 2 megaohm, the total number is 160.
std::size_t count_resistors(const std::vector<Item>& items);

// Return the total number of capacitors in the inventory.
std::size_t count_capacitors(const std::vector<Item>& items);


/* interface.h, interface.c */
// ask the user to enter a new item on the command-line;
// add the new item to the given list and return the count increased by one
// (since there is one more element in the inventory array)
void add_item(std::vector<Item>& items);

// print given item to stdout
void print_item(Item i);

// print all items, one per line
void print_items(const std::vector<Item>& items);

// command-line interface to create and manage an inventory
// start a loop that asks the user which action they want to perform
// `a` -> create a new item and add it to the inventory array
// `c` -> show the number of capacitors
// `e` -> exit the program
// `i n` -> show the n-th item (0-indexed) of the inventory array
// `h` -> show this help text
// `l` -> show the list of items
// `r` -> show the number of resistors
void cli();
```

In your existing `main(.)` add a call to `cli()`.
For now, compile and test this task manually from the commandline.


## Build Systems

### GNU Make
In order to be able to compile the above tasks conveniently, write a
GNU `Makefile` with the following high level targets:

* all - compile everything
* clean - clean up everything

Make sure to only (re-)compile what really needs to be compiled when `make`
is called. To do so, you will need to create additional targets for the
object files.

### CMake
Once the GNU `Makefile` works properly, create a `CMakeLists.txt` that
generates a `Makefile` for your platform. Test building your project out of
source with `cmake` (by convention, create the build in the `build`
subdirectory).

Finally, edit this `README.md` file and briefly explain at the beginning how
the project can be compiled. The
[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
has all the information you need on the syntax to get started.
