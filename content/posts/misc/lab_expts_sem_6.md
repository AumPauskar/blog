+++
title = 'Lab expts sem 6'
date = 2024-03-23T15:34:19+05:30
tags = ["ai", "ml", "lab", "sem6", "expts", "network", "shell", "linux", "artificial intelligence", "machine learning"]
author = "Aum Pauskar, Shriram Naik"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Lab experiments of semester 6, has AIML temworks and unix based network programming"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Lab expts sem 6

## AIML

### TW1 - DFID

```py
from collections import defaultdict

class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = defaultdict(list)

    def addEdge(self, u, v):
        self.graph[u].append(v)

    def DLS(self, src, target, maxDepth, visited):
        visited.append(src)  # Add the current node to visited
        if src == target:
            return True, visited

        if maxDepth <= 0:
            return False, visited

        for i in self.graph[src]:
            found, visited = self.DLS(i, target, maxDepth - 1, visited)
            if found:
                return True, visited
        return False, visited

    def IDDFS(self, src, target, maxDepth):
        visited = []  # Initialize the visited list
        for i in range(maxDepth + 1):  # Include maxDepth level
            found, visited = self.DLS(src, target, i, visited)
            if found:
                return True, visited
        return False, visited

# Create a graph
g = Graph(7)
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(1, 3)
g.addEdge(1, 4)
g.addEdge(2, 5)
g.addEdge(2, 6)

target = 6
maxDepth = 3
src = 0

found, visited = g.IDDFS(src, target, maxDepth)
if found:
    print("Target is reachable from source within max depth")
    print("Visited nodes:", visited)
else:
    print("Target is NOT reachable from source within max depth")
    print("Visited nodes:", visited)
```

### TW2 - BFS
```py
# Python3 Program to print BFS traversal
# from a given source vertex. BFS(int s)
# traverses vertices reachable from s.

from collections import defaultdict


# This class represents a directed graph
# using adjacency list representation
class Graph:

    # Constructor
    def __init__(self):

        # Default dictionary to store graph
        self.graph = defaultdict(list)

    # Function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)

    # Function to print a BFS of graph
    def BFS(self, s):

        # Mark all the vertices as not visited
        visited = [False] * (max(self.graph) + 1)

        # Create a queue for BFS
        queue = []

        # Mark the source node as
        # visited and enqueue it
        queue.append(s)
        visited[s] = True

        while queue:

            # Dequeue a vertex from
            # queue and print it
            s = queue.pop(0)
            print(s, end=" ")

            # Get all adjacent vertices of the
            # dequeued vertex s.
            # If an adjacent has not been visited,
            # then mark it visited and enqueue it
            for i in self.graph[s]:
                if not visited[i]:
                    queue.append(i)
                    visited[i] = True

# Driver code
if __name__ == '__main__':

    # Create a graph given in
    # the above diagram
    g = Graph()
    g.addEdge(0, 1)
    g.addEdge(0, 2)
    g.addEdge(1, 2)
    g.addEdge(2, 0)
    g.addEdge(2, 3)
    g.addEdge(3, 3)

    print("Following is Breadth First Traversal"
        " (starting from vertex 2)")
    g.BFS(2)

# This code is contributed by Neelam Yadav

# This code is modified by Susobhan Akhuli
```

### TW3 - A* algorithm
```py
import heapq
# tw3


def astar(graph, start, goal):
    # priority queue to store nodes to be explored
    open_list = [(0, start)]
    # dictionary to store parent nodes
    parents = {}
    # dictionary to store g values (cost from start node to current node)
    g_values = {node: float('inf') for node in graph}
    g_values[start] = 0
    # dictionary to store f values (estimated total cost from start to goal)
    f_values = {node: float('inf') for node in graph}
    f_values[start] = graph[start][1]

    iteration = 0

    while open_list:
        # get node with minimum f value
        current_f, current_node = heapq.heappop(open_list)

        # check if current node is the goal
        if current_node == goal:
            path = []
            while current_node in parents:
                path.append(current_node)
                current_node = parents[current_node]
            path.append(start)
            final_cost = g_values[goal]
            print(f"\nFinal Cost: {final_cost}")
            return path[::-1]

        # explore neighbors
        for child, cost in graph[current_node][0].items():
            # calculate tentative g value
            tentative_g = g_values[current_node] + cost
            if tentative_g < g_values[child]:
                # update parent and g values
                parents[child] = current_node
                g_values[child] = tentative_g
                f_values[child] = tentative_g + graph[child][1]
                # add child to open list
                heapq.heappush(open_list, (f_values[child], child))

        iteration += 1
        print(f"\nIteration {iteration}:")
        print("Current Path:", reconstruct_path(parents, start, current_node))
        print(f"Evaluation Function Value for {current_node}: {f_values[current_node]}")


# Function to reconstruct the path from start to goal using parent nodes
def reconstruct_path(parents, start, goal):
    path = [goal]
    while goal != start:
        goal = parents[goal]
        path.append(goal)
    return path[::-1]


# Example usage:
start_node = 'A'
goal_node = 'G'
graph = {
    'A': [{'B': 5, 'C': 10}, 10],
    'B': [{'D': 5, 'E': 5}, 7],
    'C': [{'F': 5}, 7],
    'D': [{'G': 10}, 3],
    'E': [{'G': 7}, 2],
    'F': [{'G': 8}, 1],
    'G': [{}, 0]
}

print("\nA* Search Path:")
path = astar(graph, start_node, goal_node)
print("Final Path:", path)
```

## USP

### Running a code

We shall use fedora to run most of the code. The code will be written in ANSI C and. \
To run the code, we shall use the following commands:

```shell
gedit <filename.c>
cc filename.c
./a.out
```

**Sample code**

```c
#include <stdio.h>
int main()
{
    #if __STDC__ == 0
    printf("CC is not ANSI C compliant");
    #else
    printf("%s compiled at %s %s this statement at line %d", __FILE__, __TIME__, __DATE__, __LINE__);
    #endif
    return 0;
}
```

In order to compile and run this code open a **new instance in the terminal** and execute the following commands:

```shell
cc <filename.c> -o <filename.out>
./filename.out
```

A **shorter version** to run this code is

```shell
cc <filename.c> -o <filename.out> && ./filename.out
```

This can be done for same in a c++ file. To initialte a c++ file, use the following command:

```shell
gedit <filename.cpp>
```

To compile and execute the file run the following commands:

```shell
g++ <filename.cpp> -o <filename.out>
./filename.out
```

Similarly to the c file to run the command in one single line use the following command:

```shell
g++ <filename.cpp> -o <filename.out> && ./filename.out
```

**Checking the version of posix**

```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199309L
#include <stdio.h>
#include <unistd.h>
#include <iostream.h>

using namespace std;

int main() {
    #ifdef _POSIX_VERSION
        cout << "POSIX compliant" << _POSIX_VERSION << endl;
    #else
        cout << "POSIX version is not defined" << endl;
    #endif
    return 0;
}
```
### TW1 - runtime constraints in C++

```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 1993309L
#include <iostream>
#include <limits.h>
#include <unistd.h>

using namespace std;

void compileTime() {
    cout << "\n\nMANIFEST CONSTANTS\n\n";
    #ifdef _SC_CLK_TCK
        cout << "SYSTEM SUPPORTS CLK_TCK which is " << _SC_CLK_TCK << endl;
    #else
        cout << "SYSTEM DOES NOT SUPPORT CLK_TCK" << endl;
    #endif

    #ifdef _POSIX_CHILD_MAX
        cout << "Man number of child processes is " << _POSIX_CHILD_MAX << endl;
    #else
        cout << "CHILD_MAX is not defined" << endl;
    #endif

    #ifdef _POSIX_PATH_MAX
        cout << "Maximum path length is " << _POSIX_PATH_MAX << endl;
    #else
        cout << "PATH_MAX is not defined" << endl;
    #endif
    #ifdef _POSIX_OPEN_MAX
        cout << "Maximum number of open files per process is " << _POSIX_OPEN_MAX << endl; 
    #else
        cout << "OPEN_MAX is not defined" << endl;
    #endif
    #ifdef _POSIX_NAME_MAX
        cout << "Maximum number of characters in a filename is " << _POSIX_NAME_MAX << endl;
    #else
        cout << "SYSTEM DOES NOT SUPPORT _POSIX_NAME_MAX" << endl;
    #endif
}

void runTime() {
    cout << "\n\nRUNTIME CONSTANTS\n\n";
    long arg_max = sysconf(_SC_ARG_MAX);
    cout << "Maximum length of arguments to exec is " << arg_max << endl;
    long child_max = sysconf(_SC_CHILD_MAX);
    cout << "Maximum number of child processes is " << child_max << endl;
    long clk_tck = sysconf(_SC_CLK_TCK);
    cout << "Number of clock ticks per second is " << clk_tck << endl;
    long open_max = sysconf(_SC_OPEN_MAX);
    cout << "Maximum number of open files per process is " << open_max << endl;
    long name_max = sysconf(_PC_NAME_MAX);
    cout << "Maximum number of characters in a filename is " << name_max << endl;
    long path_max = pathconf("/", _PC_PATH_MAX);
    cout << "Maximum path length is " << path_max << endl;
}

int main() {
    compileTime();
    runTime();
    return 0;
}
```

**Output**
```bash


MANIFEST CONSTANTS

SYSTEM SUPPORTS CLK_TCK which is 2
Man number of child processes is 25
Maximum path length is 256
Maximum number of open files per process is 20
Maximum number of characters in a filename is 14


RUNTIME CONSTANTS

Maximum length of arguments to exec is 2097152
Maximum number of child processes is 30544
Number of clock ticks per second is 100
Maximum number of open files per process is 1048576
Maximum number of characters in a filename is 65536
Maximum path length is 4096
```

### TW2 - posix job control

**Problem statement:** Write a C/C++ compliant program that print the posix defined configuration option supported on any given system using feature kept macros.
```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199309L
#include <iostream>
#include <unistd.h>

using namespace std;

int main() {
    #ifdef _POSIX_JOB_CONTROL
        cout << "System supports POSIX Job Control." << endl;
    #else
        cout << "System doesn't support POSIX Job Control." << endl;
    #endif

    #ifdef _POSIX_SAVED_IDS
        cout << "System supports saved set-UID and saved set-GID." << endl;
    #else
        cout << "System doesn't support POSIX saved IDs." << endl;
    #endif

    #ifdef _POSIX_CHOWN_RESTRICTED
        cout << "Chown restricted option is: " << _POSIX_CHOWN_RESTRICTED << endl;
    #else
        cout << "System doesn't support chown restricted option." << endl;
    #endif

    #ifdef _POSIX_NO_TRUNC
        cout << "Truncation option is: " << _POSIX_NO_TRUNC << endl;
    #else
        cout << "System doesn't support POSIX truncation." << endl;
    #endif

    #ifdef _POSIX_VDISABLE
        cout << "Disable char for terminal files: " << _POSIX_VDISABLE << endl;
    #else
        cout << "System doesn't support POSIX disability." << endl;
    #endif

    return 0;
}
```

Output
```bash
lts@POWERHOUSE:~/Documents/blog/test$ g++ test.cpp && ./a.out
System supports POSIX Job Control.
System supports saved set-UID and saved set-GID.
Chown restricted option is: 0
Truncation option is: 1
Disable char for terminal files: 
```

### TW3 - hardlink and softlink

**Problem statement:** Write a c/c++program to generate hardlink and softlink

```cpp
#include<iostream>
#include<sys/types.h>
#include<unistd.h>
#include<string.h>
using namespace std;
int main( int argc , char* argv[] )
 {
   if( ((argc<3) || (argc>4)) || (argc==4 && strcmp(argv[1],"-s")) )
    { 
      cerr<<"Usage : "<< argv[0]<<" [-s] <orig_file> <new_file> \n";
      return 1;
    }
   if( argc == 4 )   // programName -s <source_file> <destination_file>
    {
      if( symlink( argv[2] ,argv[3] ) == -1 )
        {
	  	perror("link");   		return 1;
	   }
           cout<<"Symbolic | Soft link of File created successfully\n";
    }


if( argc == 3 )  // programName <source_file> <destination_file>
    {
	   if( link(argv[1],argv[2]) == -1 )
	    {
	      perror("link"); 
	      return 1;
	    }
	   cout<<"Hard link of File created successfully\n";
    }
   return 0; 
 }
```

Output
```bash
lts@POWERHOUSE:~/Documents/blog/test$ g++ test.cpp -o link_creator
lts@POWERHOUSE:~/Documents/blog/test$ ./link_creator -s example.txt example_link.txt
Symbolic | Soft link of File created successfully

lts@POWERHOUSE:~/Documents/blog/test$ g++ test.cpp 
lts@POWERHOUSE:~/Documents/blog/test$ touch soft.txt
lts@POWERHOUSE:~/Documents/blog/test$ ./a.out soft.txt  file.txt
Hard link of File created successfully
```

### TW4 - file locking

**Problem statement:** Write a C/C++ progaram to demonstate file locking
```cpp
#include <stdio.h>
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>
#include <string.h>

int main(int argc, char *argv[])
{
    char temp[1000];
    struct flock fvar;
    int fdesc;
    char buf;
    int rc;
    off_t offset;

    if (argc != 2) {
        printf("Usage: %s <filename>\n", argv[0]);
        return 1;
    }

    fdesc = open(argv[1], O_RDWR);
    if (fdesc == -1) {
        perror("Error opening file");
        return 1;
    }

    offset = lseek(fdesc, -100, SEEK_END);
    
    fvar.l_type = F_WRLCK;
    fvar.l_whence = SEEK_CUR;
    fvar.l_start = 0;
    fvar.l_len = 100;

    if (fcntl(fdesc, F_SETLK, &fvar) == -1)
    {
        printf("\n---- File has been locked by: \n");
        while (fcntl(fdesc, F_GETLK, &fvar) != -1 && fvar.l_type != F_UNLCK)
        {
            printf("\nFile: %s is locked by process with pid: %d\n", argv[1], fvar.l_pid);
        }
    }
    else
    {
        printf("\n---- \n");
        printf("\nFile: %s was not locked and acquiring of exclusive lock was:", argv[1]);
        printf(" Successful By Process Id: %d\n", getpid());

        offset = lseek(fdesc, -50, SEEK_END);
        printf("\nLast 50 bytes of file %s = \n", argv[1]);
        while ((rc = read(fdesc, &buf, 1)) > 0) printf("%c", buf);
        
        offset = lseek(fdesc, -100, SEEK_END);
        fvar.l_type = F_UNLCK;
        fvar.l_whence = SEEK_CUR;
        fvar.l_start = 0;
        fvar.l_len = 100;

        fcntl(fdesc, F_SETLKW, &fvar);
        printf("\nFile unlocked successfully\n");
    }

    close(fdesc);
    return 0;
}
```

Output
```bash
lts@POWERHOUSE:~/Documents/blog/test$ echo "lando gets pole position" > file.txt
lts@POWERHOUSE:~/Documents/blog/test$ g++ test.cpp -o file_locking
lts@POWERHOUSE:~/Documents/blog/test$ ./file_locking file.txt 

---- 

File: file.txt was not locked and acquiring of exclusive lock was: Successful By Process Id: 13895

Last 50 bytes of file file.txt = 
lando gets pole position

File unlocked successfully
lts@POWERHOUSE:~/Documents/blog/test$ 
```

### TW5 - zombie process

**Problem statement:** Write a C/C++ program that created a zombie and then calls system execute the PS command to verify that the process is zombie
```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main() {
    pid_t child_pid;

    // Create a child process
    child_pid = fork();

    if (child_pid == 0) {
        // Child process
        printf("Child process with PID %d exiting...\n", getpid());
        exit(0);
    } else if (child_pid > 0) {
        // Parent process
        printf("Parent process with PID %d waiting...\n", getpid());

        // Don't wait for the child process to terminate (create zombie)
        sleep(5);  // Sleep for a few seconds to allow child to exit

        // Execute ps command to verify child process state
        system("ps -e -o pid,ppid,stat,cmd");
    } else {
        // Fork failed
        perror("fork");
        exit(1);
    }

    return 0;
}
```

Output
```bash
lts@POWERHOUSE:~/Documents/blog/test$ gcc test.cpp 
lts@POWERHOUSE:~/Documents/blog/test$ ./a.out 
Parent process with PID 19180 waiting...
Child process with PID 19181 exiting...
    PID    PPID STAT CMD
      1       0 Ss   /sbin/init
      2       1 Sl   /init
      6       2 Sl   plan9 --control-socket 6 --log-level 4 --server-fd 7 --pipe-fd 9 --log-truncate
     38       1 S<s  /lib/systemd/systemd-journald
     57       1 Ss   /lib/systemd/systemd-udevd
     69       1 Ssl  snapfuse /var/lib/snapd/snaps/bare_5.snap /snap/bare/5 -o ro,nodev,allow_other,suid
     70       1 Ssl  snapfuse /var/lib/snapd/snaps/core_16928.snap /snap/core/16928 -o ro,nodev,allow_other,suid
     80       1 Ssl  snapfuse /var/lib/snapd/snaps/core20_2264.snap /snap/core20/2264 -o ro,nodev,allow_other,suid
     87       1 Ssl  snapfuse /var/lib/snapd/snaps/core20_2318.snap /snap/core20/2318 -o ro,nodev,allow_other,suid
     94       1 Ssl  snapfuse /var/lib/snapd/snaps/core22_1122.snap /snap/core22/1122 -o ro,nodev,allow_other,suid
     97       1 Ssl  snapfuse /var/lib/snapd/snaps/core22_1380.snap /snap/core22/1380 -o ro,nodev,allow_other,suid
    105       1 Ssl  snapfuse /var/lib/snapd/snaps/gtk-common-themes_1535.snap /snap/gtk-common-themes/1535 -o ro,nodev,allow_other,suid
    110       1 Ssl  snapfuse /var/lib/snapd/snaps/hugo_19714.snap /snap/hugo/19714 -o ro,nodev,allow_other,suid
    115       1 Ssl  snapfuse /var/lib/snapd/snaps/hugo_19814.snap /snap/hugo/19814 -o ro,nodev,allow_other,suid
    123       1 Ssl  snapfuse /var/lib/snapd/snaps/snapd_21465.snap /snap/snapd/21465 -o ro,nodev,allow_other,suid
    130       1 Ssl  snapfuse /var/lib/snapd/snaps/snapd_21759.snap /snap/snapd/21759 -o ro,nodev,allow_other,suid
    134       1 Ssl  snapfuse /var/lib/snapd/snaps/ubuntu-desktop-installer_1284.snap /snap/ubuntu-desktop-installer/1284 -o ro,nodev,allow_
    138       1 Ssl  snapfuse /var/lib/snapd/snaps/ubuntu-desktop-installer_1286.snap /snap/ubuntu-desktop-installer/1286 -o ro,nodev,allow_
    203       1 Ss   /lib/systemd/systemd-resolved
    222       1 Ss   /usr/sbin/cron -f -P
    224       1 Ss   @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    228       1 Ss   /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    229       1 Ssl  /usr/sbin/rsyslogd -n -iNONE
    231       1 Ssl  /usr/lib/snapd/snapd
    232       1 Ss   /lib/systemd/systemd-logind
    278       1 Ss   /bin/bash /snap/ubuntu-desktop-installer/1286/bin/subiquity-server
    280       1 Ssl  /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
    288       1 Ss+  /sbin/agetty -o -p -- \u --noclear --keep-baud console 115200,38400,9600 vt220
    303       1 Ss+  /sbin/agetty -o -p -- \u --noclear tty1 linux
    326     278 Sl   /snap/ubuntu-desktop-installer/1286/usr/bin/python3.10 -m subiquity.cmd.server --use-os-prober --storage-version=2 --po
    371       2 Ss   /init
    372     371 S    /init
    373     372 Ss+  sh -c "$VSCODE_WSL_EXT_LOCATION/scripts/wslServer.sh" 5437499feb04f7a586f677b155b039bc2b3669eb stable code-server .vsco
    374       2 Ss   /bin/login -f
    376     373 S+   sh /mnt/c/Users/aumpa/.vscode/extensions/ms-vscode-remote.remote-wsl-0.88.2/scripts/wslServer.sh 5437499feb04f7a586f677
    407       1 Ss   /lib/systemd/systemd --user
    408     407 S    (sd-pam)
    413     374 S+   -bash
    449     376 S+   sh /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/bin/code-server --host=127.0.0.1 --port=0 --co
    453     449 Sl+  /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node /home/lts/.vscode-server/bin/5437499feb04f7a
    465       2 Ss   /init
    466     326 S    python3 /snap/ubuntu-desktop-installer/1286/usr/bin/cloud-init status --wait
    467     465 S    /init
    469     467 Ssl+ /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node -e const net = require('net'); process.stdin
    478       2 Ss   /init
    479     478 S    /init
    480     479 Ssl+ /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node -e const net = require('net'); process.stdin
    501     453 Sl+  /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node /home/lts/.vscode-server/bin/5437499feb04f7a
    515     453 Sl+  /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node --dns-result-order=ipv4first /home/lts/.vsco
    542     515 Sl+  /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node /home/lts/.vscode-server/bin/5437499feb04f7a
    557     453 Rl+  /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/node /home/lts/.vscode-server/bin/5437499feb04f7a
    678     557 Ss   /bin/bash --init-file /home/lts/.vscode-server/bin/5437499feb04f7a586f677b155b039bc2b3669eb/out/vs/workbench/contrib/te
  19180     678 S+   ./a.out
  19181   19180 Z+   [a.out] <defunct>
  19232   19180 S+   sh -c ps -e -o pid,ppid,stat,cmd
  19233   19232 R+   ps -e -o pid,ppid,stat,cmd
lts@POWERHOUSE:~/Documents/blog/test$ 
```
### TW6 - race condition

**Probmem statement:** Write a C/C++ program to illustate a race condition

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

static void charactertime(const char *); // Change to const char*

int main() {
    int pid;
    if ((pid = fork()) < 0) {
        printf("fork error\n");
    } else if (pid == 0) {
        charactertime("Output of the Child\n");
    } else {
        charactertime("Output of the Parent\n");
    }
    _exit(0);
}

static void charactertime(const char *str) { // Change to const char*
    const char *ptr; // Change to const char*
    int c;
    setbuf(stdout, NULL); // Disable buffering for stdout
    for (ptr = str; (c = *ptr++) != 0; ) {
        putc(c, stdout); // Output each character one at a time
    }
}
```

Output
```bash
lts@POWERHOUSE:~/Documents/blog/test$ ./a.out 
Output ofO utthpeu tP aorfe ntth
e Child
lts@POWERHOUSE:~/Documents/blog/test$ 
```
### TW7 - client server

**Problem statement:** Implementing client server communication using socket programming that uses connection oriented prototcol at transport layer

**Server code**
```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
#include <string.h>
#define PORT 4444
int main() {
 int listenfd, connfd;
 struct sockaddr_in servAddr, cliAddr;
 socklen_t clilen;
 char buffer[1024];
 
 listenfd = socket(AF_INET, SOCK_STREAM, 0);
 printf("[+] Server socket created successfully\n");
 bzero(&servAddr, sizeof(servAddr));
 servAddr.sin_family = AF_INET;
 servAddr.sin_port = htons(PORT);
 servAddr.sin_addr.s_addr = inet_addr("127.0.0.1");
 
 bind(listenfd, (struct sockaddr *) &servAddr, sizeof(servAddr));
 printf("[+] Bind to PORT %d successful\n", PORT);
 
 listen(listenfd, 5);
 printf("[+] Listening...\n");
 
 connfd = accept(listenfd, (struct sockaddr *) &cliAddr, 
&clilen);
 
 strcpy(buffer, "Hello World!");
 send(connfd, buffer, strlen(buffer), 0);
 printf("[+] Data sent to client: %s\n", buffer);
 
 printf("[+] Closing the connection\n");
 return 0;
}
```

**Client code**
```c
#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#define PORT 4444
int main() {
 int sockfd;
 struct sockaddr_in servAddr;
 char buffer[1024];
 
 sockfd = socket(AF_INET, SOCK_STREAM, 0);
 printf("[+] Client socket created successfully\n");
 
 bzero(&servAddr, sizeof(servAddr));
 servAddr.sin_family = AF_INET;
 servAddr.sin_port = htons(PORT);
 servAddr.sin_addr.s_addr = inet_addr("127.0.0.1");
 
 connect(sockfd, (struct sockaddr *) &servAddr, 
sizeof(servAddr));
 printf("[+] Connected to server\n");
 
 recv(sockfd, buffer, 1024, 0);
 printf("[+] Data received from server: %s\n", buffer);
 printf("[+] Closing the connection\n");
 return 0;
}
```

**Output**
```bash
// server output
lts@POWERHOUSE:~/Documents/blog/test$ ./server 
[+] Server socket created successfully
[+] Bind to PORT 4444 successful
[+] Listening...
[+] Data sent to client: Hello World!
[+] Closing the connection
lts@POWERHOUSE:~/Documents/blog/test$ 

// client output
lts@POWERHOUSE:~/Documents/blog/test$ ./client 
[+] Client socket created successfully
[+] Connected to server
[+] Data received from server: Hello World!�
[+] Closing the connection
lts@POWERHOUSE:~/Documents/blog/test$ 
```
### TW8 - NS3

**Problem statement:** Write a C/C++ program to simulate a network application with 2 nodes using NS2/NS3.
```c
/* -*- Mode:C++; c-file-style:"gnu"; indent-tabs-mode:nil; -*- */
/*
 * This program is free software; you can redistribute it and/or modify
 * it under the terms of the GNU General Public License version 2 as
 * published by the Free Software Foundation;
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
 */

#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
#include "ns3/netanim-module.h"

using namespace ns3;

NS_LOG_COMPONENT_DEFINE ("FirstScriptExample");

int
main (int argc, char *argv[])
{
  CommandLine cmd;
  cmd.Parse (argc, argv);
  
  Time::SetResolution (Time::NS);
  LogComponentEnable ("UdpEchoClientApplication", LOG_LEVEL_INFO);
  LogComponentEnable ("UdpEchoServerApplication", LOG_LEVEL_INFO);

  NodeContainer nodes;
  nodes.Create (2);

  PointToPointHelper pointToPoint;
  pointToPoint.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
  pointToPoint.SetChannelAttribute ("Delay", StringValue ("2ms"));

  NetDeviceContainer devices;
  devices = pointToPoint.Install (nodes);

  InternetStackHelper stack;
  stack.Install (nodes);

  Ipv4AddressHelper address;
  address.SetBase ("10.1.1.0", "255.255.255.0");

  Ipv4InterfaceContainer interfaces = address.Assign (devices);

  UdpEchoServerHelper echoServer (9);

  ApplicationContainer serverApps = echoServer.Install (nodes.Get (1));
  serverApps.Start (Seconds (1.0));
  serverApps.Stop (Seconds (10.0));

  UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
  echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
  echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
  echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

  ApplicationContainer clientApps = echoClient.Install (nodes.Get (0));
  clientApps.Start (Seconds (2.0));
  clientApps.Stop (Seconds (10.0));

  AnimationInterface anim("first, xml");
  AsciiTraceHelper ascii;
  point.EnableAsciiAll(ascii.CreateFileStream("first.tr"));
  pointToPoint.EnablePcapAll("first");

  Simulator::Run ();
  Simulator::Destroy ();
  return 0;
}
```

### TW10

**Problem statement:** Write a C/C++ program to simulate a network application with 4 nodes using NS2/NS3.
```c
```
## IOT
### Format
1. Title
2. Objective 
3. Brief Theory
4. Interfacing Block Diagram and manual calculations if any
5. Algorithm
6. Code
7. Output (Printout)
8. Conclusion
9. Course learning outcome
10. References

**Note:** The termworks may be different forr different batches

### TW1
1. **Title**: Interfacing LED's with Arduino - Generating morse code using led's controlled by arduino
2. **Objective:** The objective of this project is to create a pattern generator using LEDs interfaced with an Arduino, where the user inputs an alphanumeric character via serial input, and the corresponding Morse code is displayed using LED
3. **Brief theory**
    LEDs (Light Emitting Diodes) are semiconductor devices that emit light when an electric current passes through them. LEDs are widely used in electronic devices for various purposes due to their efficiency, compact size, and low power consumption. In this project, LEDs are employed to visually represent Morse code sequences. Each dot or dash of the Morse code is translated into a corresponding LED blink pattern, allowing users to observe and interpret the transmitted message. By interfacing LEDs with an Arduino microcontroller, we can automate the process of Morse code generation, making it accessible and versatile for educational, communication, or signaling purposes. This project highlights the synergy between digital electronics, communication systems, and human-computer interaction, showcasing how technology can bridge the gap between different modes of communication.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/9lMny52Fx4W-led-morse-code?sharecode=RRKPmBDFXpidk-w_oGs9z8sG91tTj4J9dfFONOixKPc)
5. **Algorithm:**
    - Receive input character via serial input.
    - Convert the character to Morse code.
    - Output the Morse code using LEDs.
6. **Code:**
    ```cpp
    // Define the size of the dictionary
    const int DICTIONARY_SIZE = 26;

    // Structure to represent a key-value pair
    struct MorsePair {
    char key;          // English alphabet character
    const char* value; // Morse code counterpart
    };

    // Array of key-value pairs representing the Morse code dictionary
    const MorsePair morseDictionary[DICTIONARY_SIZE] = {
    {'A', ".-"}, {'B', "-..."}, {'C', "-.-."}, {'D', "-.."}, {'E', "."}, {'F', "..-."},
    {'G', "--."}, {'H', "...."}, {'I', ".."}, {'J', ".---"}, {'K', "-.-"}, {'L', ".-.."},
    {'M', "--"}, {'N', "-."}, {'O', "---"}, {'P', ".--."}, {'Q', "--.-"}, {'R', ".-."},
    {'S', "..."}, {'T', "-"}, {'U', "..-"}, {'V', "...-"}, {'W', ".--"}, {'X', "-..-"},
    {'Y', "-.--"}, {'Z', "--.."}
    };

    // Define the pin for the LED
    const int LED_PIN = 13;

    void setup() {
    // Initialize Serial communication
    Serial.begin(9600);

    // Set LED pin as an output
    pinMode(LED_PIN, OUTPUT);
    }

    void loop() {
    // Prompt the user to enter a string
    Serial.println("Enter a string (A-Z):");

    // Read the user input
    while (!Serial.available()); // Wait for input
    String input = Serial.readStringUntil('\n'); // Read input until newline character

    // Translate input to Morse code and blink LED accordingly
    translateAndBlink(input);
    }

    // Function to translate a string to Morse code and blink LED
    void translateAndBlink(String input) {
    // Iterate through each character in the input string
    for (int i = 0; i < input.length(); i++) {
        // Convert character to uppercase
        char c = toupper(input.charAt(i));

        // Find Morse code counterpart in the dictionary
        const char* morseCode = findMorseCode(c);

        // Blink LED according to Morse code
        blinkMorseCode(morseCode);
    }
    }

    // Function to find Morse code for a given character
    const char* findMorseCode(char c) {
    for (int i = 0; i < DICTIONARY_SIZE; i++) {
        if (morseDictionary[i].key == c) {
        return morseDictionary[i].value;
        }
    }
    return ""; // Return empty string if character not found
    }

    // Function to blink LED according to Morse code
    void blinkMorseCode(const char* morseCode) {
    for (int i = 0; morseCode[i] != '\0'; i++) {
        if (morseCode[i] == '.') {
        digitalWrite(LED_PIN, HIGH);
        delay(250); // Dot duration
        digitalWrite(LED_PIN, LOW);
        delay(250); // Inter-element gap
        } else if (morseCode[i] == '-') {
        digitalWrite(LED_PIN, HIGH);
        delay(750); // Dash duration
        digitalWrite(LED_PIN, LOW);
        delay(250); // Inter-element gap
        } else if (morseCode[i] == ' ') {
        delay(750); // Inter-character gap
        }
    }
    delay(1250); // Inter-word gap
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1ZJ7CIzWlfuGDxl6ibK-RWAXvuKJzKh404-0vqsSofgQ/edit?usp=drive_link)
8. **Conclusion:** This project successfully demonstrates the interfacing of LEDs with an Arduino to generate Morse code patterns corresponding to user-input alphanumeric characters. It illustrates the practical application of Morse code and LED interfacing in educational or communication systems.
9. **Course learning outcome:** Understanding serial communication with Arduino.
Implementing logic for character-to-Morse code conversion.
Applying digital output to control LEDs.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW2
1. **Title**: Interfacing Arduino with a push button for glowing up the LED
2. **Objective**: The objective of this project is to interface a push button with an Arduino board to control the illumination of an LED. When the push button is pressed, the LED will turn on, and when it is released, the LED will turn off.
3. **Brief theory**
    - Push Button: A push button is a momentary switch that completes an electrical circuit when pressed. It is commonly used in electronic projects to provide user input or trigger actions.
    - LED (Light Emitting Diode): An LED is a semiconductor device that emits light when current flows through it. It is often used in electronic projects for visual indicators or illumination purposes.
    - Arduino: Arduino is an open-source electronics platform based on easy-to-use hardware and software. It consists of a microcontroller board and a development environment for writing and uploading code to the board.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/jnvAr1ZuwJy-push-button-basic?sharecode=bAq576muQKyDizDCJWcTdD9HF5hn9nONR0r8JFUCRkk)
5. **Algorithm:**
    - Initialize the Arduino board and configure the push button and LED pins as inputs and outputs, respectively.
    - Continuously monitor the state of the push button.
    - If the push button is pressed (input HIGH), turn on the LED by setting its pin to HIGH.
    - If the push button is released (input LOW), turn off the LED by setting its pin to LOW.
6. **Code:**
    ```cpp
    // constants won't change. They're used here to set pin numbers:
    const int buttonPin = 12;  // the number of the pushbutton pin
    const int ledPin = 13;    // the number of the LED pin

    // variables will change:
    int buttonState = 0;  // variable for reading the pushbutton status

    void setup() {
    // initialize the LED pin as an output:
    pinMode(ledPin, OUTPUT);
    // initialize the pushbutton pin as an input:
    pinMode(buttonPin, INPUT);
    }

    void loop() {
    // read the state of the pushbutton value:
    buttonState = digitalRead(buttonPin);

    // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
    if (buttonState == HIGH) {
        // turn LED on:
        digitalWrite(ledPin, HIGH);
    } else {
        // turn LED off:
        digitalWrite(ledPin, LOW);
    }
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1dF2PvUYFOZPXXnzVaKNE12ylT1uJX4PeAAjsG9yl0AI/edit?usp=drive_link)
8. **Conclusion:** This project demonstrates the basic concept of interfacing a push button with an Arduino to control an LED. By understanding how to read digital inputs from a push button and control digital outputs to an LED, users can create interactive systems and prototypes for various applications.
9. **Course learning outcome**
    - Understanding of digital input and output operations with Arduino.
    - Implementation of push button interfacing techniques for user input.
    - Practical application of LED control for visual feedback or illumination.
    - Introduction to basic circuit design and prototyping using microcontrollers.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW3
1. **Title**: Interfacing Arduino with a button to simulate a dice roll
2. **Objective**: The objective of this project is to interface a push button with an Arduino to generate and display a random number from 1-6, simulating a dice roll, on a 16x2 LCD display.
3. **Brief theory:** A push button is a momentary switch used to provide user input to microcontroller-based systems. LEDs are used to indicate the result of the simulated dice roll. The Arduino generates random numbers to mimic the rolling of a dice.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/d8LVjEjIsCN-push-button-dice?sharecode=mSXd9vECBXWRtyY0c9PEN3wPcHlT0o6yElkI8aDNCnw)
5. **Algorithm:**
    - Setup the push button and LED connections.
    - Initialize the LCD display.
    - Wait for the push button press.
    - Generate a random number between 1 and 6.
    - Display the number on the LCD.
    - Light up LEDs corresponding to the number rolled.
6. **Code:**
    ```cpp
    // C++ code
    //
    #include <LiquidCrystal_I2C.h>

    // defining constants
    const int buttonPin = 12;
    const int ledPin = 13;

    // global variables
    int buttonState = 0;
    int die;

    // defining lcd object
    LiquidCrystal_I2C lcd_1(32, 16, 2);

    void setup()
    {
    // lcd setup
    lcd_1.init();
    lcd_1.setCursor(0, 0);
    lcd_1.backlight();
    lcd_1.display();
    
    // button setup
    pinMode(buttonPin, INPUT);
    
    // random seed 
    randomSeed(analogRead(0));
    
    // button setup
    pinMode(ledPin, OUTPUT);
    }

    void refreshDisplay(int arg) {
    lcd_1.clear();
    lcd_1.setCursor(0, 0);
    lcd_1.print(arg);
    }

    int rollDice() {
    // Check if the button is pressed
    if (digitalRead(buttonPin) == HIGH) {
        // Generate a random number between 1 and 6 (inclusive)
        int randomNumber = random(1, 7);
        refreshDisplay(randomNumber);
        digitalWrite(ledPin, HIGH);
        delay(1000);
        return randomNumber;
    } else {
        // If button is not pressed, return -1 as an indication
        digitalWrite(ledPin, LOW);
        return -1;
    }
    }

    void loop()
    {
    // only for debugging
    die = rollDice();
    Serial.println(die);
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1an_sI5c3DNORjg-2KgW2bp_Qqr3NABo0Yw9quRhTN6g/edit?usp=drive_link)
8. **Conclusion:** This project effectively demonstrates the integration of push buttons, LEDs, and LCD displays with Arduino to create a simulated dice roll. It serves as a practical example for understanding user input, random number generation, and visual feedback in embedded systems.
9. **Course learning outcome**
    - Understanding digital input with Arduino.
    - Implementing random number generation.
    - Interfacing and controlling LED and LCD displays.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW4
1. **Title**: Interfacing Arduino with SR04 Ultrasonic Sensor for Distance Measurement and buzzer for alert
2. **Objective**: The objective of this project is to create a simulated parking sensor system by interfacing an SR04 ultrasonic sensor with a buzzer. The system aims to detect obstacles in a parking space and provide audible feedback to the user through the buzzer, mimicking the behavior of a real parking sensor.
3. **Brief theory**
    - SR04 Sensor: The SR04 is an ultrasonic distance sensor that measures distance by emitting ultrasonic waves and calculating the time it takes for the waves to bounce back after hitting an obstacle. It consists of a transmitter, receiver, and control circuit.
    - Buzzer: A buzzer is an electromechanical device that produces sound when an electric current is passed through it. It is commonly used in electronic projects to provide audible alerts or feedback to users.
    - Parking Sensor: In real-world applications, parking sensors use ultrasonic sensors to detect nearby obstacles when parking a vehicle. They provide feedback to the driver through visual or audible signals to assist in parking maneuvers.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/h4zhyniMwh8-copy-of-ultrasonic-distance-sensor-with-buzzer?sharecode=g99HqYIqaZYtFaHEj4ZybbZIXg2_4tryGFaNdn7FFx8)
5. **Algorithm**
    - Initialize the Arduino board and configure the SR04 sensor and buzzer pins.
    - Continuously trigger the SR04 sensor to send ultrasonic waves and measure the time it takes for the waves to bounce back.
    - Calculate the distance to the nearest obstacle based on the time-of-flight of the ultrasonic waves.
    - If an obstacle is detected within a certain threshold distance, activate the buzzer to emit an audible alert.
    - Adjust the frequency or intensity of the buzzer based on the proximity of the obstacle to simulate different warning levels.
6. **Code**
    ```cpp
    const int triggerPin = 6;  // Trigger pin of the ultrasonic sensor
    const int echoPin = 7;     // Echo pin of the ultrasonic sensor
    const int buzzerPin = 9;   // Buzzer pin

    long duration;
    int distance;

    void setup() {
    pinMode(triggerPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(buzzerPin, OUTPUT);
    Serial.begin(9600);  // Initialize serial communication at 9600 bps
    }

    void loop() {
    // Clear the trigger pin
    digitalWrite(triggerPin, LOW);
    delayMicroseconds(2);

    // Set the trigger pin HIGH for 10 microseconds
    digitalWrite(triggerPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(triggerPin, LOW);

    // Read the echo pin, and calculate the distance
    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;  // Speed of sound wave divided by 2 (go and back)

    Serial.print("Distance: ");
    Serial.println(distance);

    // Set buzzer beeping rate based on distance
    if (distance < 10) {
        tone(buzzerPin, 1000);  // Continuous beep
        delay(100);  // Small delay to avoid overload
        noTone(buzzerPin);
        Serial.println("TRIPLE CAUTION, high frequency!!!");
    } else if (distance < 20) {
        tone(buzzerPin, 1000);
        delay(200);
        noTone(buzzerPin);
        delay(200);
        Serial.println("DOUBLE CAUTION, mid frequency!!!");
    } else if (distance < 30) {
        tone(buzzerPin, 1000);
        delay(400);
        noTone(buzzerPin);
        delay(400);
        Serial.println("CAUTION, low frequency!!!");
    } else if (distance < 50) {
        tone(buzzerPin, 1000);
        delay(800);
        noTone(buzzerPin);
        delay(800);
        Serial.println("Appropriate distace, v low frequency!!!");
    } else {
        noTone(buzzerPin);  // No beep
    }

    delay(1000);  // Delay between readings
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1CaE9CIDSQp94Wd2X4D6-2GYObaCcoGroknS6wvDIBjM/edit?usp=drive_link)
8. **Conclusion:** This project demonstrates the implementation of a simulated parking sensor system using an SR04 ultrasonic sensor and a buzzer. By interfacing these components with an Arduino board and analyzing sensor data, the system can provide audible feedback to users when obstacles are detected, aiding in parking maneuvers. While this simulation does not replace the functionality of real parking sensors, it serves as an educational and prototyping tool for understanding sensor interfacing and feedback mechanisms.
9. **Course learning outcomes:**
    - Understanding of ultrasonic sensor operation and distance measurement.
    - Implementation of buzzer control for audible alerts.
    - Application of sensor data analysis for obstacle detection.
    - Integration of sensor feedback systems with microcontroller-based projects.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019


### TW5 (refer this)

1. **Title**  
Create a Program to Make a Counter Using a 7-Segment Display (Counting from 0-9 and then Back to 0)

2. **Objective**  
To design and implement a program that controls a 7-segment display to function as a counter, incrementing from 0 to 9 and then resetting back to 0, using a USB connection to a computer for power and programming.

3. **Brief Theory**  
A 7-segment display is an electronic display device consisting of seven LEDs (segments) arranged in a rectangular fashion. By illuminating specific segments, it can display decimal numerals and some alphabets. In this project, a microcontroller (such as an Arduino) will be programmed to control the 7-segment display via a USB connection to a computer. The counter will increment from 0 to 9, after which it will reset to 0 and continue counting. This project involves understanding both hardware interfacing and software programming to achieve the desired functionality.

4. **Interfacing Block Diagram and manual calculations if any**  
[Check tinkercad](https://www.tinkercad.com/things/dLAqaiOTCOr-copy-of-arduino-7-segment-display)

5. **Algorithm**  
    1. **Initialize System**  
        1. Set up the microcontroller (e.g., Arduino) with the necessary libraries and configurations.
        2. Initialize the pins connected to the 7-segment display as outputs.

    2. **Display Initialization**  
        1. Ensure the 7-segment display is properly initialized to show the number 0 at start.

    3. **Counter Logic**  
        1. Set an initial counter value to 0.  
        2. Enter a loop to increment the counter value by 1 at regular intervals (eg., every second).  
        3. Update the 7-segment display to show the current counter value.  
        4. If the counter value exceeds 9, reset it to 0.

    4. **Loop and Update Display**  
        1. Continuously check and update the counter value and display it.  
        2. Implement a mechanism to reset the counter if needed (e.g., via a button press).

6. **Code**
    ```cpp
    unsigned const int A = 13;
    unsigned const int B = 12;
    unsigned const int C = 11;
    unsigned const int D = 10;
    unsigned const int E = 9;
    unsigned const int F = 8;
    unsigned const int G = 7;
    unsigned const int H = 6;

    void setup(void)
    {
    pinMode(A, OUTPUT);
    pinMode(B, OUTPUT);
    pinMode(C, OUTPUT);
    pinMode(D, OUTPUT);
    pinMode(E, OUTPUT);
    pinMode(F, OUTPUT);
    pinMode(G, OUTPUT);
    pinMode(H, OUTPUT);
    }

    //My Functions

    void zero(void) {
    digitalWrite(A, LOW);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void one(void) {
    digitalWrite(A, LOW);
    digitalWrite(B, LOW);
    digitalWrite(C, LOW);
    digitalWrite(D, HIGH);
    digitalWrite(E, LOW);
    digitalWrite(F, LOW);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void two(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, LOW);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, LOW);
    digitalWrite(H, LOW);
    }

    void three(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, LOW);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, LOW);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void four(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, LOW);
    digitalWrite(D, HIGH);
    digitalWrite(E, LOW);
    digitalWrite(F, LOW);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void five(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, LOW);
    digitalWrite(E, LOW);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void six(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, LOW);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void seven(void) {
    digitalWrite(A, LOW);
    digitalWrite(B, LOW);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, LOW);
    digitalWrite(F, LOW);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void eight(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    void nine(void) {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, LOW);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    digitalWrite(H, LOW);
    }

    // Start
    void loop(void)
    {
    zero();
    delay(1000);
    
    one();
    delay(1000);
    
    two();
    delay(1000);
    
    three();
    delay(1000);
    
    four();
    delay(1000);
    
    five();
    delay(1000);
    
    six();
    delay(1000);
    
    seven();
    delay(1000);
    
    eight();
    delay(1000);
    
    nine();
    delay(1000);
    }
    ```

7. **Output (Printout)**  
[Check here](https://docs.google.com/document/d/1_sLY3ZDCFTrZSyVrUzgbHFK0bf1y-vgfDmAbqRh4_54/edit?usp=drive_link)

8. **Conclusion**  
The project successfully demonstrates the use of a microcontroller to control a 7-segment display counter. The counter increments from 0 to 9 and then resets to 0, providing a simple yet effective example of hardware interfacing and programming. This project enhances understanding of both the hardware and software aspects of embedded systems.

9. **Course Learning Outcome**  
- Gain practical experience with microcontroller development boards such as Arduino.
- Learn to interface and control a 7-segment display.
- Develop skills in programming and algorithm design for hardware control.
- Understand the basics of hardware interfacing and electronic component control.
- Acquire knowledge of integrating microcontrollers with computer-based programming.

10. **References**  
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

---

Feel free to fill in the specific details and code as you develop the project.

### TW5 (don't refer this)
1. **Title**: Interfacing Arduino with a 16x2 LCD Display as a stopwatch
2. **Objective**: The objective of this project is to interface an Arduino board with a 16x2 LCD display to create a stopwatch. The stopwatch will be capable of measuring elapsed time with precision and displaying it on the LCD screen.
3. **Brief theory**
    - Arduino: Arduino is an open-source electronics platform based on easy-to-use hardware and software. It consists of a microcontroller board and a development environment for writing and uploading code to the board. Arduino boards are commonly used in various projects for automation, control, and data logging.
    - 16x2 LCD Display: A 16x2 LCD (Liquid Crystal Display) module is a type of alphanumeric display that can display 16 characters per line and has 2 lines. It is widely used in electronic projects for displaying text-based information such as sensor readings, messages, or time.
    - Stopwatch: A stopwatch is a timekeeping device used to measure elapsed time with precision. It typically consists of a start/stop button and a reset button to control the timing operation.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/h3f0oU2fSLH-copy-of-arduino-stopwatch-split-time?sharecode=Fmwa9Sjcfl4fub_9e-zsu9xsgjERSuwIwua41kpm2xs)
5. **Algorithm**
    - Initialize the Arduino board and configure the connections for the 16x2 LCD display.
    - Implement functions to control the LCD display, including functions for clearing the display, setting the cursor position, and printing characters or strings.
    - Implement a function to start, stop, and reset the stopwatch.
    - Continuously update the LCD display to show the elapsed time while the stopwatch is running.
    - Handle user input from external buttons to control the stopwatch operations.
6. **Code**
    ```cpp

    // https://aeroarduino.com/arduino-hobbyist/stopwatch-with-arduino-and-lcd-on-tinkercad/

    // https://youtu.be/Sx8P1-MxHIQ

    // https://youtu.be/cjVaV6UrckU

    //https://www.tinkercad.com/things/4GNAuVVRqRL


    #include <LiquidCrystal.h>
    //PIN 5 R/W to Ground, for writing
    //LCD Mode : 4 data pin
    //Functions: Start, stop, saving up to 4 partial time in memory.
    //10 millis = 1 hundredth of a second. The chronometer measures hour, minutes, seconds, and hundredths of a second.

    //Buttons with internal Pullup, so if they get pressed we get LOW
    const int start = 8;  //Start the stopwatch
    const int pausa = 9;  //Stop
    const int partial = 10;  //Save a partial
    const int scroll_partial = 11;  //If paused, check the 4 last saved partial 
    int x = 0; //Variable to manage the loop

    //LCD
    int lcdclear = 0; //this to variables are needed for managing
    int Display = 0; //the display, to clear and print

    //chronometer
    int cents = 0;
    int seconds = 0;  
    int minutes = 0;
    int hours = 0;
    const int interval = 10; //Every 10 milliseconds i increase  1 cent
    unsigned long previousMillis = 0;
    int c1, c2, s1, s2, m1, m2, h; //Variables used to put in the form 
                                //h:m2m1:s2s1:c2c1

    //Partial: I save 4 partial, that can be seen if stopwatch is stopped
    int partial2[7]; //penultimate partial (The one that stays in Old). The last partial stays in New:
    int partial3[7]; 
    int partial4[7]; 
    int scrolling = 0; //Used to scroll the saved partial times


    LiquidCrystal lcd(2, 3, 4, 5, 6, 7); // RS-Enable-D4-D5-D6-D7 in that digitalPin

    void setup() {
    pinMode(start, INPUT_PULLUP); //In the schematic from right to left
    pinMode(pausa, INPUT_PULLUP);//there are start-pausa-partial-scroll_partial
    pinMode(partial, INPUT_PULLUP);
    pinMode(scroll_partial, INPUT_PULLUP);
    lcd.begin(16,2);
    lcd.print("Press start");

    }

    void loop() {
    if (x == 0) {  //Initially is 0
        while(digitalRead(start) == HIGH) {};  //Until i press the button, the chronometer doesn't start
    x++; //When i press the button, i go out from this cycle, x++ and i cannot return here anymore
    }
    if (lcdclear == 0){   //Condition to clear the display, used in the various functions
        lcd.clear();
        lcdclear++;
    }
    if (Display == 0){ //Also this is used to clear display
    lcd.home();
    lcd.print("Now:  ");  //With this condition, i can print "Now: " one single time, otherwise the chronometer wouldn't be precise
    Display++; 
    scrolling = 0; //When i exit from the partial menu, then if i go in the partial menu again i always get in PAR1 and PAR2
    }              
    chronometer(); //At the end of every increase, i control if stop is pressed. And also if the partial function is pressed
    pause();
    f_partial();
    }

    void chronometer(void){   //This function print:   "New: Actual time"
    unsigned long currentMillis = millis();  //If for the updating. If it is true, it means 1 cent of a second had passed. Update cents, minutes, seconds, hours and then i write on the lcd
    if (currentMillis - previousMillis >= interval) {  
        previousMillis = currentMillis;
        cents++;
        if (cents == 100){
        cents = 0;
        seconds++;
        if (seconds == 60) {
            seconds = 0;
            minutes++;
            if (minutes == 60){
            minutes = 0; 
            hours++;
            if (hours == 24)
                hours = 0;
            }
        }
    }
        int cent = cents;
        int sec = seconds;
        int minu = minutes; //Taking the digits separeted
        h = hours;  //For the other funcionts, so i can put hours = 0 and h still is the last value
        c1 = cent%10;
        cent /= 10;
        c2 = cent%10;
        s1 = sec%10;
        sec /= 10;
        s2 = sec%10;
        m1 = minu%10;
        minu /= 10;
        m2 = minu%10;
        lcd.setCursor(6, 0);
        lcd.print(h);
        lcd.print(':');
        lcd.print(m2);
        lcd.print(m1);
        lcd.print(':');
        lcd.print(s2);
        lcd.print(s1);
        lcd.print(':');
        lcd.print(c2);
        lcd.print(c1); 
    } 
    }

    void scrollPartial(void){
        while(digitalRead(scroll_partial) == LOW) {}; //Debounce, as long as i press the button the real function doesn't start
        if (scrolling == 0) { //Visualize the last 2 partials
        lcd.clear(); 
        lcd.home();
        lcd.print("PAR1:");
        lcd.setCursor(6, 0);
        lcd.print(h);
        lcd.print(':');
        lcd.print(m2);
        lcd.print(m1);
        lcd.print(':');
        lcd.print(s2);
        lcd.print(s1);
        lcd.print(':');
        lcd.print(c2);
        lcd.print(c1);
        lcd.setCursor(0, 1);
        lcd.print("PAR2:");
        lcd.setCursor(6, 1);
        lcd.print(partial2[0]);
        lcd.print(':');
        lcd.print(partial2[1]);
        lcd.print(partial2[2]);
        lcd.print(':');
        lcd.print(partial2[3]);
        lcd.print(partial2[4]);
        lcd.print(':');
        lcd.print(partial2[5]);
        lcd.print(partial2[6]); 
        Display = 0; //When i press start the display must be cleared
        lcdclear = 0; //When i press start the display must be cleared
        cents = seconds = minutes = hours  = 0;
        scrolling++;
    }
    else if (scrolling == 1){ //Visualize 3th and 4th partial
        lcd.clear();
        lcd.home();
        lcd.print("PAR3:");
        lcd.setCursor(6, 0);
        lcd.print(partial3[0]);
        lcd.print(':');
        lcd.print(partial3[1]);
        lcd.print(partial3[2]);
        lcd.print(':');
        lcd.print(partial3[3]);
        lcd.print(partial3[4]);
        lcd.print(':');
        lcd.print(partial3[5]);
        lcd.print(partial3[6]);
        lcd.setCursor(0, 1);
        lcd.print("PAR4:");
        lcd.setCursor(6, 1);
        lcd.print(partial4[0]);
        lcd.print(':');
        lcd.print(partial4[1]);
        lcd.print(partial4[2]);
        lcd.print(':');
        lcd.print(partial4[3]);
        lcd.print(partial4[4]);
        lcd.print(':');
        lcd.print(partial4[5]);
        lcd.print(partial4[6]); 
        Display = 0; //When i press start the display must be cleared
        lcdclear = 0; //When i press start the display must be cleared
        cents = seconds = minutes = hours  = 0;
        scrolling = 0;
        
    }
    
    } 


    void pause(void){  //If pause is pressed, i stop in this function until start doesn't get pressed again
        if (digitalRead(pausa) == HIGH) 
            return;
        else if (digitalRead(pausa) == LOW){ //Stuck in this cycle until i press start
            while(digitalRead(start) == HIGH) {  
            if (digitalRead(scroll_partial) == LOW) //If i press the button for seeing the partial, i enter in that function
                scrollPartial();    //When scrollPartial() ends, i'm still in this function, so if i press start the chronometer starts back normal
            }
        } 
    }

    void f_partial(void){   //If this button is pressed, i put the current value of New in Old, and a new crhonometer starts
    if (digitalRead(partial) == HIGH)
        return;
    else if (digitalRead(partial) == LOW ){ 
    lcd.clear();
    lcd.setCursor(0, 1); //The values calculated in the function chronometer can be used,  h,m,s,c
    lcd.print("Old: ");
    lcd.setCursor(6, 1);
    lcd.print(h);
    lcd.print(':');
    lcd.print(m2);
    lcd.print(m1);
    lcd.print(':');
    lcd.print(s2);
    lcd.print(s1);
    lcd.print(':');
    lcd.print(c2);
    lcd.print(c1);   //When i come here, i've got the old values for h,m,s,c,                       i save it in the partial array
    Display = 0;   //The new is written again 
    cents = 0;
    seconds = 0;
    minutes = 0;
    hours = 0;

    partial4[0] = partial3[0]; //Partial4[] is updated with the old partial3[]
    partial4[1] = partial3[1];
    partial4[2] = partial3[2];
    partial4[3] = partial3[3];
    partial4[4] = partial3[4];
    partial4[5] = partial3[5];
    partial4[6] = partial3[6];
    
        
    partial3[0] = partial2[0]; //Partial3[] is updated with the old partial2[]
    partial3[1] = partial2[1];
    partial3[2] = partial2[2];
    partial3[3] = partial2[3];
    partial3[4] = partial2[4];
    partial3[5] = partial2[5];
    partial3[6] = partial2[6];
        
    partial2[0] = h;    //Update partial2 with OLD
    partial2[1] = m2;
    partial2[2] = m1;
    partial2[3] = s2;
    partial2[4] = s1;
    partial2[5] = c2;
    partial2[6] = c1;
    
    while(digitalRead(partial) == LOW) {}; //Debounce, until i press the button i stay here
    } 
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1FiYQVSvUCVYc9rEptCCPdLAyl3Ze-tysv06xzaZ4fAU/edit?usp=drive_link)
8. **Conclusion:** This project demonstrates the integration of an Arduino board with a 16x2 LCD display to create a stopwatch. By leveraging the capabilities of Arduino in conjunction with the LCD display, users can implement a functional timing device suitable for various applications, such as sports, experiments, or projects requiring time measurement.
9. **Course learning outcomes**
    - Understanding of interfacing techniques for LCD displays with Arduino.
    - Implementation of timing and control logic for stopwatch functionality.
    - Practical application of microcontroller-based timing systems.
    - Introduction to user interface design and interaction using external buttons.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW6

---

**1. Title**  
Interface an Arduino to a 7-Segment and 16x2 LCD Display (Interfacing Arduino to Show a T-Minus Countdown on the 16x2 LCD and 7-Segment Display, and Show "LAUNCH" When the Counter Reaches 0)

**2. Objective**  
To design and implement a program that controls both a 7-segment display and a 16x2 LCD display using an Arduino. The system will display a T-minus countdown on both displays and show "LAUNCH" when the countdown reaches 0.

**3. Brief Theory**  
A 7-segment display is used to display individual digits by illuminating specific segments, while a 16x2 LCD display can show 16 characters on each of its two lines. In this project, an Arduino microcontroller will be used to control both displays. The Arduino will count down from a specified number (T-minus countdown) and simultaneously update both displays with the current countdown value. When the countdown reaches 0, the displays will show the word "LAUNCH". This project involves understanding both hardware interfacing and software programming to achieve the desired functionality.

**4. Interfacing Block Diagram and manual calculations if any**  
[Check tinkercad](https://www.tinkercad.com/things/dLAqaiOTCOr-t-minus-countdown?sharecode=rcco4cMk1Q2-_s3Ltryr7xGzqSPMc4IDITPfLgxGUsU)

5. **Algorithm**  
    1. **Initialize System**  
        1. Set up the Arduino with the necessary libraries for controlling the 7-segment display and the 16x2 LCD display.  
        2. Initialize the pins connected to the 7-segment display and the LCD as outputs.

    2. **Display Initialization**  
        1. Ensure the 16x2 LCD display is properly initialized and ready to display text.  
        2. Ensure the 7-segment display is properly initialized to show the initial countdown value.

    3. **Set Initial Countdown Value**  
        1. Set a variable for the countdown starting value (e.g., T-minus 10).

    4. **Countdown Logic**  
        1. Enter a loop to decrement the countdown value by 1 at regular intervals (e.g., every second).  
        2. Update both the 7-segment display and the 16x2 LCD display to show the current countdown value.  
        3. If the countdown value reaches 0, display "LAUNCH" on the 16x2 LCD and clear the 7-segment display or show 0.

    5. **Loop and Update Display**  
        1. Continuously check and update the countdown value and display it.  
        2. Implement a mechanism to start the countdown (e.g., via a button press).

6. **Code**  
```cpp
#include <ShiftRegister74HC595.h>
#include <LiquidCrystal.h>

// CREATE SHIFT REGISTER OBJECT (NUMBER OF SHIFT REGISTERS, DATA PIN, CLOCK PIN, LATCH PIN)
ShiftRegister74HC595<2> sr(4, 2, 3);

// Define the binary values to display numbers 0 to 9 on a 7-segment display
uint8_t numberB[] = {
  B00111111, // 0
  B00000110, // 1
  B01011011, // 2
  B01001111, // 3
  B01100110, // 4
  B01101101, // 5
  B01111101, // 6
  B00000111, // 7
  B01111111, // 8
  B01101111  // 9
};

// Initialize the LCD library with the numbers of the interface pins
const int rs = 16, en = 17, d4 = 13, d5 = 12, d6 = 11, d7 = 10;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
  // Set up the LCD's number of columns and rows
  lcd.begin(16, 2);
  // Initial message to the LCD (optional, can be removed)
  delay(2000); // Display initial message for 2 seconds
}

void loop() {
  // Countdown from 10 to 0
  for (int i = 10; i >= 0; i--) {
    // Display "T-MINUS" on the LCD
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("   T-MINUS");

    // Display the current number on the 7-segment display
    if (i < 10) {
      uint8_t pinValues[] = {B00000000, numberB[i]};
      sr.setAll(pinValues);
    } else {
      uint8_t pinValues[] = {numberB[1], numberB[0]};
      sr.setAll(pinValues);
    }

    // Display the countdown number on the LCD
    lcd.setCursor(0, 1);
    lcd.print("       ");
    lcd.print(i);

    // Delay for 1 second to simulate a timer
    delay(1000);
  }

  // When countdown reaches 0, display "LAUNCH" on the LCD
  lcd.clear();
  lcd.setCursor(4, 0); // Adjust the position as needed
  lcd.print("LAUNCH");
  delay(5000); // Display "LAUNCH" for 5 seconds

  // Optional: Reset display and go back to the initial state
  lcd.clear();
  delay(2000); // Display initial message for 2 seconds
}
```

7. **Output (Printout)**  
[Check here](https://docs.google.com/document/d/1mvH1MFPovc2XRDqLKx9Ptri_YnlAszWvKEIg9jnQ1WE/edit?usp=drive_link)

8. **Conclusion**  
The project successfully demonstrates the use of an Arduino to control both a 7-segment display and a 16x2 LCD display. The system accurately performs a T-minus countdown, displaying the countdown on both displays and showing "LAUNCH" when the countdown reaches 0. This project enhances understanding of hardware interfacing and programming for multiple display types.

9. **Course Learning Outcome**  
- Gain practical experience with Arduino microcontroller development.
- Learn to interface and control a 7-segment display and a 16x2 LCD display.
- Develop skills in programming and algorithm design for countdown timers.
- Understand the basics of hardware interfacing and multiple display management.
- Acquire knowledge of integrating microcontrollers with various display components.

10. **References**  
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW7
---

1. **Title**  
Interface Buzzer with Raspberry Pi

2. **Objective**  
To design and implement a system that interfaces a buzzer with a Raspberry Pi, allowing the buzzer to be controlled programmatically.

3. **Brief Theory**  
A buzzer is an audio signaling device commonly used for alarms, timers, and user notifications. It can be controlled by a microcontroller or single-board computer such as the Raspberry Pi. By sending a signal from the Raspberry Pi's GPIO pins to the buzzer, it can be turned on or off. This project involves understanding the basics of GPIO (General-Purpose Input/Output) pin control on the Raspberry Pi and using Python programming to manage the buzzer's operation.

4. **Interfacing Block Diagram and manual calculations if any**  
[Check google drive](https://docs.google.com/document/d/1lDTJbw59X2QkceyH3WqeFzT6MaX-54XPzXH0eW58vws/edit?usp=drive_link)

5. **Algorithm**  
    1. **Initialize System**  
        1. Set up the Raspberry Pi and ensure it has the necessary software installed (e.g., Raspbian OS, Python, GPIO libraries).
        2. Connect the buzzer to one of the GPIO pins on the Raspberry Pi (e.g., GPIO18) and connect the other terminal of the buzzer to a ground (GND) pin.

    2. **Library Import and GPIO Setup**  
        1. Import the necessary libraries for GPIO control in the Python script.
        2. Set up the GPIO pin connected to the buzzer as an output pin.

    3. **Buzzer Control Logic**  
        1. Write a function to turn the buzzer on and off by sending a high or low signal to the GPIO pin.
        2. Implement a loop or condition to control the buzzer based on specific events or time intervals.

    4. **Execution and Testing**  
        1. Run the Python script to control the buzzer.
        2. Test different scenarios such as turning the buzzer on for a set duration, creating a beeping pattern, or responding to an input signal.

6. **Code**  
    ```py
    # @Auth Xtrans Solutions Pvt. Ltd.
    # Program to test Buzzer
    # Connect RM9 to RM17

    import time
    import RPi.GPIO as gpio

    gpio.setwarnings(False)
    gpio.setmode(gpio.BOARD)
    gpio.setup(38, gpio.OUT)

    try:
        while(1):
            gpio.output(38,0)
            print("Buzzer OFF")
            time.sleep(1)
            gpio.output(38,1)
            print("Buzzer ON")
            time.sleep(1)
            #gpio.cleanup()
    except KeyboardInterrupt:
            gpio.cleanup()
            exit
    ```

7. **Output (Printout)**  
[Check google drive](https://docs.google.com/document/d/1lDTJbw59X2QkceyH3WqeFzT6MaX-54XPzXH0eW58vws/edit?usp=drive_link)

8. **Conclusion**  
The project successfully demonstrates how to interface a buzzer with a Raspberry Pi and control it programmatically using Python. This setup can be used in various applications such as alarms, notifications, and user feedback systems. The project enhances understanding of GPIO pin control and basic electronics interfacing with a Raspberry Pi.

9. **Course Learning Outcome**  
    - Gain practical experience with the Raspberry Pi single-board computer.
    - Learn to interface and control a buzzer using GPIO pins.
    - Develop skills in Python programming for hardware control.
    - Understand the basics of electronic component interfacing.
    - Acquire knowledge of integrating Raspberry Pi with various peripherals.

10. **References**  
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW8

1. **Title**  
Interface Raspberry Pi with LDR Sensor and Buzzer (So When LDR Sensor Stops Detecting Light, the Buzzer Turns On)

2. **Objective**  
To design and implement a system that interfaces an LDR (Light Dependent Resistor) sensor and a buzzer with a Raspberry Pi. The system will monitor the light level using the LDR sensor and activate the buzzer when the light level drops below a certain threshold.

3. **Brief Theory**  
An LDR sensor changes its resistance based on the amount of light it detects; it has higher resistance in the dark and lower resistance in the light. This varying resistance can be used to measure light intensity. A buzzer is an audio signaling device that can be controlled via GPIO pins on a Raspberry Pi. In this project, the Raspberry Pi reads the LDR sensor's value and triggers the buzzer when the light level falls below a predefined threshold. This involves understanding analog-to-digital conversion (since the Raspberry Pi lacks built-in ADC), GPIO pin control, and Python programming.

4. **Interfacing Block Diagram and manual calculations if any**  
[Check google drive](https://docs.google.com/document/d/1ybN5h7GHyxYkyOdVbcmY1Z0dzMGltQNB5M6m1oiKTns/edit?usp=drive_link)

5. **Algorithm**  
    1. **Initialize System**  
        1. Set up the Raspberry Pi with necessary software installed (e.g., Raspbian OS, Python, GPIO libraries, and an ADC like MCP3008 if needed).  
        2. Connect the LDR sensor in a voltage divider configuration to an ADC (e.g., MCP3008) if using one. Connect the ADC to the Raspberry Pi's SPI pins.  
        3. Connect the buzzer to one of the GPIO pins on the Raspberry Pi (e.g., GPIO18) and connect the other terminal of the buzzer to a ground (GND) pin.

    2. **Library Import and GPIO/ADC Setup**  
        1. Import the necessary libraries for GPIO and ADC control in the Python script.  
        2. Set up the GPIO pin connected to the buzzer as an output pin.  
        3. Initialize the ADC to read values from the LDR sensor.

    3. **Light Level Detection Logic**  
        1. Read the value from the LDR sensor through the ADC.  
        2. Determine a threshold value for light detection (e.g., set a value below which the light is considered to be "not detected").

    4. **Buzzer Control Logic**  
        1. Continuously monitor the LDR sensor's value.  
        2. If the sensor value drops below the threshold, turn the buzzer on by sending a high signal to the GPIO pin.  
        3. If the sensor value is above the threshold, turn the buzzer off by sending a low signal to the GPIO pin.

    5. **Execution and Testing**  
        1. Run the Python script to monitor the LDR sensor and control the buzzer.  
        2. Test the system by changing the light levels and observing the buzzer's response.

6. **Code**  
    ```py
    import RPi.GPIO as gpio
    import time

    gpio.setwarnings(False)
    gpio.setmode(gpio.BOARD)
    gpio.setup(38,gpio.OUT)
    gpio.setup(33,gpio.IN)

    try:
        while(1):
            light=gpio.input(33)
            if light==0:
                gpio.output(38,0)
                print("Light Detected , Buzzer off")
                time.sleep(1)
            elif light==1:
                gpio.output(38,1)
                print("Light not detected , Buzzer on")
            time.sleep(1)
    except KeyboardInterrupt:
        gpio.cleanup()
        exit
    ```

7. **Output (Printout)**  
[Check google drive](https://docs.google.com/document/d/1ybN5h7GHyxYkyOdVbcmY1Z0dzMGltQNB5M6m1oiKTns/edit?usp=drive_link)

8. **Conclusion**  
The project successfully demonstrates how to interface an LDR sensor and a buzzer with a Raspberry Pi. The system monitors light levels using the LDR sensor and activates the buzzer when the light level drops below a certain threshold. This setup can be used for applications such as intruder alarms or light-sensitive alerts. The project enhances understanding of analog sensor interfacing, GPIO control, and ADC usage with a Raspberry Pi.

9. **Course Learning Outcome**  
    - Gain practical experience with the Raspberry Pi single-board computer.  
    - Learn to interface and control an LDR sensor and a buzzer using GPIO pins.  
    - Develop skills in Python programming for hardware control.  
    - Understand the basics of analog-to-digital conversion and sensor interfacing.  
    - Acquire knowledge of integrating Raspberry Pi with various peripherals.

10. **References**  
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW9

1. **Title**\
    Using DHT-11 to read the current temperature, humidity and sending the data to the cloud using ThingSpeak API

2. **Objective**\
    To design a system using DHT-11 sensor to measure temperature and humidity, and transmit the data to the cloud using the ThingSpeak API for real-time monitoring and analysis.

3. **Brief Theory**
    Explain briefly about:
    - DHT-11 sensor: Introduction, working principle (how it measures temperature and humidity).
    - ThingSpeak: Introduction to IoT platform, overview of how it allows for data collection, visualization, and analysis.

4. **Interfacing Block Diagram and manual calculations if any**\
    [Check google drive](https://docs.google.com/document/d/1D97Liga_OOW8KZ5nlopOlRLf_dcudGkybWw8oHjvqGo/edit?usp=drive_link)

5. **Algorithm**
    1. Imports and Initialization:
        - Import necessary libraries (adafruit_dht, board, RPi.GPIO, requests, datetime, time).
        - Import ThingSpeak configuration (THINGSPEAK_API_KEY, THINGSPEAK_URL) from thingspeak_config.

    2. Function `get_readings()`:
        - Initializes DHT11 sensor (adafruit_dht.DHT11 on board.D4).
        - Reads temperature (temperature_c) and humidity.
        - Converts temperature to Fahrenheit (temperature_f) if valid.
        - Returns readings or error message.

    3. Function `send_to_thingspeak(temperature_c, temperature_f, humidity)`:
        - Sends sensor data (temperature_c, temperature_f, humidity) to ThingSpeak.
        - Includes timestamp and API key in the HTTP POST request.
        - Prints success or failure messages based on response status.

    4. Function `main()`:
        - Loops 20 times to collect and send sensor data to ThingSpeak.
        - Uses `get_readings()` to fetch data and `send_to_thingspeak()` to transmit it.
        - Includes a 5-second delay between iterations.

    5. Execution (`if __name__ == '__main__'`):
        - Executes `main()` function to start data collection and transmission.

6. **Code**
    ```py
    import adafruit_dht
    import board
    from RPi import GPIO
    import requests
    import datetime
    import time
    import thingspeak_config as config

    # thingspeak constants
    THINGSPEAK_API_KEY = config.THINGSPEAK_API_KEY # Replace with your API key
    THINGSPEAK_URL = config.THINGSPEAK_URL_SEND # URL to send data to ThingSpeak

    def get_readings():
        try:
            # Initialize the DHT device inside the route function
            dht_device = adafruit_dht.DHT11(board.D4)
            temperature_c = dht_device.temperature
            humidity = dht_device.humidity
            
            # Check if readings are valid
            if temperature_c is not None and humidity is not None:
                temperature_f = int(temperature_c * (9 / 5) + 32)
                return {
                    'temperature_c': temperature_c,
                    'temperature_f': temperature_f,
                    'humidity': humidity
                }
            else:
                return {'error': 'Failed to retrieve data from sensor'}
        except RuntimeError as error:
            # Catch runtime errors from the sensor
            return {'error': str(error)}
        finally:
            # Cleanup the sensor after use
            dht_device.exit()

    def send_to_thingspeak(temperature_c, temperature_f, humidity):
        current_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

        # sending the data
        response = requests.post(THINGSPEAK_URL, {
            'api_key': THINGSPEAK_API_KEY,
            'field1': current_time,
            'field2': temperature_c,
            'field3': temperature_f,
            'field4': humidity
        })

        if response.status_code != 200:
            print(f'Failed to send data to ThingSpeak: {response.text}')
        if response.status_code == 200:
            print(f'Successfully sent data to ThingSpeak: {response.text}')

    def main():
        for i in range(20):
            readings_json = get_readings()
            send_to_thingspeak(readings_json['temperature_c'], readings_json['temperature_f'], readings_json['humidity'])
            time.sleep(5)

    if __name__ == '__main__':
        main()
    ```

7. **Output (Printout)**\
[Check google drive](https://docs.google.com/document/d/1D97Liga_OOW8KZ5nlopOlRLf_dcudGkybWw8oHjvqGo/edit?usp=drive_link)

8. **Conclusion**\
Utilizing ThingSpeak API for data retrieval enhances IoT applications by providing real-time access to stored sensor data. This capability enables timely decision-making and monitoring of environmental conditions, contributing to efficient IoT deployments.

9. **Course learning outcome**\
This project aligns with the learning outcomes of understanding and implementing IoT data management solutions. By utilizing ThingSpeak API, skills such as API integration, data retrieval, and real-time monitoring are developed, essential for modern IoT applications.


10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW10
1. **Title**\
    Using ThingSpeak API to check and receive the latest data stored in the cloud

2. **Objective**\
    To demonstrate how to use the ThingSpeak API to retrieve the latest data entries from a specific channel stored in the ThingSpeak cloud platform.

3. **Brief Theory**\
    ThingSpeak API for Data Retrieval

    ThingSpeak provides an API that allows seamless integration with IoT applications for retrieving stored data. Here’s an elaboration:

    - **RESTful API**: ThingSpeak’s API follows REST principles, which means it uses standard HTTP methods (GET, POST, etc.) for data retrieval. This makes it accessible and easy to integrate into various applications.

    - **Endpoints**: Key endpoints include:
        - **Latest Entry**: Retrieves the most recent data entry from a specified channel.
        - **Channel Feeds**: Retrieves a set number of entries (feeds) from a channel, useful for historical data analysis.
        - **Field Feeds**: Allows retrieval of specific fields within a channel entry, facilitating selective data extraction.

    - **Authentication**: 
        - **API Keys**: Authentication is managed through API keys, which are included in API requests to ensure secure access to channel data.

    - **Integration with Applications**: 
        - ThingSpeak API enables integration with external applications and services for data visualization, analysis, and automation.
        - Integration with platforms like MATLAB allows for advanced data processing and visualization capabilities.

4. **Interfacing Block Diagram and manual calculations if any**\
[Check google drive](https://docs.google.com/document/d/1Tikv8IEDM_zyRpGpCfBeiaJ0PzFTozHYdQDZxUP9tTo/edit?usp=drive_link)

5. **Algorithm**
    1. Imports and Initialization:
        - Import necessary libraries (`requests`).
        - Import ThingSpeak configuration (`THINGSPEAK_READ_API_KEY`, `THINGSPEAK_CHANNEL_ID`, `THINGSPEAK_URL`) from `thingspeak_config`.

    2. Function `read_from_thingspeak()`:
        - Sends a GET request to ThingSpeak (`THINGSPEAK_URL`) with parameters:
            - `api_key`: Read API key (`THINGSPEAK_READ_API_KEY`).
            - `results`: Number of results to retrieve (1 in this case).
        - Checks if the request is successful (status code 200).
        - Parses the JSON response and retrieves the latest feed (`feeds[0]`).
        - Prints the latest feed information:
            - Timestamp (`created_at`).
            - Temperature in Celsius (`field2`).
            - Temperature in Fahrenheit (`field3`).
            - Humidity (`field4`).
        - Handles cases where no data is available or if there's an error.

    3. Function `main()`:
        - Calls `read_from_thingspeak()` to fetch and display the latest data from ThingSpeak.

    4. Execution (`if __name__ == '__main__':`):
        - Executes `main()` function when the script is run directly.


6. **Code**
    ```py
    import requests
    import thingspeak_config as config

    # ThingSpeak read API constants
    THINGSPEAK_READ_API_KEY = config.THINGSPEAK_READ_API_KEY # Replace with your read API key
    THINGSPEAK_CHANNEL_ID = config.THINGSPEAK_CHANNEL_ID  # Replace with your channel ID
    THINGSPEAK_URL = config.THINGSPEAK_URL_RECV # URL to read data from ThingSpeak

    def read_from_thingspeak():
        try:
            # Send GET request to ThingSpeak
            response = requests.get(THINGSPEAK_URL, params={'api_key': THINGSPEAK_READ_API_KEY, 'results': 1})
            
            # Check if request was successful
            if response.status_code == 200:
                data = response.json()
                feeds = data['feeds']
                if feeds:
                    latest_feed = feeds[0]
                    print('Latest Feed:')
                    print(f"Datetime: {latest_feed['created_at']}")
                    print(f"Temperature (C): {latest_feed['field2']}")
                    print(f"Temperature (F): {latest_feed['field3']}")
                    print(f"Humidity: {latest_feed['field4']}")
                else:
                    print('No data available')
            else:
                print(f'Failed to read data from ThingSpeak: {response.text}')
        except Exception as e:
            print(f'Error: {e}')

    def main():
        read_from_thingspeak()

    if __name__ == '__main__':
        main()
    ```

7. **Output (Printout)**\
[Check google drive](https://docs.google.com/document/d/1Tikv8IEDM_zyRpGpCfBeiaJ0PzFTozHYdQDZxUP9tTo/edit?usp=drive_link)

8. **Conclusion**\
Utilizing ThingSpeak API for data retrieval enhances IoT applications by providing real-time access to stored sensor data. This capability enables timely decision-making and monitoring of environmental conditions, contributing to efficient IoT deployments.

9. **Course learning outcome**\
This project aligns with the learning outcomes of understanding and implementing IoT data management solutions. By utilizing ThingSpeak API, skills such as API integration, data retrieval, and real-time monitoring are developed, essential for modern IoT applications.

10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019