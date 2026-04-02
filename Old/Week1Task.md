# Tools and Production Week 1 Task



### **Task and Reasoning**
I want to add a tool which looks at github pushes and then creates documentation through doxygen. My reasoning was that manual documentation slow and unneccessary, leading to wasted developer time during onboarding or feature implementation.

### **Approach**
I approached this by leveraging **GitHub Actions** as the "watcher" component. Instead of a custom script running on a developer machine, the repository itself triggers the documentation generation whenever code is pushed. This ensures consistency and centralization. The action runs **Doxygen** to parse the codebase and generate HTML, which is then automatically deployed to **GitHub Pages**.

---

### **Technical Implementation**
The solution uses **GitHub Actions** (yaml workflows), **Doxygen** (documentation generator), and **Graphviz** (for graphing dependencies if needed). The primary language to document is C++ within the Unreal Engine 5.6 framework.

### **Workflow Details**
I created a workflow file `.github/workflows/doxygen.yml` which defines the automation logic. The workflow:
1.  **Observes**: Triggers on every `push` event to the `main` branch.
2.  **Installs**: Sets up an Ubuntu runner and installs the `doxygen` and `graphviz` packages.
3.  **Executes**: Runs the command `doxygen Doxyfile` to process the source code.
4.  **Publishes**: Uses the `peaceiris/actions-gh-pages` action to push the generated HTML to the `gh-pages` branch for hosting.

### **Configuration and UE5 Integration**
The `Doxyfile` is the central configuration. A key challenge was handling Unreal Engine's specific macros like `UCLASS()`, `UPROPERTY()`, and `UFUNCTION()`. Standard C++ parsers often fail on these. To address this, I configured the `PREDEFINED` section in the `Doxyfile` to treat these macros as empty strings or specific tokens during the pre-processing step (`ENABLE_PREPROCESSING = YES`). This allows Doxygen to correctly identity classes and functions without syntax errors.

---


### **Result**
The final result is a fully automated documentation pipeline. Whenever a developer pushes a change to the repository, the system silently works in the background to build the new documentation site. The output is a navigable HTML website hosting the API reference.

---

## 4. Bibliography

- List all external sources used (documentation, tutorials, articles, etc.)  
- Use the universities referencing style

1.  Doxygen. (2023). *Doxygen Manual: Configuration*. Available at: https://www.doxygen.nl/manual/config.html [Accessed 9 Feb. 2026].
2.  GitHub. (n.d.). *GitHub Actions Documentation*. Available at: https://docs.github.com/en/actions [Accessed 9 Feb. 2026].
3.  Epic Games. (n.d.). *Unreal Engine 5 Documentation*. Available at: https://docs.unrealengine.com/5.0/en-US/ [Accessed 9 Feb. 2026].

---


### **AI Declaration**
**Tools: Google Gemini 3 Pro**  


---

## Submission Notes & Checklist

> Remove this section once complete — use this as a checklist before submitting

- Total word count: **500 words (±10%)** across Sections 1–3  
- **Figure captions and figure descriptions do NOT count towards the word count**  
- Use **plenty of images, GIFs, videos, screenshots, and short code snippets** where appropriate to demonstrate understanding and functionality  
- All required **source code is included in this repository**  
- Any required **executables or builds are provided via GitHub Releases**, where appropriate  
- Demonstration video link is accessible and clearly shows functionality  
- Bibliography includes all referenced material  
- AI usage is clearly declared (or explicitly stated as not used)  
- Work reflects your own understanding and professional practice  

---
