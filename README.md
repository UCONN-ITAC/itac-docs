# ITAC Documents Contributor Guide

This guide contains all the information you will need to get started with contributing to the ITAC Documents website, which is powered by **Zensical**.

The core of the website lives in the main folder: `docs/`. Any Markdown (`.md`) file or folder placed within this directory will automatically be converted into a page or a section on the live website.

---

# Table of Contents

* [I want to...](#i-want-to)
* [Adding Documents](#adding-documents)
    * [Add a New Page](#add-a-new-page)
    * [Add a New Section (Group)](#add-a-new-section)
    * [Add Images](#add-images)
* [Learn to Use GitHub (with GitHub Desktop)](#learning-to-use-github-with-github-desktop)
* [Learn to Use Markdown](#learning-to-use-markdown)

# Adding Documents

Adding information to the ITAC Documents website has two main requirements: using **GitHub** (specifically GitHub Desktop for ease of use) and writing content in **Markdown**.

## Add a New Page

A page is a single document that will appear in the website's navigation sidebar.

### Step-by-Step

1.  **Navigate to the `docs/` folder** in your local copy.
2.  **Go into the desired section folder.** For example, to add a page to the "Training" section, navigate to `docs/Training/`.
3.  **Create a new file** with the `.md` extension (Markdown).
    * **Example Filename:** `introduction.md`
4.  **Add content.** Open the new file and add your content, starting with a Level 1 heading (`#`) which will act as the page title.

    > **Example Content in `introduction.md`:**
    >
    > ```markdown
    > # Connecting to ITAC Wi-Fi
    >
    > Follow these steps to connect your device:
    > 1. Open your Wi-Fi settings...
    > 2. ...
    > ```
5.  **Commit and Publish.** Use GitHub Desktop to commit your changes and push them to the repository (see [Learning to Use GitHub](#learning-to-use-github-with-github-desktop) for details).

## Add a New Section

A **Section** is a high-level grouping that appears in the top bar and contains multiple pages. Zensical handles the section title and ordering based on the folder name.

### Step-by-Step

1.  **Navigate directly to the `docs/` folder.**
2.  **Create a new folder** for your section.
    * **Example Folder Name:** `Recommendations/`
3.  **Create the Section's Landing Page.** Inside your new folder, you **must** create a file named `index.md`. This file serves as the main overview page for the entire section.

    > **File Structure Example:**
    >
    > ```
    > docs/
    > ├── hardware-support/
    > │   └── index.md  <-- This is the main page for the section
    > └── existing-section/
    > ```
4.  **Add Content to `index.md`.** This file should contain an introduction to the section.

    > **Example Content in `Recommendations/index.md`:**
    >
    > ```markdown
    > # Hardware Support Overview
    >
    > This section contains guides for troubleshooting and requesting new IT equipment.
    > ```
5.  **Add Pages to the Section.** You can now create additional `.md` files in the new folder (e.g., `hardware-support/request-new-laptop.md`) to build out the rest of your section.
6.  **Commit and Publish.** Use GitHub Desktop to commit your changes and push them to the repository.

## Add Images

To keep the project organized, all images should be stored in a dedicated folder.

### Step-by-Step

1.  **Locate the images folder.** Inside `docs/`, find the folder named `ReferencePhotos/`.
2.  **Upload your image.** Move your image file (PNG, JPG, or GIF) into that folder.
3.  **Reference the image in Markdown.** Use the following syntax to display the image on your page:

    ```markdown
    ![Alternative text for screen readers](../ReferencePhotos/your-image-name.png)
    ```

    * **Tip:** Ensure the path matches where you saved the file. If your page is inside a subfolder, you usually need `../` to "go up" one level to find the ReferencePhotos folder.

---

# Learning to Use GitHub (with GitHub Desktop)

For simplicity, we recommend using **GitHub Desktop**, a graphical interface application, to manage your changes. 

### Initial Setup (One-Time)

1.  **Install GitHub Desktop.** Download and install the application from the official website.
2.  **Authenticate.** Sign in with your GitHub account.
3.  **Clone the Repository.** Click **File** > **Clone Repository** and choose the ITAC Documents repository. This downloads a local copy of the files to your computer.

### Making and Sharing Changes (The Loop)

The typical workflow for making an update is: Fetch $\rightarrow$ Branch $\rightarrow$ Change $\rightarrow$ Commit $\rightarrow$ Push $\rightarrow$ Pull Request.

1.  **Fetch/Pull:** Before starting, click the **Fetch origin** or **Pull origin** button to ensure your local copy is up to date with the main repository.
2.  **Create a New Branch:** It's best practice to make all changes on a new branch. Click the **Current Branch** dropdown and select **New Branch...** (e.g., `feat/add-hardware-guide`).
3.  **Make Your Changes:** Edit, create, or delete files in the `docs/` folder using your favorite text editor.
4.  **Review and Commit:**
    * GitHub Desktop will list all your changes in the **Changes** tab.
    * Review the files to make sure they are correct.
    * Enter a **Summary** (required) and a longer **Description** (optional but helpful) for your changes.
    * Click the **Commit to [your branch name]** button.
5.  **Publish/Push:** Click the **Publish branch** or **Push origin** button. This uploads your changes from your local computer to your branch on GitHub.
6.  **Create a Pull Request (PR):** After pushing, GitHub Desktop will often prompt you to **Create a Pull Request**. This is how you submit your changes for review and merging into the main documentation. Click the button and finish creating the PR on the GitHub website.

---

# Learning to Use Markdown

Markdown is a lightweight markup language that allows you to easily format plain text. All pages in the ITAC Documents site are written in Markdown.

### Basic Formatting

| Type of Formatting | Markdown Syntax | Output Example |
| :--- | :--- | :--- |
| **Heading 1 (Page Title)** | `# Heading 1` | **Heading 1** |
| **Heading 2 (Major Subtitle)** | `## Heading 2` | **Heading 2** |
| **Bold Text** | `**Bold Text**` | **Bold Text** |
| **Italic Text** | `*Italic Text*` | *Italic Text* |
| **Numbered List** | `1. First item` | 1. First item |
| **Bullet List** | `* Another item` | * Another item |
| **Internal Link** | `[Link Text](path/to/page.md)` | Link Text |
| **External Link** | `[Google](https://google.com)` | Google |
| **Code/Command Line** | `` `code goes here` `` | `code goes here` |