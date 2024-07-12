# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Yuliia Makushenko

```
I. Identify sampling stages in the model:
1. Infection simulation: Simulates how infections spread among people attending events. A random subset of attendees is infected based on the ATTACK_RATE parameter (set at 0.10). This is done using np.random.choice to randomly select which individuals get infected.
2. Primary contact tracing: After infections occur, this stage randomly decides which infected individuals get traced based on the TRACE_SUCCESS parameter (set at 0.20). np.random.rand generates random values to determine if each infected person is traced.
3. Secondary contact tracing: If two infections are traced back to the same event (controlled by SECONDARY_TRACE_THRESHOLD set to 2), all attendees of that event are tested. This stage involves sampling events based on attendance and tracing thresholds.
The sample size is 1000 individuals.
The sampling frame is 1000 individuals.
The underlying distributions:
- Infection probability distribution;
- Primary contact tracing distribution;
- Secondary contact tracing distribution.
Relation to blog post procedure:
1. The model simulates events where people gather, similar to social gatherings mentioned in the blog post (e.g., weddings, brunches).
2. It simulates how infections spread among attendees, similar to the blog's discussion on infection scenarios in different settings.
3. Primary contact tracing in the model reflects the challenges discussed in the blog regarding the effectiveness and limitations of tracing efforts.
4. Secondary contact tracing reflects the intensive tracing efforts described in the blog to identify cases linked to specific events.
5. The model calculates proportions of infections and traces attributed to different event types, highlighting biases in perceived infection sources due to tracing efficiency.


II. Comparison the Python script file as is with original blog post: The Python script was run as was with the number of simulation repetitions 1000.
Infections from Weddings. Frequency distribution: the highest frequency (~460) is centered around the 20-26% range, another significant frequency (~380) is centered around the 14-20% range. The weighted average of infections from weddings is approximately 20%. The distribution and frequencies of infections from weddings in the code as is reproduces those described in the original blog post.
Traced to Weddings. Frequency Distribution: almost equal frequency of cases centers around 20-25%, with a slight preference for 20%. The distribution and frequencies of traces to weddings in the code as is also reproduces those described in the original blog post.
The distribution patterns and frequencies for both "Infections from Weddings" and "Traced to Weddings" match the descriptions, confirming that the script is functioning properly.


III. Reproducibility check: The Python script was modified to increase the number of simulation repetitions from 1000 to 5000, and running multiple times.
Infections from Weddings: The graphs now show that the highest frequency is centered around the 18-23% range. This pattern closely matches the original blog post's results.
Traced to Weddings: The graphs display frequencies almost equally concentrated around 14,5% and 24,5%, with a slight preference for frequencies up to 22%. This also closely matches the original blog post's results.
With the increased number of repetitions (5000), the code appears to reproduce the results much more closely to those in the original blog post. The graphs for both "Infections from Weddings" and "Traced to Weddings" cases practically repeat the result in the original blog post, showing high reproducibility.


IV. Ensuring reproducibility:
1. Add the seed setting inside the simulate_event function to guarantee that the same seed is used for each simulation. It should be done before any random operation inside the simulate_event function to ensure each simulation run is identical, regardless of the overall script's randomness state.
2. By passing a unique seed to each simulation run (seed=10 + m) ensure that each run of the function uses a unique but consistent seed. This guarantees that the same random numbers are generated for each run of the loop, making the output reproducible. By initializing the seed inside the simulate_event function, we ensure that any random operations within the function use this seed, making each simulation reproducible.
3. Run the script multiple times. It should produce the same output, ensuring reproducibility.

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
