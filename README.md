# Perlfunc

Python module for calling perl functions from python.
Just declare and decorate an empty python function
and it will invoke your perl function and return the 
results.

Read more at:
https://www.boriel.com/calling-perl-from-python.html

## Sample usage

First create a small Perl script named `mymodule.pl`:
```
sub myfunc
{
    my ($a, $b) = @_;
    return $a + $b;
}

1;
```

Now let's create a Python program that will invoke
the function `myfunc()` in the module `mymodule.pl`:

```
from perlfunc import perl5lib, perlfunc, perlreq

@perlfunc
@perlreq('myfunc.pl')
def myfunc(a, b):
    pass  # Empty body

print(myfunc(1, 3))  # Should print 4
```

Explanation:

 - First we import the decorators.
 - Then we create an empty (notice the `pass` keyword) function `myfunc` with the
   same parameters as the called function.
 - Finally we wrap the function using two decorators, `@perlreq` and `@perlfunc`  
 
Now we can call our python function `myfunc(a, b)` and the Perl one will be called. :)

### Decorators

 * `perlfunc`: mandatory. Use it to invoke a perl function **with the same name** as the python function.
 * `perlreq(<perl script>)`: imports the required module where the perl function is defined.
 * `perl5lib`: optional, defines a list of path to be added to the `PERL5LIB` path env var.
 
