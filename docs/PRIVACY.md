# Privacy and public-release checklist

The included files were sanitized for release:

- Removed identifiable student cover page, contact details and institutional registration numbers by **excluding the uploaded PDF** (not a visually redacted copy).
- Removed all original Jupyter output cells, including potentially embedded HTML, plots, authentication prompts and screenshot/base64 contents.
- Removed the specific Google Cloud project identifier and replaced it with `YOUR_PROJECT_ID` in the archival notebook.
- Removed notebook execution counters, cell IDs and Colab metadata.
- No raw data, OAuth credential files, private Google Drive links or Google Cloud service-account keys are included.

Before publishing:

1. Search every file for your name, email, university/student IDs, project IDs, secrets, API keys, file paths, screenshot metadata, and notebook comments.
2. Confirm that your GitHub username and Git commit author/email are acceptable to disclose. GitHub commits have their own author metadata, **not controlled by notebook sanitization**. Consider GitHub's noreply email.
3. Never upload `credentials.json`, service account JSON, Colab credential caches, `.env`, raw BigQuery exports containing nonpublic data, or the original unsanitized PDF/notebook.
4. Check whether the dataset contains only genuinely public WDI indicators and whether any selected table uses private third-party enrichments.
5. Check `.gitignore` and run `git status` before committing.
6. Do not publish source BigQuery billing project IDs or screenshots of Cloud Console IAM/billing tabs.

The sanitization is based on the available uploaded files; no tool can guarantee privacy of files, commit metadata or assets added **after** packaging.
