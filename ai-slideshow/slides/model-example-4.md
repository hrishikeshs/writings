# Steps involved in the query tagger
input: "software-engineer-jobs-in-san-francisco"

1. Tokenization & segmentation: Split on hyphens -> ['software', 'engineer', 'jobs', 'in', 'san', 'francisco']

2. Entity recognition: Detect that "software engineer" is a _job title_ and "san francisco" is a _location_

3. Normalization: Convert 'software engineer' to 'software-engineer' or whichever normalization scheme the system uses to de-dupe similarities

4. Id resolution/lookup: Map recognized entities to database ids (e.g: jobId: 345, locationId: 4562)

5. JSON structuring: Collect the above results into the structured output.

We will look at how a simple text classifier works in the next couple of slides.
