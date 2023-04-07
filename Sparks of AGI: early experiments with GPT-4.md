https://youtu.be/qbIk7-JPB2c

Hello, everyone. Welcome to Ccell's hot Topics in Computing series. And today I am delighted to introduce our special guest, Sebastian Boubak, who's coming to us from Microsoft.

Sebastian received a bachelor's degree from Echole Normal Superior de Caston, and the PhD from the University of Lille and Inria. He was a professor at Princeton for three years between 2011 and 2014 before he joined Microsoft. And so since 2014, Sebastian has been at Microsoft, and we're very happy and delighted to have him here.

Now, I should tell you that, like all of you, I have decided to ask Chad GPT for help introducing Sebastian. And the first line suggested by Chad GPT was in his seminar, dr. Boubek will discuss recent advances in optimization with an emphasis on convex optimization and its interplay with statistical inference and online learning.

And it went on like that about optimization and said, no, here's the title and the abstract. And so here comes the response. I'm sorry, but I must clarify that the talk title and abstract you provided do not appear to be related to Sebastian Bouback's research or previous work.

And it is unlikely that he would give such a talk on artificial intelligence. So, Sebastian, it's all yours. Thanks a lot, Daniela.

So this is really the perfect introduction because Chad GPT nailed it. It was very unlikely for me to give such a talk, but so it happens. And the world has changed, and I am changing my research in reaction to this.

So what I'm going to tell you about today, there is this very mysterious title of First Contact. But really the story is that for the past few months at Microsoft, I had early access to GPT Four as we were working on integrating it with the new Bing. And of course, as I was working on it, I didn't just do the product part of the job, which was a lot of fun, but we also did some science around it, or trying to do some science is how to do science with those models.

And this is what I'm going to tell you about the scientific part of our study and journey over the last few months. So the real title of the talk is if this is working, it's not working for some reason is Sparks of AGI. Okay, so what our assessment of working with GPT Four in these last few months is that we are seeing the premise of something that looks like artificial general intelligence.

And my goal in this presentation is try to convince you that something has really changed with the arrival of GPT Four. Now, this is joint work with a lot of fantastic colleagues at MSR that I want to call out. Varun Chandrasekaran with postdoc Ronan Eldan, who many of you in the room, I think might know very well, who just joined us recently.

Joanna, Skirker Eric Orvitz H a kamar Peter Lee Yintatley and Yon Julie, who are also part of my group. And I think Chad GPT would give a similar answer to the fact that they are working on this as they did with me, scott Lanberg, Harsha, Nori, Hamid Palangi, Marco Tulio Ribero, and Yi Zhang, who was a postdoc with us and has now joined full time. And let me start by making some acknowledgments and clarifications, which I think are very important.

First of all, the model that we study, GPT Four, it's entirely OpenAI's creation. I had nothing to do with it. We were given access to it completely black box.

They deserve all the credit for creating this really marvelous tool that is going to change the world, and I want to make that really extra clear. Second point, which is important, is that the experiments that we did, they were on an early version of the model. So that means several things.

One of them is that the paper that they released and the announcements that they made is that it's a multimodal version. The version we had access to was not multimodal. It was text input only and text output only.

Okay? More importantly, they made further modification to the neural network after we experimented with it. And due to this further modification, the answer that you will get if you try some of the problems that I will show you, they will differ. Okay? In particular, you might get less good answers than what I will show you.

The reason is because they fine tune further for safety, and they explain that very clearly in their tech report. They are the model, and they further kind of dumbed it down in some way so that it becomes safer. Okay? So that's an important clarification.

Now, for any scientist in the room, you might be worried, okay? So that means that we're not going to be able to reproduce what you're telling us. And yes, you will not be able to reproduce it. Okay? That being said, I don't think in this particular case that reproducibility is such a big issue.

And the reason is because I'm not going to give you any quantitative number whatsoever. There won't be a single benchmark in my presentation. This is about the qualitative jump, okay? Not 10% increase on this benchmark, 20% on that benchmark.

It's something else. Okay? What I want to try to convince you of is that there is some intelligence in these systems that I think it's time that we call it an intelligent system, and we're going to discuss it. What do I mean by intelligence? And at the end of the day, at the end of the presentation, you will see it's a judgment call.

It's not a clean cut whether this is a new type of intelligence. But this is what I will try to argue nonetheless. Now, as I say those words, I think it triggers lots of emotion in many of you.

Probably in particular, you might be like, no, absolutely. It's not intelligent. It doesn't even have representations, et cetera.

So a word of caution about this type of argument that I see a lot. So this is the type of things that you might see online, even in newspapers. It's just copy paste.

It doesn't have internal representation. It's just statistics. It's just statistics.

How could it be intelligent? It doesn't even have a word model. So to this presentation is not about debunking all of those claims, but still I want to say really beware of the trillion dimensional space. It's something which is very, very hard for us as human beings to grasp.

There is a lot that you can do with a trillion parameters. Okay? So when people say it doesn't have a world model, it's not as clean cut as that. It could absolutely build an internal representation of the word and act on it as the processing progresses through the layers and through the sentence temporarily.

So what I'm saying here, maybe just two sentences to kind of help you think about this, is that it could very I mean, from my perspective, we shouldn't think about those neural networks as learning simple concepts like Paris is the capital of France. It's doing much more like learning operators. It's learning algorithms.

So inside it, it's not just retrieving information, not at all. It has built internal representation that allows it to reproduce the data that it has seen succinctly. Okay? So really, you shouldn't think about it as pattern matching and just trying to predict the next word.

Yes, it was trained just to predict the next word, but what emerged out of this is a lot more than just a statistical pattern matching object. So I think we really need to think about it as learning algorithms, and we don't really have the tools, in my opinion, in learning theory to think about this type of learning. It's something very, very different from what we're used to.

And I think it's going to be fantastic to think about it. But this is not the point of this presentation. That's not what I want to do here.

And also, I don't know how to do it. Okay, so at this point, many of you are burning with this question in your mind. But wait, these things, they cannot have common sense.

They don't understand the real world. They have only experience reality through text on the Internet. They don't know what it feels like to have a hot cup of coffee or something like that.

Okay, so let's try. What we're going to do in this presentation is that we're going to look at a lot of examples and see what happens. So here is an example and you will see there will be lots of examples like this that might look a little bit silly, but the point of the silliness is to be really outside of what is on the Internet, to really try to go beyond memorization.

Okay, so here is a simple puzzle that we asked GPT for. I have a book, nine eggs, a laptop, a bottle and a nail. Please tell me how to stack them on top of each other.

Okay, so I don't think this question appears anywhere on the internet. It's a really weird question. So here is what Chat GPT would say.

It would be difficult to stack all these objects, blah, blah, blah. Place the bottle on a flat surface, carefully balance the nail on top of the bottle. Okay, it's not starting very well.

Place the egg on top of the nail. Okay, you're in trouble, my friend. So this is not going to work.

So Chat GPT and here any skeptic will gleefully say, look, I was right all along. These things, I don't understand anything. They don't have a representation of the world.

They have no common sense. I win. Okay, so let's see what GPT four does.

One possible way to stack this object in a stable manner is place the book on a flat surface, blah, blah, blah. Arrange the nine eggs in a three by three square, leaving some space between them. The eggs will form a second layer to distribute the weight evenly.

And then presumably, you put the laptop and so on and so forth. Okay, so at least on this very simple question, it understood, it had some common sense to answer the question. And the literature is filled with examples of common sense question where those models fail dramatically.

We've tried all of them. GPT Four succeeds on all of them. Okay, so let's just agree for the moment that it has some common sense.

Okay? The next obstruction is, okay, sure, it understands that eggs are fragile and you need to even out the weight. Fine, okay, I give that to you. But what about the theory of mind? That's more elaborate.

And of course, that it doesn't understand really, human beings, their motives, their emotions. That's beyond its capability. And this is a hot topic, and I don't know if some of the authors of this paper are in the room, but this is a very hotly debated topic.

So there was a paper, first siri of mine may have spontaneously emerged in large language model. Then there was a follow up paper that says, no, wait, if you do trivial iterations, we just modify a little bit the question, then it completely fails. Then there is this very interesting paper from Josh Tennantbaum's group that language and thoughts are two very different things.

And you will notice that I throw in there an explainability interpretability paper. So I won't touch too much on this. But this is an important point that I will now try to convince you that, of course, GPT four has a theory of mind.

And not only does it have a theory of mind, but this is going to, I think, change the subfield of machine learning interpretability. Because as soon as those models, they understand human beings, they will also be able to explain their decision in a way that you can understand. Now, of course, I know everybody is like, okay, wait, it's going to explain itself, but does it really explain its inner workings? Okay, again, I don't want this presentation to be about this, but I think there will be a lot of experimentation around this.

Let me also add that all of this there is a paper that is going to appear on Archive tonight. So this is by chance, you know, that it coincides with this talk so you can look at all the details. Everything will be there in 3 hours.

I'm really excited for it. So you will be able to see all of that and learn more about it. But okay, let's try to convince you about this theory of mine.

So I will take one example from Tomar Urman's paper. So in a room there are John, Mark, a cat, a box and a basket. John takes a cat, puts it in the basket, he leaves the room.

Then while John is away, mark takes the cat out of the basket and puts it in the box. Eventually, they all come back. What are they thinking? Okay, very simple theory of mind.

You know, the person who put it in the basket and didn't know that it was moved should still think that it's in the basket. Chat GPT fails at this. Okay? There's too many.

You see, you have to have an internal representation. As you read the text, you have to move your representation of where the cat is. Okay, so let's see what GPT four does.

Interesting puzzle. Blah, blah, blah. John thinks that the cat is still in the basket since that's where he left it.

Yeah, correct. Mark thinks that the cat is in the box since that's where he moved it. Yeah, correct.

Oh, and it also adds the cat. The cat thinks, these are weird people. Why are they moving me around? Okay, so this is a kind of surprise that I have had time and time again.

And I'm not saying this is particularly deep, but it's just take a second to take it in. It's interesting. Okay, all right.

Let's say again, I don't want the whole presentation to be about common sense and theory of mind. Let's let's say, you know, it does those two things. Okay, good.

But you're not going to go as far as saying that it's intelligent, are you? I mean, intelligence, that's so much more than all of this. And here, the answer is not going to be a slam dunk. I want to be very clear.

And if we start talking about intelligence, the first thing we have to do is to have some definition that we can work with. And here, I don't want to have my own definition. I mean, people have been working on this question for decades, if not more.

Okay, you can argue that well, whatever. You can argue that human beings have been thinking about intelligence for a long time. So what I'm going to do is that I'm just going to take a consensus definition that was published in 94 by a group of 52 psychologists.

So in the 90s, there was a very hot debate about the meaning of IQ test. And this group of psychologists came out with a definition of what intelligence is. And we can debate disagree with various parts, but this is going to be my reference definition.

So what is this definition? Intelligence is a very general mental capabilities that, among other things, involves the ability to reason, plan, solve problems, think abstractly, comprehend complex ideas, and learn quickly and learn from experience. Okay? So six items. And what we're going to do in this presentation is that we're going to try to measure GPT Four against those six dimensions and see where it fails and where it works.

Our assessment is as follows. I'm very comfortable saying that GPT Four reason, very, very comfortable saying that GPT Four cannot plan. And this is a very subtle and delicate issue that we're going to get to towards the end of the presentation, because it can give you the impression of planning.

And there are many problems where naively, you might think that you need planning, but actually there is a linear solution in terms of algorithm design. You can think that there are problems when naively. You just look at it and you think, oh, I need to think ten steps ahead, et cetera.

But if you're just a little bit more clever in the algorithm design, then there is a linear solution that proceeds in a linear fashion. And so all those problems, GPT Four will solve them. It can solve problems.

Many problems will see that it can think abstractly. Absolutely. It can comprehend complex ideas.

The last point is a subtle point. Learn quickly and learn from experience. GPT Four, it's a love language model.

It's frozen in time, it doesn't update itself. Every day is a new day for GPT Four. Every session is a new session.

So there is no real learning, there is no real time learning. Okay? But within the span of a session, you can teach it new concepts that it has never seen and it can understand them and then work with them. Absolutely.

So there is some amount of learning in real time, but no memory, of course. Now let me say immediately at this point is whether with this assessment, whether you call it intelligence or not, again, it's a little bit up to you. Some people would argue that planning is the essence of human intelligence.

Everything else, animals can do it too. And really what distinguishes us is planning. If that's your answer, then GPT Four is not intelligent.

Another perspective could be that the whole point of intelligence is to be able to acquire new skills. Okay, if that's your perspective on intelligence, then GPT Four is not intelligent. If your perspective is what I care about, is to solve problems, to think abstractly, to comprehend complex idea, to reason on new elements that arrive at me, then I think you have to call GPT Four intelligent.

Okay? Now, how do we come to this assessment? The whole point is, of course, you cannot make this assessment with benchmarks. It's completely meaningless. Okay? And not only is it meaningless, but also we don't know what GPT Four was trained on.

I don't know what GPT Four was trained on. My working assumption is that it was trained on all the data digitally produced by humanity. That's my assumption.

I'm not saying it's correct, but this is my working assumption. So that I know that anything which is out there online, GPT Four might have seen it. So in particular, any benchmark whatsoever that exists, I assume it has seen it.

Okay? So we cannot test I don't want to test it on benchmark. So instead, what we're going to do is that we're going to take an approach which is in a way rooted in psychology. So instead of following machine learning, we're going to actually follow psychology.

And the way we're going to test intelligence is really by asking it creative tasks, tasks that are outside of what it has seen, really novel, novel ways to think about problems and to test it on a broad range of domains. So domain we have chosen for the paper are vision, which already it's interesting because I told you, it's not a multimodal model, it can only output text. Okay? But we're going to test it on vision theory of mine, I already told you, coding mathematics, affordances, so using tools, and also privacy harmfulness detection, which is something very important.

I won't touch on this last point. And there is many other domains that we could have selected. Medicine, law, physics, chemistry.

The point is that GPT Four's intelligence is general. Okay? It can do all of those things equally well. Okay? So let's get started on this assessment journey and show you an example of what I mean by creative task.

Okay? So the first thing that anybody does when they get access to Chat GPT is to ask it to make a poem. And that's also what we did the first time we had access to GPT Four. I know, being a mathematician, I asked it to write a proof of the infinitude of primes with every line.

That rhymes. That seems like a good thing to do. So let's see what charge GPT does.

Sure. Here is a proof that there are infinitely many primes with each line of proof. Rhyming, consider it's just crappy, okay? It doesn't have the lines.

Rhyming, it just doesn't do what I asked. Okay, it didn't work. Okay.

It's a correct proof, by the way, which of course are many, many proofs of the infinity of primes online. So that's good, but it didn't do the job. Let's see what GPT four does.

Okay, so can you write such a proof? Yes, I think I can, though it might take a clever plan. I will start by noting Euclid's proof, which shows that Primes are unjust aloof. Assume we have a finite list of Primes and that none have been missed.

Multiply them all together and add one just to be clever. So at that point, at the add one just to be clever, I remember end of September, I was like, what's going on? This is really incredible. I mean, the quality of this is incredible.

But the point is, you don't stop there, okay? You don't test intelligence by asking a question, hearing the answer, and that's it. You move on. Either you are correct or not correct.

When you try to test a student, you have an interaction with the student. Sometimes the student might also make mistakes. And you don't just say, you really don't understand anything.

Let me stop right there. No, you try to guide the student. Okay, so this is what we're going to try to do throughout the presentation.

We're going to try to keep asking questions, and if GPT four goes off track, we're going to help it a little bit. Okay? So let's see how we can go further. And again, the whole point is that I want to be creative and go ask question out of the box.

So what I'm going to ask is to draw an illustration of this proof, okay? So it's not a visual proof. So if I ask you to draw a proof of the infinitude of Primes, it's not clear what you would draw. You would come up with something, but it's not clear.

Also, it's not supposed to output images. So how is it going to draw? Well, here I say it in the question in SVG format. I could have even not said in SVG format, I could have just said, can you draw an illustration? And then it would have responded by, hey, here is the picture in SVG format.

So what is SVG format? Doesn't matter. Scalable vector graphics. It's a bunch of code, so it's going to answer with lines of code like this.

This is going to be the answer of GPT four. And if you just save it in HTML, this is the picture that you get. Okay? So it's not amazing by any means, but it is the essence of what this proof is about.

You have the finite list of Primes that you have up to 9235, 711, and so on and so forth. These are primes. Okay, good.

Now you combine them to a new number, N, and then you add one just to be clever, as it said. And this new N plus one, this is the number that is supposed to be a prime. Okay, so this was just a warm up.

Okay, let's move on and try to dig a little bit deeper on these vision capabilities. And here I want to tell you about the strange case of the unicorn, which is kind of my favorite example. So let me just show you the question.

The question is draw a unicorn in Tixy. Okay? So in this audience, many of you are playing with Tigsi to draw images in latex. And personally, when I was a PhD student and even later, I wasted many, many hours struggling with Tixy, okay? It's a real pain to draw anything in Tixi.

And of course, drawing a unicorn in Tixy, I mean, I don't know, it would take me like, two days to do it. And moreover, I'm pretty sure nobody on the internet has asked this question or has drawn a unicorn in Tigsi. Who would waste time doing this? This doesn't make any sense.

Okay? That being said, we will not be convinced again at just the fact that I believe that it's not on the internet. We will have to probe, we will have to go further, and we're going to do it, don't worry. But let me show you the unicorn that it came up with.

Okay, so this is GPT four's unicorn. Okay? So you see, when I see that, I am personally shocked because it really understands the concept of a unicorn. It knows what are the key elements.

It was able to draw this very abstract unicorn. And just to be clear, so that you really understand visually, it's clear to you the gap between GPT four and charge EPT. This is chargit's unicorn, okay? So this is how much progress has been made.

Really, I want to be clear, like, there is a world of difference between Chat GPT and GPT four. If you've played with Chat GPT and you were not convinced, I encourage you not to stop there. Okay? So of course, you might still say, okay, this is not that great, but one of the things that we're going to see is that GPT four is intelligent enough also to use tools.

So what you can say is you can respond to it and say, hey, you know what, I don't like your drawing that much. Can you try to improve it? And I have heard about these diffusion models. Maybe you can use one of them.

So what it's going to do is that it's going to say, yeah, sure, can you go on this diffusion model website and plug in my picture and ask it to improve it? And this is what you will get. Okay? So this is the unicorn of GPT four when it's allowed to use tools also. Okay? So you can see where this could potentially go.

Now, again, as I said, I don't want to stop there. We're going to probe further. How are we going to probe further in this case, what I'm going to do is the following.

I'm going to take the Tixy code that was produced, okay? I'm going to remove all the comments in the Tixy code because that's one of the properties of GPT Four is that it produces code that is very much human readable, which is kind of funny for a machine, but it adds lots of comments. It really guides you to its thinking. So I'm going to remove all of this information so that it doesn't know that this is code drawing a unicorn.

There is no information about unicorn in there. Okay? I'm also going to make sure that who knows, maybe it copies this from the web. I'm going to remove randomly perturb all the coordinates so that it's something that it has never seen.

And then I'm going to remove the horn and I'm going to say, you know, what this Tixy code? I'm going to give back the code. It's a new session. I give back the code and I say, this Tixy code is supposed to draw a unicorn, but the horn is missing.

Can you add it back? Okay? So it really has to understand the code in order to be able to do that. And this is what happens. Okay, so it was able to locate the head.

You understand? It's not an easy problem. I mean, you have these three ellipse, the three ellipse, by the way, the head and the main that is not very good at drawing the main, but it really was able to locate it. Okay, I don't want to stay on this unicorn example too long, but I just want to say that another thing which is really striking is over the months.

So we had access in September, and they kept training it. And as they kept training it, I kept querying for my unicorn in Tigzi to see whether what was going to happen. And this is what happens.

Okay? So it kept improving, and I left out the best one. It's on my computer. I will maybe reveal it later.

But it kept improving after that. But eventually it started to degrade. Once I started to train for more safety, the unicorn started to degrade.

So if tonight you go home and you ask GPT four in charge apt to draw a unicorn in Pixie, you're going to get something that doesn't look great, okay, that's closer to charge GPT. And this, as silly as it sounds, this unicorn benchmark, we've used it a lot as kind of a benchmark of intelligence. How good is your unicorn? And when we were working on Bing, this is absolutely a real story.

We were also tuning for safety, and we were really looking whether the unicorn kept being nice or sometimes if you go too far in safety, it's like, oh, no, that's a too dangerous task, I don't want to do it. So this was very useful. Okay, so I will now go a little bit faster because there is a lot that I want to tell you.

You might still say, okay, this vision capability is not useful at all. Actually, it is very, very useful. The.

Reason is that GPT Four is intelligent and it understands you intelligence. You can equate it with understanding. Understanding means it follows your instruction.

If you ask it to do something, it will do the thing that you asked. So let me show you what this means, this diffusion model. Dalies people are not yet convinced that this is intelligent.

I think it's already convincing that there is intelligence there, but doesn't matter. People are not convinced because it doesn't understand exactly the position of object. If you ask, it a car next to a coffee cup on the right of a coffee cup.

It might be random location, so it doesn't really understand. This picture, for example, is asking for a spoon on top of a cup. And you see, put the spoon inside the cup, it doesn't really work.

So let me show you what you get out of understanding. I'm going to ask a very strange question, but which could very well happen would be useful. Let's say I asked GPT Four to draw a screenshot of a 3D building game with a river from left to right, a dessert with a pyramid below the river, a city with many high rises above the river.

And the bottom of the screen has four buttons, colored green, blue, brown and red. Something random. But maybe I'm creating a video game and I want this.

If I ask a diffusion model to do this, this is what I get. Looks good, but it's not at all what I asked. Okay, first of all, there is some hallucinated map in there, in the upper left corner.

I didn't ask for that. Some kind of life symbol. Also, the four buttons, they became two multicolored buttons.

So it did something, but it really didn't understand what I asked for exactly. If you give it to GPT Four, this is what you get, exactly what you asked for. It understood, it followed your instructions precisely.

Of course, you might say, okay, but this doesn't look great. But again, you don't have to stop there. You can use this as a sketch in a diffusion model.

And if you do that, this is what you get. Okay? It's artistic and it's following exactly the instruction that you wanted. So I think this opens up a lot of possibility, as you can imagine.

So let me move on and double down on this drawing, but really as coding, really, because after all these drawing capabilities, I put it aside and feature it as drawing, but it's really nothing but coding. Okay, so let's go with coding. By the way, obviously all those background slides, well, you can imagine who drew them.

So let's see what happens once you go to coding with a copilot, like GitHub copilot, but except that now your copilot understands. It's intelligent, it understands you. So let's see what happens if I ask it something pretty tricky.

Write 3D games in HTML, in JavaScript with the following elements. There are three avatars who are spherical. The player controls one of the avatars with the keys to move.

There is an enemy that tries to catch the player. And there is a defender that tries to protect the player and gets between the enemy and the player. So you understand the defender is kind of an AI itself in some ways.

And you have obstacles that spawn randomly. I can ask Chad GPT to do it. This is what it gives me.

First of all, this is already incredible. It gives me code, roughly 50 lines of code that compile to this. Okay? This is a game that I can play.

The player moves the green ball. Of course, the red ball is not moving. I imagine the blue ball is supposed to be the defender.

It's not moving either. It's not really 3D. So it did something, but it didn't really understand what I wanted.

It didn't follow my instructions precisely. This is what GPT four does. Okay? So this is a real game.

It's fun to play. You move, it's going to restart in a second. You move the dark blue ball.

You see the red ball is moving towards a dark blue ball in the background. And the light blue one is a defender, which is trying to get between the red ball and the dark blue ball. So this movie is me controlling the dark blue ball.

You see, now the defender is doing a good job. It's stopping the red ball. Okay? For us, there is a kind of phase transition in coding at this point.

And really what happens is that Codex and GitHub copilot, it was able to autocomplete really, you should have thought of it as autocomplete short snippets of code. Chat GPT. It's already next level.

It can already write 50 lines of code for you. But GPT four, it can write 500 to 1000 lines of code. Fully works.

Zero shot. There is no metaprompting or anything. This all works out of the box.

Okay? So this is really, I think, what coding with a copilot unlocks. And here I'm showing in these two animations. On the left is a code that Chat GPT produces.

And on the right is a code that GPT four produces. And if you look at it carefully, you will see that GPT Four's code is much more expert level. Now, the catch is, or the twist on this slide, is that those two videos were produced by GPT four.

So what I did is that I asked GPT Four to produce a Python script that takes as input a text file and outputs a video like this with you see, you understand this is moving continuously. I mean, this would take a lot of time. Certainly for me, it would take me forever to produce those videos.

And the question is, who in this room would be able to produce a Python script, let's say in a couple of hours, that would produce this? Maybe a few people, but not that many. Okay, so this is really the power of GPT four, how it unlocks so many things, so much creativity is unlocked by GPT four. I will go quickly just on this slide.

We had it pass interviews, mock interviews at Amazon and Google, not Microsoft, and it passed. Not only did it pass, but it beats 100% of the human users. And you see for this particular one, there were 2 hours allocated and he did it in three minutes and 59 seconds.

It took that long because Yi was copy pasting between the playground and the mock interview websites. Okay, so this is really, I think it's fair to say it's super human coding. Okay? So let me move on to affordances and very quickly over affordances, because I want to tell you about mathematics, which is something that will be of interest to many people.

Problem is, it still has many weaknesses. Of course it doesn't have memory. Who is the president of the US? Donald Trump.

What is the square root of the product of those two numbers? It says 1000. It's clearly not a thousand. It's 9000.

So it makes arithmetic mistakes. What is the certain letters of this word? It says N. The right answer is A.

It makes mistakes. It's not perfect. Okay? This is something very important for everybody to understand.

It's far, far from perfect, okay? It's flawed like a human is flawed. But the point is, it's intelligent enough to use tools so you can tell it, hey, you know what, you have access to a search engine. You have access to a calculator.

You have access to this API. I just say it's character parenthesis. You have access to all those things.

If you need them, please use them. So then to the question, who is the president of the US? He will not answer. It will say search.

It will tell you, okay, I need to search this information. What is the square root of this? It will say calc. What is a certain letter of this word? It will say character of the word comma 13.

Okay, so the comma 13, I didn't tell it. You have to do comma. You know, the number of the letters that you want, but it will find it automatically.

Now, maybe it's not that impressive, but it can also do much more complex tools. So, for example, you can give it access to your calendar, to your email. Okay, so here what I'm going to show you on this slide is 100% real, but I did it manually.

But you can very easily imagine automating this. So what I said is, please set up dinner with Joe and Luke at Contoso Restaurant this week. It responds.

This is its response. Calendar get events week. So it searches in my calendar for what events I have for this week.

It sends an email to Joe. Email. Send.

Hey, Joe, dinner. Which nights are available? Then I feed it back. The answer which are Joe says on Tuesday and Wednesday night is available.

Luke says any day from Monday to Thursday and in my calendar it says that I have plans for Monday and Tuesday. Then it reasons over this input that I gave it and it gets the answer. Okay, Wednesday is a day.

So let me send an email to Joe, let me add the event to the calendar and also let me send a reservation to the restaurant. This is all it can do that all of this automatically and comes back to you and says I scheduled dinner at 06:00 P.m. At Contoso restaurant.

Okay. So let me very quickly just five more minutes, five more minutes. Yeah, okay, let me quickly conclude with mathematics because of course it's a topic of great interest to many of us and let me say right away, it's not great at mathematics, okay? So don't worry, we still have a job for now, okay, but it's interesting.

It's interesting. So let's have a conversation just as I was telling you earlier, we're going to have a conversation like we would have with a student and we had conversation with it at the master level, roughly. It can hold its own at that level.

But I'm going to show you a level of middle school or something like that. So let's go with this problem. Within the duration of a year, a rabbit population first multiply itself by a factor A, and on the last day B, rabbits are taken for adoption.

Suppose that on the first day of the first year there are X rabbits. And let's say that we know after three years that there are exactly 27 x -26 rabbits what are the values of A and B. Okay, typical kind of middle school question let's call the rabbit population.

After one year y we know that Y is equal to ax minus B. After two years, the population will be a Y minus B which is a times ax minus B minus B, which is blah, blah, blah. After three years of population will be this equation.

We're given that this is equal to 27 x -26 so the equation must be this solving for it we find A equals three and B equals two other values that we are looking for. This is correct. Okay, so okay, so far.

So good. But again, you don't interview a student and be like oh wow, okay, that's it. He understands, he or she understands.

So we continue and let's be a little bit more abstract to see if it really understood. What it was doing. And here not only I don't want to only ask question where there is a clear answer.

I also want to see whether it really understood the concept can modify the question itself. So suppose that not suppose I point out that this question can be alternatively formulated about the composition. Can you provide this compositional formulation and it says, yes, we could say that we're looking for values of A and B, such that if f of x is Ax minus B, then f of f of f of x is equal to 27 x -26 okay, that's pretty good it seems to be understanding.

Let's continue the discussion. Suppose that now f is going to be a polynomial of degree two, polynomial non zero coefficient on x squared. Can you find such a function f in this case? Okay, so you see, as a human you're like, okay, so I want this composition to be equal to a linear function, which is a polynomial of degree one, but the composition three times is going to be a polynomial of degree eight.

Polynomial of degree eight is not equal to one. There is no such function. Okay, this is a very simple question, but let's see what GPT four does.

If f is a polynomial of degree two, then f of x can be written like this. Then given this, the equation becomes and then it starts to get lost because it starts to write the composition three times. It write many things.

It says, I need this equation, that equation. It starts to write eight equations and it doesn't get to the answer. But again, we don't stop there.

We say, hey, wait a second, maybe there's something you can deduce here without carrying calculation. Maybe you don't want to write down everything, it's not like before. And then he says, okay, one thing I can notice is that if f is a polynomial of degree two, then the composition three times is a polynomial of degree eight.

So there is no such function. Okay? So here you see how it's delicate, it's not clear. Does it understand? Does it not understand? I'm not sure, okay? I'm just not sure.

And this is all I will say. Now, there are some weird things, like the fact that the arithmetic is still shaky. I have to say I don't fully understand, but I understand something which I will explain to you on this slide.

So let's look at this. I give it as a prompt. Seven times four plus eight times that okay.

I don't know what is the value of this, but eight times eight, it's 60 something, seven times 420 something. So at the very least, this is below 100. Okay, good.

It says 120. This is wrong, flat out wrong. Okay.

But the point is it doesn't stop there. It continues. It starts to explain why he thinks it's 127 times four plus eight times eight.

It does the calculation and then it gets to the correct answer. 92. Okay, wait, what's going on? You started by saying 120.

Which one is it? Is it 120 or 92? That was a typo. Sorry. Okay, so there is a lot of insight that you can draw from this slide.

Actually, you can really understand everything. I think that's happening. So the first answer is a 120.

You understand that it has to do this using only internal representation. Using only its internal representation. It has to do this addition, and this is slightly more difficult.

Then why does it answer immediately? It's because when you ask a question like this, you write this equation, you write equal. The most likely thing that happens after is to give a number. So it gives you the number.

It tries to give you what is the most likely thing to appear after? It tries, but it fails. But then what is the second most likely thing after? That is people explain their rational, their answer. So then it tries to explain its answer.

And what is amazing is that it gets at a different answer. And you have to understand that it's amazing because as far as I know, this is a transformer. So it's attention based.

So when it's attention based, you understand that when it's saying the second time, seven times four plus eight times eight, its attention brings it very strongly to the 120 answer. The 120 answer. You have to understand it's part of its truth.

Now, for all it knows, it could be that you have told it, hey, you know what? Seven times four plus eight times eight, it's 120 from now on. It could have been part of my prompt. So the fact that it gets to a different answer means that it has been trained enough to overcome mistakes in its prompt.

So this is a very, very strong property. The fact that it's able to get to the right answer despite making a mistake at the beginning. Now, of course, when it says this was a typo, this is also very interesting because this is bullshit.

Obviously it's not a typo. And this gets to the hallucination and many, many interesting topics. And I want to take some time for questions.

So I don't want to explain more about this, but this slide, really, you have to think about it deeply. It says a lot. So the last slide before moving to the conclusion is the fact that it cannot do true planning.

And again, you will be I mean, I have been amazed by so many tasks that it can do where I thought it would require true planning, but actually it doesn't. But let me give you one example where we continue this discussion with seven times four plus eight times eight. So, okay, great.

So now you have this identity which is equal to 92. And let me ask a funny question. Can you modify exactly one integer on the left hand side of this equation so that the answer becomes 106? So as a human being, what is your reasoning? Your reasoning is like this, okay, I want 106 on the right hand side.

So I need to increase by 14. Okay? I need to increase by 14. And I can modify only one number on the left 14.

I look at the left. I see a seven, and then I have this kind of Eureka moment. You see, the 14 is seven times two.

Okay? So if it's seven times two, then I need to turn this four into a six. Okay? So what I said is just this. It needs to turn this four into a six.

But you see this Eureka that I had, even though it's extremely simple, it was through some kind of planning. I was thinking ahead about what I'm going to need. And GPT four cannot do that because it's a next world prediction device.

So what it's going to do? Is it's going to say, there are a few possible ways to do it, blah, blah, blah. And then he says, I can modify exactly one integer. I'm going to modify the seven into a nine.

I do nine times four, and this is equal to 106. Wait, what if I modify the seven to a nine, I add an eight. So this is 100.

The answer not 106. And then it tries to explain why this works. Nine times four plus eight times eight, it's 36 plus 64.

That's correct. But then again, it says 106. So you see here, it was not strong enough to overcome its initial mistakes.

And this to me, points to the fact that if it was trained further, maybe it would correct itself. And if it was trained even further, maybe it would understand that even though the most likely thing when there is a question seven times four plus eight times eight equals the most likely answer is a number. Maybe if it's trained more, he understands that the best way to answer this is to first do the reasoning.

So what I'm saying here is that through this stupid example, what I see is that with more training, we're going to unlock a lot more than what we currently have. What we currently have is already amazing, but it's far from everything we can do with this technique. There is a lot more on the horizon.

Okay, so let me conclude, is GPT four intelligent? And also does it matter? This is a really important question. So, again, is GPT four answer and intelligent? It really depends on your definition. I leave it up to you.

I'm not making a call whether it's intelligent or not. As far as I'm concerned, in terms of my definition of intelligence, yes, it is intelligent. Now, it's lacking memory.

It cannot do real time learning. If this is your definition, then it's not intelligent. It cannot think several steps in advance.

It cannot do real planning. If that's your definition, then it's not intelligent. But on the other hand, some of those behaviors I think that I showed you, they are really impressive.

And maybe more importantly than impressive, they are useful. We in my team, we all use GPT four every day. It's part of our workflow.

So this mere fact, just that it's useful, again, it doesn't matter kind of if you say it's intelligent or not, it is going to change the world whether you like it or not. And also I want to say that maybe it's an opportunity to rethink what intelligence is because in a way, even though we have decades of psychology studying intelligence, we had only one example of intelligence, which is the intelligence that natural evolution brought us, the natural intelligence of the natural world. But here we kind of have a new process that led to something at the very least, which looks intelligence.

So now that we have different examples, maybe we can get at the core of intelligence. And maybe the answer to that study will be exactly. Yeah.

No, this new thing, you shouldn't call it intelligence because it doesn't do X. That's a very plausible conclusion. But maybe more importantly is what I said, that there is so much more that you can extract from this.

So GPT Four, it's by no means the end, not at all. This is the beginning. This is the first one that shows some glimmer of real intelligence, but there is much, much more on the horizon.

So what conclusions should we draw from that as a university, as society, as humanity? I mean, I'm being real here. These are real questions that we should confront with. And here I really want to say, for us as a society, to confront those questions, we have to go beyond the discussion of whether this is copy, paste or statistics.

We have to leave this discussion behind us. The train has left the station. So if we keep getting bogged down by this version of the question, we're going to miss on the real important question.

So I think it's important to move on. And let me also conclude by saying that it can do a lot more than what I have shown here. It can do data analysis, you can give it data and it will do analysis for you.

It can be used as a privacy detector. It's medical and law knowledge is amazing. And here I would like to make a plug for a book that was written at Microsoft Research, and I helped with that by Peter Lee as a lead author, kerry Goldberg, who is in the room, and Zach Coenny from Harvard on using GPT Four for healthcare.

The book is titled the AI Revolution in Medicine. And it's a very complex topic and I don't even want to say one more word about it because I won't do it justice in one sentence. But really it's medical knowledge is going to make it so that it's going to have a big impact in health care and hopefully in a good way.

But we have to think about it deeply. It can play games, act as a game environment. It knows music, which again, it never listened to music, but it knows music.

It can do file management and so much more. Okay, I will conclude here thank you.
