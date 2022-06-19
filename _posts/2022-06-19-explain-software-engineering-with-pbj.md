---
title: "Explaining Software Engineering with the Classic PB&J Problem"
sub_title: "extending the example to show realistic cases"
<!-- excerpt: -->
categories:
  - Technology
  - Education
last_modified_at: 2022-06-19
published: true
---

## The Common PB&J Problem

I'm sure we've all seen the common challenge given to students - ["Write instructions to make a peanut butter and jelly sandwich."](https://www.youtube.com/watch?v=HXl5f2azATU) Almost always, the students give some vague step or imprecise instruction and the instruction follower ends up doing something the student didn't intend to happen. I think there's definitely some weak spots in this example but showing students the step-by-step example of programming to achieve a goal holds well.

## Extending this to Software Engineering

Recently, I was thinking of ways to explain what software engineers do to family and friends and I came back to this programming introduction. At its base, the PB&J problem is a good way to explain "coding" and I believe we can extend this to exemplify common challenges software engineers face. We can start with a simple idea of loops, conditions, and failures and then we can even extend this to a scaling and grouping challenge. I think these extensions are great tools to explain more of the common complexities we face in our jobs.

If I'm explaining software engineering to someone who has heard of or done the PB&J challenge I try to add new complexities in layers. This helps people appreciate how problems can grow, complexities increase, and requirements change. I also find that older children and teens that find these extensions interesting and hard are usually the same ones who may really enjoy software engineering. 

### Student List - Loops and Conditions

The first extension is to take your PB&J function and think about how to use it to build PB&Js for the entire class. Will we just make one sandwich for how many people are in the class? What about absent students? Do we track who has gotten one so students can't ask for another?

These ideas demonstrate the complexities of looping, edge cases, and conditions. I think it's a great example of taking something like a "hacky" bash script and making it a little more dynamic to automate some menial task in your job. Someone who sees how this grows the challenge of the PB&J instruction are likely people who will also sink their teeth into programming quickly.

### Jelly Preferences - Dynamic Fields and Errors

Now that we've explored the idea of lists and conditions we can extend this challenge further. Suppose we have three jelly flavors (strawberry, grape, and blackberry). We have a list of what each student has written in as their chosen jelly and we need to modify our PB&J algorithm to support these jelly type selections. Is it easier if we make all of one type of jelly at a time? Do we need to check if that student is in class today before making their preferred jelly sandwich? What about the naughty student who wrote "chocolate" as their jelly choice? Do our brains explode or do we gracefully choose a default like strawberry? What happens if we add a new jelly or run out of one?

This modification to the challenge helps show how a software engineer needs to handle dynamic input and foresee problems that might happen. It illustrates how software can break and how engineers need to create fault tolerant, dynamic solutions. I think that people who pick up on these edges are great candidates for software engineers.

### School Cafeteria - Scaling and Databases

Our PB&J maker is now catching on in popularity and the school wants to use it in all classes. We need to further extend our instructions on how to get the student list and preferences from each classroom, determine the order to make them in, and make sure the correct sandwich counts get back to each classroom. Will students changing preferences between days cause issues? How can you write instructions for different people so that some can collect attendance and preferences while others make sandwiches?

This data lookup, grouping, and attributing is a great example of simple database interactions and how to consider scaling in a problem. I think that this extension is the best place for students and instructors to run wild with the possibilities of making the processes as fast as possible. Thinking about ways to scale this gets the engineering cogs turning.

## Potential Software Engineers

From these modifications students should start to see where the real complexities of software engineering come from. It's not always writing a simple instruction but rather the dynamic and ever changing requirements that make being a software engineer challenging and exciting. I believe that the people who grasp these complexities and can foresee how one might run into issues with them are the same people who may really latch on to software engineering. It really almost feels like a litmus test for software engineers.
