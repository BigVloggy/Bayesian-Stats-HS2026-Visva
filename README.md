# Bayesian-Stats-HS2026
Bayesian Statistics and Data Analysis, Herbstsemester 2026, ETH Zürich

<table>
  <tr>
    <td width="45%" valign="middle"><img src="assets/BT.png" alt="Bayes' theorem"></td>
    <td width="55%" valign="middle"><img src="assets/bayesian_sampling.gif" alt="Metropolis-Hastings sampling a two-dimensional posterior"></td>
  </tr>
</table>

## About this course
This course is taught in the fall term 2026 at ETH Zurich By Patrick Meyers, assisted by Uddipta Bhardwaj and Giada Badaracco.
The material covered in the course is listed in the [syllabus](SYLLABUS_HS2026.pdf) and laid out in detail in [COURSE_CONTENT_AND_RESOURCES.md](COURSE_CONTENT_AND_RESOURCES.md); it is influenced by previous generations of this course. 
It ranges from an introduction to probability theory up to Hamiltonian Monte Carlo and simulation-based inference. Since the course aims to focus mostly on showing how to use statistical analysis tools, the various topics are introduced only relatively briefly. There are many great books and courses on this topic, which go into more detail and which I encourage you to look at before the lectures. The resources listed here are all available online, either directly or through the ETH library. For example:

- *Data Analysis: A Bayesian Tutorial*, 2006. The textbook that we will follow the closest throughout this course.
- *Bayesian Data Analysis*, Gelman, 2013 — ETH library, [link](http://www.stat.columbia.edu/~gelman/book/). The title says it all.
- *Information Theory, Inference, and Learning Algorithms*, MacKay, 2003 — [link](https://www.inference.org.uk/itprnn/book.html). Heavy on the information theory but also covers inference methods nicely. The exercises come with solutions.

## Start here
**[COURSE_CONTENT_AND_RESOURCES.md](COURSE_CONTENT_AND_RESOURCES.md)** is the map of the course: the week-by-week outline of all twelve topics with the exercises attached to each, plus the literature and links to the other courses we draw on. If you only read one file in this repository, read that one.

## This repository
| Where | What |
| --- | --- |
| Start with [setting up SSH and forking the repo](help/git/setup_ssh_and_fork.md) | If you're new to the course, this is the first step and we cover this in the first lecture.|
| [COURSE_CONTENT_AND_RESOURCES.md](COURSE_CONTENT_AND_RESOURCES.md) | Course outline, week by week, and the reading list. |
| [SYLLABUS_HS2026.pdf](SYLLABUS_HS2026.pdf) | The official syllabus for the semester. |
| [lectures/](lectures/) | The lecture notebooks, which are the source for the slides and PDFs — currently [week1_intro.ipynb](lectures/week1_intro.ipynb). |
| [slides/](slides/) | Rendered slides for the lectures — currently [week1_intro.slides.html](slides/week1_intro.slides.html). |
| [exercises/](exercises/) | Exercise notebooks — currently [week1_exercise_estimate_pi.ipynb](exercises/week1_exercise_estimate_pi.ipynb). |
| [exercise_solutions/](exercise_solutions/) | Solutions to selected exercises — currently [week1_pi_exercises_solution.ipynb](exercise_solutions/week1_pi_exercises_solution.ipynb). |
| [course_tools/](course_tools/) | Plotting helpers, matplotlib styles, and the scripts that build the [slides](course_tools/make_slides.sh) and [PDFs](course_tools/make_pdf.sh). |
| [environment.yaml](environment.yaml) | The conda environment for running everything here. |
| [help](help/) | Infographics and other helpful accessories for `git`, `python` and more thanks to *Michael Coughlin*'s [repository](https://github.com/UMN-Big-Data-in-Astrophysics).|


These will be populated as the course progresses through the term; at the moment only week 1 is in place.

## Acknowledgements
This course stands on material generously shared by others:

- *Tilman Tröster and Veronika Oehl*, ETH Zürich — earlier generations of this course, which we follow closely ([repository](https://github.com/tilmantroester/bayesian_statistical_methods)).
- *Michael Coughlin*, University of Minnesota — the Big Data in Astrophysics course, from which we borrow the applied, large-dataset perspective as well as the git cheat sheets and fork-syncing guides in [our resource list](COURSE_CONTENT_AND_RESOURCES.md#other-useful-resources) ([repository](https://github.com/UMN-Big-Data-in-Astrophysics)).
- *Ben Farr*, University of Oregon — computational physics, a source of project topics and datasets ([repository](https://github.com/uo-phys/comp-phys-26)).

See [COURSE_CONTENT_AND_RESOURCES.md](COURSE_CONTENT_AND_RESOURCES.md#examples-of-other-courses) for the full set of courses and resources we draw on.
