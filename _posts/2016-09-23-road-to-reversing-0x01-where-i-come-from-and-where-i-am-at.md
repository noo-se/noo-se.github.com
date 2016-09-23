---
layout: post
title: Road to Reversing - 0x01 - Where I come from and where I am at
date: 2016-09-23 10:51:46.000000000 +03:00
type: post
published: true
status: publish
categories:
- Road to Reversing
excerpt: "some exercepr"
---

<p>Hello World.</p>

<p>This first post is special in the sense that it will include two video posts -- the intro and the actual first content post</p>

<p><a href="https://www.youtube.com/watch?v=L5E-z66sgDQ">https://www.youtube.com/watch?v=L5E-z66sgDQ</a></p>
<script>
document.write('<iframe width="560" height="315" src="https://www.youtube.com/embed/L5E-z66sgDQ" frameborder="0" allowfullscreen></iframe>');
</script>

<h1>Now for a bit of background </h1>

<p>I have a background of working as a developer and a sysadmin since 2000. Some of it was freelance, most of it was as an employee of small companies. I have always loved toying with new languages because most of them solved some new problem and thus were able to teach me a new way of looking at a certain set of issues.</p>
<p>Naturally these programming languages ranged from very high level stuff all the way to the bottom of the stack - the building blocks of assembly code.</p>
<p>On the high level you could have something like Python where you can write a simple XOR like so:
{% highlight python %}
xorred_text = [chr(ord(ch) ^ xor_key) for ch in original_text]
{% endhighlight %}
</p>
<p>Versus writing this in assembly is somewhat more verbose:
{% highlight asm %}
start:
  mov esi, OriginalTextLocation
  mov edi, XorredTextLocation
  mov ecx, 0
  mov ebx, XorKey
xorloop:
  mov eax, [esi+ecx]
  xor eax, ebx
  mov [edi+ecx], eax
  inc ecx
  cmp ecx, LengthOfText
  jne xorloop
{% endhighlight %}

(This was written off-the-cuff so it is only approximately accurate. And yes: Intel is my flavor.)
</p>

<p>Don't worry if you can't read that. That is beside the point of this point. I am just illustrating the difference between low level and high level languages. Obviously there are even more high level languages out there, but I digress.</p>

<p>So my first touch with assembly was in 2002 for a course at a polytech university on the topic of how computers (CPU, RAM etc) work. I loved the puzzle of following the instruction flow, keeping track of stack and all of those things. But I also knew that with the power that assembly programming gives you, comes also the great chance of actually messing up your computer. On high level languages the designers of the language can put in all sorts of safety measures to make sure you don't hurt yourself. But on the low level the CPU will do exactly what you tell it.</p>

<p>After that course, it took several years before I stumbled upon ASM again. This time it was in the context of reverse engineering, even though I did not yet know it was called such. The challenge was to take a binary executable file (Linux ELF) and figure out what the password was. I learned about cool little tools like <code>strings</code> and <code>objdump</code> on Linux and quickly found the password.</p>

<h1>What is reverse engineering</h1>

<p>Over the years I have become more and more intrigued by this low level process of taking the finished product of software engineering and deciphering what it actually does. I've heard of many folks out there picking apart other programs such as the operating system of gaming consoles, the file format of those old games to port them to emulators, cracking programs' commercial serial keys, fixing (i.e. binary patching) non-open source programs whose support has ended and so forth. Those are all involve the arcane art of "reverse engineering".</p>

<blockquote>Most commonly reverse engineering &mdash; or reversing &mdash; is one of two things: figuring out the logic of either a program or a data format.</blockquote>

<p>This can mean figuring out in what order your favorite creative tool writes its binary file's bits in order to manipulate those bits in an automated fashion. Or it could mean bypassing license checks on an application that is end-of-life where you cannot pay anyone even if you wanted to.</p>

<p>Of course reversing can and is also used for illegal/criminal activities. Cracking <acronym title="Digital Rights Management">DRM</acronym> protections or bypassing serial checks for commercial tools where you could buy the support are two of the most common activities you will see tarnishing the industry. I shan't discuss those further as they do not pertain to what I am about or my activities.</p>

<h1>Where I am at now</h1>

<p>So for the past 4 years or so I have had reversing on my todo list and for all that time I have gathered a bunch of good resources on the topic. So many resources in fact that when I finally moved reversing to number 1 slot on my priorities I was effectively paralyzed with the many choices for what I should start studying.</p>

<p>I have previously already consumed all of <a href="http://www.securitytube.net/groups?operation=view&groupId=5">SecurityTube: ASM Megaprimer for Linux</a> and <a href="http://www.securitytube.net/groups?operation=view&groupId=6">SecurityTube: ASM Megaprimer for Windows</a> vids. That is definitely something I would recommend. I also found this other series <a href="https://www.youtube.com/playlist?list=PL038BE01D3BAEFDB0">Open Security Training: Intro x86 (32 bite)</a>. These three sets of videos definitely overlap, but I would say that they more reinforce each other than distract.</p>

<p>This means that I am not starting this Road to Reversing series from square 1. I have already accumulated some experience of how ASM works and how the process of reversing works. But I would liken my current status with that of anyone who studied another language in school but has not used that language actively since. You might see a movie now and then and hear a familiar word or even watch a whole movie in that language and temporarily be more familiar again, but the reality is that you are pretty rusty. That is me. I am rusty without ever being competent in this subject.</p>

<p>After spending a few weeks &mdash; I'd love to say it was only a few days, but trying to stick to honesty here even ... &mdash; paralyzed with the options I had and effectively getting nothing done besides wasting time staring wide-eyed at the screen and alt-tabbing between <a href="https://www.amazon.com/Practical-Reverse-Engineering-Reversing-Obfuscation/dp/1118787315">a physical book</a>, <a href="https://beginners.re/">an ebook</a> and a bunch more resources. I finally decided that I would just start <em>doing</em> and learning as I go. And by doing I meant actually reversing some programs.</p>

<h1>... but why?</h1>

<p>My next post will contain more information about the tools and strategies I used to reverse some <em>very easy</em> crackmes from <a href="http://crackmes.de/">crackmes.de</a>, but I wanted to round off this post also with a short description of <em>why</em> someone would want to learn reversing. What are the future job opportunities that this skillset might open?</p>

<p>
    In my knowledge there are three main focuses for people pursuing reverse engineering (for legal purposes):
    <ul>
        <li>Malware analysis</li>
        <li>DFIR - Digital forensics and incident response</li>
        <li>For fun: CTFs / Crackmes</li>
    </ul>
</p>
<h2>Malware analysis</h2>
<p>Malware is a term that encompasses all software that is created for bad purposes. Previously there was talk of computer viruses and then separately as computer worms and for the most part there was confusion about how much these terms were interchangable etc. So thankfully the common term 'malware' was introduced over ten years ago, even though it really took off in late 2008.</p>
<p>
<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/744_RC08/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("TIMESERIES", {"comparisonItem":[{"keyword":"malware","geo":"","time":"all"},{"keyword":"/m/01t2j","geo":"","time":"all"}],"category":0,"property":""}, {}); </script> 
<noscript><a href="https://www.google.com/trends/explore?date=all&q=malware,%2Fm%2F01t2j">Google Trends: Malware vs Computer Worm</a></noscript>
</p>

<p>The job of malware analyst is two-fold: there are those in the antivirus industry whose job is to triage new samples of malware and try to come up with a signature that is as generic as possible so that it won't produce false positives but that it will still match the same malware even if the author changes it slightly &mdash; for example changing the <acronym title="Command and control - a server providing malware instructions on what to do next">C&amp;C</acronym> addresses.</p>

<p>For these malware analysts it is important that they are quick to read and understand the general functionality of a given application and analyse whether it is malicious, i.e. malware, or just a run-of-the-mill regular app. And if it is a malicious app, proceed with the signature creation and that's it.</p>

<p>There are also those malware analysts whose job description involves digging a bit deeper, checking for new attack patterns, a potential 0day vulnerability &mdash; a security hole for which there is no fix available from the vendor &mdash; and in general trying to understand complex malware samples more deeply and potentially co-operate with law enforcement or other investigating bodies. These analysts need a deeper understanding of the operating system's API calls and overall inner workings.</p>

<h2>DFIR</h2>
<p>Digital forensics comes into play when there has been an 'incident' that involves computers of some sort. Whether that is a suspected crime, e.g. financial crimes, leaking sensitive or copyright information; or whether it is a case of being the victim of a ransomware attack or a breach.</p>

<p>Forensic analyst have a whole swath of tools available for them, some of them are for memory analysis and others for file analysis. But reversing again plays a key role when they discover an unidentified binary lurking in memory doing something suspicious. It is the job of a reverse engineer, who can be the same person, to figure out what this program is programmed to do and whether that is illegal or against policies / contracts and thus evidence of a hostile act. Or it could be solving how a ransomware has encrypted your documents and reversing the process to recover the files.</p>

<h2>Reversing things for fun and profit - CTFs and Crackmes</h2>

<p>CTFs, or Capture The Flags, are digital competitions of varying challenges. They usually incorporate different aspects of computer security and witty^Wbad puns. Reverse engineering a binary and figuring out the password for a given username is a common type of challenge. This is so popular that it is also its own form of hobby: so called crackme challenges. The difficulty in these can be quite vast starting from a hardcoded string inside a file to code run through a 'packer' algorithm to hide it from plain view in the binary. CTFs are not limited to reversing but reversing definitely is a required skill in most.
</p>

<p>That is a very short description of the main branches of <b>RE</b> use and for me all of these three paths are relevant. I am still a generalist security consultant, but in the future I might choose to dive deeper into either malware analysis or DFIR. I do not know which yet, but as both require a good stable foundation of reversing, I am now focusing on that skillset and hence this series.</p>

<h2>Vlog 0x01 - history and current status</h2>

<p><a href="https://www.youtube.com/watch?v=W926p57uyAw">https://www.youtube.com/watch?v=W926p57uyAw</a></p>
<script>
document.write('<iframe width="560" height="315" src="https://www.youtube.com/embed/W926p57uyAw" frameborder="0" allowfullscreen></iframe>');
</script>

<hr/>

<p>Next up: RE tools and the actual process of reversing.</p>


