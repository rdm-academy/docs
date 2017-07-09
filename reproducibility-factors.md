# List of reproducibility factors

This is a growing list of high-level factors that may affect reproducibility in the short or long term. The theoretical goal is to have the results of some research be reproducible forever. Practically speaking, we are trying to maximize the likelihood of reproducibility by following best practices aggregated from the data management, software engineering, and library science disciplines.

*Please contribute to this page by clicking on the "improve this page" link above or asking a question on the [community discussion site](https://discuss.rdm.academy).*

### Table of Contents

<!-- toc -->

## Data

Data can be thought of as a materialized representation of input and output values of a process. This process could be a transformation of data, like reshaping it into a new structure, or an anlysis that computes some derived metric or result given the input. Even without knowledge of the process itself, observing the input and output data together provides some insight into what the process entailed.

#### Always download data from remote services as static inputs.
- This means to download and store the data as an input for your research workflow.
- Remote services include hosted databases in your organization or third-party services (e.g. Twitter). Since you don't control them, the underlying data may change at any time.

#### Use checksums to ensure the data hasn't changed.
- Each downstream file or result depends on the input data. A [checksum](https://www.google.com/search?q=checksum) is an easy way to determine if something has to be recomputed.
- This is especially important in a collaborative environment where multiple people may be able to change the data file.
- A checksum will protect against confusion about why a downstream result has changed from "yesterday".

#### Use common, non-proprietary, and cross-platform data formats.
- [Don't use Excel](./ref/microsoft-excel.md) as a file format to store and share tabular data for processing. Use CSV instead.

#### Use UTF-8 character encoding for text-based data.
- Interpreting the [wrong character encoding](http://stat545.com/block032_character-encoding.html#a-three-step-process-for-fixing-encoding-bugs) can change how data is processed or analyzed.

## Code

Source code provides information about the intention of the process described using a programming language. In general, the value of having source code be the source of truth for describing the process is that it is also what is executed to *do* the process. This is in contrast to a *methods* section of an academic paper where natural language or mathematics are used to describe the process. The latter is valuable for understanding, but should be supplemental to the source code rather than the other way around.

#### Version control your source code.
- Use [Git](https://git-scm.com/). It is by far the most ubiqituous [version control](https://en.wikipedia.org/wiki/Version_control) system and there are ton of tools and content available to use it effectively.

#### Host your source code on a reliable code-sharing platform.
- Suggestions include [GitHub](https://github.com/), [GitLab](https://about.gitlab.com/), or [BitBucket](https://bitbucket.org/).
- The goal is ensure long-term reliability and access and to prevent link rot.

#### Maintain an errata for bugs found post-publication.
- This can be done using the issue trackers on the code sharing platforms above.
- In addition, the errata can be listed on the README of your code repository.

#### Vendor your dependencies.
- Documenting versions of your library dependencies is good, but it doesn't prevent the authors from unpublishing their source code (see the ["leftpad" incident](https://www.sciencealert.com/how-a-programmer-almost-broke-the-internet-by-deleting-11-lines-of-code)).
- [Vendoring](https://stackoverflow.com/a/26217631/407954) is the practice of copying **all dependencies** locally into your code repository that your code relies on so it can always be built in the future.

#### Don't depend on hosted services as part of your computation.
- For example, there are a plethora of machine learning services offered by Google, AWS, and Azure.
- Hosted services can go away or change at any time, so the reproducibility of your research should not directly depend on it.

## Runtime

Although source code provides an unambiguous description of a program, it is still does not do any work without the language runtime. For those unfamiliar, a language runtime is comprised a set of tools and/or libraries that actually enable the source code to be executed on hardware.

How does this affect reproducibility? The runtime does the actual computation given the description of your program (the source code). Thus in addition to the source code, the specific used when computing the reuslts must be documented and available. In practice, access to a specific runtime version is unlikely to be a problem since most runtimes are Open Source and/or runtimes are often designed to be backwards compatible. But it is important to acknowledge that *a* compatible runtime must exist in order for the code to be executed.

### Use Open Source community-supported programming languages.
- Virtually all mainstream languages fall into this category.
- Avoid purely academic or single-author languages for the final version of the code since the corresponding runtimes of those languages may break or lose support over time.

### Prefer languages that support static compilation.
- This may be controversial, but a static binary (that is statically linked) for a specific CPU architecture is arguably more reliable in the long-term than one that is not. Non-statically linked binaries use shared libraries on the host machine which means if their versions change the program execution may change.
- It is worth noting that the most common languages for data science and statistics are Python, R, and Matlab, all of which *do not* fall into this category. The main trade-off is ease of use and speed of development with safety and correctness.

### Leverage containers to isolate a runtime environment.
- [Containers](https://aws.amazon.com/containers/) are an abstraction that provide isolation of environment.
- Rather than requiring someone to download and setup all dependencies themselves to execute your source code, a container *image* can be created which is enables creating containers that are exact copies.
- Since containers provide a full operating system-like environment, all necessary dependencies can be installed prior to running the container.
- This effectively solves the problem mentioned above about using shared libraries as well as the vendoring problem.

### Document all runtime configuration and environment variables.
- These are variables supplied when the program is executed as supposed to explicitly defined in the program itself.
- Ideally there should be zero configuration and there are strategies for achieving this.
