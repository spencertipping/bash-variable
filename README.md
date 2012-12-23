# Bash variable

A Bash variable stores a value, but in a much more powerful way than the
variables built into your shell. For example:

    $ var foo
    $ foo = uptime
    10:37:16 up 28 days, 21:00,  0 users,  load average: 0.15, 0.43, 0.40
    $ foo
    10:37:16 up 28 days, 21:00,  0 users,  load average: 0.15, 0.43, 0.40
    $ foo += cat /proc/loadavg
    10:37:16 up 28 days, 21:00,  0 users,  load average: 0.15, 0.43, 0.40
    0.13 0.37 0.38 2/180 25274
    $ foo =
    $ foo | wc -c
    0
    $

NOTE! In order to get the above behavior, you need to have `.` as one of the
entries in your `$PATH` (which has some security implications). To do this:

    $ export PATH=$PATH:.

If `.` isn't on your `$PATH`, you'll need to prefix each variable with `./`.

## Supported operators

Initialized construction:

    $ var foo = echo hi
    hi
    $ foo
    hi
    $

Reassignment, appends, and concatenation:

    $ foo + echo there
    hi
    there
    $ foo
    hi
    $ foo += echo there
    hi
    there
    $ foo
    hi
    there
    $

Comparison:

    $ var bar = foo
    $ foo == bar && echo 'same'
    same
    $ bar = echo 5
    5
    $ foo == bar || echo 'different'
    different
    $

Composition:

    $ var foo = 1
    $ var bar = 2
    $ var bif = 3
    $ foo + bar + bif
    1
    2
    3
    $

When you use variables this way, all operators are right-associative but the
variable values themselves are retrieved from leftmost to rightmost.
