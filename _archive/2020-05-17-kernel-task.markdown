---
layout: post
title: "kernel_task and CPU hijacking"
categories: [technology, operating-system, MacOS]
---

> A look at how macOS's ** kernel_task ** hijacks CPU to *supposedly* save itself from overheating

## Preface

About a week ago, I was able to get my hands on a mid 2012 Macbook pro. Now before this, I had never used any Macbook, or even an Apple product for that matter. Now this Macbook was running on macOS High Sierra, or should I say crawling. It was taking more than 15 seconds to open something as simple as `About this Mac` screen. That was pretty frustrating to say the least.

Specs wise, the Macbook was as best as it could be; a 2.9Ghz  i7 processor with 8 GB RAM, and 750GB HDD. The specs were great!

> My plan was to make it work!

- First off, and without even thinking anything, I formated the disk and reinstalled the OS that came in by default, **Mountain Lion** if I remember correctly. But that, to my disappointment, didn't help. The OS got a tad bit faster, but the major issue was right there. I thought mahybe the HDD was dead.

> Pressing ` Command + R` during the booting process started the recovery mode, which had option to reinstall the OS or to fiddle around with the disk. Now this option needed a working internet connection, and considering how it is barely 50kbps here, it was a major pain in the ass.


- The next day, I replaced the 750 GB HDD with a 250GB HDD from my old Window's Laptop. Before I could just wipe the HDD and start installing, the Macbook actually loaded the Windows OS which, to my surprise, ran pretty damn well. This at least concluded that the hardware was pretty fine, and definitely must be the software issue.


- On the 250GB HDD, I installed macOS Mojave, which is follwed by Apple's latest OS at the time of this writing, Catalina. Installing Mojave again required a working internet connection
. It took nearly 30hrs of painful day and nights of letting the laptop do its thing. It was painful to watch for a number of different reason. For one, the installation progress said something like 2 hr remaining, but with every one or so hour passed here on Earth, it was only moving barely five minutes inside the Macbook. How is this even acceptable? I thought.

- A quick Googling around then made me understand that this, this very thing of taking hours to update an OS, is quite normal. Not the most normal thing, but definitely normal. Some people were complaining of 12 plus hours which should have been done in around 2 hours give or take. That was a big surprise.

- On outside, this Macbook looked beautiful, and even elegant despite some cosmetic damages. But inside, it was nothing less than cancer.

- Over a period of 2 days (48+hrs), the Macbook was finally done with the Mojave. But to my utter disgust, it was slow as before. What a misery.

- I thought maybe updating the RAM from 8 GB to 12 GB will work, I thought. And that's what I did. But nope.

> As I unscrewed, there were signs that this wasn't the first the time laptop was opened, such as the battery screw holder was broken, and the DVD drive had a screw missing. As I was admiring at the beauty of the hardware, and also feeling a bit wasted with the broken battery hinge, I realized I had not checked the battery count. 

- Once I managed to install 8 GB of DDR3L 1600Mhz RAM alongside one of the existing 4Gb x 2 RAMs, I started the laptop. But the OS didn't show any signs of improvement. Also, the battery count had crossed the standard 1000 cycle mark, and was at around 11xx. The battery state, however, said `Normal`. Besides, the battery also held charge so that was good. But 1100 something battery count? A bit too much I thought.

- I then thought maybe the SSD will work faster, thanks to the internet community. So I installed a 256 GB SSD drive out of my old laptop. It ofcourse didn't have any macOS. So the next stop was reinstalling the whole OS again. But this time. since it was SSD, I was pretty hopeful of finishing the setup a bit early.

- 12 hours it was I think. I finally managed to install the standard Mountain Lion that came out of the box. The speed too increased by a significant bit. But the issue was still there. Opening Safari was taking more than 20 seconds, and that was unacceptable.

- I wanted to update the OS to the latest Catalina, but the one that was supported was El Capitan. I let the laptop do its thing overnight, and the next day El Capitan was running. But the issue again, was right there, in front of my eyes with all its glory and determination to make my life a living hell.


- After searching on the internet, doing whatever I could, the **Activity Manager** showed **kernel_task** process using more than 200% of CPU, the main culprit.



## kernel_task and its characteristic nature of being a resource whore
Long story short, the **kernel_task** was using more than its fair share of CPU resource, or hijacking should I say, so that other processes which actually need the resource won't be able to use the resource, and thus **supposedly** preventing the CPU from over-heating. This could be due to a number of different reasons as it turns out, such as failure of thermal sensors etc.

What solved this, and luckily it did, was changing the SMC and other hardware from a technician.

Luckily, everything is smooth for now.

`But one heck of a week for sure!`

