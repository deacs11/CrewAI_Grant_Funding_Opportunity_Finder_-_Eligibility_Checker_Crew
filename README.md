# CrewAI grant funding opportunity finder & eligibility checker

This project uses a CrewAI agent team to assist researchers and non-profits in finding potentially relevant grant funding opportunities. Instead of providing text descriptions, the user provides URLs pointing to their project and organization information. The agents extract details from these URLs, search for grants, and perform a *preliminary* check against stated eligibility criteria, compiling the results into a report.

**🚨🚨 CRITICAL DISCLAIMER: READ CAREFULLY 🚨🚨**

*   **This tool is an AI-powered ASSISTANT for informational purposes only.** It automates searching and provides a *first-pass* look at eligibility based on text analysis of provided URLs and grant descriptions.
*   **IT IS NOT A SUBSTITUTE FOR THOROUGH RESEARCH AND DUE DILIGENCE.**
*   **Eligibility assessment is PRELIMINARY and may be INCORRECT.** Grant criteria are complex and nuanced. The AI may misinterpret website content or grant guidelines. Information on websites can be outdated or incomplete.
*   **You MUST independently verify all information,** especially deadlines, funding amounts, and eligibility requirements, by carefully reading the **official grant documentation** from the funding agency.
*   **This tool does NOT guarantee finding all relevant opportunities, nor does it guarantee eligibility or funding.**
*   **This tool provides NO financial or legal advice.** Consult with grant writing experts or legal counsel as needed.
*   Use of this tool is entirely at your own risk.

## Features

*   **Information extraction from URLs:** Reads provided web pages to understand project goals and organizational details.
*   **Targeted grant search:** Looks for funding opportunities based on extracted information and optional keywords.
*   **Grant detail extraction:** Attempts to pull key details (deadline, funding, purpose, eligibility text) from grant descriptions found online.
*   **Preliminary eligibility check:** Compares extracted eligibility text against extracted organizational details to flag potential matches or mismatches.
*   **Structured reporting:** Summarizes potentially suitable opportunities with extracted details and the preliminary eligibility assessment.

## Requirements

*   Python 3.9+
*   Google Colab environment (recommended) or local Python setup.
*   **API Keys:**
    *   **OpenAI API key:** For the language model (GPT-4 Turbo strongly recommended). Requires a funded account or active credits from [platform.openai.com](https://platform.openai.com/).
    *   **Serper API key:** For web search capabilities used by multiple agents. Get one from [serper.dev](https://serper.dev/) (free tier available).
*   **Reliable Web Access:** The crew relies heavily on accessing and reading the provided URLs and grant opportunity pages.

## Setup (Google Colab)

1.  **Get the notebook:** Clone the repository or download the `.ipynb` file.
2.  **Open in Colab:** Upload and open the notebook in Google Colab ([colab.research.google.com](https://colab.research.google.com/)).
3.  **Install libraries:** Run the first cell (`# @title 1. Install...`).
4.  **Configure API keys in Colab secrets:**
    *   Open Colab secrets (Key icon `<>` left sidebar).
    *   Enable "Notebook access".
    *   Add two secrets:
        *   Name: `OPENAI_API_KEY` | Value: Your OpenAI key (`sk-...`)
        *   Name: `SERPER_API_KEY` | Value: Your Serper key
    *   Ensure the toggle switch is **ON** for both secrets.
5.  **Run Cell 2:** Execute the second cell (`# @title 2. Import Modules...`). Check the output to confirm both API keys were found.

## How to use

1.  **Define input URLs and keywords (Cell 3):**
    *   Go to Cell 3 (`# @title 3. Define project and organization URLs...`).
    *   **Modify `project_info_url`:** Enter the URL of a webpage describing the project seeking funding.
    *   **Modify `organization_info_url`:** Enter the URL of a webpage detailing the applicant organization (e.g., About Us page).
    *   **(Optional) Modify `project_keywords_override`:** Add specific keywords to help guide the grant search if the project URL is too general.
    *   **Read and understand the DISCLAIMER printed by this cell.**
2.  **Select LLM (Optional - Cell 4):**
    *   Ensure GPT-4 Turbo is selected in Cell 4 for best results, especially for information extraction from web pages.
3.  **Run cells sequentially:** Execute the remaining cells (4 through 8) in order.
    *   Cell 5 defines the agents, including the new URL extractor agents.
    *   Cell 6 defines the tasks, starting with extracting info from the URLs.
    *   **Cell 7** creates the `Crew` and runs `kickoff()`. This involves web reading, searching, and analysis. It will take time and use API credits.
    *   **Cell 8** displays the final report. **Review the output and the final disclaimer critically.**

## Workflow overview

1.  **Project info extractor (Task 0a):** Reads the `project_info_url` and summarizes project details.
2.  **Organization info extractor (Task 0b):** Reads the `organization_info_url` and extracts relevant organizational details.
3.  **Opportunity searcher (Task 1):** Finds potential grant leads online based on extracted project info and keywords.
4.  **Grant info extractor (Task 2):** Visits lead URLs and extracts key grant details, including eligibility text.
5.  **Eligibility matcher (Task 3):** Compares extracted eligibility text against extracted organization details for a preliminary check.
6.  **Report compiler (Task 4):** Filters for potentially suitable grants and compiles a structured report with details, preliminary assessment, and mandatory disclaimers.

## Limitations & critical disclaimer (reiteration)

*   **URL accessibility & parsing:** The crew's success heavily depends on the ability of the tools (`WebsiteSearchTool`, etc.) to access and correctly parse the content of the provided URLs and grant pages. Complex websites, dynamic content, or PDFs (without specific tools) can cause failures.
*   **Information accuracy:** Information extracted from websites might be incomplete, outdated, or misinterpreted by the AI.
*   **Preliminary check only:** Eligibility assessment is automated and basic. **Human verification against official grant documents is essential.**
*   **Not exhaustive search:** The grant search is limited by the search tool and keywords used; it will likely miss many opportunities.
*   **NOT financial or legal advice.**
*   **API costs apply.**
