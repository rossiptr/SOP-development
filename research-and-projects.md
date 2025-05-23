# Research and Projects Development SOP

This Standard Operating Procedure (SOP) outlines the requirements and best practices for research and development (R&D) projects in the lab. All developers and researchers must adhere to the following guidelines to ensure quality, reproducibility, and smooth handover.

- [Research and Projects Development SOP](#research-and-projects-development-sop)
  - [1. Repository Management](#1-repository-management)
  - [2. Source Code Standards](#2-source-code-standards)
  - [3. Documentation Requirements](#3-documentation-requirements)
  - [4. Core materials](#4-core-materials)
  - [5. Laboratory Leaving Procedure](#5-laboratory-leaving-procedure)
    - [5.1 Projects Handover](#51-projects-handover)
    - [5.2 Oral-Exam Requirements](#52-oral-exam-requirements)
  - [6. Graduation Procedure](#6-graduation-procedure)
    - [6.1 Qualifications](#61-qualifications)
    - [Procedures](#procedures)
      - [Before Oral Defense](#before-oral-defense)
      - [After Oral Defense](#after-oral-defense)
    - [Leaving Procedure](#leaving-procedure)


---

## 1. Repository Management

- **Create a private GitHub repository** to upload your project. Confirm with manager.
- **Maintain the repository** with source code, documentation, and progress logs.
- Ensure all code and documentation are pushed to the repository before the end of each workday.

## 2. Source Code Standards

- All source code suggest follow these standards:
  - Use clear, consistent naming conventions (e.g., PEP8 for Python, Google Style for C++/Java).
  - Use version control best practices (meaningful commit messages, frequent commits, use of branches for features/fixes).
  - Remove unused code and files before each major commit.

## 3. Documentation Requirements

- **Function Documentation:**
  - Every function and class must include a docstring or comment describing its purpose, parameters, return values, and exceptions.
  - Use Doxygen (for C/C++/Java) or Sphinx (for Python) to auto-generate API documentation.
- **Class Diagram:**
  - Generate and include a class diagram in the documentation (Doxygen/Sphinx can be configured to do this).

## 4. Core materials

- README that consists:
  - Folder structure
  - System architecture
  - How to run your program
  - For AIML:
    - Dataset
    - Dataset information/spec
    - Model generated from training sample data
    - Step-by-step to train the model including parameter and hyperparameter used
- Provide a detailed **installation guide** (refer to [NVIDIA CUDA installation guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/)).
- Include a **user manual** explaining how to use the tool, with example commands, input/output formats, and troubleshooting tips.
 

---

## 5. Laboratory Leaving Procedure

> [!IMPORTANT]
> On the beginning of 2nd year, each student need to find a 1st year student to handover the project.  

Below is the checklist for the handover process:

### 5.1 Projects Handover

- [ ] 5.1.1 [IEEE paper report](Overleaf link) - [guide](./paper-writing.md)
- [ ] 5.1.2 [GitHub project repository](GitHub repo link) containing:
  - [ ] 5.1.2.1 [Source code](GitHub repo link)
  - [ ] 5.1.2.2 [Documentation](GitHub repo link or docs link), includes:
    - [ ] 5.1.2.2.1 Function documentation (Doxygen/Sphinx)
    - [ ] 5.1.2.2.2 Installation guide (How to install your tool)
    - [ ] 5.1.2.2.3 Integration guide (How to build the end-to-end of your systems):
      - System architecture diagram - Examples: [O-RAN](https://docs.o-ran-sc.org/en/latest/_images/o-ran-architecture.png), [O-DU-High](https://docs.o-ran-sc.org/projects/o-ran-sc-o-du-l2/en/latest/overview.html#o-du-high-architecture)
      - Message Sequence Chart (MSC) + call flow - Example: [O-DU High](https://docs.o-ran-sc.org/projects/o-ran-sc-o-du-l2/en/latest/overview.html#o-du-high-functionality)
    - [ ] 5.1.2.2.4 User manual (How to use your tool)
- [ ] 5.1.3 [Demo video](pCloud link) showing deployment and overall running of the project
- [ ] 5.1.4 (**DL: 15th Aug**) Handover review by Ph.D students [Ian/Bimo] (presented by the 1st year student)

### 5.2 Oral-Exam Requirements

> [!WARNING]
> Requirement 5.2.1.2 applies only to students who have not received approval for their *Chapter IV. Results and Analysis* from the Professor.

- [ ] 5.2.1 Code Review:
  - [ ] 5.2.1.1 (**Deadline:** D-30 before oral exam) Code and project review during weekly meeting
  - [ ] 5.2.1.2 (**Deadline:** D-60 before oral exam) Code and project review during weekly meeting (**OPTIONAL**)
- [ ] 5.2.2 Simulation
  - [ ] 5.2.1.1 [RAW Dataset](Pcloud link)
  - [ ] 5.2.1.2 [Experiment results](Pcloud link) (Graphs, Figures)
  - [ ] 5.2.1.3 [Simulation guide](GitHub markdown link) (How to run your simulation)
- [ ] 5.2.3 Complete Pcloud Repository
  <details>
  <summary>Folder Structure</summary>

  ```bash
  ├── [Year-[Fall/Sptring]]-[English Full Name]-[Topic] #ex: 2023-Fall-Ian Joseph Chandra-Wireless Network Digital Twin
  │   ├── Demo video.mp4
  │   ├── Experiment
  │   │   ├── dataset #all datasets used to build your model/results
  │   │   ├── result #all results/outputs generated by your model (graphs, figures, etc.)
  ```

- [ ] 5.2.4 [slide](Google Slides or Overleaf link) (presentation slides for project defense/exam)
- [ ] 5.2.5 [Thesis book](Overleaf link) (full thesis document in Overleaf, ready for submission)

> [!TIP]
> Present your **thesis slide** & **handover progress** in weekly meeting report since the beginning of 2nd year.

---

## 6. Graduation Procedure

> [!WARNING]
> Check the updated graduation procedure on the [ECE NTUST website](https://www.academic.ntust.edu.tw/p/412-1048-8756.php?Lang=en).

### 6.1 Qualifications

Master students who meet graduation regulations can apply for the oral defense. The deadlines are:

- Spring semester: 31th January
- Fall semester: 31th July

> [!IMPORTANT]
> Please follow the [NTUST academic calendar](https://www.academic.ntust.edu.tw/p/412-1048-8756.php?Lang=en).

### Procedures
- [ ] 6.1 Complete “[The oral defense application of Master degree](https://ece.ntust.edu.tw/var/file/17/1017/img/Master_s_Academic_Degree_Examination_Orals_Recommend_Application_Form_1131008.docx)” (download from “[Forms and Links](https://ece.ntust.edu.tw/p/412-1017-1400.php?Lang=en)”)
- [ ] 6.2 Download the required documents at the Student Information System ([link](https://www.academic.ntust.edu.tw/p/412-1048-8234.php?Lang=en))
- [ ] 6.3 Upload the digital thesis at the [Taiwan Tech Electronic Thesis System](https://etheses.lib.ntust.edu.tw/cgi-bin/gs32/gsweb.cgi/ccd=PrUzwJ/webmge?switchlang=en)
- [ ] 6.4 Print the “e-Thesis Authorization Form” after uploading your thesis, then proceed with the leaving procedure

#### Before Oral Defense

> [!CAUTION]
> The following steps must be completed **at least 2 weeks before the oral defense**.

- [ ] 6.5 Prepare one copy of “Qualification Form by Master Degree Examination Committee”
- [ ] 6.6 Print copies of “Oral Defense Evaluation Form” for all committee members
- [ ] 6.7 Bring the “Receipt of Payment” (provided before the oral defense)

#### After Oral Defense

- [ ] 6.8 Submit the “Qualification Form”, “Evaluation Form”, "Thesis Academic Ethics and Authentication of Originality Statement", and “Receipt of Payment” to the ECE office
- [ ] 6.9 Attach the “Recommendation Form” and “Qualification Form” with the thesis
- [ ] 6.10 Send the PDF file of **Moodle Turnitin** Result by e-mail

> *To apply for delayed public access, download the “Application for Embargo of Thesis/Dissertation” and attach it to the first page of the thesis.*

### Leaving Procedure

**Application Deadline:** The date before the registration deadline for the next semester. (Please follow the school calendar.)

- [ ] 6.11 Upload digital thesis and submit one printed copy to the library
- [ ] 6.12 Download and complete the [School Leaving Application Form](https://www.academic.ntust.edu.tw/p/412-1048-8234.php?Lang=en) via the Student Information System
- [ ] 6.13 Submit a soft and yellow cover of the thesis to the department office
- [ ] 6.14 Submit a printed copy of the thesis and the signed e-Thesis Authorization Form (NTUST & NCL) to the library
- [ ] 6.15 Complete all steps in the School Leaving Application Form and collect your diploma at the Office of Graduate Studies

---

> Adhering to this SOP ensures that research and development projects are well-documented, maintainable, and easily transferable to new team members.
