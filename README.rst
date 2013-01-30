klee-uclibc
===========

Klee-uclibc_ is a customized libc for KLEE_ based on uClibc_ 0.9.29.
This fork of version 0.02-i386 fixes some compilation errors with clang_
3.2 and LLVM_ 3.2.

.. _Klee-uclibc: http://www.doc.ic.ac.uk/~cristic/klee/klee-uclibc-i386.html
.. _KLEE: http://klee.llvm.org/
.. _uClibc: http://www.uclibc.org/
.. _clang: http://clang.llvm.org/
.. _LLVM: http://www.llvm.org/


Encountered Errors
------------------

::

      CC libcrypt/des.os
    clang: error: unsupported option '--emit-llvm'
    make: *** [libcrypt/des.os] Error 1


::

    /bin/sh: <path>/Release+Asserts/bin/llvm-ar: No such file or directory
    make: *** [lib/libcrypt.a] Error 127


::

    In file included from libc/misc/sysvipc/semget.c:8:
    libc/misc/sysvipc/sem.c:73:12: warning: implicit declaration of
          function '__syscall_ipc' is invalid in C99
          [-Wimplicit-function-declaration]
        return __syscall_ipc(IPCOP_semget, key, nsems,...
               ^
    libc/misc/sysvipc/sem.c:73:26: error: use of undeclared
          identifier 'IPCOP_semget'
        return __syscall_ipc(IPCOP_semget, key, nsems,...
                             ^
    1 warning and 1 error generated.
    make: *** [libc/misc/sysvipc/semget.os] Error 1


::

      CC libc/inet/if_index.os
    In file included from libc/inet/if_index.c:36:
    In file included from libc/inet/netlinkaccess.h:32:
    In file included from /usr/include/linux/rtnetlink.h:6:
    /usr/include/linux/if_link.h:291:2: error: unknown type name
          '__be16'; did you mean '__u16'?
            __be16  low;
            ^~~~~~
            __u16
    libc/inet/netlinkaccess.h:28:18: note: '__u16' declared here
    typedef uint16_t __u16;
                     ^
    In file included from libc/inet/if_index.c:36:
    In file included from libc/inet/netlinkaccess.h:32:
    In file included from /usr/include/linux/rtnetlink.h:6:
    /usr/include/linux/if_link.h:292:2: error: unknown type name
          '__be16'; did you mean '__u16'?
            __be16  high;
            ^~~~~~
            __u16
    libc/inet/netlinkaccess.h:28:18: note: '__u16' declared here
    typedef uint16_t __u16;
                     ^
    2 errors generated.
    make: *** [libc/inet/if_index.os] Error 1


Usage
-----

Configure and compile with:

::

    LLVMGCC=clang GCC=gcc ./configure --with-llvm=<path>
    LLVMGCC=clang GCC=gcc make
