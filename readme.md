# Asteroids ML Training Manual

This guide is meant as an experiment to help me learn about how to train and fine tune AI models. Additionaly, I'm trying out a new form of software development I'm calling book-first development. 

The rest of this readme is just explaining what I'm doing and why. If you want to jump into the actual tutorial go to (jbeers.github.io/asteroids-ml)

## AI Training With Asteroids

I was reasearching if I could finetune Qwen3.8 27B to play the classic arcade game Asteroids. In doing this I found that a far smaller AI could likely be developed to beat Asteroids. As I only have a 4060 I thought this sounded good! I do not know much about training AI models though so I thought I would explore more. Eventually I came up with a plan.

- Build a cli app to play Asteroids
- Use it as a training harness to train dedicated small models
- Use it to learn how to fine tune a LLM
- Implement a [model factory a-la Poolside](https://poolside.ai/blog/introducing-the-model-factory)

As I started to work through my research I realized I was really just creating tutorials for myself and that others might enjoy following the process. So now I'm sharing this with others.

## Book-First Development

In addition to wanting to learning how to train an AI model I had an idea for a new workflow for developing software. Everyone is excited about agentic coding but it does have some short comings. I use to balk at the product managers who would constantly demand more features all while I lamented the failing health of my software baby. Fast forward to the now and here I am with an army of agents pumping out as many features as possible while I relentlessly crack the whip. Oh the irony.

Agentic coding has some problems

- Humans remain responsible but lack understanding
- We easily get carried away with the "implement more" mindset
- It is easy for all of our projects to become disposable rather than artisnal

So I had the idea - just because AI makes code cheap doesn't mean my software has to be cheap. How can I use my tokens in a way that makes the hard things easier, the expensive things cheaper, and the important things more reliable? 

My solution? Write a book.

I genuinely understand things better when I do my research wtih an AI companion that I can argue with and use to clarify. Everyone agrees that they make great "search engines". I genuinely struggle to know what is going on when I vibe code my 9th app of the day at 1:30 AM.

My hope is that my putting conversation first, then writing a book I will understand the problem scope far better. Once I get done writing the book I can generate a spec, roadmap, tests, and an implementation agnostic test harness. Once that is in place I can generate any implementation in any language I want and know that it follows my vision.

## Conclusion

Anywho, those are my hopes. I'm publishing this before it is ready so I can keep moving on things. There will probably be lots of broken things or stuff that doesn't make sense. I welcome all feedback and criticism and hope you enjoy the project!

Jacob