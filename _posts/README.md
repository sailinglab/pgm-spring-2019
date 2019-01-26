Lecture Notes Scribe Guidelines
-------------------------------

Scribing lectures is one of the course [requirements](https://sailinglab.github.io/pgm-spring-2019/description/#grading) for 10708 PGM class.
In spring 2019, students taking the class are asked to write up their notes in the form of blog posts using the [Distill.pub](https://distill.pub/) format (v2).
We provide a template ([source](https://github.com/sailinglab/pgm-spring-2019/blob/master/_posts/2019-01-09-lecture-notes-template.md), [rendered](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-notes-template/)) for the notes.
The template showcases the main building blocks that students may use when writing up their notes (e.g., equations, different formats of images, etc.).

## Preparation

To prepare the scribe notes, you'll need a few steps.

### Preliminary steps
- [Fork](https://help.github.com/articles/fork-a-repo/) the course repository.
- In the settings of your fork, set GitHub Pages source to the `master` branch.
- Make sure GitHub Pages correctly renders the webpage at `<your-github-username>.github.io/pgm-spring-2019/`.

If you are not familiar with GitHub, take a look the [intro tutorial](https://guides.github.com/activities/hello-world/) and the [GitHub Pages tutorial](https://guides.github.com/features/pages/).

### Rendering notes locally
For a more convenient workflow, while writing your notes, you can render them locally.
Assuming you have [Ruby](https://www.ruby-lang.org/en/downloads/) and [Bundler](https://bundler.io/) installed on your system (*hint: for ease of managing ruby gems, consider using [rbenv](https://github.com/rbenv/rbenv)*), do the following steps:
```bash
$ git clone git@github.com:<your-github-username>/pgm-spring-2019.git
$ cd pgm-spring-2019
$ bundle install
$ bundle exec jekyll serve
```
After that, you will be able to see a rendered version of the course webpage (with all your changes to the notes) by going to [http://localhost:4000](http://localhost:4000/).

### Write up lecture notes
- Using the template, write up and add your notes to `_posts/yyyy-mm-dd-lecture-xx.md` and bibliography to `assets/bibliography/yyyy-mm-dd-lecture-xx.bib` (in the BibTeX format; here is [an example](https://github.com/sailinglab/pgm-spring-2019/blob/master/assets/bibliography/2019-01-09-lecture-notes-template.bib)) in your fork of the repository.
- When writing notes, you can use a combination of Markdown and HTML (the latter for more fine-grained rendering, if necessary).
  If you are not familiar with markdown, please spend 5 min looking at this [tutorial](https://commonmark.org/help/tutorial/index.html).
- Add the images used in your post to `assets/img/notes/lecture-xx/`.
  Then, you can link the images as `<img src="{{ '/assets/img/notes/lecture-xx/img-name.png' | relative_url }}" />` in the writeup.
  Please follow the [template](https://sailinglab.github.io/pgm-spring-2019/notes/lecture-notes-template/#figures) to make your figures correctly aligned and captioned.
- Make sure the title of the notes is formatted as `Lecture xx: <lecture title>`.
- Make sure the Lecturer and the Authors information is correct.

## Submission

The due date for each set of notes is 1 week after the lecture.
To submit the notes for review, please do the following:
- Create [a pull request](https://help.github.com/articles/about-pull-requests/) (PR) into the master branch of the course repository.
- Make sure you title your PR `Lecture xx: <lecture title>`.
- Make sure the description of your PR contains a link to the rendered version of the notes.
- You will be assigned one of the TAs as an editor who will review your notes and approve or request changes.
- Once the editor is satisfied with the quality of the scribed notes, your PR will be merged.
- Once the PR is merged, authors of the submitted notes get credit for scribing.

## FAQ

1. **Q:** When I go to `<your-github-username>.github.io/pgm-spring-2019/`, I get 404 error. What should I do?

   **A:** Please make sure you followed the preliminary steps and GitHub Pages source points to the `master` branch.
Note that it takes a few minutes for the website to start rendering.

2. **Q:** What is expected from lecture notes? What should they cover?

   **A:** The notes should be well-written, stand alone reference, so that the reader does not need to go back to the lecture video or slides.

3. **Q:** Do we need to scribe reading materials?

   **A:** Highlighting important points from the reading material is encouraged (especially, if your scribe team is 3-4 people). Please make sure notes from readings coherently fit into the lecture notes (e.g., you can use footnotes to expand on some relevant points that were not covered in the lecture).
