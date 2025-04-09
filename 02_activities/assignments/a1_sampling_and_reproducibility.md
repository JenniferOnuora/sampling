# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Jennifer C. Onuora

```
Please write your explanation here...

In the simulation code in 'Whitby_Covid_tracing.py', there are three major sampling procedures. 

The first sampling occurs during infection (related code;  infected_indices = np.random.choice(ppl.index, size=int(len(ppl) * ATTACK_RATE), replace=False)). This uses the 'np.random.choice' function to sample from 1000 people and randomly infect a subset of these people (100 people). The sampling frame is the full population of 1000 people (200 wedding and 800 brunch) creating a Uniform random sampling distribution without replacement. This relates to the sampling and the 10% assumption made in the blog post. 

The second sampling occurs during primary contact tracing as shown in the code; 'ppl.loc[ppl['infected'], 'traced'] = np.random.rand(sum(ppl['infected'])) < TRACE_SUCCESS'. In this code, the sampling frame is the infected individuals and the sampling is done using the np.random.rand() function. This code simulates whether the infected individuals are sucessfully traced and relates to the primary contact tracing also described in the blog. The underlying distribution here is Bernoulli trials with success probability of 20%, ie a 20% chance of being traced back to the source event, as defined in the blog post and as defined by TRACE_SUCCESS in the code.

The third sampling occurs during secondary contact tracking as shown in the code; event_trace_counts = ppl[ppl['traced'] == True]['event'].value_counts() and
events_traced = event_trace_counts[event_trace_counts >= SECONDARY_TRACE_THRESHOLD].index. In this code, events where at least SECONDARY_TRACE_THRESHOLD infected people were successfully traced. If an event (like a wedding) has enough traced cases, the entire event gets flagged and all infected people from that event are marked as traced.

I then ran the entire code in the 'Whitby_Covid_tracing.py' file and the generated figures appears to reproduce the image in the blog post. 

I modified the repititions from 1000 to 100 and ran the script several times. The graphs generated were very inconsistent and showed greater variation, and was different from the result from 1000 repetitions. This shows that reproducibiity is limited with smaller runs/repititons and requires us to set the seed for reproduciblity. 

I modified the code to ensure reproducibilty by adding this line of code 'np.random.seed(42)' and ran the code multiple times. This time around, the output produced the same results irrespective of the number of times I ran the code. 

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 09/04/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [x] Create a branch called `assignment-1`.
- [x] Ensure that the repository is public.
- [x] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions guidelines-for-pull-request-descriptions) and adhere to them.
- [x] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
