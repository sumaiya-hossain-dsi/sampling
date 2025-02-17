# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Sumaiya Hossain

## **Analysis of Sampling in the Model**
The simulation model in `whitby_covid_tracing.py` demonstrates how contact tracing can create a biased sample of COVID-19 cases by disproportionately identifying infections from large, structured events (e.g., weddings) over smaller, less structured gatherings (e.g., brunches). 

### **Stages of Sampling in the Model**
#### **1. Event Simulation (`simulate_event(m)`)**
- The model consists of a fixed number of people who attend various events.
- Two types of events are simulated:
  - **Weddings** (large, structured, easy to trace)
  - **Brunches** (small, informal, harder to trace)
- Each person at an event has a **10% infection probability**, modeled using a binomial distribution (`np.random.binomial`).

#### **2. Primary Contact Tracing**
- Once infections occur, a **20% probability of being traced** is applied to each case (`TRACE_SUCCESS = 0.20`).
- This step creates **sampling bias**, as only a fraction of cases are recorded and linked to an event.

#### **3. Secondary Contact Tracing**
- If **two or more infections** from the same event are traced, the model assumes a full investigation of that event, identifying **all infections** at that event.
- This further **amplifies the bias**, as large, structured events like weddings are disproportionately overrepresented in the traced sample.

#### **4. Repetitions in Simulation (`repetitions = 1000`)**
- The simulation runs 1000 times (`for _ in range(repetitions):`), aggregating results to produce a final histogram.

## **Comparison to Whitby’s Blog Post Results**
Running the script as provided produced a figure closely resembling the one in Whitby’s article. The histogram clearly showed an overrepresentation of infections from weddings in traced cases, confirming the bias described in the blog post.

## **Reproducibility Analysis**
To test reproducibility, we reduced the number of repetitions from **1000 to 100** and observed the results across multiple runs. The histograms varied significantly, indicating a lack of reproducibility due to the stochastic nature of the model.

To fix this, we introduced a **random seed** (`np.random.seed(42)`) before any random operations. This ensured that the model produced identical outputs across multiple runs, improving reproducibility.

## **Final Modifications for Reproducibility**
1. **Reduced repetitions to 100**: 
   - Highlighted the variability of outputs in stochastic simulations.
2. **Introduced `np.random.seed(42)`**:
   - Ensured consistency in results across multiple executions.
   - Made the model **fully reproducible** while maintaining the original bias effects.

## **Conclusion**
This exercise demonstrates how sampling bias arises in contact tracing due to the disproportionate tracing of large, structured events. It also underscores the importance of reproducibility in simulations, which can be achieved by setting a **random seed**. The final modified script now produces **consistent** results while accurately reflecting the bias in the original model.



## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 16/02/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
