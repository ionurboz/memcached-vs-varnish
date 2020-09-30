# Memcache(d)

https://memcached.org/

Memcache module provides handy procedural and object oriented interface to memcached, highly effective caching daemon, which was especially designed to decrease database load in dynamic web applications.

The Memcache module also provides a session handler (memcache).

More information about memcached can be found at » http://www.memcached.org/.

# HOW TO: Install Memcache on XAMPP

Here are the steps that should be followed when you install memcache.

 1. start your xampp.
 2. click on 'config' and open php.ini file.
 

search for 

   `;extension=php_memcache.dll`

   If not found add

    extension=php_memcache.dll
    [Memcache]
    memcache.allow_failover = 1
    memcache.max_failover_attempts=20
    memcache.chunk_size =8192
    memcache.default_port = 11211
3. download the file `php_memecache.dll` from [windows.php.net][1]
(**make sure to check your php version and php_memcache.dll are same. Otherwise, it will through error.**)

unzip it and paste '.dll' file in the path **xampp\php\ext**, in my case it is **F:\xampp\php\ext** (I had to rename the file to ***memcache.dll***  but when you take a look on other sites that describes the steps for this, they don't tell to rename, but I have done this in my project!).


4. Download and installing Memcache server for windows

Download the **Memcache.exe** from [jellycan][2]


After completion of download, unzip and put the **memcache.exe** file into any desired directory of your choice (e.g. C:/memcached/). make sure folder name should be **memcached**


5. Open the **cmd prompt** with **“Run as Administrator”** and execute the line to install

`c:/memcached/memcached.exe -d install`

then type

`net start "memcached server"`

In case you get memcache is already installed. then just go through  line `net start "memcached server"`.
 
**Or** 

For the installation purpose you can go to the path where you have copied the *memcache.exe*. and double click to the file, memcache is installed, now just add line `net start "memcached server"` and your memcache is enabled.


6. Restart Xampp Apache

7. Restart Memcached:

    `C:\Windows\system32> net start “memcached”`

    *The memcached service is starting.
    The memcached service was started successfully.*
    
    `C:\Windows\system32> net stop  “memcached”`

    *The memcached service is stopping.
    The memcached service was stopped successfully.*

  [1]: http://windows.php.net/downloads/pecl/releases/memcache/3.0.8/php_memcache-3.0.8-5.5-ts-vc11-x86.zip
  [2]: http://code.jellycan.com/files/memcached-1.2.6-win32-bin.zip
  
  
# Varnish

http://varnish-cache.org/
  
<p>Varnish Cache is a web application accelerator also known as a caching HTTP reverse proxy. You install it in front of any server that speaks HTTP and configure it to cache the contents. Varnish Cache is really, really fast. It typically speeds up delivery with a factor of 300 - 1000x, depending on your architecture. A high level overview of what Varnish does can be seen in <a class="reference external" href="https://www.youtube.com/watch?v=fGD14ChpcL4">this video</a>.</p>

# Varnish vs Memcache(ed)

### Memcached can be used as an in-memory, distributed back-end for your application cache. Varnish can be used as a reverse proxy to externally cache HTTP requests.
### Varnish is in front of the webserver; it works as a reverse http proxy that caches.

Memcached can be used as an in-memory, distributed back-end for your application cache.
  Varnish can be used as a reverse proxy to externally cache HTTP requests.

  It seems to me that Varnish is behind the web server, caching web pages and doesn't require change in code, just configuration.
  On the other side, Memcached is general purpose caching system and mostly used to cache result from database and does require change in get method (first cache lookup).

  Varnish is in front of the webserver; it works as a reverse http proxy that caches.
  You can use both.
  Mostly write -- Varnish will need to have affected pages purged. This will result in an overhead and little benefit for modified pages.
  Mostly read -- Varnish will probably cover most of it.
  Similar read & write -- Varnish will serve a lot of the pages for you, Memcache will provide info for pages that have a mixture of known and new data allowing you to generate pages faster.

  Varnish is meant to serve webpage files, like html, js, css, images, etc. It intercepts the HTTP traffic between the internet clients and the backend application server. Varnish listens to http port 80 and speaks HTTP protocol. Neither browsers nor the backend applications need to know that Varnish exists, once it is properly configured it just works.

  Memcached is an application usually used to cache data brought from a database server to an application, in order to decrease the number of queries to the DB. Furthermore, since the data is cached on memory, its retrieval is much faster. But is the application that controls the insertion and retrieval of data from Memcached, in other words, the application must be written to make proper use of Memcached. Memcached does not speak HTTP protocol.

  Memcached:
  Memcached is a distributed, key-value, object cache in memory. This is similar to the object cache provided by APC but there are some important differences. It’s in-memory, while APC’s object cache is in shared memory. This will make Memcached faster, but will also require the memory allocation for it’s storage. The other major difference is that Memcached is distributed. This means that it runs across multiple servers. 

  Varnish:
  Varnish is a caching HTTP reverse proxy. The reverse proxy part means that it sits between your application and the outside world. Visiting your domain will actually connect to Varnish. Varnish will then make the corresponding request to your application and then deliver it to the client. It will cache the results of these requests based on a configuration file you can write in the Varnish Configuration Language.
