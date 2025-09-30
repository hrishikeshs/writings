# AI model example: a query tagger
A while ago, I worked on a system which had to show job search results if users
visited the jobs pages. The urls which users landed on looked like:
- https://linkedin.com/jobs/software-engineer-jobs-in-san-francisco
- https://linkedin.com/jobs/software-engineer-jobs-at-apple

When this request hits the server, we need to show jobs that are for: a) software engineers and b) In San Francisco.

For the second url, we need to show jobs that are: a) for software engineers and b) at the company Apple

How do we know that "software engineer" in this context is the job title?
How do we know that "San Francisco" is the location of the job?
How to know that "Apple" refers to a company?

We need to understand what the string: "software-engineer-jobs-in-san-francisco" **_means_** to serve relevant results.
