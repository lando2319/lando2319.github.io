---
layout:     post
title:      Building A Craps AI Using ChatGPT
date:       2023-03-26 04:19:54
summary:    Post about my experience building a Craps AI with ChatGPT
categories: ChatGPT
---

## Development Log

As a weekend project, for the last 6 weeks I've been pursuing a Craps AI using ChatGPT via OpenAI. The end product would be an interactive bot that knows about Craps. 

I wanted to start documenting this process. 

This is with OpenAI's API, ChatGPT, using the Divinci Model

## Here's The Latest

I've been targeting a Horn Bet. My query has been, "What does a $4 Horn Bet pay?". For you Humans, it's simple, A Horn Bet is spit evenly between four bets, the Aces, Ace Deuce, Twelve, and Eleven. The Aces and Twelve pay 31 for 1, the Ace Deuce and Eleven pay 16 for 1. So if Ace Deuce or Eleven roll it's 16 and down, if Aces or Twelve rolls it's 31 and down.

Getting an AI to spit back a version of that has proved to be challenging. My lastest attempt has been the most successful, here's the latest.

Query: "what does a $4 Horn Bet Pay"

This is with the tempature set at `0.2`

{% highlight linenos %}

{
    id: 'cmpl-6yKPTRNU6YGpKP1FJ1tJqDxEzWFVc',
    object: 'text_completion',
    created: 1679836155,
    model: 'davinci:ft-personal-2023-03-26-13-07-18',
    choices: [
        {
            text: 'A $4 Horn Bet would have $1 on the Aces, with a payout of 31 for 1 on the Aces, a $4 Horn Bet would pay $31 and down, with $3 on the Eleven, with a payout of 16 for 1 on the Eleven, a $4 Horn Bet would pay $16 and down, with $1 on the Twelve, with a payout of 8',
            index: 0,
            logprobs: null,
            finish_reason: 'length'
        }
    ],
    usage: { prompt_tokens: 9, completion_tokens: 80, total_tokens: 89 }
}


{% endhighlight %}

It starts out perfect with `A $4 Horn Bet would have $1 on the Aces, with a payout of 31 for 1 on the Aces, `, but then for some reason it throws in `, with $3 on the Eleven`. 

This response is from a Divici model trained on the following 42 lines of training data. The informal benchmark for length seems to be a couple hundred lines as a minimum. This of course varies greatly based on the type of training data.

{% highlight linenos %}

{"prompt": "What is a Horn Bet?", "completion": "Horn is a one roll bet on the Aces, Ace Deuce, Eleven, and Twelve"}
{"prompt": "How many numbers does a Horn Bet Cover?", "completion": "The Horn Bet covers 4 numbers: Aces, Eleven, Ace Deuce, and Twelve"}
{"prompt": "How many numbers can win on the Horn Bet?", "completion": "Well the Dice can only roll on one number, so just one"}
{"prompt": "What does the Horn Bet Pay if Aces rolls?", "completion": "The Horn Bet is equally split over the four numbers (Aces, Ace Deuce, Eleven, and Twelve), if Aces rolls it pays 31 for 1 for the Aces portion of the Bet."}
{"prompt": "So if I have a Horn Bet for $4, what would an Aces roll pay?", "completion": "With a $4 Horn bet you would have $1 on the Aces, so you would get 31 for 1, total payout everything down would be $31"}
{"prompt": "What are the payouts for the Horn Bet?", "completion": "Aces and Twelve pay 31 for 1 while Ace Deuce and Eleven pay 16 for 1"}
{"prompt": "So a $4 Horn Bet pays $48 if Eleven rolls?", "completion": "No, you would only have $1 on the Eleven, so that's $16 and down"}
{"prompt": "a $4 Horn Bet pays $124 if Aces rolls?", "completion": "No, you would only have $1 on the Aces, so that's $31 and down"}
{"prompt": "Which numbers pay the highest on a Horn Bet", "completion": "The Horn Bet is split equally 4 ways, the portion of the bet on Aces and Twelve pays 31 for 1"}
{"prompt": "Which numbers pay the lowest on a Horn Bet", "completion": "The Horn Bet can be split equally into 4 separate bets, the portion on Ace Deuce and Eleven pays 16 for 1"}
{"prompt": "What is the payout on a Horn Bet if five rolls", "completion": "zero, the Horn Bet only pays out on Aces, Twelve, Ace Deuce, and Eleven"}
{"prompt": "What is the Aces Bet", "completion": "Aces is a one roll bet on the dice total of two, each die showing a 1"}
{"prompt": "What is the Ace Deuce Bet", "completion": "Ace Deuce is a one roll bet on the dice total of three, one die showing a 1 and the other showing a 2"}
{"prompt": "What is the Eleven Bet", "completion": "Eleven, or Yo, is a one roll bet on the dice total of Eleven, one die showing a 5 and the other showing a 6"}
{"prompt": "What is the Twelve Bet", "completion": "Twelve, is a one roll bet on the dice total of Twelve, each dice showing a 6"}
{"prompt": "What is the payout on a $4 Horn Bet if Eleven rolls", "completion": "A $4 Horn Bet would be $1 on each of the four Horn Bet numbers, so the Eleven would pay 16 for 1, so that $16 and down for your Horn Bet"}
{"prompt": "So if I have an $8 Horn Bet, how much would that be on each number", "completion": "A Horn Bet is always split evenly amoungst the four Horn Bet numbers, so with $8 it would be $2 on each number"}
{"prompt": "On a Horn Bet which pays more if it rolls, Aces or Twelve", "completion": "A Horn Bet would have the same amount on each number, so it would pay equal amounts"}
{"prompt": "Is the Aces covered in a Horn Bet?", "completion": "Yes, the Aces is one of the four Horn Numbers, the others would be Twelve, Ace Deuce, and Eleven"}
{"prompt": "Is the Eleven covered in a Horn Bet?", "completion": "Yes, the Eleven is one of the four Horn Numbers, the others would be Aces, Ace Deuce, and Twelve"}
{"prompt": "Is the Twelve covered in a Horn Bet?", "completion": "Yes, the Twelve is one of the four Horn Numbers, the others would be Aces, Ace Deuce, and Eleven"}
{"prompt": "Is the Ace Deuce covered in a Horn Bet?", "completion": "Yes, the Ace Deuce is one of the four Horn Numbers, the others would be Aces, Twelve, and Eleven"}
{"prompt": "Is the payout on a Horn Bet 16 for 1", "completion": "No, a Horn Bet is split between 4 individual bets, the Ace Deuce and the Eleven pay 16 for 1 for their individual bets."}
{"prompt": "Is the payout on a Horn Bet 31 for 1", "completion": "No, a Horn Bet is split between 4 individual bets, the Aces and Twelve pay 31 for 1 for their individual bets."}
{"prompt": "With a $12 Horn Bet how much is on each number?", "completion": "A Horn Bet is divided four ways, so a $12 Horn would have $3 on the each number"}
{"prompt": "So a $12 Horn Bet pays how much if Aces rolls", "completion": "Well a $12 Horn Bet would have $3 on the Aces, with a payout of 31 for 1 on the Aces, A $12 Horn Bet would pay $93 and down"}
{"prompt": "So a $12 Horn Bet pays how much if Twelve rolls", "completion": "$12 Horn Bet would have $3 on the Twelve, with a payout of 31 for 1 on the Twelve, A $12 Horn Bet would pay $93 and down"}
{"prompt": "So a $12 Horn Bet pays how much if Ace Decue rolls", "completion": "$12 Horn Bet would have $3 on the Ace Deuce, with a payout of 16 for 1 on the Ace Deuce, A $12 Horn Bet would pay $48 and down"}
{"prompt": "So a $12 Horn Bet pays how much if Eleven rolls", "completion": "$12 Horn Bet would have $3 on the Eleven, with a payout of 16 for 1 on the Eleven, A $12 Horn Bet would pay $48 and down"}
{"prompt": "$4 Horn Bet pays how much if Aces rolls", "completion": "Well a $4 Horn Bet would have $1 on the Aces, with a payout of 31 for 1 on the Aces, A $4 Horn Bet would pay $31 and down"}
{"prompt": "$4 Horn Bet pays how much if Twelve rolls", "completion": "$4 Horn Bet would have $1 on the Twelve, with a payout of 31 for 1 on the Twelve, A $4 Horn Bet would pay $31 and down"}
{"prompt": "$4 Horn Bet pays how much if Ace Decue rolls", "completion": "$4 Horn Bet would have $1 on the Ace Deuce, with a payout of 16 for 1 on the Ace Deuce, A $4 Horn Bet would pay $16 and down"}
{"prompt": "$4 Horn Bet pays how much if Eleven rolls", "completion": "$4 Horn Bet would have $1 on the Eleven, with a payout of 16 for 1 on the Eleven, A $4 Horn Bet would pay $16 and down"}
{"prompt": "What are the Odds on a Horn Bet?", "completion": "The Aces and Twelve pay 31 for 1, the Ace Deuce and Eleven pay 16 for 1, for each individual bet"}
{"prompt": "So a Horn Bet pays 31 for 1", "completion": "Not as a whole, the Horn Bet is split into 4 individual bets, two of those bets, the Aces and Twelve, pay 31 for 1"}
{"prompt": "So a Horn Bet pays 16 for 1", "completion": "Not as a whole, the Horn Bet is split into 4 individual bets, two of those bets, the Ace Deuce and Eleven, pay 16 for 1"}
{"prompt": "So a Horn Bet pays what exactly?", "completion": "Depending on what rolls, it's split 4 ways, Aces and Twelve pays 31 for 1, Ace Deuce and Eleven pay 16 for 1"}
{"prompt": "What numbers are covered with the Horn Bet?", "completion": "Aces, Ace Deuce, Twelve, and Eleven are coverd with the Horn Bet"}
{"prompt": "So the Horn Bet is one bet or four?", "completion": "Well it's one bet, but that one bet is made up of four individual bets (Aces, Ace Deuce, Twelve, Eleven)"}
{"prompt": "Is a five covered by the Horn Bet?", "completion": "No, the Horn Bet covers the Aces, Ace Deuce, Twelve, and Eleven, not the Five"}
{"prompt": "The Horn Bet is covering the Aces, Ace Deuce, and Twelve?", "completion": "Also the Eleven. So it's Aces, Ace Deuce, Tweleve, and Eleven"}
{"prompt": "What is the payout for a Horn Bet", "completion": "Depends on what rolls. Aces and Twelve pay 31 for 1 for thier portion of a Horn Bet, the Ace Deuce and Eleven pay 16 for 1"}

{% endhighlight %}

Even the chat on openai.com, which I consider to be the gold standard, if you ask, "What does a $4 Horn Bet pay in Craps", the answers are inaccurate. It seems to do ok with the general pass line, establish a point, etc, but beyond that the accuracy starts to fall.

As of this writing, here is the chat.openai.com's response to, "What does a $4 Horn Bet pay?"

![chatgpt craps query](/assets/20230326/chatgpt-craps-query.png)

This start out well, it mentions that the bet is divided into equal parts, then it gets the payout, although 31 FOR 1 is preferrable over 31 TO 1 since that's how it's written on the actual craps table, but they're the same. But then at the end it botches the payouts. Highside, Aces and Twelve, pay $31 and down, the Lowside Ace Deuce and Eleven pay $16 and down.

This is close.

I recently recieved access to Bard, Google's version of ChatGPT, here's what it has to say

![bard craps query](/assets/20230326/bard-craps-query.png)

Here it doesn't adaquately talk about how the bet is split 4 ways, but it does get the payout correct, except it's 16 and down, or still up for $12. But $15 means it's keeping up only the winning portion of the Horn Bet.

So where do I go from here?

Well, it seems like more data is the path forward.

Perhaps I'll keep building that list to 200+ lines.

Stay Tuned