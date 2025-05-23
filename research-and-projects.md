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

---

## 5. Project Handover (Final Year to First Year Student)

> [!IMPORTANT]
> On the beginning of 2nd year, each student need to find a 1st year student to handover the project.  

Below is the checklist for the handover process:

**Projects**:

- [ ] [IEEE paper report](Overleaf link) - [guide](./paper-writing.md)
- [ ] [GitHub project repository](GitHub repo link) containing:
  - [ ] [Source code](GitHub repo link)
  - [ ] [Documentation](GitHub repo link or docs link), includes:
    - [ ] Function documentation (Doxygen/Sphinx)
    - [ ] Installation guide (How to install your tool)
    - [ ] Integration guide (How to build the end-to-end of your systems):
      - System architecture diagram - Examples: [O-RAN](https://docs.o-ran-sc.org/en/latest/_images/o-ran-architecture.png), [O-DU-High](https://docs.o-ran-sc.org/projects/o-ran-sc-o-du-l2/en/latest/overview.html#o-du-high-architecture)
      - Message Sequence Chart (MSC) + call flow - Example: [O-DU High](https://docs.o-ran-sc.org/projects/o-ran-sc-o-du-l2/en/latest/overview.html#o-du-high-functionality)
    - [ ] User manual (How to use your tool)
- [ ] [Demo video](pCloud link) showing deployment and overall running of the project

**Thesis**:

- [ ] [slide](Google Slides or Overleaf link) (presentation slides for project defense/exam)
- [ ] [Thesis book](Overleaf link) (full thesis document in Overleaf, ready for submission)

> [!TIP]
> Present your thesis slide in weekly meeting report since the beginning of 2nd year.

---

## 6. Graduation Procedure

> [!WARNING]
> Check the updated graduation procedure on the [ECE NTUST website](https://www.academic.ntust.edu.tw/p/412-1048-8756.php?Lang=en).

### Qualifications

Master students who meet graduation regulations can apply for the oral defense. The deadlines are:

- Spring semester: 31th January
- Fall semester: 31th July

> [!IMPORTANT]
> Please follow the [NTUST academic calendar](https://www.academic.ntust.edu.tw/p/412-1048-8756.php?Lang=en).

### Procedures

- [ ] Complete “[The oral defense application of Master degree](https://ece.ntust.edu.tw/var/file/17/1017/img/Master_s_Academic_Degree_Examination_Orals_Recommend_Application_Form_1131008.docx)” (download from “[Forms and Links](https://ece.ntust.edu.tw/p/412-1017-1400.php?Lang=en)”)
- [ ] Download the required documents at the Student Information System ([link](https://www.academic.ntust.edu.tw/p/412-1048-8234.php?Lang=en))
- [ ] Upload the digital thesis at the [Taiwan Tech Electronic Thesis System](https://etheses.lib.ntust.edu.tw/cgi-bin/gs32/gsweb.cgi/ccd=PrUzwJ/webmge?switchlang=en)
- [ ] Print the “e-Thesis Authorization Form” after uploading your thesis, then proceed with the leaving procedure

#### Before Oral Defense 

> [!CAUTION]
> The following steps must be completed **at least 2 weeks before the oral defense**.

- [ ] Prepare one copy of “Qualification Form by Master Degree Examination Committee”
- [ ] Print copies of “Oral Defense Evaluation Form” for all committee members
- [ ] Bring the “Receipt of Payment” (provided before the oral defense)

#### After Oral Defense

- [ ] Submit the “Qualification Form”, “Evaluation Form”, "Thesis Academic Ethics and Authentication of Originality Statement", and “Receipt of Payment” to the ECE office
- [ ] Attach the “Recommendation Form” and “Qualification Form” with the thesis
- [ ] Send the PDF file of **Moodle Turnitin** Result by e-mail

> *To apply for delayed public access, download the “Application for Embargo of Thesis/Dissertation” and attach it to the first page of the thesis.*

### Leaving Procedure

**Application Deadline:** The date before the registration deadline for the next semester. (Please follow the school calendar.)

- [ ] Upload digital thesis and submit one printed copy to the library
- [ ] Download and complete the [School Leaving Application Form](https://www.academic.ntust.edu.tw/p/412-1048-8234.php?Lang=en) via the Student Information System
- [ ] Submit a soft and yellow cover of the thesis to the department office
- [ ] Submit a printed copy of the thesis and the signed e-Thesis Authorization Form (NTUST & NCL) to the library
- [ ] Complete all steps in the School Leaving Application Form and collect your diploma at the Office of Graduate Studies

---

> Adhering to this SOP ensures that research and development projects are well-documented, maintainable, and easily transferable to new team members.
