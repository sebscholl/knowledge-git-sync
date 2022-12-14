# G.A.M.E Framework for Metrics
The GAME framework is a **4-step process that can define metrics for any feature or product**. For the remainder of the post, I will refer to a hypothetical “product” but feel free to substitute in “feature” whenever a “product” is discussed.

*MANTRA: Defining metrics is AS IMPORTANT as defining feature requirements!*

Good metrics quantify/measure the **actions** a user takes within the product to extract value and achieve their **goals**. Tracking these actions overtime becomes **metrics**.

The **GAME** framework is a mental model for developing and leveraging metrics. It follows the 4-steps and can be used to define metrics for any feature or product:

1. **Goals**
2. **Actions**
3. **Metrics**
4. **Evaluations**

## Goals
There are two types of *goals* to consider; User and Business goals. 

**User Goals**
- How will my users benefit from my product/feature?
- What problems do my users want my product/feature to solve for them?
- How will my users interact with the product?
- How will my users feel when they use the product?
- What is my vision for how this product will integrate into my users' life?

**Business Goals**
- What are the tactical or strategic business benefits?
- Will this product/feature increase revenue?
- Will this product/feature decrease cost?
- Does this product or feature make us more competitive?
- Will this product/feature lead to entering a new market?
- What does my business look like if this product/feature is successful?
- **4 Ways a Product can be Valuable to a Business**
	-> Increase sales
	-> Decrease cost
	-> Decrease risk (If a quantifiable risk impacts sales/cost and removing it helps)
	-> Improve opportunity (Changes that lead to increased opportunities)

## Actions
Actions should become a quantitative list of things you want your user to do within your product. Don't worry about numbers or trackability; you're still creating a narrative.

A sub-framework is the ARM framework which helps categorize the actions you aim to take. ARM stands for the following items, each of which you should consider whether one or more best represent your **goal(s)**.

**Acquisition & Activation**
- How will my prospective users hear about my product?
- What actions do my prospective user have to complete to become a user of my product?
- What actions do my users have to take to get value from my product?
- At what point is my product solving a real problem for my users?

**Retention & Engagement**
- What gets my users to come back to my product?
- What do my users do when they are engaged with and interested in my product?
- What are the actions that provide my users repeat value?
- How often does it make sense for my users to take those actions?

**Monetization & Revenue**
- What form of investment does my user purchase with, money or time?
- What actions do my users take for my product to start charging?
- If my product is free, what are the reasons my users will opt to pay for it?
- Do they pay me directly, or does someone else pay me when my users take action (e.g. ad/affiliate)?
- Do they pay me for every action (transaction) or do they pay me periodically (subscription)?

## Metrics
Once you've defined your **goals** and **actions**, it's time to start tackling metrics. And that said, there are different types of metrics, many of which are calculations using other metrics. However, think of this exercise as turning a qualitative user action into a measurable and trackable quantitative value.

**Direct vs. Proxy**
- Can the action be directly tracked?
	- Example, `clicks = direct`  while `views = proxy('Was it scrolled over?')`

**Individual vs. Aggregate**
- Can you group many actions for an overview, the separate out slices for later analysis?
	- Example, `total_revenu -> sum(revenue_by_product_line) -> sum(revenue_by_product)`

**Magnitude vs. Ratio**
- Does it matter more for you to measure the overall magnitude of the action?
- Should you track as a comparison using a ratio, whether it be a rate (per time) or a normalizing factor (percentage, per user, etc)?
	- Example, `total_revenue || avg_revenue_per_day || avg_revenue_per_customer`

**Intrinsic vs. Heuristic**
- Can you derive more knowledge from the measure intrinsically?
- Do you have to rely on heuristics for the metric to be valuable?
	- Example(intrinsic), `daily active users`
	- Example(heuristic), `paying users active in last 30 days`
		- Hueristic is when we need to label the meaning of the metric, such as "engaged user". There is no clear definition of "engaged user", unlike a count or aggregate. 
- How would you prove the effectiveness of acquiring new merchants on Facebook vs. Instagram?
- How will you know if a product is successful?

>BAD METRIC ALERT: It's important to parse out vanity metrics, as well as identify and account for where metrics can be gamed. Example, `Inflate page_views using pagination || slide shows.`

#### Sample Metrics 
Here is a list of popular metrics you can use and tweak if needed:
- **Mau/Dau** `monthly_active_users || daily_active_users`
- **Customer Conversion Rate:** `state_1 / state_2`
- **Churn:** `customers_lost / total_customers`
- **NPS/CST:** `survey_result`
- **Customer Lifetime Value:** `avg_order_val * purchase_freq * avg_lifetime`
- **Customer Acquisition Cost:** `marketing_spend / total_users`
- **MRR / ARR:** `subscription_revenue`


## Evaluations
Metrics evolve. Once you start collecting them, it's time to start testing them, analyzing them, and improving them. 

That said, the number one test of a metric is **DOES IT PROVIDE FUNCTIONAL USEFULNESS**.
- Example, `∆ in metric = false-positive || false-negative`
- Example, `(issue occurs == ∆ in metric)?`

At the evaluation stage, there is really the opportunity to step back an evaluate all parts of the **GAME**.

**Evaluating Metrics**
- Is the data trending in the way you expected?
- Is the metric stable over time?
- Is the metric flagging issues with your product and prompting further analysis?
- Are these the correct data points to collect?

**Evaluating Actions**
- Are these actions reflective of product, user, or business goals?
- Are you key actions telling the correct story about user behavior?
- Does you action set cover all emerging user behaviors?
- Are your actions safe from being "games" by users or teams?

**Evaluating Goals**
- Is the metric correlating to business or user success?
- Are your users happier when your metrics are positive?