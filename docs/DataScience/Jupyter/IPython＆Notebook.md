# IPython & Notebook

## 参考資料

* [Documentation](https://ipython.readthedocs.io/en/stable/)
* [IPython Cookbook](https://ipython-books.github.io)

```python
?


    IPython -- An enhanced Interactive Python
    =========================================
    
    IPython offers a fully compatible replacement for the standard Python
    interpreter, with convenient shell features, special commands, command
    history mechanism and output results caching.
    
    At your system command line, type 'ipython -h' to see the command line
    options available. This document only describes interactive features.
    
    GETTING HELP
    ------------
    
    Within IPython you have various way to access help:
    
      ?         -> Introduction and overview of IPython's features (this screen).
      object?   -> Details about 'object'.
      object??  -> More detailed, verbose information about 'object'.
      %quickref -> Quick reference of all IPython specific syntax and magics.
      help      -> Access Python's own help system.
    
    If you are in terminal IPython you can quit this screen by pressing `q`.
    
    
    MAIN FEATURES
    -------------
    
    * Access to the standard Python help with object docstrings and the Python
      manuals. Simply type 'help' (no quotes) to invoke it.
    
    * Magic commands: type %magic for information on the magic subsystem.
    
    * System command aliases, via the %alias command or the configuration file(s).
    
    * Dynamic object information:
    
      Typing ?word or word? prints detailed information about an object. Certain
      long strings (code, etc.) get snipped in the center for brevity.
    
      Typing ??word or word?? gives access to the full information without
      snipping long strings. Strings that are longer than the screen are printed
      through the less pager.
    
      The ?/?? system gives access to the full source code for any object (if
      available), shows function prototypes and other useful information.
    
      If you just want to see an object's docstring, type '%pdoc object' (without
      quotes, and without % if you have automagic on).
    
    * Tab completion in the local namespace:
    
      At any time, hitting tab will complete any available python commands or
      variable names, and show you a list of the possible completions if there's
      no unambiguous one. It will also complete filenames in the current directory.
    
    * Search previous command history in multiple ways:
    
      - Start typing, and then use arrow keys up/down or (Ctrl-p/Ctrl-n) to search
        through the history items that match what you've typed so far.
    
      - Hit Ctrl-r: opens a search prompt. Begin typing and the system searches
        your history for lines that match what you've typed so far, completing as
        much as it can.
    
      - %hist: search history by index.
    
    * Persistent command history across sessions.
    
    * Logging of input with the ability to save and restore a working session.
    
    * System shell with !. Typing !ls will run 'ls' in the current directory.
    
    * The reload command does a 'deep' reload of a module: changes made to the
      module since you imported will actually be available without having to exit.
    
    * Verbose and colored exception traceback printouts. See the magic xmode and
      xcolor functions for details (just type %magic).
    
    * Input caching system:
    
      IPython offers numbered prompts (In/Out) with input and output caching. All
      input is saved and can be retrieved as variables (besides the usual arrow
      key recall).
    
      The following GLOBAL variables always exist (so don't overwrite them!):
      _i: stores previous input.
      _ii: next previous.
      _iii: next-next previous.
      _ih : a list of all input _ih[n] is the input from line n.
    
      Additionally, global variables named _i<n> are dynamically created (<n>
      being the prompt counter), such that _i<n> == _ih[<n>]
    
      For example, what you typed at prompt 14 is available as _i14 and _ih[14].
    
      You can create macros which contain multiple input lines from this history,
      for later re-execution, with the %macro function.
    
      The history function %hist allows you to see any part of your input history
      by printing a range of the _i variables. Note that inputs which contain
      magic functions (%) appear in the history with a prepended comment. This is
      because they aren't really valid Python code, so you can't exec them.
    
    * Output caching system:
    
      For output that is returned from actions, a system similar to the input
      cache exists but using _ instead of _i. Only actions that produce a result
      (NOT assignments, for example) are cached. If you are familiar with
      Mathematica, IPython's _ variables behave exactly like Mathematica's %
      variables.
    
      The following GLOBAL variables always exist (so don't overwrite them!):
      _ (one underscore): previous output.
      __ (two underscores): next previous.
      ___ (three underscores): next-next previous.
    
      Global variables named _<n> are dynamically created (<n> being the prompt
      counter), such that the result of output <n> is always available as _<n>.
    
      Finally, a global dictionary named _oh exists with entries for all lines
      which generated output.
    
    * Directory history:
    
      Your history of visited directories is kept in the global list _dh, and the
      magic %cd command can be used to go to any entry in that list.
    
    * Auto-parentheses and auto-quotes (adapted from Nathan Gray's LazyPython)
    
      1. Auto-parentheses
            
         Callable objects (i.e. functions, methods, etc) can be invoked like
         this (notice the commas between the arguments)::
           
             In [1]: callable_ob arg1, arg2, arg3
           
         and the input will be translated to this::
           
             callable_ob(arg1, arg2, arg3)
           
         This feature is off by default (in rare cases it can produce
         undesirable side-effects), but you can activate it at the command-line
         by starting IPython with `--autocall 1`, set it permanently in your
         configuration file, or turn on at runtime with `%autocall 1`.
    
         You can force auto-parentheses by using '/' as the first character
         of a line.  For example::
           
              In [1]: /globals             # becomes 'globals()'
           
         Note that the '/' MUST be the first character on the line!  This
         won't work::
           
              In [2]: print /globals    # syntax error
    
         In most cases the automatic algorithm should work, so you should
         rarely need to explicitly invoke /. One notable exception is if you
         are trying to call a function with a list of tuples as arguments (the
         parenthesis will confuse IPython)::
           
              In [1]: zip (1,2,3),(4,5,6)  # won't work
           
         but this will work::
           
              In [2]: /zip (1,2,3),(4,5,6)
              ------> zip ((1,2,3),(4,5,6))
              Out[2]= [(1, 4), (2, 5), (3, 6)]
    
         IPython tells you that it has altered your command line by
         displaying the new command line preceded by -->.  e.g.::
           
              In [18]: callable list
              -------> callable (list)
    
      2. Auto-Quoting
        
         You can force auto-quoting of a function's arguments by using ',' as
         the first character of a line.  For example::
           
              In [1]: ,my_function /home/me   # becomes my_function("/home/me")
    
         If you use ';' instead, the whole argument is quoted as a single
         string (while ',' splits on whitespace)::
           
              In [2]: ,my_function a b c   # becomes my_function("a","b","c")
              In [3]: ;my_function a b c   # becomes my_function("a b c")
    
         Note that the ',' MUST be the first character on the line!  This
         won't work::
           
              In [4]: x = ,my_function /home/me    # syntax error
```

```python
quickref

    
    IPython -- An enhanced Interactive Python - Quick Reference Card
    ================================================================
    
    obj?, obj??      : Get help, or more help for object (also works as
                       ?obj, ??obj).
    ?foo.*abc*       : List names in 'foo' containing 'abc' in them.
    %magic           : Information about IPython's 'magic' % functions.
    
    Magic functions are prefixed by % or %%, and typically take their arguments
    without parentheses, quotes or even commas for convenience.  Line magics take a
    single % and cell magics are prefixed with two %%.
    
    Example magic function calls:
    
    %alias d ls -F   : 'd' is now an alias for 'ls -F'
    alias d ls -F    : Works if 'alias' not a python name
    alist = %alias   : Get list of aliases to 'alist'
    cd /usr/share    : Obvious. cd -<tab> to choose from visited dirs.
    %cd??            : See help AND source for magic %cd
    %timeit x=10     : time the 'x=10' statement with high precision.
    %%timeit x=2**100
    x**100           : time 'x**100' with a setup of 'x=2**100'; setup code is not
                       counted.  This is an example of a cell magic.
    
    System commands:
    
    !cp a.txt b/     : System command escape, calls os.system()
    cp a.txt b/      : after %rehashx, most system commands work without !
    cp ${f}.txt $bar : Variable expansion in magics and system commands
    files = !ls /usr : Capture system command output
    files.s, files.l, files.n: "a b c", ['a','b','c'], 'a\nb\nc'
    
    History:
    
    _i, _ii, _iii    : Previous, next previous, next next previous input
    _i4, _ih[2:5]    : Input history line 4, lines 2-4
    exec _i81        : Execute input history line #81 again
    %rep 81          : Edit input history line #81
    _, __, ___       : previous, next previous, next next previous output
    _dh              : Directory history
    _oh              : Output history
    %hist            : Command history of current session.
    %hist -g foo     : Search command history of (almost) all sessions for 'foo'.
    %hist -g         : Command history of (almost) all sessions.
    %hist 1/2-8      : Command history containing lines 2-8 of session 1.
    %hist 1/ ~2/     : Command history of session 1 and 2 sessions before current.
    %hist ~8/1-~6/5  : Command history from line 1 of 8 sessions ago to
                       line 5 of 6 sessions ago.
    %edit 0/         : Open editor to execute code with history of current session.
    
    Autocall:
    
    f 1,2            : f(1,2)  # Off by default, enable with %autocall magic.
    /f 1,2           : f(1,2) (forced autoparen)
    ,f 1 2           : f("1","2")
    ;f 1 2           : f("1 2")
    
    Remember: TAB completion works in many contexts, not just file names
    or python names.
    
    The following magic functions are currently available:
    
    %alias:
        Define an alias for a system command.
    %alias_magic:
        ::
    %autoawait:
        
    %autocall:
        Make functions callable without having to type parentheses.
    %automagic:
        Make magic functions callable without having to type the initial %.
    %autosave:
        Set the autosave interval in the notebook (in seconds).
    %bookmark:
        Manage IPython's bookmark system.
    %cat:
        Alias for `!cat`
    %cd:
        Change the current working directory.
    %clear:
        Clear the terminal.
    %colors:
        Switch color scheme for prompts, info system and exception handlers.
    %conda:
        Run the conda package manager within the current kernel.
    %config:
        configure IPython
    %connect_info:
        Print information for connecting other clients to this kernel
    %cp:
        Alias for `!cp`
    %debug:
        ::
    %dhist:
        Print your history of visited directories.
    %dirs:
        Return the current directory stack.
    %doctest_mode:
        Toggle doctest mode on and off.
    %ed:
        Alias for `%edit`.
    %edit:
        Bring up an editor and execute the resulting code.
    %env:
        Get, set, or list environment variables.
    %gui:
        Enable or disable IPython GUI event loop integration.
    %hist:
        Alias for `%history`.
    %history:
        ::
    %killbgscripts:
        Kill all BG processes started by %%script and its family.
    %ldir:
        Alias for `!ls -F -G -l %l | grep /$`
    %less:
        Show a file through the pager.
    %lf:
        Alias for `!ls -F -l -G %l | grep ^-`
    %lk:
        Alias for `!ls -F -l -G %l | grep ^l`
    %ll:
        Alias for `!ls -F -l -G`
    %load:
        Load code into the current frontend.
    %load_ext:
        Load an IPython extension by its module name.
    %loadpy:
        Alias of `%load`
    %logoff:
        Temporarily stop logging.
    %logon:
        Restart logging.
    %logstart:
        Start logging anywhere in a session.
    %logstate:
        Print the status of the logging system.
    %logstop:
        Fully stop logging and close log file.
    %ls:
        Alias for `!ls -F -G`
    %lsmagic:
        List currently available magic functions.
    %lx:
        Alias for `!ls -F -l -G %l | grep ^-..x`
    %macro:
        Define a macro for future re-execution. It accepts ranges of history,
    %magic:
        Print information about the magic function system.
    %man:
        Find the man page for the given command and display in pager.
    %matplotlib:
        ::
    %mkdir:
        Alias for `!mkdir`
    %more:
        Show a file through the pager.
    %mv:
        Alias for `!mv`
    %notebook:
        ::
    %page:
        Pretty print the object and display it through a pager.
    %pastebin:
        Upload code to dpaste's paste bin, returning the URL.
    %pdb:
        Control the automatic calling of the pdb interactive debugger.
    %pdef:
        Print the call signature for any callable object.
    %pdoc:
        Print the docstring for an object.
    %pfile:
        Print (or run through pager) the file where an object is defined.
    %pinfo:
        Provide detailed information about an object.
    %pinfo2:
        Provide extra detailed information about an object.
    %pip:
        Run the pip package manager within the current kernel.
    %popd:
        Change to directory popped off the top of the stack.
    %pprint:
        Toggle pretty printing on/off.
    %precision:
        Set floating point precision for pretty printing.
    %prun:
        Run a statement through the python code profiler.
    %psearch:
        Search for object in namespaces by wildcard.
    %psource:
        Print (or run through pager) the source code for an object.
    %pushd:
        Place the current dir on stack and change directory.
    %pwd:
        Return the current working directory path.
    %pycat:
        Show a syntax-highlighted file through a pager.
    %pylab:
        ::
    %qtconsole:
        Open a qtconsole connected to this kernel.
    %quickref:
        Show a quick reference sheet 
    %recall:
        Repeat a command, or get command to input line for editing.
    %rehashx:
        Update the alias table with all executable files in $PATH.
    %reload_ext:
        Reload an IPython extension by its module name.
    %rep:
        Alias for `%recall`.
    %rerun:
        Re-run previous input
    %reset:
        Resets the namespace by removing all names defined by the user, if
    %reset_selective:
        Resets the namespace by removing names defined by the user.
    %rm:
        Alias for `!rm`
    %rmdir:
        Alias for `!rmdir`
    %run:
        Run the named file inside IPython as a program.
    %save:
        Save a set of lines or a macro to a given filename.
    %sc:
        Shell capture - run shell command and capture output (DEPRECATED use !).
    %set_env:
        Set environment variables.  Assumptions are that either "val" is a
    %store:
        Lightweight persistence for python variables.
    %sx:
        Shell execute - run shell command and capture output (!! is short-hand).
    %system:
        Shell execute - run shell command and capture output (!! is short-hand).
    %tb:
        Print the last traceback.
    %time:
        Time execution of a Python statement or expression.
    %timeit:
        Time execution of a Python statement or expression
    %unalias:
        Remove an alias
    %unload_ext:
        Unload an IPython extension by its module name.
    %who:
        Print all interactive variables, with some minimal formatting.
    %who_ls:
        Return a sorted list of all interactive variables.
    %whos:
        Like %who, but gives some extra information about each variable.
    %xdel:
        Delete a variable, trying to clear it from anywhere that
    %xmode:
        Switch modes for the exception handlers.
    %%!:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%HTML:
        Alias for `%%html`.
    %%SVG:
        Alias for `%%svg`.
    %%bash:
        %%bash script magic
    %%capture:
        ::
    %%debug:
        ::
    %%file:
        Alias for `%%writefile`.
    %%html:
        ::
    %%javascript:
        Run the cell block of Javascript code
    %%js:
        Run the cell block of Javascript code
    %%latex:
        Render the cell as a block of latex
    %%markdown:
        Render the cell as Markdown text block
    %%perl:
        %%perl script magic
    %%prun:
        Run a statement through the python code profiler.
    %%pypy:
        %%pypy script magic
    %%python:
        %%python script magic
    %%python2:
        %%python2 script magic
    %%python3:
        %%python3 script magic
    %%ruby:
        %%ruby script magic
    %%script:
        ::
    %%sh:
        %%sh script magic
    %%svg:
        Render the cell as an SVG literal
    %%sx:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%system:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%time:
        Time execution of a Python statement or expression.
    %%timeit:
        Time execution of a Python statement or expression
    %%writefile:
        ::
```

## GLOBAL 変数(履歴)  

* _i: 一個前の入力
* _ii: 二個前の入力
* _iii: 三個前の入力
* _ih, In : 入力のリスト(input history)
* _i<number\>: number番目の入力
* _: 一個前の出力
* __: 二個前の出力
* ___: 三個前の出力
* _oh, Out: 出力履歴の辞書(output history)
* _<number\>: number番目の出力
* _dh: アクセスしたディレクトリの履歴(directory history)

## Object 内観

```python
import numpy as np
import pandas as pd

df = pd.DataFrame(np.arange(20).reshape(5, 4), columns=list("abcd"))
```

```python
df?
# `?df`と同じ

df??
# `??df`と同じ効果
print?
# この様に、関数やメソッドにも応用できる
```

```python
import numpy as np

np.lookfor("create array")

    Search results for 'create array'
    ---------------------------------
    numpy.array
        Create an array.
    numpy.memmap
        Create a memory-map to an array stored in a *binary* file on disk.
    numpy.diagflat
        Create a two-dimensional array with the flattened input as a diagonal.
    numpy.fromiter
        Create a new 1-dimensional array from an iterable object.
    numpy.partition
        Return a partitioned copy of an array.
    numpy.ctypeslib.as_array
        Create a numpy array from a ctypes array or POINTER.
    numpy.ma.diagflat
        Create a two-dimensional array with the flattened input as a diagonal.
    numpy.ma.make_mask
        Create a boolean mask from an array.
    numpy.lib.Arrayterator
        Buffered iterator for big arrays.
    numpy.ctypeslib.as_ctypes
        Create and return a ctypes object from a numpy array.  Actually
    numpy.ma.mrecords.fromarrays
        Creates a mrecarray from a (flat) list of masked arrays.
    numpy.ma.mvoid.__new__
        Create a new masked array from scratch.
    numpy.ma.MaskedArray.__new__
        Create a new masked array from scratch.
    numpy.ma.mrecords.fromtextfile
        Creates a mrecarray from data stored in the file `filename`.
    numpy.asarray
        Convert the input to an array.
    numpy.ndarray
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.recarray
        Construct an ndarray that allows field access using attributes.
    numpy.chararray
        chararray(shape, itemsize=1, unicode=False, buffer=None, offset=0,
    numpy.exp
        Calculate the exponential of all elements in the input array.
    numpy.pad
        Pad an array.
    numpy.asanyarray
        Convert the input to an ndarray, but pass ndarray subclasses through.
    numpy.cbrt
        Return the cube-root of an array, element-wise.
    numpy.copy
        Return an array copy of the given object.
    numpy.diag
        Extract a diagonal or construct a diagonal array.
    numpy.exp2
        Calculate `2**p` for all `p` in the input array.
    numpy.fmax
        Element-wise maximum of array elements.
    numpy.fmin
        Element-wise minimum of array elements.
    numpy.load
        Load arrays or pickled objects from ``.npy``, ``.npz`` or pickled files.
    numpy.modf
        Return the fractional and integral parts of an array, element-wise.
    numpy.rint
        Round elements of the array to the nearest integer.
    numpy.sort
        Return a sorted copy of an array.
    numpy.sqrt
        Return the non-negative square-root of an array, element-wise.
    numpy.array_equiv
        Returns True if input arrays are shape consistent and all elements equal.
    numpy.dtype
        Create a data type object.
    numpy.expm1
        Calculate ``exp(x) - 1`` for all elements in the array.
    numpy.isnan
        Test element-wise for NaN and return result as a boolean array.
    numpy.isnat
        Test element-wise for NaT (not a time) and return result as a boolean array.
    numpy.log10
        Return the base 10 logarithm of the input array, element-wise.
    numpy.log1p
        Return the natural logarithm of one plus the input array, element-wise.
    numpy.power
        First array elements raised to powers from second array, element-wise.
    numpy.ufunc
        Functions that operate element by element on whole arrays.
    numpy.choose
        Construct an array from an index array and a set of arrays to choose from.
    numpy.nditer
        Efficient multi-dimensional iterator object to iterate over arrays.
    numpy.maximum
        Element-wise maximum of array elements.
    numpy.minimum
        Element-wise minimum of array elements.
    numpy.swapaxes
        Interchange two axes of an array.
    numpy.full_like
        Return a full array with the same shape and type as a given array.
    numpy.ones_like
        Return an array of ones with the same shape and type as a given array.
    numpy.bitwise_or
        Compute the bit-wise OR of two arrays element-wise.
    numpy.empty_like
        Return a new array with the same shape and type as a given array.
    numpy.zeros_like
        Return an array of zeros with the same shape and type as a given array.
    numpy.asarray_chkfinite
        Convert the input to an array, checking for NaNs or Infs.
    numpy.bitwise_and
        Compute the bit-wise AND of two arrays element-wise.
    numpy.bitwise_xor
        Compute the bit-wise XOR of two arrays element-wise.
    numpy.float_power
        First array elements raised to powers from second array, element-wise.
    numpy.ma.exp
        Calculate the exponential of all elements in the input array.
    numpy.diag_indices
        Return the indices to access the main diagonal of an array.
    numpy.nested_iters
        Create nditers for use in nested loops
    numpy.ma.sqrt
        Return the non-negative square-root of an array, element-wise.
    numpy.ma.log10
        Return the base 10 logarithm of the input array, element-wise.
    numpy.chararray.tolist
        a.tolist()
    numpy.put_along_axis
        Put values into the destination array by matching 1d index and data slices.
    numpy.ma.choose
        Use an index array to construct a new array from a set of choices.
    numpy.ma.maximum
        Element-wise maximum of array elements.
    numpy.ma.minimum
        Element-wise minimum of array elements.
    numpy.ma.mrecords.MaskedRecords.__new__
        Create a new masked array from scratch.
    numpy.savez_compressed
        Save several arrays into a single file in compressed ``.npz`` format.
    numpy.matlib.rand
        Return a matrix of random values with given shape.
    numpy.datetime_as_string
        Convert an array of datetimes into an array of strings.
    numpy.ma.bitwise_or
        Compute the bit-wise OR of two arrays element-wise.
    numpy.ma.bitwise_and
        Compute the bit-wise AND of two arrays element-wise.
    numpy.ma.bitwise_xor
        Compute the bit-wise XOR of two arrays element-wise.
    numpy.ma.make_mask_none
        Return a boolean mask of the given shape, filled with False.
    numpy.ma.tests.test_subclassing.MSubArray.__new__
        Create a new masked array from scratch.
    numpy.core._multiarray_umath.clip
        Clip (limit) the values in an array.
    numpy.core.tests.test_overrides._new_duck_type_and_implements
        Create a duck array type and implements functions.
    numpy.ma.tests.test_subclassing.SubMaskedArray.__new__
        Create a new masked array from scratch.
    numpy.ma.mrecords.fromrecords
        Creates a MaskedRecords from a list of records.
    numpy.core._multiarray_umath.empty_like
        Return a new array with the same shape and type as a given array.
    numpy.f2py.tests.test_array_from_pyobj.Array.has_shared_memory
        Check that created array shares data with input array.
    numpy.core._dtype._construction_repr
        Creates a string repr of the dtype, excluding the 'dtype()' part
    numpy.abs
        Calculate the absolute value element-wise.
    numpy.add
        Add arguments element-wise.
    numpy.cos
        Cosine element-wise.
    numpy.log
        Natural logarithm, element-wise.
    numpy.mod
        Return element-wise remainder of division.
    numpy.lib.recfunctions.require_fields
        Casts a structured array to a new dtype using assignment by field-name.
    numpy.sin
        Trigonometric sine, element-wise.
    numpy.tan
        Compute tangent element-wise.
    numpy.ceil
        Return the ceiling of the input, element-wise.
    numpy.conj
        Return the complex conjugate, element-wise.
    numpy.cosh
        Hyperbolic cosine, element-wise.
    numpy.fabs
        Compute the absolute values element-wise.
    numpy.fmod
        Return the element-wise remainder of division.
    numpy.less
        Return the truth value of (x1 < x2) element-wise.
    numpy.log2
        Base-2 logarithm of `x`.
    numpy.sign
        Returns an element-wise indication of the sign of a number.
    numpy.sinh
        Hyperbolic sine, element-wise.
    numpy.tanh
        Compute hyperbolic tangent element-wise.
    numpy.core._multiarray_umath.datetime_as_string
        Convert an array of datetimes into an array of strings.
    numpy.equal
        Return (x1 == x2) element-wise.
    numpy.floor
        Return the floor of the input, element-wise.
    numpy.frexp
        Decompose the elements of x into mantissa and twos exponent.
    numpy.hypot
        Given the "legs" of a right triangle, return its hypotenuse.
    numpy.isinf
        Test element-wise for positive or negative infinity.
    numpy.ldexp
        Returns x1 * 2**x2, element-wise.
    numpy.trunc
        Return the truncated value of the input, element-wise.
    numpy.arccos
        Trigonometric inverse cosine, element-wise.
    numpy.arcsin
        Inverse sine, element-wise.
    numpy.arctan
        Trigonometric inverse tangent, element-wise.
    numpy.around
        Evenly round to the given number of decimals.
    numpy.divide
        Returns a true division of the inputs, element-wise.
    numpy.divmod
        Return element-wise quotient and remainder simultaneously.
    numpy.source
        Print or write to a file the source code for a NumPy object.
    numpy.square
        Return the element-wise square of the input.
    numpy.arccosh
        Inverse hyperbolic cosine, element-wise.
    numpy.arcsinh
        Inverse hyperbolic sine element-wise.
    numpy.arctan2
        Element-wise arc tangent of ``x1/x2`` choosing the quadrant correctly.
    numpy.arctanh
        Inverse hyperbolic tangent element-wise.
    numpy.deg2rad
        Convert angles from degrees to radians.
    numpy.degrees
        Convert angles from radians to degrees.
    numpy.greater
        Return the truth value of (x1 > x2) element-wise.
    numpy.rad2deg
        Convert angles from radians to degrees.
    numpy.radians
        Convert angles from degrees to radians.
    numpy.signbit
        Returns element-wise True where signbit is set (less than zero).
    numpy.spacing
        Return the distance between x and the nearest adjacent number.
    numpy.copysign
        Change the sign of x1 to that of x2, element-wise.
    numpy.diagonal
        Return specified diagonals.
    numpy.isfinite
        Test element-wise for finiteness (not infinity or not Not a Number).
    numpy.multiply
        Multiply arguments element-wise.
    numpy.negative
        Numerical negative, element-wise.
    numpy.subtract
        Subtract arguments, element-wise.
    numpy.heaviside
        Compute the Heaviside step function.
    numpy.logaddexp
        Logarithm of the sum of exponentiations of the inputs.
    numpy.nextafter
        Return the next floating-point value after x1 towards x2, element-wise.
    numpy.not_equal
        Return (x1 != x2) element-wise.
    numpy.left_shift
        Shift the bits of an integer to the left.
    numpy.less_equal
        Return the truth value of (x1 =< x2) element-wise.
    numpy.logaddexp2
        Logarithm of the sum of exponentiations of the inputs in base-2.
    numpy.logical_or
        Compute the truth value of x1 OR x2 element-wise.
    numpy.nan_to_num
        Replace NaN with zero and infinity with large finite numbers (default
    numpy.reciprocal
        Return the reciprocal of the argument, element-wise.
    numpy.bitwise_not
        Compute bit-wise inversion, or bit-wise NOT, element-wise.
    numpy.einsum_path
        Evaluates the lowest cost contraction order for an einsum expression by
    numpy.histogram2d
        Compute the bi-dimensional histogram of two data samples.
    numpy.logical_and
        Compute the truth value of x1 AND x2 element-wise.
    numpy.logical_not
        Compute the truth value of NOT x element-wise.
    numpy.logical_xor
        Compute the truth value of x1 XOR x2, element-wise.
    numpy.right_shift
        Shift the bits of an integer to the right.
    numpy.ma.abs
        Calculate the absolute value element-wise.
    numpy.ma.add
        Add arguments element-wise.
    numpy.ma.cos
        Cosine element-wise.
    numpy.ma.log
        Natural logarithm, element-wise.
    numpy.ma.mod
        Return element-wise remainder of division.
    numpy.ma.sin
        Trigonometric sine, element-wise.
    numpy.ma.tan
        Compute tangent element-wise.
    numpy.floor_divide
        Return the largest integer smaller or equal to the division of the inputs.
    numpy.ma.ceil
        Return the ceiling of the input, element-wise.
    numpy.ma.cosh
        Hyperbolic cosine, element-wise.
    numpy.fft.ifft
        Compute the one-dimensional inverse discrete Fourier Transform.
    numpy.ma.fabs
        Compute the absolute values element-wise.
    numpy.ma.fmod
        Return the element-wise remainder of division.
    numpy.ma.less
        Return the truth value of (x1 < x2) element-wise.
    numpy.ma.log2
        Base-2 logarithm of `x`.
    numpy.ma.sinh
        Hyperbolic sine, element-wise.
    numpy.ma.tanh
        Compute hyperbolic tangent element-wise.
    numpy.greater_equal
        Return the truth value of (x1 >= x2) element-wise.
    numpy.fft.ifftn
        Compute the N-dimensional inverse discrete Fourier Transform.
    numpy.ma.equal
        Return (x1 == x2) element-wise.
    numpy.ma.floor
        Return the floor of the input, element-wise.
    numpy.ma.hypot
        Given the "legs" of a right triangle, return its hypotenuse.
    numpy.busdaycalendar
        A business day calendar object that efficiently stores information
    numpy.ma.arccos
        Trigonometric inverse cosine, element-wise.
    numpy.ma.arcsin
        Inverse sine, element-wise.
    numpy.ma.arctan
        Trigonometric inverse tangent, element-wise.
    numpy.ma.divide
        Returns a true division of the inputs, element-wise.
    numpy.lib.recfunctions.unstructured_to_structured
        Converts and n-D unstructured array into an (n-1)-D structured array.
    numpy.ma.arccosh
        Inverse hyperbolic cosine, element-wise.
    numpy.ma.arcsinh
        Inverse hyperbolic sine element-wise.
    numpy.ma.arctan2
        Element-wise arc tangent of ``x1/x2`` choosing the quadrant correctly.
    numpy.ma.arctanh
        Inverse hyperbolic tangent element-wise.
    numpy.ma.greater
        Return the truth value of (x1 > x2) element-wise.
    numpy.ma.multiply
        Multiply arguments element-wise.
    numpy.ma.negative
        Numerical negative, element-wise.
    numpy.ma.subtract
        Subtract arguments, element-wise.
    numpy.ma.tests.test_subclassing.SubArray
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.ma.conjugate
        Return the complex conjugate, element-wise.
    numpy.ma.not_equal
        Return (x1 != x2) element-wise.
    numpy.ma.remainder
        Return element-wise remainder of division.
    numpy.ma.empty_like
        empty_like(prototype, dtype=None, order='K', subok=True, shape=None)
    numpy.ma.less_equal
        Return the truth value of (x1 =< x2) element-wise.
    numpy.ma.logical_or
        Compute the truth value of x1 OR x2 element-wise.
    numpy.ma.logical_and
        Compute the truth value of x1 AND x2 element-wise.
    numpy.ma.logical_not
        Compute the truth value of NOT x element-wise.
    numpy.ma.logical_xor
        Compute the truth value of x1 XOR x2, element-wise.
    numpy.ma.true_divide
        Returns a true division of the inputs, element-wise.
    numpy.ma.floor_divide
        Return the largest integer smaller or equal to the division of the inputs.
    numpy.ma.greater_equal
        Return the truth value of (x1 >= x2) element-wise.
    numpy.core.tests.test_function_base.PhysicalQuantity2
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.lib.tests.test_stride_tricks.SimpleSubClass
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.ma.tests.test_subclassing.ComplicatedSubArray
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.lib.tests.test_stride_tricks.VerySimpleSubClass
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.core.tests.test_multiarray.TestArrayPriority.Foo
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.core.tests.test_multiarray.TestArrayPriority.Bar
        ndarray(shape, dtype=float, buffer=None, offset=0,
    numpy.testing._gen_alignment_data
        generator producing data with different alignment and offsets
    numpy.random.RandomState.rand
        Random values in a given shape.
```

## modules & namespaces search

```python
pd.read_*?

    pd.read_clipboard
    pd.read_csv
    pd.read_excel
    pd.read_feather
    pd.read_fwf
    pd.read_gbq
    pd.read_hdf
    pd.read_html
    pd.read_json
    pd.read_orc
    pd.read_parquet
    pd.read_pickle
    pd.read_sas
    pd.read_spss
    pd.read_sql
    pd.read_sql_query
    pd.read_sql_table
    pd.read_stata
    pd.read_table
```

## System Shell Access

```python
!ping www.google.com -t 5

    PING www.google.com (172.217.174.100): 56 data bytes
    64 bytes from 172.217.174.100: icmp_seq=0 ttl=118 time=6.139 ms
    64 bytes from 172.217.174.100: icmp_seq=1 ttl=118 time=6.260 ms
    64 bytes from 172.217.174.100: icmp_seq=2 ttl=118 time=12.443 ms
    64 bytes from 172.217.174.100: icmp_seq=3 ttl=118 time=12.003 ms
    64 bytes from 172.217.174.100: icmp_seq=4 ttl=118 time=6.224 ms
    
    --- www.google.com ping statistics ---
    5 packets transmitted, 5 packets received, 0.0% packet loss
    round-trip min/avg/max/stddev = 6.139/8.614/12.443/2.950 ms
```

Windowsの場合は、デフォルトで`cmd`にてコマンドを実行  
`powershell`を呼び出したいなら、以下を実行

```python
import os
os.environ['comspec']='powershell.exe'
```

```python
!Get-Process
```

```python
myfiles = !ls 
myfiles # この様に、変数に保存できるのは便利

    ['IPython＆Notebook.ipynb', 'MagicCommands.ipynb']
```

## Automatic parentheses and quotes

```python
def my_function(*args):
    print(args)
```

```python
>>> /print "hello world"

hello, world
```

```python
>>> ,my_function a b c    
# becomes my_function("a","b","c")

('a', 'b', 'c')
```

```python
>>> ;my_function a b c    
# becomes my_function("a b c")

('a b c',)
```

> いずれの場合、`/`, `,`, `;`は頭文字にならなければならない

## Suppress output

```python
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```python
df;
```

## Multimedia Display

```python
from IPython.display import HTML, SVG, YouTubeVideo
```

```python
HTML('''
<table style="border: 2px solid black;">
''' +
     ''.join(['<tr>' +
              ''.join([f'<td>{row},{col}</td>'
                       for col in range(5)]) +
              '</tr>' for row in range(5)]) +
     '''
</table>
''')
```

<table style="border: 2px solid black;">
<tr><td>0,0</td><td>0,1</td><td>0,2</td><td>0,3</td><td>0,4</td></tr><tr><td>1,0</td><td>1,1</td><td>1,2</td><td>1,3</td><td>1,4</td></tr><tr><td>2,0</td><td>2,1</td><td>2,2</td><td>2,3</td><td>2,4</td></tr><tr><td>3,0</td><td>3,1</td><td>3,2</td><td>3,3</td><td>3,4</td></tr><tr><td>4,0</td><td>4,1</td><td>4,2</td><td>4,3</td><td>4,4</td></tr>
</table>

```python
SVG('''<svg width="600" height="80">''' +
    ''.join([f'''<circle
              cx="{(30 + 3*i) * (10 - i)}"
              cy="30"
              r="{3. * float(i)}"
              fill="red"
              stroke-width="2"
              stroke="black">
        </circle>''' for i in range(10)]) +
    '''</svg>''')
```

![svg](IPython%EF%BC%86Notebook_files/IPython%EF%BC%86Notebook_31_0.svg)

```python
# VSCode上開けないが、ブラウザの場合は開ける
YouTubeVideo('OSX3ik9Z4X8')
```

## Include Markdown Output

```python
from IPython.display import Markdown, display

def print_md(some_string):
    display(Markdown(some_string))

print("normal text")
print_md("**bold text**")
```

```python
# VSCode上は色が見えないけど
def print_md(something, color=None):
    color_str = f"<span style='color:{color}'>{something}</span>"
    display(Markdown(color_str))

print_md("**bold and blue**", color="blue")
```

<span style='color:blue'>**bold and blue**</span>

## 高解析度

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
```

```python
from IPython.display import set_matplotlib_formats
set_matplotlib_formats('retina')
```

## 複数のものを同時出力

```python
from IPython.core.interactiveshell import InteractiveShell

InteractiveShell.ast_node_interactivity = "all"
```

```python
a = "hello"
b = "world"
a
b
```

## プログラム実行完了後通知を受ける

```python
# Windows
import winsound

duration = 1000 # milliseconds
freq = 440 #Hz
winsound.Beep(freq, duration)
```

```python
# Mac
import os
os.system("say '実行完了しました'")
```

## [Extensions](https://github.com/mauhai/awesome-jupyterlab)

## PandasのDataFrameをより多く見える

```python
import pandas as pd

pd.set_option("display.max_rows", 500) # 例として
pd.set_option("display.max_columns", 500)
```

## widgets

```python
import ipywidgets as widgets
from ipywidgets import HBox, VBox
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import display
%matplotlib inline
```

```python
@widgets.interact
def f(x=5):
    print(x)
```

    interactive(children=(IntSlider(value=5, description='x', max=15, min=-5), Output()), _dom_classes=('widget-in…

```python
@widgets.interact(x=(0, 5))
def f(x=5):
    print(x)
```

    interactive(children=(IntSlider(value=5, description='x', max=5), Output()), _dom_classes=('widget-interact',)…

```python
@widgets.interact_manual(
    color=['blue', 'red', 'green'], lw=(1., 10.))
def plot(freq=1., color='blue', lw=2, grid=True):
    t = np.linspace(-1., +1., 1000)
    fig, ax = plt.subplots(1, 1, figsize=(8, 6))
    ax.plot(t, np.sin(2 * np.pi * freq * t),
            lw=lw, color=color)
    ax.grid(grid)
```

    interactive(children=(FloatSlider(value=1.0, description='freq', max=3.0, min=-1.0), Dropdown(description='col…

```python
freq_slider = widgets.FloatSlider(
    value=2.,
    min=1.,
    max=10.0,
    step=0.1,
    description='Frequency:',
    readout_format='.1f',
)
freq_slider
```

    FloatSlider(value=2.0, description='Frequency:', max=10.0, min=1.0, readout_format='.1f')

```python
range_slider = widgets.FloatRangeSlider(
    value=[-1., +1.],
    min=-5., max=+5., step=0.1,
    description='xlim:',
    readout_format='.1f',
)
range_slider
```

    FloatRangeSlider(value=(-1.0, 1.0), description='xlim:', max=5.0, min=-5.0, readout_format='.1f')

```python
grid_button = widgets.ToggleButton(
    value=False,
    description='Grid',
    icon='check'
)
grid_button
```

    ToggleButton(value=False, description='Grid', icon='check')

```python
color_buttons = widgets.ToggleButtons(
    options=['blue', 'red', 'green'],
    description='Color:',
)
color_buttons
```

    ToggleButtons(description='Color:', options=('blue', 'red', 'green'), value='blue')

```python
title_textbox = widgets.Text(
    value='Hello World',
    description='Title:',
)
title_textbox
```

    Text(value='Hello World', description='Title:')

```python
color_picker = widgets.ColorPicker(
    concise=True,
    description='Background color:',
    value='#efefef',
)
color_picker
```

    ColorPicker(value='#efefef', concise=True, description='Background color:')

```python
button = widgets.Button(
    description='Plot',
)
button
```

    Button(description='Plot', style=ButtonStyle())

```python
def plot2(b=None):
    xlim = range_slider.value
    freq = freq_slider.value
    grid = grid_button.value
    color = color_buttons.value
    title = title_textbox.value
    bgcolor = color_picker.value

    t = np.linspace(xlim[0], xlim[1], 1000)
    f, ax = plt.subplots(1, 1, figsize=(8, 6))
    ax.plot(t, np.sin(2 * np.pi * freq * t),
            color=color)
    ax.grid(grid)
```

```python
@button.on_click
def plot_on_click(b):
    out.clear_output(wait=True)
    with out:
        plot2()
        plt.show()
```

```python
tab1 = VBox(children=[freq_slider,
                      range_slider,
                      ])
tab2 = VBox(children=[color_buttons,
                      HBox(children=[title_textbox,
                                     color_picker,
                                     grid_button]),
                                     ])
```

```python
out = widgets.Output()
tab = widgets.Tab(children=[tab1, tab2])
tab.set_title(0, 'plot')
tab.set_title(1, 'styling')
VBox(children=[tab, button, out])
```

    VBox(children=(Tab(children=(VBox(children=(FloatSlider(value=2.0, description='Frequency:', max=10.0, min=1.0…

```python

```
