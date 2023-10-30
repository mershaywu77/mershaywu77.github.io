# Stack Tracing
The following example sets a breakpoint on the kernel function fioFormatV(). Then it calls func() in a user partition; func() makes a call to printf(), which uses fioFormatV(). The application is frequently calling printf(), and therefore the breakpoint will be hit shortly after it is set. Once the breakpoint is hit, you can trace the call using tt().
     [pd1] -> b fioFormatV:vxWorks

    value = 0 = 0x0

     

    [pd1] -> b

     

    ADDRESS    SYMBOL              TASK       PD         CNT TYPE

    ---------- ------------------- ---------- ---------- --- ---------------

    0x00033324 fioFormatV          all        0x000fb0a8 0

    value = 0 = 0x0

     

    Break at   0x00033324:fioFormatV            Task: 0x001fa5d0 (pdt2)

                                                PD  : 0x000fb0a8 (pd1)

    Called function encountered a breakpoint (returning 0).

    value = 0 = 0x0

     

    [pd1] -> ptt

    0x200140b0 func           +38 : printf ()

    0x00032d54 printf         +7c : fioFormatV ()

    value = 0 = 0x0

# Vxworks telnet can not show task information
It was found when telnet to a vxworks image, the command "i" or "help" can not show the result. 

It was confirmed it is related to the MTU size, see https://en.wikipedia.org/wiki/Maximum_transmission_unit

Solution:

Manual change the MTU size make sure it >1536 see https://support.zen.co.uk/kb/Knowledgebase/Changing-the-MTU-size-in-Windows-Vista-7-or-8
Enable the jumbo mode of the interface. 
 Note: netsh is a command available in power shell (but change setting need run as Administrator)