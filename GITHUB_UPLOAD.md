# Uploading this project to GitHub

## Option 1: GitHub website

1. Create a new empty repository on GitHub.
2. Extract `poi-context-next-poi-github-ready.zip`.
3. Open the repository page and choose **Add file → Upload files**.
4. Upload the extracted files and folders.
5. Commit the upload.

## Option 2: Git command line

Open a terminal inside the extracted project folder:

```bash
git init
git add .
git commit -m "Add context-aware next-POI recommendation project"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

Before committing, run:

```bash
git status
```

Confirm that no Parquet datasets, API keys, tokens, caches, or credentials are staged.

## Updating a notebook later

After saving changes in Colab, use **File → Save a copy in GitHub**, or download the
notebook and replace the matching file under `notebooks/`, then commit:

```bash
git add notebooks/
git commit -m "Update experiment notebook"
git push
```
