---
title: "citation standards"
date: 
draft: true
---

I have always been annoyed with existing citation standards that are arcane and arbitrary to the degree that you either need to check back against templates for each content type, or use some software tool that enforces its own structure on your citation to hide the complexity of the ultimate output.  

Is it possible to come up with a citation formatting standard that optimally balances this matrix of competing goals:

  - encoding efficiency for both human actors and code, which implies the need for an approach with a simple set of rules to keep cognitive load low,

  - decoding efficiency for both human actors and code, 

Code requires a fairly high level of precision to consistently decode data. Human actors can efficiently decode data that is much lower in precision.

With encoding standards like this, trade-off between two competing goals: making a format that is easily human readable, and a format that is also easily machine parseable.
An individual citation is a string of comma separated values, characterized by:

  1. citation metadata fields are separated by commas,

  2. commas embedded in field values should be escaped,

  3. line breaks are not allowed in field values, which I believe deals with our only other possible (but unlikely) issue,

  4. Field order is significant. For now, I would say that only the first two fields are 

Dates in YYYY-MM-DD format, and in cases where only part of a date is known, the missing values are zeroes. So "March 1916" would be encoded as "1916-03-00".



  if code is unable to parse the string as valid CSV, or parsing the 

Commas are the standard delimiter, and it is natural for human actors to use in this way.

Rule 1 is simple to remember and is equally friendly to human consumers as it is to code. Rules 2 and 3 really don't really add to cognitive overload because they are edge cases. Commas are not that common in titles to begin, and I think that as the person is in the act of typing commas anyway, typing one where it would not normally be should be an adequate 

A few more things not fully considered in the rules above: in the first two fields, what is the date being represented, and what is the role of the person whose name
But how to implement rule 2? On the one hand, a backslash is definitive, but may be a bit unfriendly to the many, and is certainly more disruptive than say, using double commas to indicate the escape. However, this doesn't fully account for a desire to indicate an empty value, and so rules may have to be added that every field must have a value

Citations have to be proofread regardless, and it could be argued that taking this structured approach can actually help expose encoding errors. 

Other common situations include a sources that request that you use their preferred citation format. Obviously, multiple sources can request conflicting formats, and some will adhere to their own judgement, and I have experienced these situations personally. And there have been times where it just makes sense to include some piece of data, or format data in such a way, that is simply going to be non-standard no matter what. But these issues are not unique to my approach either obviously. 

The way I am inclined to handle this in my approach is to favor the needs of the human actor and prefer a less structured approach that can accommodate a significant level of chaos. One of the most obvious ways that this would manifest would be in allowing sparsely populated citation strings to make make basic encoding and decoding much more efficient. The human is the actor that we most immediately need to accommodate, and the approach is simple enough that code should be able to be fairly robust in the face of say, sparsely populated citations, or fail gracefully in more severe circumstances. 

So, for example, I think that as a general rule, any error or other unexpected state in code should result in the raw citation data being output, treating the raw string as a default output value, and trusting that the raw string will still be intelligible to a human actor, as it is designed to be. Certainly, dates in YYYY-MM-DD format are inaesthetic, but citations are not judged on their appearance, if they are judged at all, it is by their effectiveness as a tool, and I believe that dates in that format are no worse that dates in others, and in fact, these dates may actually be more user-friendly to a human actor from a purely utilitarian perspective.  

Additional thoughts: allow markdown formatting within fields? This is certainly an interesting possibility with obvious advantages, but equally obvious pitfalls. A basic style guide would have to be adopted, and perhaps this should also become part of the recommended conventions. Aside from the issues of enforcing the style guide, the additional cognitive load on human encoders starts to lean this approach heavily in the direction of recreating the arcane citation structures I was trying to avoid in the first place, and an even more devastating fault is that it immediately degrades the human-readability of the raw string, an essential feature I would like to preserve. Obviously, the option is there, and may make sense for your particular needs, but significant forethought is needed. (Perhaps including a migration plan for when you inevitably change your mind!) 

Ultimately, the exact order is not really all that important, although obviously, I think there are certain orderings that are more natural and logical. But again, human actors easily tolerate a high level of imprecision with this type of data, as patterns of dates, people's names, location names, page numbers, along with all the common formatting variations of each, are instantly recognizable. And although I would strongly encourage consistency as a sane cultural value, humans can tolerate a surprising amount of inconsistency in formatting and field order, because they are so adept at pattern matching. And when someone is looking up a citation, this is often done on a per case basis, they are certainly not comparing the formatting of one citation to another, and so I suspect it would take a significant degree of inconsistency to truly negatively impact human decoding in the majority of cases. 

This concept put another way: after a certain point, the benefits of greater precision and structure greatly diminish for humans but remain proportional for code. 

Design strategy: a minimal ruleset to handle the most common situations and needs encountered. By design, it does not seek to handle *all* situations and needs. In atypical situations, the approach can still be used, with the addition of minimal conventions needed for that particular situation. For example, requiring that all fields be populated, as discussed above, to allow for reliable importing into spreadsheets or parsing by code for the purposes of analyzing the citations themselves. Again, this is not a need most will have, but it can be accommodated easily. I think a requirement of any decoding algorithm should be the collapsing of empty fields, in which case, these added conventions would not break the output formatting code.

If all else fails, fail gracefully and acceptably, so that as long as the most basic rules are followed, the raw string output will likely be adequate for most purposes. 


> This sentence is one field value,, containing one embedded comma.



