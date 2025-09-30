# AI model example: a query tagger continued...

One option: Make an exhaustive list of all job titles, companies, locations in the world and try to look them up by splitting the string "software-engineer-jobs-in-san-francisco" on hyphens

**Pros**: Easy to implement after spending a lot of time collecting the data

**Cons**: Hard to change. Doesn't pick up new job titles automatically. Inflexible, and leads to a ton of if-else code to handle edge cases which grow as the dataset grows (thousands of lines to account for corner cases, different languages, etc). Doesn't work when the same word can map to multiple entities: For example: "Newton" maps to a company name as well as a location name
