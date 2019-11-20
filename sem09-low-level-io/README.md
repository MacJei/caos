```python
get_ipython().run_cell_magic('javascript', '', '// setup cpp code highlighting\nIPython.CodeCell.options_default.highlight_modes["text/x-c++src"] = {\'reg\':[/^%%cpp/]} ;')

# creating magics
from IPython.core.magic import register_cell_magic, register_line_magic
from IPython.display import display, Markdown

@register_cell_magic
def save_file(fname, cell):
    cell = cell if cell[-1] == '\n' else cell + "\n"
    cmds = []
    with open(fname, "w") as f:
        for line in cell.split("\n"):
            if line.startswith("%"):
                run_prefix = "%run "
                assert line.startswith(run_prefix)
                cmds.append(line[len(run_prefix):].strip())
            else:
                f.write(line + "\n")
    for cmd in cmds:
        display(Markdown("Run: `%s`" % cmd))
        get_ipython().system(cmd)

@register_cell_magic
def cpp(fname, cell):
    save_file(fname, cell)

@register_cell_magic
def asm(fname, cell):
    save_file(fname, cell)
    
@register_cell_magic
def makefile(fname, cell):
    assert not fname
    save_file("makefile", cell.replace(" " * 4, "\t"))
        
@register_line_magic
def p(line):
    try:
        expr, comment = line.split(" #")
        display(Markdown("`{} = {}`  # {}".format(expr.strip(), eval(expr), comment.strip())))
    except:
        display(Markdown("{} = {}".format(line, eval(line))))
    
```


    <IPython.core.display.Javascript object>



```python
%p 1 + 1 # 1
```


`1 + 1 = 2`  # 1


# \xd0\x9d\xd0\xb8\xd0\xb7\xd0\xba\xd0\xbe\xd1\x83\xd1\x80\xd0\xbe\xd0\xb2\xd0\xbd\xd0\xb5\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb2\xd0\xb2\xd0\xbe\xd0\xb4-\xd0\xb2\xd1\x8b\xd0\xb2\xd0\xbe\xd0\xb4

## Linux

\xd0\x97\xd0\xb4\xd0\xb5\xd1\x81\xd1\x8c \xd0\xbf\xd0\xbe\xd0\xbb\xd0\xb5\xd0\xb7\xd0\xbd\xd0\xbe \xd1\x80\xd0\xb0\xd1\x81\xd1\x81\xd0\xbc\xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbf\xd1\x80\xd0\xbe\xd1\x86\xd0\xb5\xd1\x81\xd1\x81 \xd0\xba\xd0\xb0\xd0\xba \xd0\xbe\xd0\xb1\xd1\x8a\xd0\xb5\xd0\xba\xd1\x82 \xd0\xb2 \xd0\xbe\xd0\xbf\xd0\xb5\xd1\x80\xd0\xb0\xd1\x86\xd0\xb8\xd0\xbe\xd0\xbd\xd0\xbd\xd0\xbe\xd0\xb9 \xd1\x81\xd0\xb8\xd1\x81\xd1\x82\xd0\xb5\xd0\xbc\xd0\xb5. \xd0\x9f\xd0\xbe\xd0\xbc\xd0\xb8\xd0\xbc\xd0\xbe \xd0\xbe\xd1\x81\xd0\xbd\xd0\xbe\xd0\xb2\xd0\xbd\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd0\xb5\xd0\xbb\xd1\x8c\xd1\x81\xd0\xba\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xbf\xd0\xbe\xd1\x82\xd0\xbe\xd0\xba\xd0\xb0 \xd0\xb2\xd1\x8b\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8f \xd1\x83 \xd0\xbf\xd1\x80\xd0\xbe\xd1\x86\xd0\xb5\xd1\x81\xd1\x81\xd0\xb0-\xd0\xbe\xd0\xb1\xd1\x8a\xd0\xb5\xd0\xba\xd1\x82\xd0\xb0 \xd0\xb5\xd1\x81\xd1\x82\xd1\x8c \xd0\xbc\xd0\xbd\xd0\xbe\xd0\xb6\xd0\xb5\xd1\x81\xd1\x82\xd0\xb2\xd0\xbe \xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd0\xbe\xd0\xb2.

\xd0\xa1\xd0\xbe\xd0\xb2\xd0\xb5\xd1\x82\xd1\x83\xd1\x8e \xd0\xbf\xd1\x80\xd0\xbe\xd1\x87\xd0\xb8\xd1\x82\xd0\xb0\xd1\x82\xd1\x8c [\xd1\x81\xd1\x82\xd0\xb0\xd1\x82\xd1\x8c\xd1\x8e \xd0\xbd\xd0\xb0 \xd1\x85\xd0\xb0\xd0\xb1\xd1\x80\xd0\xb5](https://habr.com/ru/post/423049/#definition), \xd0\xb2\xd1\x80\xd0\xbe\xd0\xb4\xd0\xb5 \xd1\x82\xd0\xb0\xd0\xbc \xd0\xb2\xd1\x81\xd0\xb5 \xd0\xbe\xd1\x87\xd0\xb5\xd0\xbd\xd1\x8c \xd0\xbd\xd0\xb5\xd0\xbf\xd0\xbb\xd0\xbe\xd1\x85\xd0\xbe \xd0\xbd\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd0\xbe.

\xd0\xa1\xd0\xb5\xd0\xb3\xd0\xbe\xd0\xb4\xd0\xbd\xd1\x8f \xd0\xbd\xd0\xb0\xd1\x81 \xd0\xb1\xd1\x83\xd0\xb4\xd1\x83\xd1\x82 \xd0\xb8\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd0\xb5\xd1\x81\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb5 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b. \xd0\x9a\xd0\xb0\xd0\xb6\xd0\xb4\xd0\xbe\xd0\xbc\xd1\x83 \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd0\xbe\xd0\xbc\xd1\x83 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd1\x83 \xd0\xb8 \xd1\x81\xd0\xbe\xd0\xb5\xd0\xb4\xd0\xb8\xd0\xbd\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8e \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd1\x83\xd0\xb5\xd1\x82 \xd1\x87\xd0\xb8\xd1\x81\xd0\xbb\xd0\xbe (int). \xd0\xad\xd1\x82\xd0\xbe \xd1\x87\xd0\xb8\xd1\x81\xd0\xbb\xd0\xbe \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd1\x83\xd0\xb5\xd1\x82\xd1\x81\xd1\x8f \xd0\xba\xd0\xb0\xd0\xba \xd0\xb8\xd0\xb4\xd0\xb5\xd0\xbd\xd1\x82\xd0\xb8\xd1\x84\xd0\xb8\xd0\xba\xd0\xb0\xd1\x82\xd0\xbe\xd1\x80 \xd0\xb2 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd1\x8f\xd1\x85, \xd1\x80\xd0\xb0\xd0\xb1\xd0\xbe\xd1\x82\xd0\xb0\xd1\x8e\xd1\x89\xd0\xb8\xd1\x85 \xd1\x81 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0\xd0\xbc\xd0\xb8/\xd1\x81\xd0\xbe\xd0\xb5\xd0\xb4\xd0\xb8\xd0\xbd\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8f\xd0\xbc\xd0\xb8.


* 0 - stdin - \xd1\x81\xd1\x82\xd0\xb0\xd0\xbd\xd0\xb4\xd0\xb0\xd1\x80\xd1\x82\xd0\xbd\xd1\x8b\xd0\xb9 \xd0\xbf\xd0\xbe\xd1\x82\xd0\xbe\xd0\xba \xd0\xb2\xd0\xb2\xd0\xbe\xd0\xb4\xd0\xb0
* 1 - stdout - \xd1\x81\xd1\x82\xd0\xb0\xd0\xbd\xd0\xb4\xd0\xb0\xd1\x80\xd1\x82\xd0\xbd\xd1\x8b\xd0\xb9 \xd0\xbf\xd0\xbe\xd1\x82\xd0\xbe\xd0\xba \xd0\xb2\xd1\x8b\xd0\xb2\xd0\xbe\xd0\xb4\xd0\xb0
* 2 - stderr - \xd1\x81\xd1\x82\xd0\xb0\xd0\xbd\xd0\xb4\xd0\xb0\xd1\x80\xd1\x82\xd0\xbd\xd1\x8b\xd0\xb9 \xd0\xbf\xd0\xbe\xd1\x82\xd0\xbe\xd0\xba \xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xbe\xd0\xba

\xd0\x9f\xd1\x80\xd0\xb8\xd0\xbc\xd0\xb5\xd1\x80\xd1\x8b \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x8f \xd0\xb2 bash:

* `grep String < file.txt` <-> `grep String 0< file.txt`
* `mkdir a_dir 2> /dev/null`
* `./some_program < in.txt 1> out.txt` <-> `./some_program < in.txt > out.txt` 




```python
%%cpp linux_example.c
%run gcc linux_example.c -o linux_example.exe
%run echo "Hello students!" > linux_example_input_001.txt
%run ./linux_example.exe linux_example_input_001.txt

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
    // printf("Linux by printf"); // where it will be printed?
    char linux_str[] = "Linux by write\n";
    write(1, linux_str, sizeof(linux_str)); // 1 - \xd0\xb8\xd0\xb7\xd0\xbd\xd0\xb0\xd1\x87\xd0\xb0\xd0\xbb\xd1\x8c\xd0\xbd\xd0\xbe \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd1\x8b\xd0\xb9 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80 \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd1\x83\xd1\x8e\xd1\x89\xd0\xb8\xd0\xb9 stdout
                                            // linux_str - \xd1\x83\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd1\x82\xd0\xb5\xd0\xbb\xd1\x8c \xd0\xbd\xd0\xb0 \xd0\xbd\xd0\xb0\xd1\x87\xd0\xb0\xd0\xbb\xd0\xbe \xd0\xb4\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd1\x85, 
                                            // sizeof(linux_str) - \xd1\x80\xd0\xb0\xd0\xb7\xd0\xbc\xd0\xb5\xd1\x80 \xd0\xb4\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd1\x85, \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b\xd0\xb5 \xd1\x85\xd0\xbe\xd1\x82\xd0\xb8\xd0\xbc \xd0\xb7\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd1\x82\xd1\x8c
                                            // \xd0\x92\xd0\x90\xd0\x96\xd0\x9d\xd0\x9e, \xd1\x87\xd1\x82\xd0\xbe write \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xb5\xd1\x82 \xd0\xb7\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbd\xd0\xb5 \xd0\xb2\xd1\x81\xd0\xb5 \xd0\xb4\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd0\xb5 
                                            //        \xd0\xb8 \xd1\x82\xd0\xbe\xd0\xb3\xd0\xb4\xd0\xb0 \xd0\xb5\xd0\xb3\xd0\xbe \xd0\xbd\xd0\xb0\xd0\xb4\xd0\xbe \xd0\xbf\xd0\xb5\xd1\x80\xd0\xb5\xd0\xb7\xd0\xb0\xd0\xbf\xd1\x83\xd1\x81\xd1\x82\xd0\xb8\xd1\x82\xd1\x8c
                                            //        \xd0\xbd\xd0\xbe \xd0\xb2 \xd0\xb4\xd0\xb0\xd0\xbd\xd0\xbd\xd0\xbe\xd0\xbc \xd0\xbf\xd1\x80\xd0\xb8\xd0\xbc\xd0\xb5\xd1\x80\xd0\xb5 \xd1\x8d\xd1\x82\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xbd\xd0\xb5\xd1\x82
                                            // \xd0\x9f\xd0\xbe\xd0\xb4\xd1\x80\xd0\xbe\xd0\xb1\xd0\xbd\xd0\xb5\xd0\xb5 \xd0\xb2 `man 2 write`
    if (argc < 2) {
        printf("Need at least 2 arguments\n");
        return 1;
    }
    int fd = open(argv[1], O_RDONLY); // \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb \xd0\xb8 \xd0\xbf\xd0\xbe\xd0\xbb\xd1\x83\xd1\x87\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x81\xd0\xb2\xd1\x8f\xd0\xb7\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd0\xb9 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80
                                      // O_RDONLY - \xd1\x84\xd0\xbb\xd0\xb0\xd0\xb3 \xd0\xbe \xd1\x82\xd0\xbe\xd0\xbc, \xd1\x87\xd1\x82\xd0\xbe \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd0\xb2 read-only \xd1\x80\xd0\xb5\xd0\xb6\xd0\xb8\xd0\xbc\xd0\xb5
                                      // \xd0\xbf\xd0\xbe\xd0\xb4\xd1\x80\xd0\xbe\xd0\xb1\xd0\xbd\xd0\xb5\xd0\xb5 \xd0\xb2 `man 2 open`
    if (fd < 0) {
        perror("Can't open file"); // \xd0\x92\xd1\x8b\xd0\xb2\xd0\xbe\xd0\xb4\xd0\xb8\xd1\x82 \xd1\x83\xd0\xba\xd0\xb0\xd0\xb7\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x83\xd1\x8e \xd1\x81\xd1\x82\xd1\x80\xd0\xbe\xd0\xba\xd1\x83 \xd0\xb2 stderr 
                                   // + \xd0\xb4\xd0\xbe\xd0\xb1\xd0\xb0\xd0\xb2\xd0\xbb\xd1\x8f\xd0\xb5\xd1\x82 \xd1\x81\xd0\xbe\xd0\xbe\xd0\xb1\xd1\x89\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd0\xb8 \xd0\xbf\xd0\xbe\xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd0\xbd\xd0\xb5\xd0\xb9 \xd0\xbf\xd1\x80\xd0\xbe\xd0\xb8\xd0\xb7\xd0\xbe\xd1\x88\xd0\xb5\xd0\xb4\xd1\x88\xd0\xb5\xd0\xb9 \xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xba\xd0\xb5 
                                   // \xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xba\xd0\xb0 \xd1\x85\xd1\x80\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x82\xd1\x81\xd1\x8f \xd0\xb2 errno
        return -1;
    }
    
    char buffer[4096];
    int bytes_read = read(fd, buffer, sizeof(buffer)); // fd - \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80 \xd0\xb2\xd1\x8b\xd1\x88\xd0\xb5 \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0
                                                       // 2 \xd0\xb8 3 \xd0\xb0\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd1\x8b \xd0\xba\xd0\xb0\xd0\xba \xd0\xb2\xd0\xbe write
                                                       // \xd0\xa2\xd0\xb0\xd0\xba \xd0\xb6\xd0\xb5 \xd0\xba\xd0\xb0\xd0\xba \xd0\xb8 write \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xb5\xd1\x82 \xd0\xbf\xd1\x80\xd0\xbe\xd1\x87\xd0\xb8\xd1\x82\xd0\xb0\xd1\x82\xd1\x8c \xd0\x9c\xd0\x95\xd0\x9d\xd0\xac\xd0\xa8\xd0\x95
                                                       //   \xd1\x87\xd0\xb5\xd0\xbc \xd0\xb7\xd0\xb0\xd0\xbf\xd1\x80\xd0\xbe\xd1\x88\xd0\xb5\xd0\xbd\xd0\xbe \xd0\xb2 3\xd0\xbc \xd0\xb0\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd0\xb5
                                                       //   \xd1\x8d\xd1\x82\xd0\xbe \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xb5\xd1\x82 \xd0\xb1\xd1\x8b\xd1\x82\xd1\x8c \xd1\x81\xd0\xb2\xd1\x8f\xd0\xb7\xd0\xb0\xd0\xbd\xd0\xbe \xd0\xba\xd0\xb0\xd0\xba \xd1\x81 \xd0\xba\xd0\xbe\xd0\xbd\xd1\x86\xd0\xbe\xd0\xbc \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0
                                                       //   \xd1\x82\xd0\xb0\xd0\xba \xd0\xb8 \xd1\x81 \xd0\xba\xd0\xb0\xd0\xba\xd0\xb8\xd0\xbc-\xd1\x82\xd0\xbe \xd0\xb1\xd0\xbe\xd0\xbb\xd0\xb5\xd0\xb5 \xd0\xbf\xd1\x80\xd0\xb8\xd0\xbe\xd1\x80\xd0\xb8\xd1\x82\xd0\xb5\xd1\x82\xd0\xbd\xd1\x8b\xd0\xbc \xd1\x81\xd0\xbe\xd0\xb1\xd1\x8b\xd1\x82\xd0\xb8\xd0\xb5\xd0\xbc
    if (bytes_read < 0) {
        perror("Error reading file");
        close(fd); // \xd0\xb7\xd0\xb0\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb \xd1\x81\xd0\xb2\xd1\x8f\xd0\xb7\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd0\xb9 \xd1\x81 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xbc \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd0\xbe\xd0\xbc. \xd0\x9d\xd1\x83 \xd0\xb8\xd0\xbb\xd0\xb8 \xd0\xbd\xd0\xb5 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb. 
                   // \xd0\xa1\xd1\x82\xd0\xb0\xd0\xbd\xd0\xb4\xd0\xb0\xd1\x80\xd1\x82\xd0\xbd\xd1\x8b\xd0\xb5 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b 0, 1, 2 \xd1\x82\xd0\xbe\xd0\xb6\xd0\xb5 \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd1\x82\xd0\xb0\xd0\xba \xd0\xb7\xd0\xb0\xd0\xba\xd1\x80\xd1\x8b\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c
        return -1;
    }
    char buffer2[4096];
    // \xd1\x84\xd0\xbe\xd1\x80\xd0\xbc\xd0\xb8\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x81\xd1\x82\xd1\x80\xd0\xbe\xd0\xba\xd0\xb8 \xd1\x81 \xd1\x82\xd0\xb5\xd0\xba\xd1\x81\xd1\x82\xd0\xbe\xd0\xbc
    int written_bytes = snprintf(buffer2, sizeof(buffer2), "Bytes read: %d\n'''%s'''\n", bytes_read, buffer);
    write(1, buffer2, written_bytes);
    close(fd);
    return 0;
}
```


Run: `gcc linux_example.c -o linux_example.exe`



Run: `echo "Hello students!" > linux_example_input_001.txt`



Run: `./linux_example.exe linux_example_input_001.txt`


    Linux by write
    Bytes read: 16
    '''Hello students!
    '''
    123

### \xd0\xad\xd0\xba\xd0\xb7\xd0\xbe\xd1\x82\xd0\xb8\xd1\x87\xd0\xb5\xd1\x81\xd0\xba\xd0\xb8\xd0\xb9 \xd0\xbf\xd1\x80\xd0\xb8\xd0\xbc\xd0\xb5\xd1\x80-\xd0\xb8\xd0\xb3\xd1\x80\xd1\x83\xd1\x88\xd0\xba\xd0\xb0


```python
%%cpp strange_example.c
%run gcc strange_example.c -o strange_example.exe
%run echo "Hello world!" > a.txt
%run ./strange_example.exe 5< a.txt > strange_example.out
%run cat strange_example.out

#include <unistd.h>
#include <stdio.h>

int main(int argc, char *argv[])
{ 
    char buffer[4096];
    int bytes_read = read(5, buffer, sizeof(buffer)); 
    if (bytes_read < 0) {
        perror("Error reading file");
        return -1;
    }
    int written_bytes = write(1, buffer, bytes_read);
    if (written_bytes < 0) {
        perror("Error writing file");
        return -1;
    }
    return 0;
}
```


Run: `gcc strange_example.c -o strange_example.exe`



Run: `echo "Hello world!" > a.txt`



Run: `./strange_example.exe 5< a.txt > strange_example.out`



Run: `cat strange_example.out`


    Hello world!


### Retry of read


```python
%%cpp retry_example.c
%run gcc retry_example.c -o retry_example.exe
%run echo "Hello world!" > a.txt
%run ./retry_example.exe < a.txt 

#include <unistd.h>
#include <stdio.h>
#include <errno.h>


int read_retry(int fd, char* data, int size) {
    char* cdata = data;
    while (1) {
        int read_bytes = read(fd, cdata, size);
        if (read_bytes == 0) {
            return cdata - data;
        }
        if (read_bytes < 0) {
            if (errno == EAGAIN || errno == EINTR) {
                continue;
            } else {
                return -1;
            }
        }
        cdata += read_bytes;
        size -= read_bytes;
        if (size == 0) {
            return cdata - data;
        }
    }
}


int main(int argc, char *argv[])
{ 
    char buffer[4096];
    int bytes_read = read_retry(0, buffer, sizeof(buffer)); 
    if (bytes_read < 0) {
        perror("Error reading file");
        return -1;
    }
    int written_bytes = write(1, buffer, bytes_read);
    if (written_bytes < 0) {
        perror("Error writing file");
        return -1;
    }
    return 0;
}
```


Run: `gcc retry_example.c -o retry_example.exe`



Run: `echo "Hello world!" > a.txt`



Run: `./retry_example.exe < a.txt`


    Hello world!



```python

```


```python

```

\xd0\x9f\xd1\x80\xd0\xb8 \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd0\xb8\xd0\xb8 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 \xd1\x81 \xd1\x84\xd0\xbb\xd0\xb0\xd0\xb3\xd0\xbe\xd0\xbc \xd1\x81\xd0\xbe\xd0\xb7\xd0\xb4\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x8f (O_WRONLY | O_CREAT) \xd0\xb2\xd0\xb0\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xb0\xd0\xb4\xd0\xb5\xd0\xba\xd0\xb2\xd0\xb0\xd1\x82\xd0\xbd\xd0\xbe \xd0\xbf\xd1\x80\xd0\xbe\xd1\x81\xd1\x82\xd0\xb0\xd0\xb2\xd0\xbb\xd1\x8f\xd1\x82\xd1\x8c \xd0\xbc\xd0\xb0\xd1\x81\xd0\xba\xd1\x83 \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2 \xd0\xb4\xd0\xbe\xd1\x81\xd1\x82\xd1\x83\xd0\xbf\xd0\xb0. \xd0\x94\xd0\xb0\xd0\xb2\xd0\xb0\xd0\xb9\xd1\x82\xd0\xb5 \xd1\x81 \xd0\xbd\xd0\xb5\xd0\xb9 \xd1\x80\xd0\xb0\xd0\xb7\xd0\xb1\xd0\xb5\xd1\x80\xd0\xb5\xd0\xbc\xd1\x81\xd1\x8f.

\xd0\x97\xd0\xb0\xd0\xbc\xd0\xb5\xd1\x82\xd0\xba\xd0\xb0 \xd0\xbe \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2\xd0\xbe\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb8: **Attribute, \xd0\xbd\xd0\xbe \xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82**


```python
!echo "Hello jupyter!" > a.txt  # \xd1\x81\xd0\xbe\xd0\xb7\xd0\xb4\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb8\xd0\xba \xd1\x81 \xd0\xbe\xd0\xb1\xd1\x8b\xd1\x87\xd0\xbd\xd1\x8b\xd0\xbc\xd0\xb8 "\xd0\xbd\xd0\xb0\xd1\x81\xd1\x82\xd1\x80\xd0\xbe\xd0\xb9\xd0\xba\xd0\xb0\xd0\xbc\xd0\xb8"
!mkdir b_dir 2> /dev/null

import os  # \xd0\x92 \xd0\xbc\xd0\xbe\xd0\xb4\xd1\x83\xd0\xbb\xd0\xb5 os \xd0\xb5\xd1\x81\xd1\x82\xd1\x8c \xd0\xbf\xd0\xbe\xd1\x87\xd1\x82\xd0\xb8 \xd0\xb2 \xd1\x87\xd0\xb8\xd1\x81\xd1\x82\xd0\xbe\xd0\xbc \xd0\xb2\xd0\xb8\xd0\xb4\xd0\xb5 \xd0\xbf\xd0\xbe\xd1\x87\xd1\x82\xd0\xb8 \xd0\xb2\xd1\x81\xd0\xb5 \xd1\x81\xd0\xb8\xd1\x81\xd1\x82\xd0\xb5\xd0\xbc\xd0\xbd\xd1\x8b\xd0\xb5 \xd0\xb2\xd1\x8b\xd0\xb7\xd0\xbe\xd0\xb2\xd1\x8b: write, read, open...
from IPython.display import display

%p os.stat("a.txt") # \xd0\x90\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 `a.txt`
%p oct(os.stat("a.txt").st_mode)  # \xd0\x98\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd0\xb5\xd1\x81\xd0\xbd\xd1\x8b \xd0\xbf\xd0\xbe\xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x82\xd1\x80\xd0\xb8 \xd0\xb2\xd0\xbe\xd1\x81\xd1\x8c\xd0\xbc\xd0\xb5\xd1\x80\xd0\xb8\xd1\x87\xd0\xbd\xd1\x8b\xd0\xb5 \xd1\x86\xd0\xb8\xd1\x84\xd1\x80\xd1\x8b. 664 - \xd1\x8d\xd1\x82\xd0\xbe \xd0\xbe\xd0\xb1\xd1\x8b\xd1\x87\xd0\xbd\xd1\x8b\xd0\xb5 \xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2

%p oct(os.stat("./linux_example.exe").st_mode)  # \xd0\x90\xd1\x82\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2 \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd1\x8f\xd0\xb5\xd0\xbc\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0

%p oct(os.stat("b_dir").st_mode)  # \xd0\x97\xd0\xb0\xd0\xb1\xd0\xb0\xd0\xb2\xd0\xbd\xd1\x8b\xd0\xb9 \xd1\x84\xd0\xb0\xd0\xba\xd1\x82, \xd0\xbd\xd0\xbe \xd0\xb2\xd1\x81\xd0\xb5 \xd0\xbc\xd0\xbe\xd0\xb3\xd1\x83\xd1\x82 "\xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd1\x8f\xd1\x82\xd1\x8c \xd0\xb4\xd0\xb8\xd1\x80\xd0\xb5\xd0\xba\xd1\x82\xd0\xbe\xd1\x80\xd0\xb8\xd1\x8e". [\xd0\x91\xd0\xbe\xd0\xbb\xd0\xb5\xd0\xb5 \xd0\xbf\xd0\xbe\xd0\xb4\xd1\x80\xd0\xbe\xd0\xb1\xd0\xbd\xd0\xbe \xd0\xbd\xd0\xb0 stackoverflow](https://unix.stackexchange.com/questions/21251/execute-vs-read-bit-how-do-directory-permissions-in-linux-work)

```


`os.stat("a.txt") = os.stat_result(st_mode=33204, st_ino=1344254, st_dev=2049, st_nlink=1, st_uid=1000, st_gid=1000, st_size=15, st_atime=1572422090, st_mtime=1573021499, st_ctime=1573021499)`  # \xd0\x90\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 `a.txt`



`oct(os.stat("a.txt").st_mode) = 0o100664`  # \xd0\x98\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd0\xb5\xd1\x81\xd0\xbd\xd1\x8b \xd0\xbf\xd0\xbe\xd1\x81\xd0\xbb\xd0\xb5\xd0\xb4\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x82\xd1\x80\xd0\xb8 \xd0\xb2\xd0\xbe\xd1\x81\xd1\x8c\xd0\xbc\xd0\xb5\xd1\x80\xd0\xb8\xd1\x87\xd0\xbd\xd1\x8b\xd0\xb5 \xd1\x86\xd0\xb8\xd1\x84\xd1\x80\xd1\x8b. 664 - \xd1\x8d\xd1\x82\xd0\xbe \xd0\xbe\xd0\xb1\xd1\x8b\xd1\x87\xd0\xbd\xd1\x8b\xd0\xb5 \xd0\xb0\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2



`oct(os.stat("./linux_example.exe").st_mode) = 0o100775`  # \xd0\x90\xd1\x82\xd1\x82\xd1\x80\xd0\xb8\xd0\xb1\xd1\x83\xd1\x82\xd1\x8b \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2 \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd1\x8f\xd0\xb5\xd0\xbc\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0



`oct(os.stat("b_dir").st_mode) = 0o40775`  # \xd0\x97\xd0\xb0\xd0\xb1\xd0\xb0\xd0\xb2\xd0\xbd\xd1\x8b\xd0\xb9 \xd1\x84\xd0\xb0\xd0\xba\xd1\x82, \xd0\xbd\xd0\xbe \xd0\xb2\xd1\x81\xd0\xb5 \xd0\xbc\xd0\xbe\xd0\xb3\xd1\x83\xd1\x82 "\xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd1\x8f\xd1\x82\xd1\x8c \xd0\xb4\xd0\xb8\xd1\x80\xd0\xb5\xd0\xba\xd1\x82\xd0\xbe\xd1\x80\xd0\xb8\xd1\x8e". [\xd0\x91\xd0\xbe\xd0\xbb\xd0\xb5\xd0\xb5 \xd0\xbf\xd0\xbe\xd0\xb4\xd1\x80\xd0\xbe\xd0\xb1\xd0\xbd\xd0\xbe \xd0\xbd\xd0\xb0 stackoverflow](https://unix.stackexchange.com/questions/21251/execute-vs-read-bit-how-do-directory-permissions-in-linux-work)



```python
!ls -la
```

    total 288
    drwxrwxr-x  5 pechatnov pechatnov   4096 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:25 .
    drwxrwxr-x 13 pechatnov pechatnov   4096 \xd0\xbd\xd0\xbe\xd1\x8f  2 23:11 ..
    -rw-rw-r--  1 pechatnov pechatnov     15 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:24 a.txt
    drwxrwxr-x  2 pechatnov pechatnov   4096 \xd0\xbe\xd0\xba\xd1\x82 28 20:45 b
    drwxrwxr-x  2 pechatnov pechatnov   4096 \xd0\xbe\xd0\xba\xd1\x82 28 20:46 b_dir
    -rw-rw-r--  1 pechatnov pechatnov      5 \xd0\xbe\xd0\xba\xd1\x82 30 11:34 b.txt
    drwxrwxr-x  2 pechatnov pechatnov   4096 \xd0\xbe\xd0\xba\xd1\x82 28 21:58 .ipynb_checkpoints
    -rw-rw-r--  1 pechatnov pechatnov   3289 \xd0\xbe\xd0\xba\xd1\x82 30 10:48 linux_example.c
    -rwxrwxr-x  1 pechatnov pechatnov   8976 \xd0\xbe\xd0\xba\xd1\x82 30 10:48 linux_example.exe
    -rw-rw-r--  1 pechatnov pechatnov     16 \xd0\xbe\xd0\xba\xd1\x82 30 10:48 linux_example_input_001.txt
    -rw-rw-r--  1 pechatnov pechatnov    847 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:23 linux_file_hello_world.c
    -rwxrwxr-x  1 pechatnov pechatnov   8888 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:23 linux_file_hello_world.exe
    --w-r-x---  1 pechatnov pechatnov     13 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:23 linux_file_hello_world.out
    -rw-rw-r--  1 pechatnov pechatnov  31575 \xd0\xbd\xd0\xbe\xd1\x8f  6 09:25 low-level-io.ipynb
    -rw-rw-r--  1 pechatnov pechatnov   1317 \xd0\xbe\xd0\xba\xd1\x82 30 11:34 lseek_example.c
    -rwxrwxr-x  1 pechatnov pechatnov   9032 \xd0\xbe\xd0\xba\xd1\x82 30 11:34 lseek_example.exe
    -rw-rw-r--  1 pechatnov pechatnov  17693 \xd0\xbd\xd0\xbe\xd1\x8f  2 23:09 README.md
    -rw-rw-r--  1 pechatnov pechatnov    958 \xd0\xbe\xd0\xba\xd1\x82 30 10:54 retry_example.c
    -rwxrwxr-x  1 pechatnov pechatnov   8872 \xd0\xbe\xd0\xba\xd1\x82 30 10:54 retry_example.exe
    -rw-rw-r--  1 pechatnov pechatnov    407 \xd0\xbe\xd0\xba\xd1\x82 30 10:49 strange_example.c
    -rwxrwxr-x  1 pechatnov pechatnov   8776 \xd0\xbe\xd0\xba\xd1\x82 30 10:49 strange_example.exe
    -rw-rw-r--  1 pechatnov pechatnov     16 \xd0\xbe\xd0\xba\xd1\x82 30 09:21 strange_example.in
    -rw-rw-r--  1 pechatnov pechatnov     13 \xd0\xbe\xd0\xba\xd1\x82 30 10:49 strange_example.out
    -rw-rw-r--  1 pechatnov pechatnov   1458 \xd0\xbe\xd0\xba\xd1\x82 30 10:15 winapi_example.c
    -rwxrwxr-x  1 pechatnov pechatnov 104184 \xd0\xbe\xd0\xba\xd1\x82 30 10:15 winapi_example.exe
    -rw-rw-r--  1 pechatnov pechatnov     16 \xd0\xbe\xd0\xba\xd1\x82 30 10:15 winapi_example_input_001.txt



```python
%%cpp linux_file_hello_world.c
%run gcc linux_file_hello_world.c -o linux_file_hello_world.exe
%run ./linux_file_hello_world.exe
%run cat linux_file_hello_world.out

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main(int argc, char *argv[])
{   
    int fd = open("linux_file_hello_world.out", O_WRONLY | O_CREAT, S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH); 
    // S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH == 0664
    // \xd0\xbf\xd0\xbe\xd0\xbf\xd1\x80\xd0\xbe\xd0\xb1\xd1\x83\xd0\xb9\xd1\x82\xd0\xb5 \xd0\xbd\xd0\xb5 \xd1\x83\xd0\xba\xd0\xb0\xd0\xb7\xd1\x8b\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c 0664   
    // (\xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xba\xd0\xb0 \xd1\x82\xd0\xb0\xd0\xba\xd0\xb0\xd1\x8f \xd0\xb6\xd0\xb5 \xd0\xba\xd0\xb0\xd0\xba \xd0\xb2 printf("%d");)
    // \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x81\xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2\xd0\xba\xd0\xb8 `man 2 open`
     
    if (fd < 0) {
        perror("Can't open file");
        return -1;
    }
    char buffer[] = "Hello world!";
    int bytes_written = write(fd, buffer, sizeof(buffer));
    if (bytes_written < 0) {
        perror("Error writing file");
        close(fd);
        return -1;
    }
    printf("Bytes written: %d (expected %d)\n", bytes_written, (int)sizeof(buffer));
    close(fd);
    return 0;
}
```


Run: `gcc linux_file_hello_world.c -o linux_file_hello_world.exe`



Run: `./linux_file_hello_world.exe`


    Bytes written: 13 (expected 13)



Run: `cat linux_file_hello_world.out`


    Hello world!


```python
!rm -f linux_file_hello_world.out
```


```python
!ls -la linux_file_hello_world.out
```

    -rw-rw-r-- 1 pechatnov pechatnov 13 Oct 30 11:14 linux_file_hello_world.out



```python
oct(os.stat("linux_file_hello_world.out").st_mode)
```




    '0o100775'




```python

```

## lseek - \xd1\x87\xd1\x82\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x81 \xd0\xbf\xd1\x80\xd0\xbe\xd0\xb8\xd0\xb7\xd0\xb2\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xbd\xd0\xbe\xd0\xb9 \xd0\xbf\xd0\xbe\xd0\xb7\xd0\xb8\xd1\x86\xd0\xb8\xd0\xb8 \xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb5

\xd0\xa1\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8\xd1\x82 \xd0\xbd\xd0\xb0 \xd0\xb2\xd1\x82\xd0\xbe\xd1\x80\xd0\xbe\xd0\xb9 \xd1\x81\xd0\xb8\xd0\xbc\xd0\xb2\xd0\xbe\xd0\xbb \xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb5, \xd1\x87\xd0\xb8\xd1\x82\xd0\xb0\xd0\xb5\xd1\x82 \xd0\xb5\xd0\xb3\xd0\xbe, \xd0\xb8\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd0\xbf\xd1\x80\xd0\xb5\xd1\x82\xd0\xb8\xd1\x80\xd1\x83\xd0\xb5\xd1\x82 \xd0\xba\xd0\xb0\xd0\xba \xd1\x86\xd0\xb8\xd1\x84\xd1\x80\xd1\x83 \xd0\xb8 \xd1\x83\xd0\xb2\xd0\xb5\xd0\xbb\xd0\xb8\xd1\x87\xd0\xb8\xd0\xb2\xd0\xb0\xd0\xb5\xd1\x82 \xd1\x8d\xd1\x82\xd1\x83 \xd1\x86\xd0\xb8\xd1\x84\xd1\x80\xd1\x83 \xd0\xbd\xd0\xb0 1.


```python
%%cpp lseek_example.c
%run gcc lseek_example.c -o lseek_example.exe
%run ./lseek_example.exe b.txt
%run cat b.txt

#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <assert.h>

int main(int argc, char *argv[])
{   
    assert(argc >= 2);
    // O_RDWR - \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd0\xb8\xd0\xb5 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 \xd0\xbd\xd0\xb0 \xd1\x87\xd1\x82\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd0\xb8 \xd0\xb7\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd1\x8c \xd0\xbe\xd0\xb4\xd0\xbd\xd0\xbe\xd0\xb2\xd1\x80\xd0\xb5\xd0\xbc\xd0\xb5\xd0\xbd\xd0\xbd\xd0\xbe
    int fd = open(argv[1], O_RDWR | O_CREAT, S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH); 
    
    // \xd0\x9f\xd0\xb5\xd1\x80\xd0\xb5\xd0\xbc\xd0\xb5\xd1\x89\xd0\xb0\xd0\xb5\xd0\xbc\xd1\x81\xd1\x8f \xd0\xbd\xd0\xb0 \xd0\xba\xd0\xbe\xd0\xbd\xd0\xb5\xd1\x86 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0, \xd0\xbf\xd0\xbe\xd0\xbb\xd1\x83\xd1\x87\xd0\xb0\xd0\xb5\xd0\xbc \xd0\xbf\xd0\xbe\xd0\xb7\xd0\xb8\xd1\x86\xd0\xb8\xd1\x8e \xd0\xba\xd0\xbe\xd0\xbd\xd1\x86\xd0\xb0 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 - \xd1\x8d\xd1\x82\xd0\xbe \xd1\x80\xd0\xb0\xd0\xb7\xd0\xbc\xd0\xb5\xd1\x80 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0
    int size = lseek(fd, 0, SEEK_END);
    
    printf("File size: %d\n", size);
    
    // \xd0\xb5\xd1\x81\xd0\xbb\xd0\xb8 \xd1\x80\xd0\xb0\xd0\xb7\xd0\xbc\xd0\xb5\xd1\x80 \xd0\xbc\xd0\xb5\xd0\xbd\xd1\x8c\xd1\x88\xd0\xb5 2, \xd1\x82\xd0\xbe \xd0\xb4\xd0\xbe\xd0\xbf\xd0\xb8\xd1\x81\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x86\xd0\xb8\xd1\x84\xd1\x80\xd1\x8b
    if (size < 2) {
        const char s[] = "10";
        lseek(fd, 0, SEEK_SET);
        write(fd, s, sizeof(s) - 1);
        printf("Written bytes: %d\n", (int)sizeof(s) - 1);    
        size = lseek(fd, 0, SEEK_END);
        printf("File size: %d\n", size);
    }
    
    // \xd1\x87\xd0\xb8\xd1\x82\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x81\xd0\xb8\xd0\xbc\xd0\xb2\xd0\xbe\xd0\xbb \xd1\x81\xd0\xbe 2\xd0\xb9 \xd0\xbf\xd0\xbe\xd0\xb7\xd0\xb8\xd1\x86\xd0\xb8\xd0\xb8
    lseek(fd, 1, SEEK_SET);
    char c;
    read(fd, &c, 1);
    c = (c < '0' || c > '9') ? '0' : ((c - '0') + 1) % 10 + '0';
    
    // \xd0\xb7\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd1\x8b\xd0\xb2\xd0\xb0\xd0\xb5\xd0\xbc \xd1\x81\xd0\xb8\xd0\xbc\xd0\xb2\xd0\xbe\xd0\xbb \xd0\xb2 2\xd1\x8e \xd0\xbf\xd0\xbe\xd0\xb7\xd0\xb8\xd1\x86\xd0\xb8\xd1\x8e
    lseek(fd, 1, SEEK_SET);
    write(fd, &c, 1);
    
    close(fd);
    return 0;
}
```


Run: `gcc lseek_example.c -o lseek_example.exe`



Run: `./lseek_example.exe b.txt`


    File size: 5



Run: `cat b.txt`


    H5llo


```python
!echo -n "Hello" > b.txt
```


```python
!cat b.txt
```

    10

# Windows

* \xd0\x92\xd0\xbc\xd0\xb5\xd1\x81\xd1\x82\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd1\x85 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd0\xbe\xd0\xb2 - HANDLE (\xd0\xb2\xd1\x80\xd0\xbe\xd0\xb4\xd0\xb5 \xd1\x8d\xd1\x82\xd0\xbe \xd0\xbf\xd1\x80\xd0\xbe\xd1\x81\xd1\x82\xd0\xbe void*)
* \xd0\x9c\xd0\xbd\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xb0\xd0\xbb\xd0\xb8\xd0\xb0\xd1\x81\xd0\xbe\xd0\xb2 \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x82\xd0\xb8\xd0\xbf\xd0\xbe\xd0\xb2 \xd0\xb2\xd1\x80\xd0\xbe\xd0\xb4\xd0\xb5 HANDLE, DWORD, BOOL, LPTSTR, LPWSTR
* \xd0\x9e\xd1\x87\xd0\xb5\xd0\xbd\xd1\x8c \xd0\xbc\xd0\xbd\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xb0\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd0\xbe\xd0\xb2 \xd1\x83 \xd0\xb2\xd1\x81\xd0\xb5\xd1\x85 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb9
* \xd0\x9f\xd0\xbb\xd0\xbe\xd1\x85\xd0\xb0\xd1\x8f \xd0\xb4\xd0\xbe\xd0\xba\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd0\xb0\xd1\x86\xd0\xb8\xd1\x8f, \xd0\xb3\xd1\x83\xd0\xb3\xd0\xbb\xd0\xb8\xd1\x82\xd1\x81\xd1\x8f \xd0\xb2\xd1\x81\xd0\xb5 \xd0\xbf\xd0\xbb\xd0\xbe\xd1\x85\xd0\xbe
* \xd0\x9d\xd0\xb0\xd0\xb4\xd0\xbe \xd1\x83\xd1\x81\xd1\x82\xd0\xb0\xd0\xbd\xd0\xbe\xd0\xb2\xd0\xb8\xd1\x82\xd1\x8c `wine` \xd0\xb8 `mingw-w64`


```python
%%cpp winapi_example.c
%run i686-w64-mingw32-gcc winapi_example.c -o winapi_example.exe
%run echo "Hello students!" > winapi_example_input_001.txt
%run wine winapi_example.exe winapi_example_input_001.txt

#include <windows.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
#ifdef WIN32
    printf("Defined WIN32\n");
#else
    printf("Not WIN32\n");
#endif
    if (argc < 2) {
        printf("Need at least 2 arguments\n");
        return 1;
    }
    HANDLE fileHandle = CreateFileA(
        argv[1], GENERIC_READ, FILE_SHARE_READ, NULL,
        OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, NULL);
    if (fileHandle == INVALID_HANDLE_VALUE) {
        char errorBuffer[1024];
        if (!FormatMessage(FORMAT_MESSAGE_FROM_SYSTEM | FORMAT_MESSAGE_IGNORE_INSERTS,
                           NULL, GetLastError(),
                           MAKELANGID(LANG_NEUTRAL, SUBLANG_DEFAULT),
                           errorBuffer, sizeof(errorBuffer), NULL))
        {
            printf("Format message failed with 0x%x\n", GetLastError());
            return -1;
        }
        printf("Can't open file: %s\n", errorBuffer);
        return -1;
    }
    
    char buffer[4096];
    memset(buffer, 0, sizeof(buffer));
    DWORD bytes_read;
    BOOL success;
    success = ReadFile(fileHandle, buffer, sizeof(buffer),
                       &bytes_read, NULL);
    if (!success) {
        perror("Error reading file"); // \xd0\xad\xd1\x82\xd0\xbe \xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xba\xd0\xb0, perror \xd1\x81\xd0\xbc\xd0\xbe\xd1\x82\xd1\x80\xd0\xb8\xd1\x82 \xd0\xb2 errno, \xd0\xb0 \xd0\xbd\xd0\xb5 \xd0\xb2 GetLastError()
        CloseHandle(fileHandle);
        return -1;
    }
    printf("Bytes read: %d\n'''%s'''\n", bytes_read, buffer);
    CloseHandle(fileHandle);
    return 0;
}
```


Run: `i686-w64-mingw32-gcc winapi_example.c -o winapi_example.exe`



Run: `echo "Hello students!" > winapi_example_input_001.txt`



Run: `wine winapi_example.exe winapi_example_input_001.txt`


    [?1h=Defined WIN32
    Bytes read: 16
    '''Hello students!
    '''



```python

```


```python
from IPython.display import HTML, display
display(HTML('<iframe width="560" height="315" src="https://sekundomer.net/onlinetimer/" frameborder="0" allowfullscreen></iframe>'))
```


<iframe width="560" height="315" src="https://sekundomer.net/onlinetimer/" frameborder="0" allowfullscreen></iframe>


## \xd0\x9c\xd0\xb8\xd0\xba\xd1\x80\xd0\xbe\xd1\x82\xd0\xb5\xd1\x81\xd1\x82:
1. \xd0\xb2\xd0\xb0\xd1\x80\xd0\xb8\xd0\xb0\xd0\xbd\xd1\x82
  1. \xd0\x9e\xd0\xbf\xd1\x80\xd0\xb5\xd0\xb4\xd0\xb5\xd0\xbb\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd0\xb0. \xd0\xa1\xd1\x82\xd0\xb0\xd0\xbd\xd0\xb4\xd0\xb0\xd1\x80\xd1\x82\xd0\xbd\xd1\x8b\xd0\xb5 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80\xd1\x8b \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd1\x8b\xd0\xb5 \xd0\xbf\xd1\x80\xd0\xb8 \xd1\x81\xd1\x82\xd0\xb0\xd1\x80\xd1\x82\xd0\xb5 \xd0\xbf\xd1\x80\xd0\xbe\xd0\xb3\xd1\x80\xd0\xb0\xd0\xbc\xd0\xbc\xd1\x8b.
  1. \xd0\x9a\xd0\xb0\xd0\xba\xd0\xb8\xd1\x85 \xd0\xb3\xd0\xb0\xd1\x80\xd0\xb0\xd0\xbd\xd1\x82\xd0\xb8\xd0\xb9 \xd0\xbd\xd0\xb5 \xd0\xb4\xd0\xb0\xd1\x8e\xd1\x82 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8 read \xd0\xb8 write? \xd0\x9a\xd1\x82\xd0\xbe \xd0\xb2\xd0\xb8\xd0\xbd\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82 \xd0\xb8 \xd1\x87\xd1\x82\xd0\xbe \xd1\x81 \xd1\x8d\xd1\x82\xd0\xb8\xd0\xbc \xd0\xbf\xd1\x80\xd0\xb8\xd1\x85\xd0\xbe\xd0\xb4\xd0\xb8\xd1\x82\xd1\x81\xd1\x8f \xd0\xb4\xd0\xb5\xd0\xbb\xd0\xb0\xd1\x82\xd1\x8c?
  1. \xd0\x90\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd1\x8b \xd0\xb8 \xd0\xb2\xd0\xbe\xd0\xb7\xd0\xb2\xd1\x80\xd0\xb0\xd1\x89\xd0\xb0\xd0\xb5\xd0\xbc\xd0\xbe\xd0\xb5 \xd0\xb7\xd0\xbd\xd0\xb0\xd1\x87\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8 lseek
  1. \xd0\xa1 \xd0\xba\xd0\xb0\xd0\xba\xd0\xb8\xd0\xbc\xd0\xb8 \xd0\xbf\xd1\x80\xd0\xb0\xd0\xb2\xd0\xb0\xd0\xbc\xd0\xb8 \xd1\x81\xd1\x82\xd0\xbe\xd0\xb8\xd1\x82 \xd1\x81\xd0\xbe\xd0\xb7\xd0\xb4\xd0\xb0\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbe\xd0\xb1\xd1\x8b\xd1\x87\xd0\xbd\xd1\x8b\xd0\xb9 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb? (3\xd0\xb9 \xd0\xb0\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82 open)
1. \xd0\xb2\xd0\xb0\xd1\x80\xd0\xb8\xd0\xb0\xd0\xbd\xd1\x82
  1. \xd0\x90\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd1\x8b \xd0\xb8 \xd0\xb2\xd0\xbe\xd0\xb7\xd0\xb2\xd1\x80\xd0\xb0\xd1\x89\xd0\xb0\xd0\xb5\xd0\xbc\xd0\xbe\xd0\xb5 \xd0\xb7\xd0\xbd\xd0\xb0\xd1\x87\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8 read. \xd0\x9e\xd0\xb1\xd1\x80\xd0\xb0\xd0\xb1\xd0\xbe\xd1\x82\xd0\xba\xd0\xb0 \xd0\xbe\xd1\x88\xd0\xb8\xd0\xb1\xd0\xbe\xd0\xba \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8
  1. \xd0\xa3 \xd0\xb2\xd0\xb0\xd1\x81 \xd0\xb5\xd1\x81\xd1\x82\xd1\x8c \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80 \xd0\xbe\xd1\x82\xd0\xba\xd1\x80\xd1\x8b\xd1\x82\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0. \xd0\x9a\xd0\xb0\xd0\xba \xd1\x83\xd0\xb7\xd0\xbd\xd0\xb0\xd1\x82\xd1\x8c \xd1\x80\xd0\xb0\xd0\xb7\xd0\xbc\xd0\xb5\xd1\x80 \xd1\x8d\xd1\x82\xd0\xbe\xd0\xb3\xd0\xbe \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0?
  1. \xd0\x90\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd1\x8b \xd0\xb8 \xd0\xb2\xd0\xbe\xd0\xb7\xd0\xb2\xd1\x80\xd0\xb0\xd1\x89\xd0\xb0\xd0\xb5\xd0\xbc\xd0\xbe\xd0\xb5 \xd0\xb7\xd0\xbd\xd0\xb0\xd1\x87\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd0\xb2\xd1\x8b\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0 open. \xd0\x9e\xd1\x81\xd0\xbe\xd0\xb1\xd0\xb5\xd0\xbd\xd0\xbd\xd0\xbe\xd1\x81\xd1\x82\xd1\x8c \xd0\xbf\xd0\xb5\xd1\x80\xd0\xb5\xd0\xb4\xd0\xb0\xd1\x87\xd0\xb8 \xd0\xb0\xd1\x80\xd0\xb3\xd1\x83\xd0\xbc\xd0\xb5\xd0\xbd\xd1\x82\xd0\xbe\xd0\xb2 \xd0\xb2 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd1\x8e
  1. \xd0\x9a\xd0\xb0\xd0\xba \xd0\xb2\xd1\x8b\xd0\xb2\xd0\xb5\xd1\x81\xd1\x82\xd0\xb8 \xd1\x84\xd0\xbe\xd1\x80\xd0\xbc\xd0\xb0\xd1\x82\xd0\xb8\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x83\xd1\x8e \xd1\x81\xd1\x82\xd1\x80\xd0\xbe\xd0\xba\xd1\x83 printf("S=%d, F=%f", 42, 1.23) \xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xbe\xd0\xb2\xd1\x8b\xd0\xb9 \xd0\xb4\xd0\xb5\xd1\x81\xd0\xba\xd1\x80\xd0\xb8\xd0\xbf\xd1\x82\xd0\xbe\xd1\x80?



```python

```