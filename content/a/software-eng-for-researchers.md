*This content was originally posted on [bluesky](https://bsky.app/profile/leknarf.com/post/3l7iwxhnjbf2r), in response to a question from a computational neuroscientist professor asking for help with managing research software projects.*

There’s no silver bullet, but all software engineering projects are fundamentally research projects. Recognizing that, there are a lot of useful practices we can borrow from industry. I’ll try to summarize some of the key insights that are applicable to academic research coding projects:

The goal is to do things that are helpful and stop doing things that are harmful. You don’t need to do anything merely because someone claims it’s “the right way”. Relative to most fields, software is easy to change. Whenever you’re unsure how to proceed, prioritize moving quickly.

Regarding project management, the keyword “Agile” is popular. Much of this is written for a corporate environment and is irrelevant for academics. Please don’t feel you need to adopt a formal agile framework to get the benefits.

For research teams, I’d focus on the four “ceremonies”: planning, stand-ups, demos, and retrospectives. The retrospective is the most important. This is a regular meeting where you discuss what went well, what didn’t go well, and what should change in the future. This lets you iteratively improve.

The Atlassian blog has good material on the subject. I’d suggest starting with this description of the four “ceremonies”: [link](https://www.atlassian.com/agile/scrum/ceremonies)

As you read about Agile, you’ll inevitably come across the terms “Scrum” and “Kanban”. Both can work well. The key question is when you and your students prefer to check-in.

If you like to set soft deadlines (let’s do A, B, and C by next Tuesday), then you’ll like Scrum. If you prefer to outline tasks (let’s do A, after that’s done we’ll start B, and then we’ll move on to C), then you’ll like Kanban.

For managing software projects, it’s helpful to step away from the code and to instead view the project at a high level using tickets. I’ve worked with some software managers that never read code and exclusively manage software projects through the high-level view of the ticketing system.

The goal for both is to track what has changed, when, by whom, and for what reason. These tools are your lab notebooks. Research is inherently confusing and there’s always going to be uncertainty. Tickets are how you record your intentions and understanding as the project evolves.

Jira is the most popular issue tracker for industry work, but Jira is probably overkill for an academic lab. You might prefer Github issues, Notion, or Trello instead.

Machine learning projects are particularly difficult. In a traditional (non-ML) software project, you only need to track changes to code. With ML, you now need to consider the interactions of code, data, and ML artifacts (i.e. models).

An experiment tracker is essential for collecting and organizing all the combinations of results. WandB is popular because it’s easy to use (and free for academics). You might also consider Comet or MLFlow.

I’ll wrap up with some additional links that may be helpful:

- The good research code handbook, written by a computational neuroscientist
[goodresearch.dev](http://goodresearch.dev)
- MIT’s missing semester, summarizes basic skills CS students are expected to know: [Missing Semester](http://missing.csail.mit.edu)
- The pragmatic programmer, a classic and readable software engineering textbook [Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/)

