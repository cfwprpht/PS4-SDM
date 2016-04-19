/* 
 *                          ____   ____   _  _          ____   ____   _  __
 *                         |  _ \ / ___| | || |        / ___| |  _ \ | |/ /
 *                         | |_) |\___ \ | || |_  _____\___ \ | | | || ' / 
 *                         |  __/  ___) ||__   _||_____|___) || |_| || . \ 
 *                         |_|    |____/    |_|        |____/ |____/ |_|\_\
 *                                          5053342D53444B                                       
 *
 *   Contributors: @CTurt, @xerpi, @psxdev, @bigboss-ps3dev, @patrickgill, @masterzorag., @kR105 various anonymous dev's and me, @cfwprpht
 *
 *   Special thx for testing, inspiration, supporting and various other stuff:
 *              @Senaxx, @da_supporterDude, 
 */
 
 
 Initial started by CTurt. This library is a fork and a moddification of CTurt's Open Source PS4 Scene SDK. In case of it didn't full fill my need's
 and in case of to not compromise CTurt's repo i decided to do my own moddification.
 
 We're now not only restricted to user land code execution. The SDK it self will not provide any kernel exploit. But i started and will continue to extend the 
 features and add as much i can.
 
 Why libMemoria ?
 This is in Memoria of all the great guys that needed to left us allready and can't be hear with us any more. It is a Tribut to them to not let the scene die 
 and build something solid, something usefull, something that is from the scene for the scene where every one is wellcome to contribute. Where no one will be judged 
 in case of his colour or the way he speak or the god he belive in. And so if we don't judge on them....who can then some one else judge on free work, done by free 
 peoples, in their free time, with love to that what they do, in love to want to understand which is since yeartousend's the base of us humans and which is 
 held for all the human ever reached. So how can some one judge on a few lines of code and declear them as evil and not to include them, into the SDK ?
 
 This is for:
              Bushing        XX XXX      1979 - XX XXX      2016 (aged 36)  Ben Byer
              ViperMM        XX XXX      1987 - 18 March    2013 (aged 26)  Joshua Lerom Obituary
              graf_chokolo   (although he is still alife, he can't be here with us)
              Barnaby Jack   22 November 1977 - 25 July     2013 (aged 35)  Barnaby Michael Douglas Jack
              Karl Koch      22 July     1965 - 23 May      1989 (aged 23)  Karl Werner Lothar Koch
              Ian Murdock    28 April    1973 - 28 December 2015 (aged 42)  Ian Ashley Murdock
              
 
 [v0.1]
 What is new ?
 Well i started to add several things like a system and a elf header. Variables which we will need sooner or later. More structs, defination's, i sorted the 
 whole thing a bit. Everything that is from libkernel.sprx is back into the kernel.c. I keeped the pthread.c and .h for backwards compatibility of allready 
 written code that is based on Cturt's original scene SDK. I embeded the debungetwork.c from @bigboss ps4link repo and made it match for the PS4-SDK. Also this 
 would be extendet and developers can now either set up a UDP or a TCP network or if they may want a double network which runs a TCP and a UDP line over a own port.
 Then i included Marcan's kernel.c into the SDK and renamed it to kernel2.c for consistence. With that we know allready have some kernel system call's use able
 for our project's in the library. But keep in mind: to be able to use the kernel call'S you need first to be in kernel mem or under kernel rights and second 
 you need to initialize the kernel2 with kernel_init2(); as example. Not only that, we have now also a function call that can install a developers custom system 
 call. Later i will see to also may embed ps4-kexec it self. But as next i will go on and add PS4Link to the SDK. I can imagine that a developer may need not only 
 a debug network to see what is going on, he also might want to send some lines of code to the process and run it without to reset everything. Yea the elf header 
 should be self explaining, the system header contains assembler call's allready defined as common syntax like nope(), cli(), sti(), and so on. Also it contains the 
 write protection functions which are normally also base of a SDK or a kernel how ever, hence the name system header.
 I sorted all defines, types and struct's into a own header wtih the same name. Like structs.h. For the Pad i added 2 new defines USER1 and USER2 which hold the 
 user account number, example #define USER1 = 10000000;, then i added a additional level (or better say 3) for the debug network which are KDEBUG (kernel debug 6) 
 KERROR (kernel error 5) and KINFO (kernel info 4). I defined two easy sycall'S for the debug network named SEND() which will based on the LEVEL you overload 
 automaticly sned out the message via sceNetSend() [userland] or sys_sendto() [kernel]. The last named function is also added and defined in the debug network so 
 you can right start developing from kernel mem or under kernel rights too. If you don't define a network to use, dbg net will automaticly set up a UDP network.
 if you want to use a TCP or may a doublenetwork, you can define your own debug structure config. Also here i added some entry's for our need's. Which are 
 sockUDP, sockTCP, portUDP, portTCP, protocol, and will help us to keep the dbg net automated. If you use a double network, please use SEND2() to refer to which 
 net you wnat to talk to, UDP, TCP or maybe both together ?
 Then i started to add a own tools.c which will hold some usefull functions a developer may can need. Such as disableWP() (disable write protection) and which hase 3
 flags 0, 1, 2 and which will tell the function if you wnat to use disable_interrupts or kern.sched_unpin() or maybe no one of both, simple disable WP. Since dub2() 
 is not allowed on the ps4, i wrote a psydo dub2 which will clean up the mass right after it broth the port to the desired file descriptor. Then i added a simple 
 wait() (well what this does should every one be clear) and a function which will return a flag and tell the librarys if they shall use DBG output or not. But 
 keep in mind that if the level set in your dbg net is lower then the normal debug (3) it will not show the debugging output of the ps4-sdk librarys.
 Also i started to add documentations about function calls from either FreeBSD, Unix or Linus. How ever, it really depends on from where sony did take it. As example 
 sceNetSend() and sys_sendto() are the same function like from FreeBSD send2() which consist's of send(), sendto(), and sendmsg(). But then on the other hand 
 if you compare the FreeBSD setsockopt() call against the one from the PS4, the function credentials do not match. So i googled for Unix setsockopt() and surprise 
 surprise, the function did match the one form the PS4. (also included into the documentation folder).
 
 I'll welcome every one that want to contribute to libMemoria to extend it to something even more better. If you wan't to stay anonymous for various reason's 
 then you can contact me in private too.
 
   -peace cfwprpht-
