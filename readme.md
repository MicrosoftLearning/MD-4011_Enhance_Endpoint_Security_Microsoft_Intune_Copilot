# MD-4011: Enhance endpoint security with Microsoft Intune and Microsoft Security Copilot

<!-- Review the notes in the index.md file to set up the repo for GitHub Pages -->

This repo contains exercises and supporting files for Microsoft skilling content.

The exercises may be used in both self-paced skilling experiences on [Microsoft Learn](https://learn.microsoft.com) and in Microsoft authorized instructor-led training.
<!-- Update the paragraph above with a link to a specific Learning Path or course as appropriate -->

## Information for MCTs
<!-- You can remove this section if the exercises will not be used to support Microsoft Official Curriculum ILT -->

**Are you an MCT?** - Have a look at our [GitHub User Guide for MCTs](https://microsoftlearning.github.io/MCT-User-Guide/)

Any MCT (Microsoft Certified Trainer) can submit a pull request to the code or content in the GitHub repro. Microsoft and the course author will then triage and include content and lab code changes as needed. You can submit bugs, changes, improvement, and ideas. Find a new Azure or Microsoft 365 feature before we have? Submit a new demo!

## Lab site and content checks

The lab site is published with GitHub Pages from this repo. It uses a course layout in `_layouts/lab.html` and `assets/course`, and its navigation in `_data/course.yml` is generated from the lab files.

After you add or change a lab, run `python tools/check_labs.py --write` (requires Python and PyYAML). It updates the site navigation and checks front matter, links, and lab files. Course settings, such as groups and Microsoft Learn links, are in `_data/course_config.yml`. The same checks and a site build run in GitHub Actions on every pull request.
