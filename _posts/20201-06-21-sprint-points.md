---
title: Sprint points
category: foundations
layout: post
---

# Sprint points
Story points are an Agile estimation technique that gives you a relative estimate of how much work and effort will go into a particular task.

## What is Agile?
Agile is a project management approach that has been widely used in software development and project delivery. It breaks down the entire project into shorter development cycles (called an iteration or sprint), which lasts only about 2-4 weeks.

The main goal of the [Agile methodology](https://clickup.com/blog/agile/agile-project-management/) is to involve customers at every step of the development process. 

How does it do that?

At the end of every iteration, you develop a version of your product called an increment. You present this increment to the customers for their feedback.

You then incorporate this feedback into your next iteration planning process and repeat until you have a final product.

## What Are Agile Story Points?
Before we talk about what a story point is, we need to understand two terms: ‘user story’ and ‘product backlog’ 

* A user story is an informal explanation of features that your user wants in the system.  A real-world user story example is: “As a gamer, I want my hero to be able to fly.” 

* A product backlog contains a list of every user story that needs to be worked on and implemented into the final product.

A `story point` is a unit assigned to a user story to express how much time and energy would be required for that job.

It’s sort of like the difficulty level in a game. A higher number means a more difficult level.

However, this is where most people get it wrong. In a video game, level 2 doesn’t necessarily mean it’s twice as difficult as level 1. But that’s not the case in story points.

Story points are a relative estimation technique (also called relative sizing). 

Relative estimation means that values are assigned on a comparison basis. That means there are no standard units for story points.  

For example, if a user story A has a point 2 and user story B has a story point 1, it’ll mean that A will take twice the amount of effort as compared to completing B. So, story points have one similarity: points of reference.

For example, let’s say two teams are building two similar puzzle mobile games. Level 10 in the first puzzle game wouldn’t necessarily be as difficult as level 10 in the second puzzle game, right?

Similarly, your team could assign a story point value of 8 to one user story, and another team can make a point estimate of 13 points to a similar story. The value of your story points is totally dependent on your team and your task.

Story points allow you to calculate team velocity and estimate work in an objective way.

## Story points values
0.5, 1, 2, 3, 5, 8, 13, 20, 40, 100

### What Goes Into a Story Point?
The Agile Methods like XP(`Extreme Programming`) and Scrum have a planning phase for development team members to discuss each prioritised backlog item and collectively estimate the effort involved to complete, and then make a Sprint forecast outlining how much work the team can achieve within the Sprint. The collective effort estimation is where story points come in. Story points represent the overall effort required to fully implement a product backlog item or any other piece of work. In the Scrum literature, the effort is a multi-facet construct consisting of risk, complexity and repetition.

![effort in Scrum](/wiki/assets/img/effort.png)

Because story points represent the effort to develop a story, a team’s estimate must include everything that can affect the effort. That could include:
- The amount of work to do
- The complexity of the work
- Any risk or uncertainty in doing the work. You should consider dependencies you might have as you work, these can be both internal (i.e. an MS someone else developed and you have no prior knowledge of) and external (i.e. a third party integration such as Auth0)

When estimating with story points, be sure to consider each of these factors. Let’s see how each impacts the effort estimate given by story points.

### Consider Everything in the Definition of Done

A story point estimate must include everything involved in getting a product backlog item all the way to do.

- Docs (If required)
- Tests (unit, integration tests)
- PR

## Team velocity can be calculated
Your team’s [velocity](https://clickup.com/blog/agile/velocity-chart/) is an important metric that you simply can’t ignore. 

By calculating your team’s velocity, you can visualize:

* Efficiency of your Agile team
* Speed at which your Agile team is progressing 
* You can make better predictions for your future project schedule.

### Velocity
The velocity (also called sprint velocity) shows the amount of work that has been done in each sprint. It’s the total completed story points divided by the total number of sprints.

For example, let’s say that your team finishes 50 story points in 2 sprints. 

Then, their sprint velocity will be (50/2) = 25 points per sprint.

## Estimate without specific time-commitments
Things don’t always go according to plan, even in an Agile project.

And when you’re using a time estimate, you’re only specifying an approximate time. You might spend more time on tasks that you thought would be completed in a jiffy, and vice versa. 

The bottom line is, it’s difficult to estimate the precise amount of time needed for a technical task.

Since story points are an Agile estimating method, they make no definite commitment (like within one week or next Friday). Instead, they provide a relative estimation of the overall effort that’ll go into a task.

This will help reduce the unnecessary stress of meeting tight, unrealistic deadlines. Instead, you’re left with a far more reasonable and accurate estimate.

## Story points aren’t subjective
Sometimes, people differ in their estimations for how long a task in an Agile project is going to take. This often leads to subjectivity while using time estimates.

That’s why this approach doesn’t always provide an accurate estimate.

For example, a senior developer might assign a task ‘7 hours’ according to their standard, but it might take the junior developer 15 hours to complete that same task. You can’t compare a novice gamer to a pro programer!)

While calculating an Agile story point, the whole team sits together and decides what points to assign to the user story.

## Key Factors That Affect Story Points
### How much work needs to be done (story size)
Not every backlog item is equal; one product backlog item may require more work than another one.

For example, suppose there are two different backlog items:

* I want a new weapon for the main hero, Monkey King
* I want new weapons for all heroes

Which one do you think will take more time?

The second story, of course! Compared to it, the first story won’t take much work.

So the second story will get more points than the first one because of the greater story size.

### Risk and uncertainty 
EEveryproject has its risks and uncertainties, especially with certain types of backlog items.

For example: if the product backlog item involves working with a new framework that your team doesn’t have much experience with, that risk factor will increase the story point value.

### Complexity 
Complexity is definitely a very important factor for any Agile estimating technique. Here are two similar stories with different acceptance criteria:

* ‘I want a new costume for the character Geralt’
* ‘I want a new special attack for Geralt’

The first one is a piece of cake, just some tweaks here and there and voila!. The second one requires you to code a new special attack and see how it works in the game. Then, you’ll have to test for bugs.

Naturally, during the effort estimation process, such user stories clearly earn more points.

## How Story Points Are Calculated In Agile?
You can calculate Agile story points by creating a base story, choosing your scale and estimation technique, and then calculated accordingly.

Story point estimation is usually done by using a method called ‘the planning poker.’
### Set up the poker table (create a base story)
The first step of the estimation technique is to create a reference story or baseline story. 

It’s a completed user story from an earlier iteration cycle assigned with a story point value (generally 1 for simplicity). 

This will be your normalized story point. The product backlog is also presented with all the new user stories.

### Deal the cards (choose a scale for estimation)
There are two scales used for story point estimation:

Linear scale: contains natural numbers like 1, 2, 3, and so on
Fibonacci scale: numbers from the Fibonacci series like 1, 2, 3, 5, 8, and so on
For simplicity’s sake, most Agile teams tend to pick the Fibonacci series for their story points estimation.

In this estimation technique, the Fibonacci scale is then inserted into a table where you can assign any user story to a value.

Here’s how an estimation table looks like when the team first starts filling it in!
![sprint point table](/wiki/assets/img/sprint_points.png)

### Planning poker
Planning poker is an Agile estimation technique that focuses on general consensus. This estimation technique is also used for estimating things other than user story points.

During this Agile estimation meeting:

* Each estimator receives a set of cards containing numbers from the Fibonacci scale 
* One backlog item is presented at a time and estimators have a detailed discussion about it
* After the discussion is over, each estimator selects a card with a Fibonacci number 
* Everyone reveals their card together (just like poker, all cards on the table)
* If all the estimates match then the value is assigned
* If they don’t match, the estimators discuss further to reach a consensus

By the end of the planning poker, our table will be filled with user stories beside their assigned points. 

Expect the story point estimation matrix to look something like this:

![sprint point table fullfilled](/wiki/assets/img/sprint_points_full.png)

`Important Disclaimer!`

Many times when a team is nos sync, the person who will take a task will have the last word about the sprint point number to be assigned, remember that the practice makes you perfect and no one should force you to have the same rhythm also if you are starting with a new team.

Sprint points technique allows you and your teams to become technically equal when time passes and is a very flexible technique.

### Calculating team velocity and planning project schedule 
After the estimation meeting, the [sprint backlog](https://clickup.com/blog/sprint-backlog/) is created after a backlog refinement session, and the team works on the stories.

The story points Agile help you track the team’s performance and make better forecasts.

After the first sprint is over, there’s a sprint [retrospective meeting](https://clickup.com/blog/scrum-meetings/).

This provides you with the data to calculate the team velocity (the number of story points completed during a sprint).

Once you get the sprint velocity, you can determine how many sprints it’ll take your project team to complete the whole project. 

Iif your Agile project has a total story point estimate of 480 and your actual velocity is 48, then you can calculate that it’ll take your team 10 sprints to complete the entire project.

This makes it easy to plan your Agile project schedule.

## Ways of Estimating Story Points
The effort estimated in a Sprint is a latent concept, meaning cannot be directly observed or measured, unlike observable concepts such as temperature and distance. Therefore, it is not surprising to see different even contradictory views on how effort should be estimated, particularly if story points should be a function of time.

Due to the different views on the story point and the under-defined steps to estimate, it is not surprising to observe several methods used to estimate story point in practice.

### Use the First Story as a Benchmark
Assign a number for the first story. Any other story in this Sprint will be compared to the first story. Future Sprints will repeat this process and align on the same scale. For example, if a story is about the same amount of work as the one you have already sized, give it the same number of points. It is clear that the effort estimation is done relatively.
#### Pros

* The human brain is good at comparing, and therefore, this method has a less cognitive load.
* Since only need to compare with the first story, the estimation is relatively lightweight in cognitive processing and time-efficient.
* Independent to development time, this method rewards team members for solving problems and focus on value delivery.
* The story points are in the interval scale and are meaningful in summation, subtraction, and medium. The interval scale is sufficient for the velocity calculation.

#### Cons
* The initial point assigned to the first story is entirely arbitrary. Even though the value doesn’t matter as all the following points are assigned relatively, the initial point and story do matter as they set up the story point system’s scale.
* Although it is easy to compare the efforts between tasks, it is difficult to gauge the magnitude of difference as the numeric values don’t pertain to anything directly measurable/observable.
* This method doesn’t translate from story points to the time required to completed and therefore, couldn’t answer a common question from stakeholder: how long will feature A be completed?


### T-Shirt Sizes
Use multiple sizes such as extra-small (XS), small (S), medium (M), large (L) and extra-large (XL) to estimate the effort at a high level. Each size corresponds to a value from the Fibonacci sequence, e.g. XS — 1, S — 2, M — 3, L — 8, XL — 13.
#### Pros
* As it gives a quick and rough estimate for how much work is expected for a project, it is time-efficient.
* Independent to time, this method rewards team members for solving problems and focus on value delivery.

#### Cons
* It is unclear how risk, complexity and repetition attribute to the size estimation, and therefore difficult to achieve consistency over time.
* The nature of the various T-Shirt sizes is ordered categories, corresponding to the ordinal scale. When converting to the Fibonacci sequence as story points, the value assignment is arbitrary. Someone can easily challenge why a size gets assigned to one value instead of another.
* The summation, subtraction and average on the story points are not meaningful, e.g. Does the difference in effort between a medium size story and a small size story is an extra-small size story? What does velocity as 20 story points mean, e.g. two large and two small stories?
* This method doesn’t translate from story points to the time required to completed and therefore, couldn’t answer a common question from stakeholder: how long will feature A be completed?

Note: Some other methods refer to effort different from T-Shirt sizes, such as animals and gummy bears. Essentially they’re the same idea.

### Use Ideal Hours or Days
This method is from the XP methodology. For each story, the delivery team discusses how many ideal days or hours it requires. The ideal day or hour, using the Fibonacci sequence, can be based on the average time a dev needs, or the time an average dev needs. To determine when a feature can be finished, we can use a load factor (i.e. an ideal day equals to 3 actual days) or a percentage (i.e. assume in a day, we only have 70% of the time to do actual work) to convert the ideal days or hours into the actuals.

#### Pros
* Using ideal hours or days to estimate effort promotes story points to the ratio scale. This allows meaningful comparison between story points in various ways, such as summation, subtraction, multiplication, division, medium, etc. For example, a story with story points as 8 means 4 times more effortful to complete than a story with story points as 2. The ratio scale also allows producing any metric of interest, e.g. error metrics.
* The measurement of effort is more well-defined and easy to explain.
* The three aspects of effort can be easily captured by time.
* Can directly generalise the average times needed for specific tasks, e.g. 2 ideal days for writing tests, 0.5 ideal days for documentation,

#### Cons
* Human is not good at estimating effort in time as we are inclined to overestimate our capability and thus, under-estimate the ideal days or hours needed.
* Management may hold the hours or days against the delivery team on why the development falls behind.


## Fuentes
* Peck H., C.(Noviembre 2020). *The Ultimate Guide to Agile Story Points(2020)*, ClickUp. https://clickup.com/blog/agile/agile-story-points/
* Fan S. C.(07 Enero 2021). *Best Way to Estimate Effort Using Story Points in Sprint Planning*, Serious Scrum. Medium. https://medium.com/serious-scrum/best-way-to-estimate-effort-using-story-point-in-sprint-planning-f43ad2d6fa91

