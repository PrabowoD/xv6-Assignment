# 2. SysCall
## syscall.c
```diff
void
syscall(void)
{
  int num;
  struct proc *curproc = myproc();

  num = curproc->tf->eax;
  if(num > 0 && num < NELEM(syscalls) && syscalls[num]) {
    curproc->tf->eax = syscalls[num]();
  + #ifdef PRINT_SYSCALLS
  +   cprintf("%s -> %d \n", syscallnames[num], curproc->tf->eax);
  + #endif
  } else {
    cprintf("%d %s: unknown sys call %d\n",
            curproc->pid, curproc->name, num);
    curproc->tf->eax = -1;
  }
}
```

# 4. Date Call System
## makefile
```diff
- CS333_PROJECT ?= 0
+ CS333_PROJECT ?= 1
PRINT_SYSCALLS ?= 0
CS333_CFLAGS ?= -DPDX_XV6
ifeq ($(CS333_CFLAGS), -DPDX_XV6)
CS333_UPROGS +=	_halt _uptime
endif

ifeq ($(CS333_PROJECT), 1)
CS333_CFLAGS += -DCS333_P1
- CS333_UPROGS += #_date
+ CS333_UPROGS += _date
endif
```
