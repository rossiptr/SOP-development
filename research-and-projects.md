# Research and Projects Development SOP

This Standard Operating Procedure (SOP) outlines the requirements and best practices for research and development (R&D) projects in the lab. All developers and researchers must adhere to the following guidelines to ensure quality, reproducibility, and smooth handover.

---

## 1. Repository Management
- **Create a private GitHub repository** for each R&D project.
- **Update the repository daily** with source code, documentation, and progress logs.
- Ensure all code and documentation are pushed to the repository before the end of each workday.

## 2. Source Code Standards
- All source code must follow these standards:
  - Use clear, consistent naming conventions (e.g., PEP8 for Python, Google Style for C++/Java).
  - Write modular, reusable functions and classes.
  - Include error handling and input validation.
  - Use version control best practices (meaningful commit messages, frequent commits, use of branches for features/fixes).
  - Remove unused code and files before each major commit.

## 3. Documentation Requirements
- **Function Documentation:**
  - Every function and class must include a docstring or comment describing its purpose, parameters, return values, and exceptions.
  - Use Doxygen (for C/C++/Java) or Sphinx (for Python) to auto-generate API documentation.
- **Class Diagram:**
  - Generate and include a class diagram in the documentation (Doxygen/Sphinx can be configured to do this).

## 4. Installation and User Guide
- Provide a detailed **installation guide** (refer to [NVIDIA CUDA installation guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/)).
- Include a **user manual** explaining how to use the tool, with example commands, input/output formats, and troubleshooting tips.

## 5. Project Handover (Final Year to First Year Student)
Upon project completion, ensure the following items are handed over (checklist):

- [ ] [IEEE Overleaf paper template](Overleaf link) of the project (with all sections filled as appropriate)
- [ ] [GitHub project repository](GitHub repo link) containing:
  - [ ] [Source code](GitHub repo link)
  - [ ] [Documentation (including installation and user guides)](GitHub repo link or docs link)
- [ ] [Demo video](pCloud link) showing deployment and overall running of the project
- [ ] [Oral exam slide deck](Google Slides or Overleaf link) (presentation slides for project defense/exam)
- [ ] [Thesis book Overleaf](Overleaf link) (full thesis document in Overleaf, ready for submission)

---

> Adhering to this SOP ensures that research and development projects are well-documented, maintainable, and easily transferable to new team members.
