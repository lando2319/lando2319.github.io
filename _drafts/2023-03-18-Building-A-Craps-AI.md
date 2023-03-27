---
layout:     post
title:      Building A Craps AI OVERFLOW
css: /css/custom.css
date:       2023-03-18 04:19:54
summary:    Post about my experience building a Craps AI OVERFLOW
categories: ChatGPT
---


// THIS IS OVERFLOW WRITING


Let me bring you up to speed thus far.

Once I was up and running on openai's API, I learned how the system worked, in short, it's platform as a service. You come with your data, you upload it, and 'train' one of their models. Then there is an API for answering the question. It's pay per use, including the questions. For some reason in the beginning I thought I would be able to export the model and perhaps get it to run on and iOS device. In other words, have the model exist on the device, interact with it through a Swift app. I believe that's possible, but not with openAI's models.

At this point I had a code repo, I was uploading jsonl files, and then training my model. For some reason I was under the illusion that I could just simply tell my model how to calcualte a Horn Bet in Craps, and it would just, you know, learn... Now I see, that is not how this technology works, it does not train based on logic, you cannot just appeal to it's logic. It learns by patterns. The first couple weeks, I would just upload a few dozen questions and then the model would just spit back gibberish. 

From here I went through and made all my questions more verbose, repeating things, restating things, this helped a little but it was still, 'overfitting'. Too much noise they say.

So what to do?

My target was a simple question, "What does a $4 Horn Bet pay in Craps?", after learning to be verbose, my quintessential prompt/completion pair is the following

{% highlight linenos %}

{
    "prompt": "How much does a $4 Horn Bet pay", 
    "completion": "A $4 Horn Bet in Craps is $1 on each of the four Horn Numbers. The Four Numbers included in a Horn Bet are: Aces, Ace Deuce, Eleven, and Twelve. If Aces rolls the Horn Bet pays 31 for 1 for your $1 on the Aces. If a Twelve rolls the Horn Bet pays 31 for your $1 on the Twelve, if Ace Deuce rolls the Horn Bet pays 16 for your $1 on the Ace Deuce. If Eleven rolls the Horn Bet will pay 16 for your $1 on the Eleven"
}

{% endhighlight %}

For the Horn Bet specifically, there are just a handful of questions I want to train on. So it dawned on me to just use ChatGPT to rephrase the same question 50 times.

Here's the result [ IMAGE HERE ], I managed to go to 40 examples. This worked pretty good, but when I asked it to spin my verbose answer, it only went to 7.

[ IMAGE HERE ]

From here I decided to see if there was a site I could use to get a quick 100 spins of my verbose answer. Sure, I can just keep asking over and over, but I wondered if there was a way to get a lot more examples per pull? After some Googling, I found [ site ].

Here are the first 5 results [ IMAGE ]

[ Code block ]

It should be pointed out how ridiculous this is, spinning a single question so my robot can 'learn' because apparently repetition helps. We'll see.





LEFT OFF HERE
SUNDAY MORNING, LET'S GET IT



TALK ABOUT the need to edit
In Craps, a $4 Horn Bet places a $1 wager on each of the four Horn Numbers. Aces, Ace Deuce, Eleven, and Twelve are the Four Numbers in a Horn Bet. If an Ace is rolled, the Horn Bet pays $1 on the Aces 31 to 1. If a twelve is rolled, the horn bet pays 31 for your dollar stake on the twelve, and if an ace of deuces is rolled, the horn bet pays 16 for your dollar stake on the ace of deuces. If an eleven is rolled, the Horn Bet will pay 16 for your one dollar wager on the eleven.

This once came out good, worded slightly different than what I would have said, but nevertheless, correct, except for saying, "ace of dueuce". 


The four numbers that make up a horn bet in craps are as follows: Aces, Ace Deuce, Eleven, and Twelve. Each of the four numbers is covered by a $4 wager. The Horn Bet pays 31 to 1 for your $1 bet on Aces if they are rolled. If a 12 is rolled, the Horn Bet pays 31 for your $1 bet on the 12, and if an Ace Deuce is rolled, the Horn Bet pays 16 for your $1 bet on the Ace Deuce. If an eleven is rolled, your $1 wager on the horn bet will be paid out at a rate of 16.

Notice with this one, subtle but significant, it got the Twelve right with, "pays 31 for your $1 bet", but then look at Aces, "pays 31 to 1" which is not correct, should be, "31 FOR 1". This seems to be a common theme where the spinning software with treat these as synonmous. .

Once I had about two dozen spun questions with answers, I decided to spin the spun questions, see what happens.

With this tool paraphrasingtool.ai, it limits you to 20,000 for the free version. So I loaded up roughly 20,000 lines of my recently spun answers

The chat at chat.openai.com, the OG Chat as I call it, is defintiely more accurate, the other tools I tried made predictable mistakes like saying, "Ace" instead of "Aces", or saying the word, "drawn" instead of rolled. The OG Chat would never do that, the OG Chat knows Craps is not a card game, smh.

So after getting a slew of poorly spun articles I'm back using the OG Chat at 7 spins each query. It's slow going, but I'm making progress. My target is 200 lines, 180 of which are around spun from one question, "how much does a $4 Horn Bet pay".

Things have taken a turn for the strange. After coming back to the OG Chat, I successfully ask for some more spun acticles [ IMAGE HERE ]

After going through and editing the answers to be more robust and complete, I decided to try again, at this point I was expecting more of the same, nicely spun answers. But instead the OG Chat come out of nowhere with some stock investing advice. So I tried to use the exact same pre text, "please rephrase these lines individually one by one". Here suprisingly, the OG Chat returns just a single question for me, "What is the definition of a reverse mortgage?"... I'm stumped.

Back to the other paraphrasing tools.

So apparently I've hit some sort of threshold, because when I go to big numbers ~5,000 characters or so, it will start reducing my paraphrasing down to just 7 translations of the line.

Now I've resorted to spinning about 5 times per online tool, then going to another one.
















- show off some spins
- do some formatting with my blog text
- show off my 
- get RSS feed on my twitter elsewhere


show off going from 1 => 5 questions and show off that I'm using chatGPT to advance 

Talk about my target of 200 lines

END THE post with my query and the result, and how much money I spent


get all my setting over to a shared user