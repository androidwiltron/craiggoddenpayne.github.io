### As the saying goes, when you’re starting a software project, choose the best tool for the job!

This works so well, and for as long as I can remember, I have worked in environments where we are able to choose the right tool for the job by council.

There are many benefits of this such as it motivates the employee to feel like they've had input, it allows them to expand their knowledge as as an individual and research what is currently out there, building self confidence and increasing their skills. 

### What are the impacts when this is taken away?

Being forced to use a tool that someone doesn't understand, or not giving them the chance to understand it, or them knowing about a technology that would work much better just annoys the employee, it stems creativity and productivity also nosedives.

I have worked with people who will just sit and do what they are told and also "free thinkers" that want to change the world. 

I've seen in my career that the latter have always been the ones with the most drive, the most productive and have the most impact on a business, because they usually are a more well rounded individual and have the businesses best interests at heart.

They are most likely to embrace freedom of choice, and most likely to just ship when they feel oppressed, leaving the subservient developers behind.

### What happened to us?

Recently, I've been in a situation where I have gone from having the freedom and ability to choose what is best by council, to being told exactly what tech to use, from source control, to project management and now looks like even CI/CD. 

Decisions made with, what I can only understand as lack of experience, and not listening to the developers under.

This kind of micromanagement had a very negative on one of the best teams I have worked with.

### What changed for us:

- We were told to use Jira instead of Trello
- No pairing, and we are to duplicate tickets where pairing is involved
- We were moved from Github to BitBucket
- We were advised to use branch models, as they could be tracked better in Jira rather than using mainline, which affected CI/CD
- We have gone from having CI/CD where we can release many times a day to looking like a single release every 2 weeks
- We had evolving from scrum to #noestimates and breaking down work to equal sizes to being moved back to scrum estimating 1 point as 1 day
- We no longer found solutions to problems, tickets were solutionised for us, and we had to just build the code
- We were moved from Kanban to Scrum
- Our workload went from identifying problems and solutionising ourselves and working on features, to being told to fix a certain thing, not being involved in proper sprint planning, no sprint goal.

bearing in mind that we were also told in the same breath, that we were given a hard deadline to deliver some functionality, and "we need to put the fire out before we start building new things"

As you can imagine, 6 employees (out of 9) left within a couple of months, and every decision was questioned with very vague answers such as "we are an atlassian company, we should be using all atlassian products"

FACEPALM

### Decisions we made recently:

- Working on a dashboard, which displays graph and tabular summaries of data. It has to get this data from elasticsearch and many apis. We chose GraphQL for its ability to do just that. 
- On the dashboard we needed a pie chart, a bar chart, and a map view. For these we did some research and chose Chart.js 
- The dashboard had to be responsive, reacting to various changes and user actions. For this we used react.