**Overview**

- **Purpose**: This repository automates screening of paper abstracts using the Copilot CLI. It uses a GitHub Actions workflow to detect new or changed BibTeX files under the papers/ folder and runs the Copilot model to accept or reject abstracts according to the selection criteria expressed in prompt.md.

**Requirements**
- **Node.js**: Install Node.js (tested with Node 22).
- **Copilot CLI**: The workflows use the `@github/copilot` CLI. Install with `npm install -g @github/copilot`.
- **GitHub secret**: A repository secret named `COPILOT_GITHUB_TOKEN` must be set for the Actions workflow.

**Reproduce Screening (locally)**
- **1) Install prerequisites**: ensure Node.js and npm are available and install the Copilot CLI.

```bash
# Install Copilot CLI globally
npm install -g @github/copilot
```

- **2) Set your Copilot token** (locally for testing). Export a token with the same name used in the workflow:

```bash
export COPILOT_GITHUB_TOKEN="<your-token-here>"
```

- **3) Run the screening command**. You can run Copilot directly against the repository BibTeX files. Example (runs the model once over all bib files):

```bash
copilot --model gpt-5-mini -p "follow the prompt.md file to decide whether to accept or reject the articles' abstracts in papers/**/*.bib"
```

Notes:
- When running locally you may pass a specific list of files instead of the glob. The GitHub Actions workflow computes the list of added files, but falling back to all `papers/**/*.bib` when none were added.

**GitHub Actions workflow**
- The workflow is defined in [.github/workflows/copilot-screening.yml](.github/workflows/copilot-screening.yml).
- Triggers: `workflow_dispatch` (manual) and `push` events that change files under `papers/**/*.bib` or the workflow file itself.
- Key steps:
  - Checkout repository.
  - Install Node (Node 22) and the Copilot CLI.
  - Detect newly added `.bib` files. If none are added, it falls back to all BibTeX files under `papers/`.
  - Run Copilot with model `gpt-5-mini` and the prompt referencing `prompt.md`. The run uses a matrix `iteration: [1,2,3,4,5]` so Copilot runs multiple iterations per screening.

**Important files**
- **Prompt**: [prompt.md](prompt.md)
- **Papers**: `papers/*.bib` (BibTeX files to screen)
- **Workflow**: [.github/workflows/copilot-screening.yml](.github/workflows/copilot-screening.yml)

**Tips and troubleshooting**
- Ensure `COPILOT_GITHUB_TOKEN` is valid and has the required access for the Copilot CLI.
- If you want to test a single file, replace the glob in the Copilot command with the path to that `.bib` file.
- The workflow runs multiple iterations (matrix). To change the number of iterations, edit the matrix in the workflow file.
