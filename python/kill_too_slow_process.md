# Kill function call after some time
Let `foo` a function such that for some argument, it takes to much time to execute the call. 
How terminate that call?
Use: [`multiprocessing`](https://stackoverflow.com/a/14920854) with [shared variable](https://stackoverflow.com/a/10415215) to communicate.

```python
import multiprocessing
import time

def foo(t):
    '''
    Your usual function which returns something.
    This function just sleep for:
     `t` seconds 
    before set and return:
     `x`
    '''
    time.sleep(t)
    x=666
    return x

def run(t,d):
    '''
    Special multiprocessing function with special multiprocessing dictionary: 
     `d`
    to capture: 
     `foo` → `return`
    '''
    d['return']=None
    x=foo(t)
    d['return']=x

#Shared variable: In this case a `dict`
d=multiprocessing.Manager().dict()

t_kill=3
for t in [1,6,2]:
    if t<t_kill:
        print("="*20)
        print('The Proccess with `foo` runs normally')
    if t>=t_kill:
        print('The Procces with `foo` fails to set `x`')

    #define Process
    p = multiprocessing.Process(target=run, name="Run", args=(t,d))
    #launch the p
    p.start()
    # Wait a maximum of `t_kill` seconds for foo
    # Usage: join([timeout in seconds])
    p.join(t_kill)

    # If thread is active
    if p.is_alive():
        print ("foo is running... let's kill it...")

        # Terminate foo
        p.terminate()
        #cleanup
        p.join()

    #cleanup
    p.join()
    #result
    print(f"Output for t={t} is: {d['return']}")
    print("="*20)
```
Output:
```bash

====================
The Proccess with `foo` runs normally
Output for t=1 is: 666
====================
The Procces with `foo` fails to set `x`
foo is running... let's kill it...
Output for t=6 is: None
====================
====================
The Proccess with `foo` runs normally
Output for t=2 is: 666
====================
```
