A bunch of kernel tasks/ideas that can be taken by Kernel newbies.

## TODOs from Kernel Source Code:

1. [GPU DRM Subsystem](https://www.kernel.org/doc/html/v4.12/gpu/todo.html)
2. Check the TODO files under drivers/staging directory in the Linux Source code. There are bunch of tasks that can be handled.
3. Grep the kernel source code with 'TODO' and 'FIXME' keyword. These are the issues driver authors/developers may plan to tackle in future. Note that depending upon the subsystem/area the teakss can vary from small to medium level.
So, sometimes it's better to ask about it in the mailing list CC'ing the original developer/author who put the FIXME or TODO line in the file (Use 'git blame' and 'git show' to get the original developer name). :)
4. The following task will give you an understanding how kernel drivers embed a generic data structure in a driver-specific data structure and use the [container_of()](https://elixir.bootlin.com/linux/latest/source/include/linux/kernel.h#L995) macro to cast from the embedded data structure to the outer data structure. This is a very common pattern in the kernel and often referred to as "subclassing": A number of [MMC host drivers](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/drivers/mmc/host) are doing it wrong and fail to use the macro. A [patch](https://patchwork.kernel.org/patch/10794583/) was submitted to the list which fixes the issue for a single driver. The patch claims that two data structures are always adjacent in memory. Verify that by finding out how the data structures are allocated. There are 32 other drivers affected by the same anti-pattern. Your quest is to fix as many of them as you can by following the example of the existing patch. Use `git grep -e '->mmc = ' -- drivers/mmc/host` to identify drivers which need fixing. Be sure to at least compile-test every driver you change. Use a cross-compiler if necessary. Use `git log` as well as [get_maintainer.pl](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/scripts/get_maintainer.pl) to identify people who might be able to test or review your change. Good luck!

## TOOLs

List of bunch of tools used by kernel community. Note that depending upon how actively tool is used and plans from project developers, tasks can vary.

1. [Syzkaller](https://github.com/google/syzkaller)
2. [Coccinelle](https://github.com/coccinelle/coccinelle)
3. [LDV Project](http://linuxtesting.org/ldv)
4. [Sparse](https://kernelnewbies.org/Sparse)

Bunch of other scripts/projects can be found under scripts/ directory in the kernel source code.

## Contributing to ongoing Projects

1. [Kernel Self protection project](https://kernsec.org/wiki/index.php/Kernel_Self_Protection_Project)

Check the wiki and TODO list. If unsure about the tasks from TODO, drop a mail in the mailing list.

2. Documentation project:

Kernel community decided to move from .txt files to using Sphinix for kernel documentation. Check [Jonathan's talk](https://www.youtube.com/watch?v=UHbq1SzmfUE) from 2016 on more details about the project. Lot of work has been done but still there many subsystems which are still using DocBook. Check if the subsystem maintainer is willing to move documenattion from DocBook to Sphinix. (Usually mailing in the mailing list should work]

3. Attribute Documentation:

Outreachy intern Aishwarya Pant worked on attribute documentation during her internship period and developed a tool named ['abi2doc'](https://github.com/aishpant/attribute-documentation). There are still many sysfs attributes which can be documented. Check her [last post](https://aishpant.github.io/blog/outreachy-recap/) on the project.

You can checkout bunch of other ideas by Laura Abbott [here](https://www.labbott.name/blog/2016/08/15/ideas-for-getting-started-in-the-linux-kernel/)
