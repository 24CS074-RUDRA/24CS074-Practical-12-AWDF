# Practical 12 screenshot checklist

Save genuine screenshots in this folder, then insert them in the matching
evidence box in `Practical 12 - CI-CD Report.docx`. The Word report contains
captions and reminders of what must be visible in each capture.

## Capture and insert screenshots

1. Open the relevant file, terminal, browser page, or GitHub Actions run.
2. Press **Windows + Shift + S** and drag a selection around the evidence.
   Include the relevant title, status, or test output; avoid unrelated desktop
   content.
3. Save the image as the exact PNG filename below in this folder.
4. Open the Word report, select the matching placeholder, and use **Insert >
   Pictures > This Device** to insert the saved screenshot. Resize it to fit
   the page without cropping out status or output.
5. Save the Word report after replacing the placeholder.

Never include passwords, JWTs, `.env` contents, access tokens, or other secrets
in screenshots.

| File | Evidence to capture |
| --- | --- |
| `01-docker-stack.png` | `docker compose ps` showing frontend/backend running and MongoDB healthy; optionally include the app at `http://localhost:5173`. |
| `02-workflow-file.png` | `.github/workflows/ci.yml` in VS Code with the push trigger, install step, and test step visible. |
| `03-passing-ci.png` | A green GitHub Actions run with the install and test steps visible. |
| `04-failing-ci.png` | The deliberately failing test run, including the red job and failed assertion. Capture before restoring the test. |
| `05-fixed-ci.png` | The next green Actions run after correcting the expected value. |
| `06-readme-badge.png` | Practical 12 GitHub README with the current green CI badge visible. |

## Produce the fail-then-fix evidence

The repository already has a passing baseline. To produce the required red
failure and a subsequent green run:

1. Open `backend/app.test.js` and temporarily change the first test's
   expectation from `401` to `200`.
2. Commit and push that intentional test-only failure:

   ```powershell
   git add backend/app.test.js
   git commit -m "Demonstrate a failing CI test"
   git push
   ```

3. In GitHub, open **Actions > CI Pipeline**, select this commit's run, expand
   **Run automated tests**, and capture `04-failing-ci.png`. Do not fix or push
   the test until this screenshot is saved.
4. Change the expected status back to `401`, then commit and push the fix:

   ```powershell
   git add backend/app.test.js
   git commit -m "Fix the CI test expectation"
   git push
   ```

5. Wait for the newest Actions run to finish successfully, then capture
   `05-fixed-ci.png`.

Refresh the Actions page if the run has not appeared yet. A missing test path
also fails CI, but its log reports that no tests were found; a deliberately
wrong expected status reports an assertion failure.
