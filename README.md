# Project Elara 2024 Research Report

This repository houses the sources for Project Elara's 2024 research report.

A live version of the paper can be [freely viewed online](https://elaraproject.github.io/2024-research-report/).

> :warning: **IMPORTANT:** Project Elara has switched over to the open-source forge [Codeberg](https://codeberg.org/). The Project Elara repositories have been moved to [this Codeberg page](https://codeberg.org/elaraproject/). **This GitHub repository is no longer maintained**.

## Development

> Everything in this report is released to the **public domain** like the rest of [Project Elara](https://github.com/elaraproject/), meaning it is essentially **unlicensed research**, so you can use it for basically any project you want, _however_ you want, with or without attribution.

This report is built with [MyST](https://mystmd.org/). To get started, first clone the repository:

```sh
git clone https://github.com/elaraproject/2024-research-report
```

Ensure you have [Python](https://www.python.org/) and [pip](https://pypi.org/project/pip/) installed. Then install MyST with:

```sh
pip install mystmd
```

To start a live development server, run:

```
myst start
```

To build the PDF, you must have [LaTeX installed](https://www.latex-project.org/get/). With a working LaTeX installation, the PDF can then be built with:

```
myst build --pdf
```
