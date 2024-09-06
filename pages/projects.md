---
title: Projects - Anthony Fu
display: Projects
description: List of projects that I am proud of
wrapperClass: 'text-center'
art: dots
projects:
  Current Focus:
    - name: 'code analyzer for code review'
      link: ''
      desc: 'A code analyzer that helps developers and testers identify potential issues by scanning for code risks based on git diff information. This project is still in the early stages and is not yet ready for public use.'
      icon: ''

---

<!-- @layout-full-width -->
<ListProjects :projects="frontmatter.projects" />
