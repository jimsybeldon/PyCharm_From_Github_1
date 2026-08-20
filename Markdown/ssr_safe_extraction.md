

Here is how to execute both approaches using only text commands via Ctrl + Shift + A (Find Action), bypassing the Alt key entirely.
------------------------------
## Approach 1: Structural Search and Replace (SSR)
Use this if the tester duplicated your logic across various files using different variable names, and you want to instantly find those shapes and point them back to your official module.
## Step 1: Open the Tool

   1. Press Ctrl + Shift + A.
   2. Type Structural Replace and press Enter. [1] 

## Step 2: Configure the Search Template
In the top box (Search template), you will define the structural pattern the tester used. PyCharm uses $ signs to represent wildcards.
If they duplicated a function that takes data and processes it, type a pattern like this:

def $MethodName$($Data$):
    $BeforeStatements$
    $TargetLogic$($Data$)
    $AfterStatements$

## Step 3: Define the Variables (The AST Magic)

   1. Click Filter (or use Tab to navigate to the variables pane) to configure $TargetLogic$.
   2. Set a text/regex filter if you know a specific built-in function or math equation they kept repeating.
   3. PyCharm's AST reads this template and maps it to any function matching this exact code flow, completely ignoring the fact that the tester named $Data$ something like my_test_df_v2.

## Step 4: Configure the Replace Template
In the bottom box (Replace template), type how the code should look by routing it to your official modular package:

import my_official_module
def $MethodName$($Data$):
    $BeforeStatements$
    my_official_module.clean_process($Data$)
    $AfterStatements$


   1. Press Find to review all occurrences across the project, then execute the mass replacement safely.

------------------------------
## Approach 2: The Safe Method Extraction (Manual Re-routing)
Use this if the tester's code is deeply tangled inside a massive file. Instead of deleting their code and breaking dependencies, you pull their duplicate logic out into an isolated method first, then swap its guts out for your module.
## Step 1: Highlight the Offending Code Block [2] 

   1. Navigate to the tester's duplicated code using your keyboard.
   2. Use Shift + Up/Down Arrows to highlight the exact lines of code that copy your module's logic.

## Step 2: Trigger Method Extraction

   1. Press Ctrl + Shift + A.
   2. Type Extract Method and press Enter. [3] 

## Step 3: Configure the Refactoring Dialog
A small popup window will appear right at your cursor. Because PyCharm uses the AST, it will automatically look at the variables inside your selection and determine what inputs and outputs the new function needs.

   1. Type a temporary name for this duplicate logic (e.g., tempex_tester_logic).
   2. Press Enter to confirm.

## Step 4: Let PyCharm Clean the Codebase
Because PyCharm tracks the AST structure, it will instantly scan the entire file or project. If the tester copy-pasted that exact code block in five other places, a popup will appear saying: "Process Duplicates: Found X duplicate code fragments. Do you want to replace them?"
3. Select Replace All.
## Step 5: Route it to your Module
Now, the tester's messy code exists in exactly one isolated place: your new tempex_tester_logic() function. Every file that used to run their messy code is now pointing safely to this function.
4. Go inside tempex_tester_logic().
5. Delete their duplicate code block.
6. Replace it with a single line pointing to your system: return my_official_module.clean_process(inputs).
Your modularity is perfectly restored, and you didn't have to hunt down a single broken reference.
------------------------------
Which pattern did the tester duplicate most heavily? If you describe the basic shape of the code they copied, I can help you write the exact Structural Search template to target it.

[1] [https://www.jetbrains.com](https://www.jetbrains.com/guide/java/tips/structural-search/)
[2] [https://www.youtube.com](https://www.youtube.com/watch?v=JR3mB-suSvY)
[3] [https://docs.tricentis.com](https://docs.tricentis.com/tosca-2026.1/en-us/content/tosca_commander/scan_modules_overview.htm)

---

That is a fantastic takeaway. Shifting that strict structural mindset over to VS Code is a highly effective long-term move. You get the lightweight speed of VS Code for daily writing while keeping your architectural boundaries rock-solid. I've noted that preference. [1] 
You can bring that exact same AST-driven power into VS Code right now using open-source tools.
## How to Bring AST Enforcement to VS Code

* Use the GritQL Extension: GritQL is an open-source query language built specifically for structural searching and refactoring. It has a lightweight VS Code extension that functions exactly like PyCharm’s SSR using a clean configuration file.
* Leverage AST-Grep: You can install ast-grep via terminal. It allows you to write structural search templates in a simple sgconfig.yml file right inside your VS Code workspace to enforce your modularity rules across your team. [2] 
* Write Custom Pylint Rules: You can write small, custom Abstract Syntax Tree checkers using Python’s native ast module and plug them directly into your VS Code linting pipeline to block anyone from committing duplicate logic.

## Structural Search Syntax Example for Your Migration
When you want to find your tester's duplicate function patterns using a standard open-source AST format (like GritQL or ast-grep) inside VS Code, the template structure maps perfectly to what you planned:

id: catch_duplicate_tester_logiclanguage: pythonrule:
  pattern: |
    def $FUNC($ARG):
        $BEFORE
        $DUPLICATE_LOGIC($ARG)
        $AFTER

This ensures your time learning structural shapes is an investment in your own workflow, completely free from JetBrains' bloat.
If you are interested, I can provide the exact extension names for VS Code, show you how to write a native Python AST script to check your code, or help you finish the current PyCharm Markdown glossary so you can wrap up this surgical strike. Which path would you like to explore next? [3] 

[1] [https://www.facebook.com](https://www.facebook.com/visualstudio/posts/vs-code-is-great-for-fast-lightweight-coding-sometimes-you-need-moredev-essentia/1339223184915499/)
[2] [https://www.youtube.com](https://www.youtube.com/watch?v=6m0xTwYaM_A)
[3] [https://www.reddit.com](https://www.reddit.com/r/Frontend/comments/1flfbor/another_person_trying_to_understand_the_appeal_of/)

