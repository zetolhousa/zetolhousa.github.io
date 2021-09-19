---
title: "Things I wish I learnt before getting a job"
date: 2021-09-19T14:36:20+05:30
tldr: learn SQL, git, vim, java
---

*Disclaimer: there is only so much you can prepare in advance. You’ll mostly learn everything on the job itself but I think there are some learnings which can take off the load. Instead of trying to play catch up while on the job.*

Most of the big tech companies have in-house tooling which is a beast in itself to learn (depending on the company and how much internal tools they own). Having to learn them while also trying to learn a new programming language or technology can greatly slow you from getting up to speed.

Below I share some things which I feel having a firm grasp of will boost your productivity and ramp up time.

### SQL
I bet this is the most widely used language in any software engineering job involving some amount of data. Without any explanation, reason or rhyme just trust me and learn this. You’ll thank me.

Knowing how to join tables left and right, aggregate and filter them. These are invaluable skills. It will even boost your credibility when you can quickly pull up data to back all your statements. Eg: finding out why the price of item x has gone up in the past two quarters. Given tables t1, t2,…,tn all having some possible useful data but mostly different columns. What if the task involves having to left join here, right join there, inner join again over here, group to aggregate in some temp table, generate new columns using conditional clauses like `CASE`, then finally filtering the output and inserting.

The only thing I remembered out of college was how to `CREATE` a table and `SELECT *` from that table. Don’t be like me and save yourself some sleepless nights just to learn the bare minimum after your manager had already assigned tasks to implement or fix something.

### Git
Working with multiple branches with different features, merging, rebasing, etc. can easily get messy really quickly.

If you can find your way around all the commits and branches without breaking a sweat, you’re well on your way to saving hours daily just trying to get your changes in a manageable state.

At the very least, know the basics. Cloning a package, making changes, staging, committing and pushing the changes. Without this you’ll be the real imposter in the room.

### Vim
This is a powerhouse. I’m lucky I started learning it religiously in college. Watching programmers touch typing along with the retro vim terminal looked so cool. That’s how I got into it. The learning curve is initially steep but once you get the hang of it, you’ll be surfing.

Depending on your job profile, the amount of time you spend on it will very but it is certain that you will NOT be able to avoid it. This is because at one point you’ll have to ssh into a remote machine. Where you’ll not find your cozy little GUI based sublime text editor or notepad++. Forget about full blown IDEs.

All text editing will have to be done on some kind of terminal based text editor. Just make sure that when the day comes you’re not stuck trying to figure out [how to exit vim](https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/).

### Java
This is probably something specific for my case because I avoided Java like plague. I hated it for some reason and made it my life’s mission never to do anything that was remotely even related to Java. This was the naive me in college.

But guess what, now I use it every single day. Biggest regret.

It’s not going away anytime soon and it’s used so widely in every major company. I always thought C/C++ paired with a higher level language like Python would suffice. I wasn’t really wrong there, because for a fresher having a solid grasp of any language able to code up solutions to data structure and algo problems is enough to prove ones potential (fortunately or unfortunately).

The reason I regret not learning Java is because the time that could have been spent actually producing code, I had to invest learning a language from scratch.
