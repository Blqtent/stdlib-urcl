# stdlib-urcl
stdlib interpretation in URCL
Currently contains functions:
- `malloc` (`size goes into R1`)
- `free` (`pointer goes into R1`)
- `printf` (`string pointer goes into R1, additional arguments can be used via PSH`)
- `print_str` (`string pointer goes into R1, literally just prints string`)
- `memcpy` (`destination pointer goes into R1, source pointer goes into R2, size goes into R3`)
- `init_malloc` (`no arguments, required for malloc and free to work`)
- `render_string` (`R1 - string pointer`)

# `malloc`
```
// ...
IMM R1 5 // size
CAL .malloc // output in R1
// ...
```
# `free`
```
IMM R1 5
CAL .malloc
// ...
MOV R1 R2 // putting pointer in R1
CAL .free // now there is no data in memory location at R1
```
# `printf`
```
IMM R1 .str
PSH .str2
CAL .printf // output in console: "hello world\n"

.str
  dw [ "hello %s" 0xa0 0 ]
.str2
  dw [ "world" 0 ]
```
# `print_str`
```
IMM R1 .str
CAL .print_str // output in console: "hello world\n"
.str
  DW [ "hello world" 0xa0 0 ]
```
# `memcpy`
```
IMM R1 .some_pointer // some pointer may be M0 or smth
IMM R2 .str
IMM R3 5 // size of .str, or amount of chars u want to copy
CAL .memcpy // now in R1 (.some_pointer) store some amount of chars from .str
```
# `init_malloc`
```
CAL .init_malloc // this simple
```
