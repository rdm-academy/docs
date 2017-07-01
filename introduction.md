# Introduction

In January of 2017, [Nature](https://www.nature.com) published [A manifesto for reproducible science](https://www.nature.com/articles/s41562-016-0021), an article describing the current state of reproducibility in research. The article cites a profound statistic estimating that **85% of biomedical research efforts are wasted** due to the lack of being able to reproduce the research. In the article, they identify a set of measures that they "believe will improve research efficiency and robustness of scientific findings by directly targeting specific threats to reproducible science."

One measure the authors propose is "encouraging transparency and open science" by making data, materials, and software available[^1]. The article introduces its importance by putting it in terms of credibility.

> The credibility of scientific claims is rooted in the evidence supporting them, which includes the methodology applied, the data acquired, and the process of methodology implementation, data analysis and outcome interpretation. Claims become credible by the community reviewing, critiquing, extending and reproducing the supporting evidence. However, without transparency, claims only achieve credibility based on trust in the confidence or authority of the originator. Transparency is superior to trust.

Making all relevant data, materials, and software available that contributed to producing the claims made makes the research transparent and enables anyone to independently determine its credibility.

*Transparency is superior to trust.*

## What is reproducibility?

To take a step back, what exactly is *reproducibility*? Leek and Peng describe reproducibility as "the ability to recompute results". They contrast it with *replicability* which is "the chances other experimenters will achieve a consistent result" and conclude that they are "two foundational characteristics of successful scientific research."[^2]

The distinction is that replicability assumes an independent method of reproducing the result whereas reproducibility involves the original methods used by the author to produce the result.

## Factors affecting reproducibility

At a conceptual level, a research workflow consists of several computational or manual (human) steps each of which made take data inputs and produce outputs. The research *concludes* once the hypothesis in question has been confirmed or rejected. Thus a model of this workflow can be expressed in terms of data, computation, and human processes.

Any one of these components in the workflow may have many factors influencing the likelihood or cost of being reproducible. Collectively, this has a compounding effect on the final result since differences in each output will affect all downstream results. Therefore it is important to understand the factors at play and how they can affect the reproducibility of research as a whole.

### Data

The first set of factors that will be discussed pertain to data. Data represents both the input to processes as well as their outputs. Data must be interpretable which means it must be able to be viewed or opened for interpretation.

For example, the humble CSV file is a text-based file format that can be opened and viewed on virtually every device without requiring special software to view it.

Contrast this with a similar and nearly familiar file format, Microsoft Excel spreadsheets. Although Excel is ubiquitous, it is not universal nor is it free and open. Thus if Excel is used as the file format to store data for a research workflow, any researcher wanting to reproduce the steps would require having a license to Excel possibly of a specific version in order to view the data[^3].

Beyond data formats, there more subtle issues like [character encoding](https://en.wikipedia.org/wiki/Character_encoding) which determines how certain text characters are encoded in the data itself. Character encoding is notorious for causing programs to throw an error or file viewers to interpret and render the wrong character.

For a growing list of reproducibility factors pertaining to data, see the [data section]() of the reference.

### Software/Code

Where there is data, there is software to process or analyze it, yielding new data for a subsequent step or results. While data is static in its role within a research workflow, software is inherently dynamic since it must actively take inputs and produce outputs. Any change introduced in the software can affect the output and thus has a higher chance of breaking the reproducibility goal.

---

[^1]: For a summarized table of these measures see [table 1 from the article](https://www.nature.com/articles/s41562-016-0021/tables/1).

[^2]: Leek, Jeffrey T; Peng, Roger D (February 10, 2015). "Reproducible research can still be wrong: Adopting a prevention approach". Proceedings of the National Academy of Sciences of the United States of America. 112 (6): 1645–1646. doi:10.1073/pnas.1421412111. Retrieved March 9, 2017.

[^3]: Fortunately there are a host of free and Open Source Excel parsers in a variety of programming lanuages that enable working with the XML-based format, but that requires additional effort and does not necessarily provide the same set of functionality as the native application.
