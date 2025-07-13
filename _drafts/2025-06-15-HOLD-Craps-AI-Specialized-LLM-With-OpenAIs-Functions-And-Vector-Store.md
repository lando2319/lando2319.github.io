---
layout:     post
title:      Craps AI - Specialized LLM with OpenAI's functions and vector store
date:       2025-06-15 06:27:43
summary:    Creating an LLM app that specalizes in one area, use functions to reduce hallucinations, and vector store to influence responses
categories: AI
---


// This is duplicated from a WIP post
// the top stuff is unused

In Craps Prop bet are calculated with by, ‘for 1’, instead of ‘to 1’. The reason for this is for calculating payout and determining if a bet is staying up, if a Horn Bet has 4 units, you want a, 'total and down' amount then you can just subtract the amount of the bet for a, 'still up to win' amount. Even though, '16 *for* 1' is the same as, '15 *to* 1'. The AIs are just too smart to understand.

The AI’s always want to reduce to ‘to 1’. See my earlier post for more details. Having been a Craps Dealer for 5 years in my early days, I noticed lots of areas for improvement with the responses AI gave to questions about Craps. This began my first attempt at building a Craps AI. Here is the repo.

At the time (Early ‘23) fine-tuning was the main B2B solution being offered by OpenAI for influencing a model's response. Fast forward to today when OpenAI offers function calling and vector store. Also it seems to be better at taking system instructions overall.






OLD STUFF















Say that in the LLM world this is a small vector store, and it's still working




FINALLY

Talk about the improvment cycle

Embed my tiktok



Close on how the name of the game is identifying an area to focus on, and crafting a solutions using...









// Here is how I setup Craps AI
// - Functions - to reduce hallucinations
// - Vector Store - to priortize MY Craps knowledge


// REWORD
The AI’s always want to reduce to ‘to 1’. See my [earlier post](/chatgpt/2023/03/26/Building-A-Craps-AI) for more details. Having been a Craps Dealer for 5 years in my early days, I noticed lots of areas for improvement with the responses AI gave to questions about Craps.





VECTOR STORE HEADER
































[Intro with exaplinging better for 1 and to 1]


DUMP THIS SECTION
In Craps, Prop bet are calculated with by, ‘for 1’, instead of ‘to 1’. The reason for this is ease of calculation, and determining if a bet is staying up. If a Horn Bet has 4 units, you want a, 'total and down' amount, then you can just subtract the amount of the bet for a, 'still up to win' amount. Even though, '16 *for* 1' is the same as, '15 *to* 1'. The AIs are just too smart to understand.

The AI’s always want to reduce to ‘to 1’. See my [earlier post](/chatgpt/2023/03/26/Building-A-Craps-AI) for more details. Having been a Craps Dealer for 5 years in my early days, I noticed lots of areas for improvement with the responses AI gave to questions about Craps.

There are two main components I'm using on Craps AI’s for my openAI solution: Function calling and Vector Store. The function calling is calculating bets, LLMs are notorious for hallucinating (you don’t call it, ‘lying’ because that means intent and machines don’t do that). So now instead of the LLM calculating the payout of a horn bet, it understands when it’s being asked to calculate a bet, it extracts bet name from the question (and knows bets that don’t exist), and extracts what the roll is. [ say something about vecrtor store since I started the paragraph with it ]

# OpenAI Functions

So a question might be, “What does a $4 Horn Bet pay if 12 rolls?”, the AI will return something like this

[




































// WHAT AM I REALLY TRYING TO SAY






// Do some better segue



There are two main components I'm using on Craps AI’s for my openAI solution: Function calling and Vector Store. The function calling is calculating bets, LLMs are notorious for hallucinating (you don’t call it, ‘lying’ because that means intent and machines don’t do that). So now instead of the LLM calculating the payout of a horn bet, it understands when it’s being asked to calculate a bet, it extracts bet name from the question (and knows bets that don’t exist), and extracts what the roll is. [ say something about vecrtor store since I started the paragraph with it ]

# OpenAI Functions

So a question might be, “What does a $4 Horn Bet pay if 12 rolls?”, the AI will return something like this