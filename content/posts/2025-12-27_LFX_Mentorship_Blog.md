+++
title = "LFX Linux Kernel Mentorship"
date = "2025-12-27"

[taxonomies]
tags = ["Linux", "LFX"]
+++

I have been a Linux user for quite a long time now and have always been curious about how the internals work. My first exposure to Linux was during my diploma in Mechanical Engineering, when I was exploring alternatives to paid software such as Windows and AutoCAD. That was when I came across the world of FOSS (Free and Open Source Software), with Linux leading the way. Ever since then, I have tried to contribute to open-source projects as much as my ability allows.

# Getting Accepted

I remember one day coming across a post on LinkedIn about the Linux Kernel Mentorship program by The Linux Foundation. I was very fascinated by the program and took the logical step of putting in the work to learn more about it.

The program had prerequisite tasks required to qualify as an applicant. These tasks included essential exercises that a mentee would go through during the course of the program, such as building the kernel from source, writing kernel modules, decoding stack traces, and creating patches starting with simple documentation changes. Each task taught me a lot and helped me realize how much I didn’t know about software development, it was truly a humbling experience.

# Initial Stage

I remember it was midnight while I was working on a project when I received an email from Shuah Khan, who would soon become my mentor for the program, informing me that I had been selected. I was overjoyed, but there was also a sense of fear, as I had very little exposure to kernel internals and it was my first time getting hands-on experience with the Linux Kernel.

At the early stage, although I had experience with some low-level projects, the Linux Kernel seemed far beyond my ability. Its internals were very complex for someone like me, who only had experience as an end-user. I vividly remember Shuah in our onboarding meeting saying something along the lines (paraphrased): *“Do you find the kernel overwhelming? Good! It is supposed to be overwhelming; this is where learning happens.”* This statement encouraged me to push myself and put in more effort.

In the early stages, I used to find navigating the code base difficult, but with time and experience in certain subsystems, I became more familiar with the kernel. I consider myself fortunate to have mentors who are so mature and experienced in their respective fields, such as Shuah Khan, David Hunter, and Khalid Aziz. During the mentorship, they taught me many new things that I might not have learned otherwise, including using QEMU for cross-platform compiling and testing modules on different system architectures. I vividly remember Shuah’s tutorials and still maintain my notes from her talks regarding techniques for better debugging of the kernel code base. David Hunter was also immensely helpful, gracefully correcting many of my mistakes in the patches I submitted as a beginner.

# Getting Patches Accepted

Initially, as a newcomer to Linux Kernel development, I struggled to find valid issues. Many problems I encountered seemed too complex to attempt, and I spent a lot of time trying to solve issues I did not fully understand. This led to some lost time, which was critical since the mentorship program is only three months long, and I was expected to have at least five patches accepted into the upstream source tree.

I started off using static analysis tools such as Smatch, Sparse, and Clang, but I encountered some false positives and eventually stopped relying on them. By then, I had already spent around two months searching for issues. Although I found some good problems, they involved major changes, and due to time constraints, I refrained from working on them.

Eventually, I created a patch series containing three patches for the ``hangcheck-timer`` driver module, using the checkpatch.pl script to identify minor code-style issues. These included:

* Fixing an incorrect format specifier (`%Ld` → `%lld`)
* Updating the internal API for consistent debugging of warning logs (``printk(KERN_CRIT ...)`` → ``pr_crit(...)``)
* Minor code spacing adjustments

Initially, my patches had some issues pointed out by Greg Kroah-Hartman, the mentor for the Character Device Driver subsystem. Thankfully, he was quick in giving feedback, and I submitted a v2 of the patch, which was later accepted.

After these patches, I worked on the `dummy_hcd` module, part of the USB subsystem. I created a patch series for it, but it was rejected by Greg Kroah-Hartman, which made sense, as I wasn’t aware enough to know that my changes could potentially break systems. Greg was very gracious about it, and David (my mentor) guided me through the mistakes. With help from David and Alan Stern, I was able to overcome the rejection.

One of the graduation criteria for the program was that the five accepted patches should not be simple spacing or spelling corrections. I needed three more substantive patches. After careful search and debugging, I found issues in the kselftest of certain subsystems: filesystems, ublk, and coredump. The patches were:

* **Filesystem/anon_inode**: Replaced a NULL pointer passed as a function parameter with an empty array containing a NULL pointer
* **ublk/kublk**: Updated `_Static_assert` to use C11 syntax instead of C23 syntax
* **Coredump**: Replaced dereferencing a NULL pointer with `__builtin_trap()` to intentionally crash the program safely, as the compiler might otherwise optimize away the crash <br> <br>

#### NOTE: Make sure to test the patches well before you send, regardless of how minor the change may be!! 

# Conclusion

I am very grateful for the opportunity to interact with experienced mentors such as Greg Kroah-Hartman and Alan Stern. Their guidance and critical feedback helped me navigate the development process confidently. I am thankful to have learned how the Linux Kernel, one of the world’s largest and fastest-moving open-source projects, operates at scale and the crucial role of trust, the high-quality standards expected by maintainers, and the rigor of the development process.

Overall, i can say with confidence that this mentorship experience was one of the best learning experience thus far i had in my life considering the amount of learning and complexity i came across. I would want to thank Shuah Khan, David Hunter, Khalid Aziz and The Linux Foundation for taking their time in making the Mentorship a reality. Hope to cross paths again.
