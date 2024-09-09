# GSoC-2024 

This is an overview of the work that I did over the last 14 weeks for this project as part of GSoC 2024 for [Arviz](https://python.arviz.org/en/stable/), under the NumFocus umbrella organization. Links to pushed code/relevant PRs and illustrations are included below and can be checked for more details. 

## Project Overview: Arviz Plotting Refactoring

The overarching goal of this GSoC project was to further the refactoring of existing Arviz’ plotting functionality into the new Arviz-Plots module- one of 3 (the others being Arviz-Base and Arviz-Stats) that Arviz is being split into. There were issues with the way the existing implementation was structured and coded that necessitated this, and Arviz-Plots aims to be much better in a lot of ways. Some planning, brainstorming and work towards this refactoring had already happened before my GSoC project- my work was an extension of these developments. 

Key characteristics of the refactored approach include the use of a large new class that serves a managerial role, facetting plots and removing redundancy between plots for common utility and looping functions- `PlotCollection`, some ‘visual element’ functions that act as atomic plotting elements and prevent redundancy between plot implementations (since ArviZ has a lot of plots with some commonalities), and a common plotting interface for the backend (to allow easier extensibility to other backends). 

Another important feature of the refactored version is the approach of having ‘batteries-included’ inclusions that assert certain biases/defaults for each plot, like for aesthetics and mapping them to plot elements. 

My work was to add 8 new batteries-included plotting functions to Arviz-Plots, including the documentation and tests via Pytest and Hypothesis for each, and any related functions and utilities directly related to these. 

## My Work

Although implementing a total of 8 plotting functions was my goal -as outlined in my initial project proposal- I only managed to work on 7, with individual PRs for each of these. Some of the logic involved, working with the existing codebase and the main dependencies worked with was technically harder than I had anticipated. The `PlotCollection` class and Arviz-Plots’ other paradigms like the visual element functions with common backend interfaces were used for this and relevant patterns followed. I also worked on adding support for histograms to the preexisting `plot_dist`, with a custom utility function for processing the histogram data that lasted until an Arviz-Stats update meant it was no longer required. 

The initial stage of the project was personally the most challenging, with the `plot_ppc` function that I started off with still slightly short of being mergeable at the time of writing this. However, there are only a few issues with tests left to be resolved. Others were easier, like plot_ridge, owing to being based off of plot_forest which was already in place and stable. 

A new plot that doesn’t exist yet in legacy Arviz was also added- `plot_rootogram`. A way of viewing this plot is as being analogous to `plot_ppc`, but more suited for discrete values, with hanging ‘predictive’ bars from ‘observed’ data points. [This issue](https://github.com/arviz-devs/arviz-plots/issues/52) explains these better, with an ArXiv link to a paper where these plots and their relevance is explained even further.

Apart from these, `plot_ess`, `plot_ess_evolution` and `plot_mcse` were also added - inference diagnostic functions that are related but different. 

And finally `plot_violin`, which like `plot_dist` is another way of representing density and distribution. This plot is still being worked on, although initial drafts are ready and outputs viewable on the PR. 

Along with the core plotting functions that each of these have, many of these call similar visual element functions behind the hood that were also developed directly in the same PRs and can be viewed there as well. Some of the Pytest fixture enhancements for the tests for these plots are also similar. 


