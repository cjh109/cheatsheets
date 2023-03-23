# Open-Source App Lets Anyone Create a Virtual Army of Hackintoshes
[![](https://video-images.vice.com/topics/57a205628cb727dec795a6b1/callout_logo/1614199980283-screen-shot-2021-02-24-at-34918-pm.png?resize=240:*)
](https://www.vice.com/en/topic/cyber)

Hacking. Disinformation. Surveillance. CYBER is Motherboard's podcast and reporting on the dark underbelly of the internet.

The average person probably doesn’t think of MacOS as … scalable. It’s intended as a desktop operating system, and while it’s a very functional operating system, Apple generally expects it to run on a single piece of hardware.

But as any developer or infrastructure architect can tell you, virtualization is an impressive technique that allows programmers and infrastructure pros to expand reach and scale things up far beyond a single user. And a Github project that has gotten a bit of attention in recent months aims to make MacOS scalable in ways that it has basically never been.

Its secret weapon? A serial code generator. Yes, just like the kind you sheepishly used to get out of paying for Windows XP or random pieces of shareware back in the day. But rather than generating serials for software, [Docker-OSX](https://github.com/sickcodes/Docker-OSX) has the ability to generate serial codes for unique pieces of MacOS hardware, and its main developer, an open-source developer and security researcher who goes by the pseudonym [Sick Codes](https://twitter.com/sickcodes), recently released [a standalone serial code generator](https://github.com/sickcodes/osx-serial-generator) that can replicate codes for nonexistent devices by the thousands. Just type in a command, and it will set up a CSV file full of serial codes.

“You can generate hundreds and thousands of serial numbers, just like that,” Sick Codes, who used a pseudonym due to the nature of his work, said. “And it just generates a massive list.”

Why would you want this? Easy—a valid serial code allows you to use Apple-based tools such as iMessage, iCloud, and the App Store inside of MacOS. It’s the confirmation that you’re using something seen as valid in the eyes of Apple.

Previously, this process was something of guesswork. Hackintosh users have long had this problem, but have basically had to use guesswork to figure out valid serial codes so they could use iMessage. (In my Hackintoshing endeavors, for example, I just went on the Apple website and … uh, guessed.) Sick Codes said he developed a solution to this problem after noticing that the serials for the client would get used up.

“In the Docker-OSX client, we were always in the same serials,” he said in an interview. “Obviously, no one can log into iMessage that way.”

But when he looked around to see how others were coming up with unique ways to generate product serials, he found more myth than reality. So he went through a variety of tests, uncovering a method to generate consistently reliable serial numbers, as well as a low-selling device that would be unlikely to have a lot of serial numbers in the wild—and landed on the iMac Pro.

“I actually went through, and I've got like 15 iMac Pros in my Apple account now, and it says that they're all valid for iMessage,” he said. “Obviously I was going to delete them after, but I was just testing, one by one, seeing if that's the reason why it does work.”

Beyond making it possible to use iMessage to hold a conversation in a VM, he noted that random security codes like this are actually desirable for security researchers for bug-reporting purposes. Sick Codes adds that it is also an effective tool that could be used as one part of the process for jailbreaking an iPhone.

(At one point, he speculated, possibly in jest, that he might have been the reason [the iMac Pro was recently discontinued](https://lifehacker.com/apple-is-discontinuing-the-imac-pro-now-what-1846430699).)

An Army of Virtual Hackintoshes
-------------------------------

On its own, the serial code thing is interesting, but the reason it exists is because MacOS is not currently designed to work at a scale fitting of Docker, a popular tool for containerization of software that can be replicated in a cloud environment. It could—with its use of the Mach kernel and roots in BSD Unix, there is nothing technically stopping it—but Apple does not encourage use of VMs in the same way that, say, Linux does.

A side effect of hacking around Apple’s decision not to directly cater to the market means that it could help making Hackintoshing dead simple.

Let’s take a step back to explain this a little bit. Hackintoshing, throughout its history, has tended to involve installing MacOS on “bare metal,” or on the system itself, for purposes of offering more machine choice or maximizing power. 

But virtualization, by its nature, allows end users to work around differences in machines by putting an abstraction layer between the system and its many elements. And virtualization is incredibly sophisticated these days. Docker-OSX relies on kernel-based virtual machines, or KVMs, Linux-based hypervisors that allow virtual machines to get very close to the Linux kernel, able to run at nearly full speed though a common open-source emulator, QEMU.

Comparable to things like Oracle’s Virtualbox or the Parallels virtualization tool on MacOS, they are very technical in the way they work, and are often managed through the command line, requiring a complex mishmash of code that can be hard to figure out. (One common challenge is getting graphics cards to work, as the main interface is already using the resource, requiring something known as a “passthrough.”)

But the benefit of KVMs is that, if you tweak them the right way, you can get nearly the full performance of the main machine, something that has made KVMs popular for, say, letting Linux users play Windows games when the desire strikes. And since they’re disk images on hard drives, backing one up is as easy as duplicating the file.

At the same time, improvements to Hackintoshing have opened up new possibilities for doing things. In the past year or so, the Clover approach of Hackintoshing ([as I used in this epic piece](https://www.vice.com/en_us/article/8xznw4/how-to-make-a-hackintosh-laptop)) has given way to a new boot tool, [OpenCore](https://dortania.github.io/OpenCore-Install-Guide/), and a [more “vanilla” approach to Hackintoshing](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/) that leaves the operating system itself in a pure form. (There is a [project dedicated to Hackintoshing](https://github.com/kholia/OSX-KVM) over KVM, OSX-KVM.)

The benefit of Docker-OSX is that, while command-line codes are required (and while you’ll still need to do passthrough to take advantage of a GPU), it hides much of the complicated stuff away from the end user both on the KVM side and the Hackintosh side. (And, very important for anything involving a project like this: It is incredibly well-documented, with many use cases covered.) Effectively, if you know how to install Docker, you can whip up a machine. Or a dozen. Or, depending on your workload, a thousand.

Sick Codes explained this to me by whipping up a DigitalOcean image in which he at one point put four separate installs of MacOS on the screen, each using a modest 2 gigabytes of RAM. I was able to interact with them [over a VNC connection](https://www.vice.com/en/article/y3g4ex/why-remote-access-software-is-almost-too-useful), which is basically nerd heaven if you’re a fan of virtualization.

“Why is it better than Hackintosh? It’s not Hackintosh, it’s like your own army of virtual throwaway Hackintoshes,” Sick Codes explained.

There are two areas where this approach comes particularly in handy—for programming and compiling code for Apple-based platforms such as iOS and iPad OS, which benefit from scale, and for security research, which has seen a rise in interest in recent years.

With more than 50,000 downloads—including some by known companies—and, in one case, a container so large that it won’t even fit [on the Docker Hub website](https://hub.docker.com/r/sickcodes/docker-osx), Docker-OSX has proven a useful choice for installing virtual Macs at scale.

Macs in the Server Room
-----------------------

In a way, Apple kind of set things in motion for an open-source solution like this to emerge, in part because of the unusual (and for a time, unspoken) restrictions that it puts on virtual machines.

For years, a niche of Apple-specific cloud providers, most notably [MacStadium](https://www.macstadium.com/), have emerged to help serve the market for development use cases, and rather than chopping up single machines into small chunks, as providers like DigitalOcean do, users end up renting machines for days or weeks at a time—leading to unusual situations like the company [buying thousands of 2013 Mac Pros for customers six years after its release](https://www.vice.com/en/article/pajmk9/who-kept-buying-the-mac-pro-everyone-hated).

(MacStadium offers a cloud-based competitor to Docker-OSX, [Orka](https://www.macstadium.com/orka).)

Apple does not sell traditional server hardware that could be better partitioned out in a server room, instead recommending Mac Minis, and with the release of Big Sur, it put in a series of guidelines in its end user license agreement that allowed for virtualization [in the way that MacStadium was doing things](https://blog.macstadium.com/blog/developers-big-sur-and-vindication)—but not in the more traditional rent-by-the-hour form. (Competitors, such as [Amazon Web Services](https://aws.amazon.com/about-aws/whats-new/2020/11/announcing-amazon-ec2-mac-instances-for-macos/), have also started selling virtualized Macs under this model.)

Licensing agreements aside, given the disparity between Apple’s devices and how the rest of the cloud industry doles out infrastructure, perhaps it was inevitable someone was going to make something like Docker-OSX. And again, the tool turns things that used to be a headache, like generating unique serial codes for virtual Macs, into something painless.

“If you run a \[command-line\] tag that says, generate unique, and then set it to true, it will just make your new Mac with a new serial number that you can use to log straight into iMessage,” Sick Codes explained. “If you keep doing that, keep logging in, you'll have like 45 Macs in your account, and they'll all be valid Macs.”

In recent years, companies like [Corellium](https://corellium.com/), which sells access to virtualized smartphones to developers and security researchers, have effectively built their services without worrying about EULA limitations [and faced lawsuits from Apple over it](https://www.vice.com/en/article/d3a8jq/apple-corellium-lawsuit). Sick Codes, generally working in the open-source community and helping to uncover technical issues, is very much in this spirit.

It’s possible that something might happen to stop the spread of fake iMac Pro serial codes in virtual machines all over the internet—as I started reporting this, _[MacRumors](https://www.macrumors.com/2021/03/09/apple-randomized-serial-numbers-early-2021/)_ [revealed that](https://www.macrumors.com/2021/03/09/apple-randomized-serial-numbers-early-2021/), according to an internal support document, Apple is about to redo its approach to serial numbers to make the numbers more random and harder to mimic. ([Repair advocates are not happy about this](https://twitter.com/RDKLInc/status/1369697562614194178).) But there’s only so much Apple could do about the machines currently on the market, given that there are so many millions of them.

But for people who want to install MacOS on a cheap box somewhere and don’t care about things like Apple Silicon, it’s now as easy as installing Linux, installing Docker, and typing in a couple of commands. Sick Codes noted that, beyond the scalability and security advantages, this opens up opportunities for users who can’t afford the “Apple tax.”

“Feels pretty wholesome knowing anyone can participate in Apple's bug bounty program now, or publish iOS and Mac apps,” Sick Codes said. “App development shouldn't be only for people who can afford it.”