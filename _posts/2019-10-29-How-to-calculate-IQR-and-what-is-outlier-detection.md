---
title: "How to calculate IQR and what is outlier detection"
date: 2019-10-29 21:46:00
category: ["Data Analysis", "Data Engineering"]
tag: ["DescriptiveStatistics library",
        "IQR",
        "Outlier detection"]
---

Some system needs to find and deal with outliers item, people, objects, etc.

For example, we needs to show search movie results which people might interest. If so, we need to find boring contents among search results.

Let's assume we have fun score for all movie and fun score is Normal Population(N(0,σ2)). Then we can find extremely boring movie.

The outlier detection formula is

> Lower bound : Q1 - 1.5 * IQR  
> Upper bound : Q3 + 1.5 * IQR  
> Q1, Q3 could set 25%, 75% value of object range. IQR could calculate Q3 - Q1.

**Extremely boring movie < Lower bound < Acceptable movie < Upper bound < Extremely fun movie**

```java
import org.apache.commons.math3.stat.descriptive.DescriptiveStatistics;

@Test
public void getBoringMovieAndFunMovie() {
    double data[] = {53.75,  94.06, 52.12, 74.73, 69.79, 50.41, 71.51, 
                        86.33, 54.44, 58.21,  9.16, 42.09, 85.13, 59.51};
    DescriptiveStatistics da = new DescriptiveStatistics(data);
    double percentile75 = da.getPercentile(75);
    double percentile25 = da.getPercentile(25);
    double iqr = percentile75 - percentile25;

    double lowerBound = percentile25 - 1.5 * iqr; //13.23
    double upperBound = percentile75 + 1.5 * iqr; //115.78
}
```

After running the code, lowerBound of fun score is 13.23 and upperBound is 115.78.  
So, outliar of these movie is 9.16 movie and this one is **Extremely boring movie** according outlier detection formula.

