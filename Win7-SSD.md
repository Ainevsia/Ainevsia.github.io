---
title: Reinstall my Win7 Ultimate
date: 2018-02-10 20:10:21
---
## Triggers
My old ThinkPad E430c, which my father bought in about 2012, is operatering more and more slowly nowadays. A few days ago, it even experienced several bruescreens breakups, and it took me a whole morning to just start it. After examing the hard-drive, I found that it was severely damaged, maybe due to the bumping on the road. So last night, I bought a SSD (TOSHIBA Q200 240G) ![2.5inch SATA3 SSD](https://img14.360buyimg.com/n0/jfs/t14575/253/1200396077/329424/fafc920b/5a4af4abN5d6f692d.jpg)
## Preparations
After searching the Internet for almost a whole day, I decided to still install the Win7 Ultimate. I also learned a lot through searching. :D I finally found a detailed tutorial called [xitongcheng](http://www.xitongcheng.com/jiaocheng/xtazjc_article_29173.html). It guided me to turn my original onlydisk into a USB setup disk. What I need now is only a Win7 system now (from [msdn](https://msdn.itellyou.cn/)).
## Place the SSD in place and start your computer
Here comes a terrible question.![grub](http://www.dabaicai.org/uploads/allimg/170328/6-1F32P9421A57.jpg)
What should I do? I googled it and founded the solution.

just type in three commands:
```
find --set-root /bootmgr
chainloader /bootmgr
boot
```
and it entered the PE system. Then just choose the Win7 Ultimate. It works.
## install the DRIVER
First of all, you should make sure that your computer can have access to the Internet. Then everything went on smoothly without explaination.
# Inflections
>I don't want to reinstall any system any longer!

>It's really complicated!
