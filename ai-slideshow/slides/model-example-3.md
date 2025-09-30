## A better approach
 Training a text-classifier "AI model" which takes an input string and spits out structured output that looks something like:

```
 {
    jobTitle: "software engineer",

    jobTitleId: 456,

    location: "San Francisco, CA",

    locationId: 335555,

    confidence: 0.87
 }
```

The text classifier would be trained on a large amount of text, so the model
"learns" what terms are _probably_ job titles, and what terms are _probably_
locations. This model can then be queried by the server side code by passing it
the string "software-engineer-jobs-in-san-francisco". When the server gets back
the structured output, it can do a straightforward query to it's job postings
database, and return relevant responses
