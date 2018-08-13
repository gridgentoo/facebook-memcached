# Какие проблемы были у Facebook с Оптимизацией Много-Ядерных серверов и для чего они писали Патчи к Memcached
https://docs.google.com/document/d/104mnPN_zJFZgZFTKbno98eaDb5h2wXLA0-sDjaBXb7g/edit


Dependencies:

   -- libevent, http://www.monkey.org/~provos/libevent/ (libevent-dev)

If using Linux, you need a kernel with epoll.  Sure, libevent will
work with normal select, but it sucks.

epoll isn't in Linux 2.4 yet, but there's a backport at:

    http://www.xmailserver.org/linux-patches/nio-improve.html
     
You want the epoll-lt patch (level-triggered).

If you're using MacOS, you'll want libevent 1.1 or higher to deal with 
a kqueue bug.

Also, be warned that the -k (mlockall) option to memcached might be
dangerous when using a large cache.  Just make sure the memcached machines
don't swap.  memcached does non-blocking network I/O, but not disk.  (it
should never go to disk, or you've lost the whole point of it)

The memcached website is at:

    http://www.danga.com/memcached/
