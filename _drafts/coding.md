When you're learning a new skill, there are three different types of progress
* gear acquisition
    * In the very beginning, gear acquisition provides the biggest perceived jump in your progress. 
    * After all, to get started, you have to get the tools needed to do the thing, but a lot of people get stuck in this stage and they fall victim to what's called gear acquisition syndrome, or they keep buying new and better gear because they think it's gonna make them better, but they shouldn't because with gear, there is a very real law of diminishing returns.
* conceptual learning,
    * A lot of people also get stuck in conceptual learning, just one more course, one more book,one more podcast episode.
    * They never go apply lessons.
    * They're learning for themselves.
* deliberate practice.
    * The real progress in any skill, anything you could learn happens with deliberate practice, putting in the reps, and getting the feedback that you need.
    * If you wanna make real progress, if you wanna actually achieve mastery, then you have to put in the reps.
    * So get the minimum viable gear, learn what you need to learn upfront, and then go and do the work.

How important it is to learn programming for cyber security?
and the lawyerly answer is, it depends.
* Starting off
    * there’s many roles that don’t really require you to code, and based on how advanced you want to get, programming may or may not be all that important for you.

we cover the relationships between cyber security tooling and expertise, an on-the-job scenario where I wished I knew how to code but couldn’t, and ending with some advice for all the non-programmers out there just starting out.

Let’s break it down!

### So how important is coding really?
Just about all the tools you use in cyber security are written in code, and programming lets you write tools. 

* what are tools, and what’s the value in knowing how to build them?
    * On a conceptual level, tools extend your ability to change the environment around you, whether in the physical or digital world.
    * Combined with intent, they let you create action and change.
    * So the more advanced your tools are, the more leverage you have, and the wider range of actions and change you can achieve.
> Archimedes once said “give me a lever long enough and a place to stand and I’ll move the Earth.”

If he was standing in something more sophisticated like the Death Star, he’d also have the ability to blow it up; if he knew how to operate it, of course.

In the cyber world, it’s no different.

Being able to get results in cyber depends on the types of software tooling at your disposal and your expertise at using them.

So the first principle to keep in mind is that it’s the combination of tools and skills that really determine your overall cyber abilities, whether for an individual or for a team.

So to improve your overall effectiveness, it’s important to be balanced in both.

Currently in the field of cyber security, most people fall into one of three categories: Blackbox Users, Tool Operators, and Developers

* blackbox users
    * Most blackbox users will usually only know the basics of using one or a few different software systems, and only in situations that they’ve been trained in.
    * These guys might even have a few certifications, but aren’t able to apply their training to solve problems independently in more complex scenarios without the help or mentorship of more experienced practitioners.
    * Being able to modify tools or craft new ones is out of the question.
    * The vast majority of people in cyber security would fall in this category, and knowing how to code isn’t all that important for them, because they’ve yet to master many of the most common tools in the role they’re already in, whether it’s Wireshark, Metasploit, Autopsy, Burp Suite, Volatility, Cellebrite, Group Policy, et cetera.
    * You’ll be much better off first focusing on the fundamental principles like understanding computer networking, operating system architecture, and solving technical problems.
* tool operators
* developers


In the next category, we have tool operators who are quite experienced at using a variety of software to get things done, and can creatively chain them together in real-world scenarios.

These guys are the backbone of companies’ IT and security shops, and are often the workhorses getting things done. 

But for those without the ability to code, the downside is that when you’re in a situation without an immediately apparent tool available, there’s not much you can do about it.

Taking the time to learn some programming can really amplify your ability at this stage, since it lets you automate many of the tasks that you once performed manually.

Now as for tool developers, especially those who are actively involved in operations, they can understand the ins and outs of the tools they use.

Knowing how to program lets you modify existing software or craft something more custom
to solve specialized cyber security problems.

The operator-developer types tend to be some of the best cyber practitioners you’ll meet in the field and are hard to come by, depending on the team you’re on.

In terms of overall ability, you’ll find that people who can chain tools together or write custom-built code have increasing levels of expertise that are orders of magnitude higher.

And I tend to find that those with programming backgrounds tend to progress faster and deeper
in their learning journeys than those who don’t.

Here’s an exam

When I was first starting off in the field, I worked as a security analyst in three-man team with no certifications and a very basic understanding of code.

We were monitoring for malicious activity on the network using a software called Splunk,
which lets you build advanced queries to search across large datasets, like network logs.

In many enterprise networks, the only traffic allowed to exit are common protocols like NTP, DNS, HTTP, HTTPS, which is what you’d expect from internal users browsing the web or servers fetching updates.

These services typically get hosted on ports 123, 53, 80, and 443.

Firewalls would drop any other type of traffic destined for other ports to limit the risk of data exfiltration.

To bypass this, malware will often hide their communication traffic within these common protocols as covert channels to evade detection.

I pushed the idea of monitoring DNS traffic for signs of malicious activity, after reading about the technique in some academic white papers.

I wanted to develop a way to assign DNS queries in our logs weighted risk scores depending on the number of subdomains, the length, and overall entropy of the query.

Because I didn’t know how to code, I had to chain together an incredibly massive Splunk query to calculate everything.

Even though this method worked and discovered outbreaks on the network, it was pretty slow and bogged down the system, and I had to rely on one of the other more senior guys on the team to re-implement my solution as a module in Python to do the same thing, but more efficiently.

On one hand, having the curiosity and persistence made me a valuable member of the team.

But at the same time, had I learned the most basic programming skills, it would have given me the flexibility to describe the outcome of what I wanted to do using the language of code.

This experience later prompted me to act and take coding more seriously to patch-up my skill gap.

One caveat I do want to make is that it's important to draw the line between scripting and software development, since many people will use the word “programming” or “coding” interchangeably to describe both of them.

Scripting would normally refers to writing short snippets of code in an interpreted language to automate tasks or glue the functionality of other tools together.

Software development on the other hand, is a broader term that covers scripting, but also involves writing algorithms or libraries as part of a larger, more complex toolchain.

People often consider Python or Bash as scripting languages, and compiled ones like C++ or Java to be more geared towards software development, but generally it depends on the complexity of the tool and your into whether quick and dirty or something more robust and enduring.

Now on the operator versus developer axis, you’re going to see a lot more scripts closer to the operator side, and more compiled languages on the developer side.

This isn’t true across the board, since people can bounce around the spectrum, but it’s a decent rule of thumb.

For instance, in 2016 a group called “The Shadow Brokers” dumped a bunch of hacking tools used by the NSA, which you can now easily find and study on GitHub.

You’ll notice there’s a mix of Python scripts more geared towards operators to run by hand and compiled binaries for implants and exploits that definitely takes a team of engineers to craft.

For those of you who really really aren’t into software development-level programming, you can get pretty far by at least learning how to read and write scripts, since on the operator side of the spectrum, your focus is primarily on the pre-built tools with some degree of customized automation thrown in.

In this case, it’s not massively critical to have a coding background, because in my experience, most computer science programs are much more heavily focused on topics like applied math, programming theory, and software development at the academic level.

I personally think it’s better to start off learning scripting, which can be quick to pick up and a bit more pragmatic for day-to-day technical tasks.

Three books I recommend for learning scripting 
* Automating The Boring Stuff with Python 
* Learn Powershell in a Month of Lunches
* Unix and Linux System Administration Handbook, for learning Bash.

For practice, one of my favorite resources is a site called runcode.ninja, which hosts scripting challenges that you can do in just about any language of your choice.

Definitely check it out, since they’ve got hundreds of practical exercises covering everything from encryption, forensics, to reverse engineering.

All in all, it’s totally possible to have a successful journey in cyber security without programming skills.

But as you progress in experience, you’ll quickly find that the types of problems you’ll be dealing with aren’t easily fixed by readily available tools.

All you can do is maybe rely on someone else on your team to help you implement a solution, or learn how to do it yourself.

Being able to craft your own tools with code makes you so much more versatile and well-rounded of a cyber professional.

It really turns the tables and puts you in the position of helping others on the team be more effective, which at the end of the day, translates into more opportunities in different organizations.

So what’s your take?

How important do you think coding is for people in the cyber security field?

I’d love to hear more about your thoughts in the comments below.