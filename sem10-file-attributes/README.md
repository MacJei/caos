```python
# initialize magics, look at previous notebooks for not compressed version
exec('get_ipython().run_cell_magic(\'javascript\', \'\', \'// setup cpp code highlighting\\nIPython.CodeCell.options_default.highlight_modes["text/x-c++src"] = {\\\'reg\\\':[/^%%cpp/]} ;\')\n\n# creating magics\nfrom IPython.core.magic import register_cell_magic, register_line_magic\nfrom IPython.display import display, Markdown\n\n@register_cell_magic\ndef save_file(fname, cell):\n    cell = cell if cell[-1] == \'\\n\' else cell + "\\n"\n    cmds = []\n    with open(fname, "w") as f:\n        for line in cell.split("\\n"):\n            if line.startswith("%"):\n                run_prefix = "%run "\n                assert line.startswith(run_prefix)\n                cmds.append(line[len(run_prefix):].strip())\n            else:\n                f.write(line + "\\n")\n    for cmd in cmds:\n        display(Markdown("Run: `%s`" % cmd))\n        get_ipython().system(cmd)\n\n@register_cell_magic\ndef cpp(fname, cell):\n    save_file(fname, cell)\n\n@register_cell_magic\ndef asm(fname, cell):\n    save_file(fname, cell)\n    \n@register_cell_magic\ndef makefile(fname, cell):\n    assert not fname\n    save_file("makefile", cell.replace(" " * 4, "\\t"))\n        \n@register_line_magic\ndef p(line):\n    try:\n        expr, comment = line.split(" #")\n        display(Markdown("`{} = {}`  # {}".format(expr.strip(), eval(expr), comment.strip())))\n    except:\n        display(Markdown("{} = {}".format(line, eval(line))))\n')
```


    <IPython.core.display.Javascript object>


# \xd0\x90\xd1\x82\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2

\xd0\xa1\xd0\xb8\xd0\xb3\xd0\xbd\xd0\xb0\xd1\x82\xd1\x83\xd1\x80\xd1\x8b \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb9, \xd1\x81 \xd0\xbf\xd0\xbe\xd0\xbc\xd0\xbe\xd1\x89\xd1\x8c\xd1\x8e \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd1\x85 \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xbf\xd0\xbe\xd0\xbb\xd1\x83\xd1\x87\xd0\xb8\xd1\x82\xd1\x8c \xd0\xb0\xd1\x82\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int stat(const char *pathname, struct stat *buf);
int fstat(int fd, struct stat *buf);
int lstat(const char *pathname, struct stat *buf);

#include <fcntl.h>           /* Definition of AT_* constants */
#include <sys/stat.h>

int fstatat(int dirfd, const char *pathname, struct stat *buf,
		   int flags);
```


\xd0\x9e\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x81\xd1\x82\xd1\x80\xd1\x83\xd0\xba\xd1\x82\xd1\x83\xd1\x80\xd1\x8b \xd0\xb8\xd0\xb7 `man 2 stat`:

```c
struct stat {
   dev_t     st_dev;         /* ID of device containing file */
   ino_t     st_ino;         /* inode number */
   mode_t    st_mode;        /* protection */
   nlink_t   st_nlink;       /* number of hard links */
   uid_t     st_uid;         /* user ID of owner */
   gid_t     st_gid;         /* group ID of owner */
   dev_t     st_rdev;        /* device ID (if special file) */
   off_t     st_size;        /* total size, in bytes */
   blksize_t st_blksize;     /* blocksize for filesystem I/O */
   blkcnt_t  st_blocks;      /* number of 512B blocks allocated */

   /* Since Linux 2.6, the kernel supports nanosecond
      precision for the following timestamp fields.
      For the details before Linux 2.6, see NOTES. */

   struct timespec st_atim;  /* time of last access */
   struct timespec st_mtim;  /* time of last modification */
   struct timespec st_ctim;  /* time of last status change */

#define st_atime st_atim.tv_sec      /* Backward compatibility */
#define st_mtime st_mtim.tv_sec
#define st_ctime st_ctim.tv_sec
};
```

\xd0\x9e\xd1\x81\xd0\xbe\xd0\xb1\xd1\x8b\xd0\xb9 \xd0\xb8\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd0\xb5\xd1\x81 \xd0\xb1\xd1\x83\xd0\xb4\xd0\xb5\xd1\x82 \xd0\xbf\xd1\x80\xd0\xb5\xd0\xb4\xd1\x81\xd1\x82\xd0\xb0\xd0\xb2\xd0\xbb\xd1\x8f\xd1\x82\xd1\x8c \xd0\xbf\xd0\xbe\xd0\xbb\xd0\xb5 `.st_mode`

\xd0\x91\xd0\xb8\xd1\x82\xd1\x8b \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd1\x83\xd1\x8e\xd1\x89\xd0\xb8\xd0\xb5 \xd0\xbc\xd0\xb0\xd1\x81\xd0\xba\xd0\xb0\xd0\xbc:
* `0170000` - \xd1\x82\xd0\xb8\xd0\xbf \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0.

  \xd0\xad\xd1\x82\xd0\xb8 \xd0\xb1\xd0\xb8\xd1\x82\xd1\x8b \xd1\x81\xd1\x82\xd0\xbe\xd0\xb8\xd1\x82 \xd1\x80\xd0\xb0\xd1\x81\xd1\x81\xd0\xbc\xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xba\xd0\xb0\xd0\xba \xd0\xbe\xd0\xb4\xd0\xbd\xd0\xbe \xd1\x87\xd0\xb8\xd1\x81\xd0\xbb\xd0\xbe, \xd0\xbf\xd0\xbe \xd0\xb7\xd0\xbd\xd0\xb0\xd1\x87\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8e \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xbe\xd0\xbf\xd1\x80\xd0\xb5\xd0\xb4\xd0\xb5\xd0\xbb\xd0\xb8\xd1\x82\xd1\x8c \xd1\x82\xd0\xb8\xd0\xbf \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0. \xd0\xa1\xd1\x80\xd0\xb0\xd0\xb2\xd0\xbd\xd0\xb8\xd0\xb2\xd0\xb0\xd1\x8f \xd1\x8d\xd1\x82\xd0\xbe \xd1\x87\xd0\xb8\xd1\x81\xd0\xbb\xd0\xbe \xd1\x81:  
    * `S_IFSOCK   0140000   socket`
    * `S_IFLNK    0120000   symbolic link`
    * `S_IFREG    0100000   regular file`
    * `S_IFBLK    0060000   block device`
    * `S_IFDIR    0040000   directory`
    * `S_IFCHR    0020000   character device`
    * `S_IFIFO    0010000   FIFO`
* `0777` - \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2\xd0\xb0 \xd0\xbd\xd0\xb0 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb.

  \xd0\xad\xd1\x82\xd0\xb8 \xd0\xb1\xd0\xb8\xd1\x82\xd1\x8b \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd1\x80\xd0\xb0\xd1\x81\xd1\x81\xd0\xbc\xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xba\xd0\xb0\xd0\xba \xd0\xbd\xd0\xb5\xd0\xb7\xd0\xb0\xd0\xb2\xd0\xb8\xd1\x81\xd0\xb8\xd0\xbc\xd1\x8b\xd0\xb5 \xd0\xb1\xd0\xb8\xd1\x82\xd1\x8b, \xd0\xba\xd0\xb0\xd0\xb4\xd0\xb6\xd1\x8b\xd0\xb9 \xd0\xb8\xd0\xb7 \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd1\x85 \xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x87\xd0\xb0\xd0\xb5\xd1\x82 \xd0\xb7\xd0\xb0 \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2\xd0\xbe (\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd0\xb5\xd0\xbb\xd1\x8f, \xd0\xb5\xd0\xb3\xd0\xbe \xd0\xb3\xd1\x80\xd1\x83\xd0\xbf\xd0\xbf\xd1\x8b, \xd0\xb2\xd1\x81\xd0\xb5\xd1\x85 \xd0\xbe\xd1\x81\xd1\x82\xd0\xb0\xd0\xbb\xd1\x8c\xd0\xbd\xd1\x8b\xd1\x85) (\xd1\x87\xd0\xb8\xd1\x82\xd0\xb0\xd1\x82\xd1\x8c/\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd1\x82\xd1\x8c/\xd0\xb2\xd1\x8b\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd1\x8f\xd1\x82\xd1\x8c) \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb.

**fstat** - \xd1\x81\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd0\xbe\xd0\xbc\xd1\x83 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd1\x83


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir
%run ./stat.exe < tmp/a
%run ./stat.exe < tmp/dir
%run ./stat.exe < tmp/a_link

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{   
    struct stat s;
    fstat(0, &s); // get stat for stdin
    printf("is regular: %s\n", ((s.st_mode & S_IFMT) == S_IFREG) ? "yes" : "no"); // can use predefined mask
    printf("is directory: %s\n", S_ISDIR(s.st_mode) ? "yes" : "no"); // or predefined macro
    printf("is symbolic link: %s\n", S_ISLNK(s.st_mode) ? "yes" : "no"); 
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir`



Run: `./stat.exe < tmp/a`


    is regular: yes
    is directory: no
    is symbolic link: no



Run: `./stat.exe < tmp/dir`


    is regular: no
    is directory: yes
    is symbolic link: no



Run: `./stat.exe < tmp/a_link`


    is regular: yes
    is directory: no
    is symbolic link: no


\xd0\x9e\xd0\xb1\xd1\x80\xd0\xb0\xd1\x82\xd0\xb8\xd1\x82\xd0\xb5 \xd0\xb2\xd0\xbd\xd0\xb8\xd0\xbc\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5, \xd1\x87\xd1\x82\xd0\xbe \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8 \xd1\x80\xd0\xb5\xd0\xb7\xd1\x83\xd0\xbb\xd1\x8c\xd1\x82\xd0\xb0\xd1\x82 \xd0\xbf\xd0\xbe\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd0\xbd \xd0\xba\xd0\xb0\xd0\xba \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x80\xd0\xb5\xd0\xb3\xd1\x83\xd0\xbb\xd1\x8f\xd1\x80\xd0\xbd\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0, \xd0\xbd\xd0\xb0 \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd0\xb9 \xd0\xbe\xd0\xbd\xd0\xb0 \xd1\x81\xd1\x81\xd1\x8b\xd0\xbb\xd0\xb0\xd0\xb5\xd1\x82\xd1\x81\xd1\x8f.
\xd0\xa2\xd1\x83\xd1\x82, \xd0\xb2\xd0\xb5\xd1\x80\xd0\xbe\xd1\x8f\xd1\x82\xd0\xbd\xd0\xbe, \xd0\xb7\xd0\xb0\xd0\xbc\xd0\xb5\xd1\x88\xd0\xb0\xd0\xbd bash, \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd0\xb9 \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd1\x82 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb \xd0\xbd\xd0\xb0 \xd0\xbc\xd0\xb5\xd1\x81\xd1\x82\xd0\xb5 stdin \xd0\xb4\xd0\xbb\xd1\x8f \xd0\xbd\xd0\xb0\xd1\x88\xd0\xb5\xd0\xb9 \xd0\xbf\xd1\x80\xd0\xbe\xd0\xb3\xd1\x80\xd0\xb0\xd0\xbc\xd0\xbc\xd1\x8b. \xd0\x92\xd0\xb8\xd0\xb4\xd0\xbd\xd0\xbe, \xd1\x87\xd1\x82\xd0\xbe \xd0\xbe\xd0\xbd \xd0\xbf\xd1\x80\xd0\xbe\xd1\x85\xd0\xbe\xd0\xb4\xd0\xb8\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc.

**stat** - \xd1\x81\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8 \xd0\xbf\xd0\xbe \xd0\xb8\xd0\xbc\xd0\xb5\xd0\xbd\xd0\xb8 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0, \xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd1\x83\xd0\xb5\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir
%run ./stat.exe tmp/a
%run ./stat.exe tmp/dir
%run ./stat.exe tmp/a_link

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{   
    assert(argc == 2);
    struct stat s;
    stat(argv[1], &s); // \xd0\xa1\xd0\xbb\xd0\xb5\xd0\xb4\xd1\x83\xd0\xb5\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc
    printf("is regular: %s\n", ((s.st_mode & S_IFMT) == S_IFREG) ? "yes" : "no"); 
    printf("is directory: %s\n", S_ISDIR(s.st_mode) ? "yes" : "no");
    printf("is symbolic link: %s\n", S_ISLNK(s.st_mode) ? "yes" : "no");
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir`



Run: `./stat.exe tmp/a`


    is regular: yes
    is directory: no
    is symbolic link: no



Run: `./stat.exe tmp/dir`


    is regular: no
    is directory: yes
    is symbolic link: no



Run: `./stat.exe tmp/a_link`


    is regular: yes
    is directory: no
    is symbolic link: no


\xd0\x9e\xd0\xb1\xd1\x80\xd0\xb0\xd1\x82\xd0\xb8\xd1\x82\xd0\xb5 \xd0\xb2\xd0\xbd\xd0\xb8\xd0\xbc\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5, \xd1\x87\xd1\x82\xd0\xbe \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8 \xd1\x80\xd0\xb5\xd0\xb7\xd1\x83\xd0\xbb\xd1\x8c\xd1\x82\xd0\xb0\xd1\x82 \xd0\xbf\xd0\xbe\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd0\xbd \xd0\xba\xd0\xb0\xd0\xba \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x80\xd0\xb5\xd0\xb3\xd1\x83\xd0\xbb\xd1\x8f\xd1\x80\xd0\xbd\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0, \xd0\xbd\xd0\xb0 \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd0\xb9 \xd0\xbe\xd0\xbd\xd0\xb0 \xd1\x81\xd1\x81\xd1\x8b\xd0\xbb\xd0\xb0\xd0\xb5\xd1\x82\xd1\x81\xd1\x8f.

**lstat** - \xd1\x81\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8\xd1\x82 \xd0\xbf\xd0\xbe \xd0\xb8\xd0\xbc\xd0\xb5\xd0\xbd\xd0\xb8 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0, \xd0\xbd\xd0\xb5 \xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd1\x83\xd0\xb5\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc.


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir
%run ./stat.exe tmp/a
%run ./stat.exe tmp/dir
%run ./stat.exe tmp/a_link

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{   
    assert(argc == 2);
    struct stat s;
    lstat(argv[1], &s); // \xd0\x9d\xd0\xb5 \xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd1\x83\xd0\xb5\xd1\x82 \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc, \xd1\x82\xd0\xbe \xd0\xb5\xd1\x81\xd1\x82\xd1\x8c \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd1\x83\xd0\xb7\xd0\xbd\xd0\xb0\xd1\x82\xd1\x8c stat \xd1\x81\xd0\xb0\xd0\xbc\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8
    printf("is regular: %s\n", ((s.st_mode & S_IFMT) == S_IFREG) ? "yes" : "no"); 
    printf("is directory: %s\n", S_ISDIR(s.st_mode) ? "yes" : "no");
    printf("is symbolic link: %s\n", S_ISLNK(s.st_mode) ? "yes" : "no");
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir`



Run: `./stat.exe tmp/a`


    is regular: yes
    is directory: no
    is symbolic link: no



Run: `./stat.exe tmp/dir`


    is regular: no
    is directory: yes
    is symbolic link: no



Run: `./stat.exe tmp/a_link`


    is regular: no
    is directory: no
    is symbolic link: yes


\xd0\xa1\xd0\xb5\xd0\xb9\xd1\x87\xd0\xb0\xd1\x81 \xd1\x80\xd0\xb5\xd0\xb7\xd1\x83\xd0\xbb\xd1\x8c\xd1\x82\xd0\xb0\xd1\x82 \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8 \xd0\xbf\xd0\xbe\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd0\xbd \xd0\xba\xd0\xb0\xd0\xba \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xb0\xd0\xbc\xd0\xbe\xd0\xb9 \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8. \xd0\xa2\xd0\xb0\xd0\xba \xd0\xba\xd0\xb0\xd0\xba \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd1\x83\xd0\xb5\xd0\xbc \xd1\x81\xd0\xbf\xd0\xb5\xd1\x86\xd0\xb8\xd0\xb0\xd0\xbb\xd1\x8c\xd0\xbd\xd1\x83\xd1\x8e \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd1\x8e.

**open(...O_NOFOLLOW | O_PATH) + fstat** - \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb \xd1\x82\xd0\xb0\xd0\xba, \xd1\x87\xd1\x82\xd0\xbe\xd0\xb1\xd1\x8b \xd0\xbd\xd0\xb5 \xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc \xd0\xb8 \xd0\xb4\xd0\xb0\xd0\xbb\xd0\xb5\xd0\xb5 \xd1\x81\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8\xd0\xbc \xd0\xb5\xd0\xb3\xd0\xbe stat
\xd0\x9a\xd1\x81\xd1\x82\xd0\xb0\xd1\x82\xd0\xb8, \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd0\xbd\xd0\xb5 \xd0\xbe\xd1\x87\xd0\xb5\xd0\xbd\xd1\x8c \xd1\x87\xd0\xb5\xd1\x81\xd1\x82\xd0\xbd\xd0\xbe. \xd0\xa1 \xd0\xbe\xd0\xbf\xd1\x86\xd0\xb8\xd0\xb5\xd0\xb9 O_PATH \xd0\xbd\xd0\xb5\xd0\xbb\xd1\x8c\xd0\xb7\xd1\x8f \xd0\xbf\xd0\xbe\xd1\x82\xd0\xbe\xd0\xbc \xd0\xbf\xd1\x80\xd0\xb8\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x8f\xd1\x82\xd1\x8c read, write \xd0\xb8 \xd0\xb5\xd1\x89\xd0\xb5 \xd0\xbd\xd0\xb5\xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd0\xb5 \xd0\xbe\xd0\xbf\xd0\xb5\xd1\x80\xd0\xb0\xd1\x86\xd0\xb8\xd0\xb8.


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir
%run ./stat.exe tmp/a
%run ./stat.exe tmp/dir
%run ./stat.exe tmp/a_link

#define _GNU_SOURCE // need for O_PATH

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{   
    assert(argc == 2);
    struct stat s;
    int fd = open(argv[1], O_RDONLY | O_NOFOLLOW | O_PATH);
    assert(fd >= 0);
    fstat(fd, &s); 
    printf("is regular: %s\n", ((s.st_mode & S_IFMT) == S_IFREG) ? "yes" : "no"); 
    printf("is directory: %s\n", S_ISDIR(s.st_mode) ? "yes" : "no");
    printf("is symbolic link: %s\n", S_ISLNK(s.st_mode) ? "yes" : "no");
    close(fd);
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp && touch tmp/a && ln -s ./a tmp/a_link && mkdir tmp/dir`



Run: `./stat.exe tmp/a`


    is regular: yes
    is directory: no
    is symbolic link: no



Run: `./stat.exe tmp/dir`


    is regular: no
    is directory: yes
    is symbolic link: no



Run: `./stat.exe tmp/a_link`


    is regular: no
    is directory: no
    is symbolic link: yes


\xd0\x97\xd0\xb4\xd0\xb5\xd1\x81\xd1\x8c \xd1\x82\xd0\xbe\xd0\xb6\xd0\xb5 \xd1\x80\xd0\xb5\xd0\xb7\xd1\x83\xd0\xbb\xd1\x8c\xd1\x82\xd0\xb0\xd1\x82 \xd0\xbf\xd0\xbe\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd0\xbd \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xb0\xd0\xbc\xd0\xbe\xd0\xb9 \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb8, \xd0\xbf\xd0\xbe\xd1\x81\xd0\xba\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xba\xd1\x83 \xd0\xb2\xd1\x8b\xd0\xb7\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc open \xd1\x81\xd0\xbe \xd1\x81\xd0\xbf\xd0\xb5\xd1\x86\xd0\xb8\xd0\xb0\xd0\xbb\xd1\x8c\xd0\xbd\xd1\x8b\xd0\xbc\xd0\xb8 \xd0\xbe\xd0\xbf\xd1\x86\xd0\xb8\xd1\x8f\xd0\xbc\xd0\xb8, \xd1\x87\xd1\x82\xd0\xbe\xd0\xb1\xd1\x8b \xd0\xbd\xd0\xb5 \xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbf\xd0\xbe \xd1\x81\xd0\xb8\xd0\xbc\xd0\xbb\xd0\xb8\xd0\xbd\xd0\xba\xd0\xb0\xd0\xbc.

**\xd0\x9f\xd0\xbe\xd1\x8d\xd1\x82\xd0\xbe\xd0\xbc\xd1\x83 \xd0\xb2\xd0\xb0\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xbf\xd0\xbe\xd0\xbd\xd0\xb8\xd0\xbc\xd0\xb0\xd1\x82\xd1\x8c, \xd0\xba\xd0\xb0\xd0\xba\xd0\xbe\xd0\xb5 \xd0\xbf\xd0\xbe\xd0\xb2\xd0\xb5\xd0\xb4\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd0\xb2\xd1\x8b \xd1\x85\xd0\xbe\xd1\x82\xd0\xb8\xd1\x82\xd0\xb5 \xd0\xb8 \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c stat, fstat \xd0\xb8\xd0\xbb\xd0\xb8 lstat**

## \xd0\x98\xd0\xb7\xd0\xb2\xd0\xbb\xd0\xb5\xd1\x87\xd0\xb5\xd0\xbc \xd0\xb2\xd1\x80\xd0\xb5\xd0\xbc\xd1\x8f \xd0\xb4\xd0\xbe\xd1\x81\xd1\x82\xd1\x83\xd0\xbf\xd0\xb0 \xd0\xb8\xd0\xb7 \xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd0\xbe\xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe

%run rm -rf tmp && mkdir tmp 
%run touch tmp/a && sleep 2 
%run ln -s ./a tmp/a_link && sleep 2 
%run mkdir tmp/dir

%run ./stat.exe < tmp/a
%run ./stat.exe < tmp/dir 
%run ./stat.exe < tmp/a_link


#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>
#include <time.h>

int main(int argc, char *argv[])
{   
    struct stat s;
    fstat(0, &s); 
    
    printf("update time: %s\n", asctime(gmtime(&s.st_mtim.tv_sec)));
    printf("access time: %s\n", asctime(gmtime(&s.st_atim.tv_sec)));

    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp`



Run: `touch tmp/a && sleep 2`



Run: `ln -s ./a tmp/a_link && sleep 2`



Run: `mkdir tmp/dir`



Run: `./stat.exe < tmp/a`


    update time: Wed Nov  6 08:06:22 2019
    
    access time: Wed Nov  6 08:06:22 2019
    



Run: `./stat.exe < tmp/dir`


    update time: Wed Nov  6 08:06:26 2019
    
    access time: Wed Nov  6 08:06:26 2019
    



Run: `./stat.exe < tmp/a_link`


    update time: Wed Nov  6 08:06:22 2019
    
    access time: Wed Nov  6 08:06:22 2019
    


## example from man 2 stat


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe

%run rm -rf tmp && mkdir tmp 
%run touch tmp/a
%run ln -s ./a tmp/a_link
%run mkdir tmp/dir

%run ./stat.exe tmp/a
%run ./stat.exe tmp/dir 
%run ./stat.exe tmp/a_link

#include <sys/types.h>
#include <sys/stat.h>
#include <time.h>
#include <stdio.h>
#include <stdlib.h>

int
main(int argc, char *argv[])
{
   struct stat sb;

   if (argc != 2) {
       fprintf(stderr, "Usage: %s <pathname>\n", argv[0]);
       exit(EXIT_FAILURE);
   }

   if (stat(argv[1], &sb) == -1) {
       perror("stat");
       exit(EXIT_FAILURE);
   }

   printf("File type:                ");

   switch (sb.st_mode & S_IFMT) {
   case S_IFBLK:  printf("block device\n");            break;
   case S_IFCHR:  printf("character device\n");        break;
   case S_IFDIR:  printf("directory\n");               break;
   case S_IFIFO:  printf("FIFO/pipe\n");               break;
   case S_IFLNK:  printf("symlink\n");                 break;
   case S_IFREG:  printf("regular file\n");            break;
   case S_IFSOCK: printf("socket\n");                  break;
   default:       printf("unknown?\n");                break;
   }

   printf("I-node number:            %ld\n", (long) sb.st_ino);

   printf("Mode:                     %lo (octal)\n",
           (unsigned long) sb.st_mode);

   printf("Link count:               %ld\n", (long) sb.st_nlink);
   printf("Ownership:                UID=%ld   GID=%ld\n",
           (long) sb.st_uid, (long) sb.st_gid);

   printf("Preferred I/O block size: %ld bytes\n",
           (long) sb.st_blksize);
   printf("File size:                %lld bytes\n",
           (long long) sb.st_size);
   printf("Blocks allocated:         %lld\n",
           (long long) sb.st_blocks);

   printf("Last status change:       %s", ctime(&sb.st_ctime));
   printf("Last file access:         %s", ctime(&sb.st_atime));
   printf("Last file modification:   %s", ctime(&sb.st_mtime));

   exit(EXIT_SUCCESS);
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp && mkdir tmp`



Run: `touch tmp/a`



Run: `ln -s ./a tmp/a_link`



Run: `mkdir tmp/dir`



Run: `./stat.exe tmp/a`


    File type:                regular file
    I-node number:            1344257
    Mode:                     100664 (octal)
    Link count:               1
    Ownership:                UID=1000   GID=1000
    Preferred I/O block size: 4096 bytes
    File size:                0 bytes
    Blocks allocated:         0
    Last status change:       Wed Nov  6 11:06:57 2019
    Last file access:         Wed Nov  6 11:06:57 2019
    Last file modification:   Wed Nov  6 11:06:57 2019



Run: `./stat.exe tmp/dir`


    File type:                directory
    I-node number:            1344259
    Mode:                     40775 (octal)
    Link count:               2
    Ownership:                UID=1000   GID=1000
    Preferred I/O block size: 4096 bytes
    File size:                4096 bytes
    Blocks allocated:         8
    Last status change:       Wed Nov  6 11:06:57 2019
    Last file access:         Wed Nov  6 11:06:57 2019
    Last file modification:   Wed Nov  6 11:06:57 2019



Run: `./stat.exe tmp/a_link`


    File type:                regular file
    I-node number:            1344257
    Mode:                     100664 (octal)
    Link count:               1
    Ownership:                UID=1000   GID=1000
    Preferred I/O block size: 4096 bytes
    File size:                0 bytes
    Blocks allocated:         0
    Last status change:       Wed Nov  6 11:06:57 2019
    Last file access:         Wed Nov  6 11:06:57 2019
    Last file modification:   Wed Nov  6 11:06:57 2019


# get user string name


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run mkdir tmp2
%run touch tmp2/a # && sudo touch tmp2/b # create this file with sudo
%run ./stat.exe < tmp2/a  # created by me
%run ./stat.exe < tmp2/b  # created by root (with sudo)

#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <pwd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{
    struct stat s;
    fstat(0, &s);
    struct passwd *pw = getpwuid(s.st_uid);
    assert(pw);
    printf("%s\n", pw->pw_name);
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `mkdir tmp2`


    mkdir: cannot create directory \xe2\x80\x98tmp2\xe2\x80\x99: File exists



Run: `touch tmp2/a # && sudo touch tmp2/b # create this file with sudo`



Run: `./stat.exe < tmp2/a  # created by me`


    pechatnov
    42



Run: `./stat.exe < tmp2/b  # created by root (with sudo)`


    root
    42


# \xd0\x9f\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb5\xd1\x80\xd0\xba\xd0\xb0 \xd1\x81\xd0\xb2\xd0\xbe\xd0\xb8\xd1\x85 \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2


```python
%%cpp stat.c
%run gcc stat.c -o stat.exe
%run rm -rf tmp2 && mkdir tmp2
%run touch tmp2/a 
%run touch tmp2/b && chmod +x tmp2/b 
%run ./stat.exe tmp2/a  # usual
%run ./stat.exe tmp2/b  # executable

#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{
    assert(argc >= 1);
    struct stat s;
    printf("Can execute: %s\n", (access(argv[1], X_OK) == 0) ? "yes" : "no");
    return 0;
}
```


Run: `gcc stat.c -o stat.exe`



Run: `rm -rf tmp2 && mkdir tmp2`



Run: `touch tmp2/a`



Run: `touch tmp2/b && chmod +x tmp2/b`



Run: `./stat.exe tmp2/a  # usual`


    Can execute: no



Run: `./stat.exe tmp2/b  # executable`


    Can execute: yes



```python

```