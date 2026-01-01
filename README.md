Elbette, işte GitHub repon için Markdown formatında hazırlanmış, kopyalayıp yapıştırabileceğin tertemiz bir `README.md` dosyası.

Bunu projenin ana dizinine `README.md` ismiyle kaydet.

```markdown
# LaTeX Automated Response Letter Template 🔄

> **A "Single Source of Truth" workflow for academic peer-review response letters.**

This LaTeX template solves the common pain point of syncing revisions between your manuscript and your response letter. It allows you to edit your revision text in the manuscript **once**, and automatically propagates that text (along with the correct Section and Page numbers) to your response letter.

**No more copy-pasting errors. No more outdated page references.**

---

## ✨ Key Features

* **Single Source of Truth:** Write your revision in the manuscript; it automatically appears in the response letter.
* **Auto-Sync Metadata:** Automatically fetches the **Section Number** and **Page Number** where the revision is located.
* **Multi-Reviewer Support:** Map a single revision to multiple reviewers easily (e.g., if Reviewer 2 and Reviewer 3 requested the same fix).
* **Phantom Box Technique:** Copies text to the clipboard without duplicating it visually in the manuscript PDF.
* **Professional Visuals:**
    * 🔴 **Reviewer Comments:** Distinctive style.
    * 🔵 **Author Responses:** Clear and separate.
    * 🟢 **Revisions:** Auto-generated evidence boxes.

## 📂 File Structure

* `manuscript.tex`: The main paper. You apply edits here using the `\revised` macro.
* `response_letter.tex`: The letter to reviewers. It pulls data from the manuscript using `\AutoRevision`.

## 🚀 How to Use

### 1. In `manuscript.tex` (The Source)

Use the `\revised{ID}{Text}` macro to mark your changes. The ID acts as a unique barcode for that change.

```latex
% Scenario 1: Simple Revision (Reviewer 1.1)
\revised{1.1}{We have clarified the specific contribution of our method...}

% Scenario 2: Multi-Reviewer Map (Reviewer 2.1 and 3.4 asked for the same thing)
\revised{2.1, 3.4}{We utilized a 5-fold cross-validation strategy...}

% Scenario 3: Split Revision (One comment led to changes in two places)
\revised{1.2a}{Defined alpha parameter in Intro...}
...
\revised{1.2b}{Discussed alpha parameter in Conclusion...}

```

### 2. In `response_letter.tex` (The Output)

Use the `ReviewCycle` environment to structure your response and `\AutoRevision{ID}` to fetch the proof.

```latex
% Simple Usage
\begin{ReviewCycle}{Reviewer 1, Comment 1}
    \ReviewerText{The contribution is unclear.}
    \AuthorResponse{We have updated the abstract.}
    \AutoRevision{1.1} % -> Fetches text, section, and page automatically
\end{ReviewCycle}

% Multi-Revision Usage (Fetching multiple parts)
\begin{ReviewCycle}{Reviewer 1, Comment 2}
    \ReviewerText{Fix the inconsistency in Intro and Conclusion.}
    \AuthorResponse{Fixed in both sections.}
    \AutoRevision{1.2a, 1.2b} % -> Lists both changes sequentially
\end{ReviewCycle}

```

---

## ⚠️ Compilation Order (Crucial)

Since the system relies on auxiliary files (`.aux` and `.cpy`) to pass data between documents, the compilation order matters:

1. **COMPILE `manuscript.tex` FIRST.**
* *Why?* This generates the `.cpy` (clipboard) file containing the text and the `.aux` file containing page numbers.


2. **COMPILE `response_letter.tex` SECOND.**
* *Why?* This reads the generated files to populate the boxes.



*If you change the text in the manuscript, re-compile the manuscript first, then the response letter.*

---

## 🛠 Dependencies

This template uses standard LaTeX packages included in most distributions (TeX Live, MiKTeX, Overleaf):

* `clipboard` (For text transfer)
* `xr` (For cross-referencing page numbers)
* `etoolbox` (For handling loops and lists)
* `tcolorbox` (For the beautiful UI)
* `xcolor`

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

---

*Created by [Huseyin Karaca*](https://github.com/huseyin-karaca)

```

```