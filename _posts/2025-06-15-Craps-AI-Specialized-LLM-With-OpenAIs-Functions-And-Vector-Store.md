---
layout:     post
title:      Craps AI – Specialized LLM with OpenAI Functions & Vector Store
date:       2025-07-12 08:11:23
summary:    Creating an LLM app that specalizes in one area, use functions to reduce hallucinations, and vector store to influence responses
categories: AI
---

> The AIs were just too smart for Craps...

Which is more, '15 to 1' or '16 for 1'? Well the AIs know they are they're the same thing; and when it came to Craps they would constantly provide payouts as 'to 1'. Presumably this was just a natural tendency to reduce. But with Craps, it actually is, 'for 1', it's written on the table that way. It's not just convention, this would throw off people's understanding when bets would have more than one unit. 

This began my pursuit of a Craps AI what would give responses like me (I was a Craps dealer in the Vegas area in my early days).

So the problem I was looking to solve was the AIs forcing, 'to 1' payouts for Craps payouts that are, 'for 1', and to get the AI to embody my own Craps knowledge instead of it's own. And also to reduce hallucinations when calculating bets.

There are two main components I'm using on Craps AI’s for my openAI solution: Function calling and Vector Store. The function calling is calculating bets, LLMs are notorious for hallucinating (you don’t call it, ‘lying’ because that means intent and machines don’t do that). So now instead of the LLM calculating the payout of a horn bet, it understands when it’s being asked to calculate a bet, it extracts bet name from the question (and knows bets that don’t exist), and extracts what the roll is. The Vector store is data that I produce about Craps which it will then prioritize over what it already knows.

### OpenAI Functions

So a question might be, “How much does a five dollar horn high 12 pay if aces hits?”, the AI will return something like this

```
calculate_horn_highs_payout({
  "bet_amount": 5,
  "roll": 2,
  "target": "twelve"
})
```

Requesting the calculation, then regular determinative JavaScript code would return this

```
{"totalPayout":31,"stillUpToWin":26}
```

This response is then feed into another API call to openAI where it will use this info to craft a nice response. So the cost was an additional API call and the reward was reducing the chance of a hallucination on calculations. Now it just needs to know the elements for the calculation. Regular JavaScript is good at calculating a Horn bet if you provide the elements, it works the same way every time.

Even with this setup at first the AI was not using my nice function until I added this to the system instructions

> DO NOT CALCULATE PAYOUTS ON YOUR OWN, USE THE CALCULATION FUNCTIONS  "type": "function"

### OpenAI Vector Store

This is where your message can shine through. Similar to telling the AI to use my functions, my system instructions included, “Priortize my Vector Store Data”. One way this showed up for Craps is calculating the max bet on a Don’t Pass Bet. Some things vary by casino and other things are universal, calculating the max bet on the don’ts is universal. After noticing the AI using the word typically I updated my vector store for Don’t Pass and Don’t Come to make sure the AI knew, this was how it’s calculated, so it shouldn’t use the work, ‘typically’ or ‘usually’. You see the AIs, they’re not like us humans, they haven’t been on those tables, they’ve never had green felt under their fingernails.

The vector store for Craps AI is a directory of markdown files explaining each bet. This is where I can influence the AI's responses. For instance a question came in about taking down a Don't Come Bet, since the AI didn't mention, 'no action', I added this to it's vector store doc

> A player can take down their Don't Come bet at any time. In addition while in the Don't Come area, before traveling to behind a number, a player can say, 'no action', and the dealer will leave the bet in the DC and not move it to behind the number rolled. If a question is about taking down the Don't Come Bet, mention the ability to call, 'no action'.

Most times after adding this, it would mention, 'no action' but sometimes it would not mention it and you have to decide how much you want to press it knowing that pressing might cause it to focus too much there and loss integrity elsewhere.

### Evaluation Test Cycle 

Finally here is my work flow for improving the responses.

First I’m checking the logs, reading the questions and responses. Once I find a response with room for improvement, I add it to a file for evaluation testing. I create an obj with the question, an example answer, and the evaluation criteria. 

So I copy over the question, copy over the response, edit the response to be optimal, then add what I am looking for, what makes a good response.

In order to evaluate and score the response, I'm using another AI model the high reasoning model, which is also supplyed with the same vector store data.

In this case a question came in about takind down a Don't Come Bet, the answer was good. Except in craps you can say, ‘no action’, and elect to not travel your DC bet, this definitely should have been included.

So I just added on to the original answer.

Then instructed the evaluating AI to look for the following

- Say YES (player can take down their Don't Come Bet)
- Say player has the advantage
- Say player can do, 'no action'

Very important, I ran this test with no updates so I could replicate the error. Naturally it didn’t mention, ‘no action’ since I had not added that to the vector store yet, thus my evaluation model scored it low.

So then I added the lines about, 'no action', to my vector store file. This caused the AI’s response to include, ‘no action’ most of the times.

---

### 🔄 Tight evaluate–patch loop

1. **Read production logs.** Spot answers with room for improvement.
2. **Turn the Q&A into a test case.** Save the question, an *ideal* answer, and criteria.
3. **Run an eval model**—also armed with the vector store.
4. **Patch** either the vector docs or the function set, then rerun the test.

That cycle catches regressions early and keeps the knowledge base improving

---

*Thinking about a specialized LLM?*


[![Craps AI](/crapsAIIconDownload.png)](https://apps.apple.com/us/app/craps-ai/id6743343228)
