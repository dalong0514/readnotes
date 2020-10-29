Figure 6.4

From UN demographics report.

Credit: United Nations, Department of Economic and Social Affairs Statistics Division

Think about what this means: certainly you’d expect the total number of deaths to change year by year; the overall population increases year by year, and the death rate changes as well—just much less than the overall growth in population.

OK, so now we have a slightly different question to answer: Can we find the CDC data from 2015 to be comparable with the UN data?

I noticed that in the CDC report I found above, the actual text in the paper was this:

In 2014, a total of 2,626,418 resident deaths were registered in the United States.

I know that these kinds of reports are often written from a template. (That is, the CDC probably just copied the report and plugged in the new numbers for 2015.) So I did this query to find the report for 2015:

[「In 2015, a total of * resident deaths」]

Notice that I changed the year to 2015 and used the * operator (for more details, see how to use the * operatorA) to match the new number for that year, and I double quoted the whole thing to find a match for this exact phrase.

Voilà! That takes me directly to the 2015 CDC report, where we find out that「a total of 2,712,630 resident deaths were registered in the United States in 2015.」

Let’s compare these numbers from the United Nations and CDC:

2014

United Nations	2,626,418

CDC	2,626,418

2015

United Nations	2,712,630

CDC	2,712,630

Notice anything odd about these numbers? Both the United Nations and CDC numbers are exactly the same! If you go back a few years, you’ll see more of this pattern. Which makes me wonder, Where does the United Nations get its numbers? From the CDC! (After looking around, I found that nugget in a footnote, of course.)

Which means that although you might think you’ve「double sourced」this data, this actually is NOT two different sources; the United Nations is just taking whatever data the CDC hands it.

You might be tempted to think that the United Nations is getting its data from a different US source; after all, it gives its data citation as coming from the「U.S. National Center for Health Statistics」in its「National Vital Statistics Report.」But when you look up the National Center for Health Statistics, you discover that it’s a department of the CDC. It turns out that it consists of the same people who collect the data in the CDC!

This is an interesting insight: the simple question, How many people die each year in the United States? turns out to have a more complicated answer. It varies by year, and as you might imagine, it varies depending on how you measure it.

WHAT? Isn’t a death a death? Can’t you just count death certificates?

Well, yes, but are you also counting people who disappear? What about US citizens who die overseas? Are they listed as a US death or a death in that country? Are you counting from January to January, or just one monthlong period and multiplying by twelve? Are abortions counted as deaths? Are stillbirths counted? What about people in Puerto Rico, the US Virgin Islands, and other territories? (Why are the Virgin Islands broken out into a separate line item in the CDC report?) What about military deaths in non-US locations?

As frequently happens, once you start digging into a research question, you learn a lot about the area. You learn the little details about your question that deepen your understanding of the question you’re asking. This happens all the time when we do our research questions; what starts out as a simple, straightforward question turns into something larger and with more nuance than you thought at the start.

In each of the questions I asked above, when looking for the definitions, you can often find the answers in the data commentary that’s usually at the bottom of the data set. (Sometimes it’s scattered around in the text itself.) But it looks like this, typically presented as footnotes in the article. Here’s an example from that UN data set (figure 6.5).

Figure 6.5

Credit: Wikipedia

The notes describe the properties of the data; in this case, footnote 36 in that report tells us that military and US civilians who die outside the country are NOT included in the totals.

In this instance, we found out that which year you’re asking about makes a big difference.

Now, what about that other question—the causes of death in the United States?

Those same reports also break down the causes by the percentages of all US deaths. From the CDC report on health issued in 2017 (with data from 2015), we find that the top five causes of death in the United States are:

1. Heart disease (23.4 percent)

2. Cancer (22 percent)

3. Chronic lower respiratory disease (CLRD) (5.7 percent)

4. Accidents (5.4 percent)

5. Strokes (5.2 percent)

The CDC illustrates this nicely with a chart (from the previous CDC reference). (See figure 6.6.)

As you can see, heart disease and cancer are the two largest causes of death, accounting for 45 percent of all deaths in 2015. CLRD, the next most common cause, is only around one-fourth as much.4

Figure 6.6

From a CDC report, National Center for Health Statistics, Health, United States, 2016: With Chartbook on Long-Term Trends in Health (Hyattsville, MD: National Center for Health Statistics, 2017), 18.

Credit: Centers for Disease Control

When I look back at my guesses (at the top of this post), I see my intuition was really wrong. Accidents of all kinds are around 5.4 percent of the total (which means that car accidents are less than that).

We may worry about mass murders or the latest version of the flu, but the big killers each year are heart disease and cancer. They are much more significant in terms of public health than anything else by far.

When you look at the causes of death over time from this same report, it’s a fascinating piece of data (figure 6.7).

What is so striking is how constant many of these numbers of deaths are. Why do roughly the same number of people die each year in accidents?

This chart also has good and bad news: we’re getting better at managing heart disease, but the overall cancer rate hasn’t changed much in forty years.

Figure 6.7

From a CDC report, National Center for Health Statistics, Health, United States, 2016: With Chartbook on Long-Term Trends in Health (Hyattsville, MD: National Center for Health Statistics, 2017), 18. Notice that the y-axis is a log scale, which means that a little bit of change going down (e.g., heart disease or stroke) is actually MUCH bigger than it might seem. That decline seems much less impressive than it really is. The improvement over forty years is amazingly good. Note also that CLRD is a new disease label that combines asthma, bronchitis, and emphysema. In 1999, the disease coding system changed to recognize those diseases as a cause of death, and separated out pneumonia and the flu into another category.

Credit: Centers for Disease Control

And of course, another big factor in the causes of death is age at time of death. People die of different causes at different ages. I saw a data table that suggested this, so I wanted to follow up and see if I could find a summary chart from the CDC. But how can I search just the CDC website? That’s easy; you use the site: operatorB, as in this query to search only the CDC.gov site:

[site:cdc.gov causes of death by age]

That led me to this chart (table 6.1) in the CDC chart collection for causes of death in the United States, which shows how people die for different reasons at different ages.5 While cancer and heart disease are the largest causes of death, they come into play only after age forty-four. Before that, you’re more likely to die of an accident.

Research Lessons

1. When looking at data, be SURE you understand WHEN it was collected and WHAT it’s measuring. As we saw, different sources all draw on slightly different resources from different times. This can make a big difference in your results. Remember also that if two sites have exactly the same data, they’re probably both using data from the same source, and that’s not the same as getting two different perspectives on the data.

2. Consider other factors that might influence your data; in this case, death rates vary a LOT by age. (They vary by other factors too, such as gender, race, and location—but I just focused on age here.) Be sure you understand all the aspects of the data that are important to you.

3. When you need the「next document in the series,」remember that those documents often use boilerplate language, which you can find with a fill-in-the-blank query like [「In 2015, a total of * resident deaths」]. This is an amazingly handy trick to remember when you’re looking for documents that have patterns of text that you know. You can use the * to fill in the missing text as a way to search for that kind of content, which is especially useful for series.

4. Be sure you know where your data comes from! I naively thought that the United Nations would have different data than the CDC, but noticing that its numbers are all the same drove me to check where the UN data came from—and it was from the CDC. This data is NOT truly double sourced!

Table 6.1

Top Five Causes of Death by Age Group 2015

Rank < 1 1–4 5–9 10–14 15–24 25–34 35–44 45–54 55–64 65+

1

Congenital abnormality:

4,925

Unintentional injury: 1,235

Unintentional injury:

755

Unintentional injury:

763

Unintentional injury:

12,514

Unintentional injury:

19,795

Unintentional injury:

17,818

Malignant neoplasm:

43,054

Malignant neoplasm:

116,122

Heart disease:

507,139

2

Short gestation:

4,084

Congenital abnormality:

435

Malignant neoplasm:

437

Malignant neoplasm:

428

Suicide:

5,491

Suicide:

6,947

Malignant neoplasm:

10,909

Heart disease:

34,248

Heart disease:

76,872

Malignant neoplasm:

419,389

3

SIDS:

1,568

Homicide:

369

Congenital anomality:

181

Suicide:

409

Homicide:

4,733

Homicide:

4,863

Heart disease:

10,387

Unintentional injury:

21,499

Unintentional injury:

19,388

Chronic low respiratory disease:

131,804

4

Maternal pregnancy complication:

1,522

Malignant neoplasm:

354

Homicide:

140

Homicide:

158

Malignant neoplasm:

1,469

Malignant neoplasm:

3,704

Suicide:

6,936

