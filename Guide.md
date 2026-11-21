# Build a Personal Notes System with Obsidian, Git, GitHub and ChatGPT

*A beginner's guide to keeping your notes local, tracking their history, storing a remote copy and using AI to help you work with them.*

This guide is for someone starting from zero. You do not need to know Git, use Obsidian already, or have a GitHub repository. We will set everything up from scratch and explain what each part is for

## 1. What are we building?

The goal is a personal notes system that is comfortable to use, easy to back up, portable between computers and useful with an AI assistant.

Four tools work together:

| Tool | Its job | In plain English |
| --- | --- | --- |
| **Obsidian** | Write and organize notes | The notebook you use every day |
| **Git** | Track changes | A history that records saved versions of your notes |
| **GitHub** | Store the repository online | A remote home for your notes and their history |
| **ChatGPT** | Help you work with the information | An assistant that can search, explain, summarize and help improve your notes |

The relationship looks like this:

```text
       YOU
        |
        v
    OBSIDIAN
  Write and organize
        |
        v
       GIT
 Record changes locally
        |
    push / pull
        |
        v
     GITHUB
 Remote repository
        |
  authorized access
        |
        v
    CHATGPT
 Search, explain, summarize,
 compare and suggest changes
        |
   You review and apply
   accepted changes
        |
        v
    OBSIDIAN
```

These tools do different jobs. Obsidian is where you work with your notes. Git keeps their history. GitHub stores a remote copy. ChatGPT is an optional assistant that can use the notes you authorize it to access.

## 2. Why use this instead of one all-in-one notes app?

### You keep control of your files

Obsidian notes are ordinary Markdown files stored in a folder on your computer. They are not locked inside an online notes service or a proprietary database. You can open them in a text editor, move them to another computer or use another Markdown application.

### You get a history of your work

Git records snapshots called **commits**. You can see what changed, compare two versions and restore an earlier version if you make a mistake.

This is useful for more than software projects. It works for personal notes, research, plans, journaling, hobby documentation, shopping lists and reference material.

### You have a remote copy

GitHub stores the repository online. If your computer fails, the remote repository still contains the commits you pushed. You can also clone the repository onto another computer.

### Your AI assistant can use your actual notes

With the supported GitHub connection enabled, ChatGPT can retrieve content from repositories you have authorized. Instead of repeatedly copying and pasting notes into a conversation, you can ask it to look up relevant information in your repository.

For example:

- "Summarize the projects I'm currently working on."
- "Find the note where I wrote down my PC specifications."
- "Compare these two plans and point out contradictions."
- "Turn these rough notes into a clear how-to guide."
- "Look through my ideas and group related ones together."

ChatGPT is an assistant, not the owner or storage location of your notes. The repository remains the durable record.

This system can also serve as an extension to ChatGPT's built-in memory. By keeping personal knowledge, project history, preferences and important decisions in an organized, persistent repository, ChatGPT can retrieve relevant information when needed rather than relying entirely on its limited conversational memory. This creates a more detailed, user-controlled and portable knowledge base that can grow alongside the user and remain useful even when switching AI assistants.


## 3. What you need before starting

You need:

1. A computer running Windows, macOS or Linux.
2. An internet connection for downloading software and using GitHub.
3. An Obsidian installation.
4. Git installed on the computer.
5. A free GitHub account.
6. A ChatGPT account and access to the GitHub app/connector in the ChatGPT experience you use, if you want the AI part.

Obsidian's local note-taking features can be used without paying for Obsidian Sync. Git and GitHub also have free ways to use the workflow described here. Service plans and features can change, so check current terms before relying on a particular feature.

## 4. Install the tools

### A. Install Obsidian

1. Visit [obsidian.md](https://obsidian.md/).
2. Download the version for your operating system.
3. Install and open it.
4. You can close it for the moment; we will create the vault after the GitHub repository is ready.

Obsidian stores notes in a **vault**. A vault is simply a folder on your computer that Obsidian treats as your notes workspace.

### B. Install Git

Git is a separate program. Installing Obsidian does not install Git.

1. Visit the official [Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
2. Download Git for your operating system and follow the installer instructions.
3. On Windows, Git for Windows includes Git Bash, a terminal where you can run Git commands.
4. On macOS and Linux, use the Terminal application. Your distribution may offer Git through its normal package manager.

To check that Git is installed, open a terminal and run:

```bash
git --version
```

You should see a version number. If the command is not found, Git is either not installed or not available in your terminal's PATH.

### C. Create a GitHub account

1. Visit [github.com](https://github.com/).
2. Create an account or sign in.
3. Verify your email address if asked.

GitHub is the online service that will store your remote repository.

## 5. Create your first repository on GitHub

A **repository** (often shortened to *repo*) is a folder whose files and change history are tracked by Git.

1. Sign in to GitHub.
2. Use the **New repository** option.
3. Give it a simple name, for example `MyNotes`.
4. Add a short description if you like.
5. Choose **Private** if the notes are intended for you alone. Choose Public only if you are comfortable with anyone being able to read them.
6. You can select **Add a README file** to give the repository a starting page.
7. Create the repository.

You now have an online repository, but it has not yet been copied onto your computer.

**A privacy reminder:** A private repository limits who can browse it, but it is not a personal encrypted vault. Do not store passwords, recovery codes, private keys, payment details or other secrets in it. Also remember that when you authorize an app such as ChatGPT to access a repository, the app may process content from that repository under its own terms.

## 6. Copy the repository onto your computer

The next step is to **clone** the repository. Cloning downloads the files and Git history and connects the local copy to GitHub.

1. Open your new repository on GitHub.
2. Select the green **Code** button.
3. Choose **HTTPS** and copy the clone address. It should look like:

```text
https://github.com/YOUR-USERNAME/MyNotes.git
```

4. Choose where you want to keep your notes on your computer. For example, create a folder called `Notes` in your Documents folder.
5. Open a terminal in that parent folder.
6. Run the clone command, replacing the example address with your own:

```bash
git clone https://github.com/YOUR-USERNAME/MyNotes.git
```

Git creates a `MyNotes` folder. That folder contains your notes repository and a hidden `.git` directory containing its history and settings.

If Git asks you to authenticate, use a supported GitHub sign-in method. Do not enter your normal GitHub account password as a Git password. GitHub recommends HTTPS with a credential helper such as Git Credential Manager, or SSH key authentication. See [GitHub's authentication guide](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github).

### Set your Git author details

Git records who made each commit. If it asks for your identity, set a name and email in the terminal:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Use an email address you are happy to associate with your commits. GitHub also provides a private no-reply email address if you prefer not to expose your normal email in commit metadata.

## 7. Turn the folder into an Obsidian vault

Now we connect Obsidian to the folder that Git cloned.

1. Open Obsidian.
2. Choose **Open folder as vault** (the wording may vary slightly by version).
3. Browse to the `MyNotes` folder created by Git.
4. Select it.

That's it. The folder is now an Obsidian vault, and any Markdown notes you create there are also files inside your Git repository.

Create a test note called `Welcome` and add a few lines. Obsidian saves the file in the vault folder.

**Important:** Do not create a separate empty vault and then clone the repository somewhere else by accident. The folder you open in Obsidian should be the same folder that contains the repository's hidden `.git` directory.

## 8. Add Git controls inside Obsidian

You can use Git from the terminal, but a community plugin makes common operations easier to access inside Obsidian.

1. In Obsidian, open **Settings → Community plugins**.
2. Enable community plugins or turn off Restricted mode when prompted.
3. Choose **Browse**.
4. Search for **Git** (the community plugin commonly known as **Obsidian Git**, by Vinzent).
5. Install it and enable it.
6. Open the Command Palette and search for commands beginning with `Git:`.

The plugin can help you review changes, commit, pull, push and inspect history without leaving Obsidian.

The plugin does not replace the Git program installed in the previous steps. It provides an Obsidian interface for using it.

### A note about Obsidian settings

Obsidian creates a hidden `.obsidian` folder for vault settings and plugin configuration. Some settings may be useful to share between computers; others are personal to a particular device. Do not blindly upload every configuration file.

A simple optional `.gitignore` file can exclude temporary workspace and operating-system files:

```gitignore
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/
.DS_Store
Thumbs.db
desktop.ini
```

Do not ignore the entire `.obsidian` folder unless you deliberately want every Obsidian setting to remain local. Before committing plugin settings, check that they do not contain API keys, passwords or tokens.

## 9. Make your first commit and push

You have a local vault and a remote GitHub repository. Now test the complete workflow.

1. In Obsidian, create or edit a small note.
2. Open the Obsidian Git plugin's Source Control view or Command Palette.
3. Review the changed files and the diff (the diff shows what changed).
4. Commit the changes with a message that describes them, for example:

```text
Add my first notes
```

5. Push the commit to GitHub.
6. Open the repository in your browser and check that the note appears.

A **commit** saves a named snapshot to the local Git history. A **push** sends that commit to GitHub. These are separate actions: committing does not automatically upload the change.

The basic Git commands behind the workflow are:

```bash
git status
git add .
git commit -m "Add my first notes"
git push
```

The Obsidian Git plugin can run the equivalent operations for you. Review changes before committing so you know what is being uploaded.

## 10. Connect GitHub to ChatGPT

This part is optional. You can use Obsidian, Git and GitHub perfectly well without ChatGPT.

The ChatGPT GitHub app/connector is a **separate connection** from Git authentication on your computer.

1. Open ChatGPT settings.
2. Find **Apps** (the exact menu name and availability may vary).
3. Look for **GitHub** and choose Connect.
4. You will be sent to GitHub to authorize the ChatGPT app.
5. Choose which repositories the app is allowed to access. For a first test, select only the notes repository you created.
6. Return to ChatGPT and check whether the repository is available.

A newly authorized or private repository may take a little time to appear. If it does not show up, open the GitHub app settings on GitHub and check that the correct account and repository have been granted access. Some organizations require an administrator to approve the connection.

### What ChatGPT can do with the connection

In supported ChatGPT experiences, you can ask it to search and analyze repository content, including Markdown notes and documentation. Try a simple request:

> Search my MyNotes repository and summarize the notes it contains. Tell me which files you used.

Then try something more useful:

> Find notes that mention projects or goals. Group them into a short overview and cite the files you found them in.

You should know one important limitation: **the standard ChatGPT GitHub app is read-only.** It can retrieve and analyze repository content, but connecting it does not give ChatGPT permission to commit edits or push changes to your repository. If you want to change a note, ask ChatGPT to draft the revised content, review it, paste or apply the accepted changes in Obsidian, and use Git to commit and push them.

GitHub availability can vary by ChatGPT plan and product surface. If GitHub is not available in your normal chat, check the app directory and current plan/feature availability. See [OpenAI's current GitHub connection guide](https://help.openai.com/en/articles/11145903-connecting-github-to-chatgpt).

The connection retrieves authorized content when needed. It does not continuously mirror your entire notes folder into ChatGPT, and it does not replace pushing your notes to GitHub.

## 11. The normal day-to-day routine

Once everything is installed, the workflow is straightforward.

### When you write notes

1. Open Obsidian.
2. Write or update your notes.
3. Review the files changed in the Git plugin.
4. Commit the changes with a clear message.
5. Push to GitHub.

A commit message can be simple:

- `Add notes from today's research`
- `Update project plan`
- `Add shopping list`

Start with manual commits and pushes. Once you understand the process, you can explore automatic commit-and-sync features in Obsidian Git. Automation is convenient, but manual review is a better way to learn and catch mistakes.

### When you want ChatGPT's help

1. Push your latest notes to GitHub first.
2. Ask ChatGPT to search or analyze the repository.
3. Tell it which files or subject matter are relevant.
4. Review its answer and any proposed changes.
5. Apply changes you accept in Obsidian.
6. Commit and push the updated notes.

This keeps you in control of what becomes part of your permanent notes.

### When you use another computer

1. Install Git and Obsidian on that computer.
2. Clone the same GitHub repository.
3. Open the cloned folder as an Obsidian vault.
4. Before editing, pull the latest changes.
5. After editing, commit and push.

Avoid editing the same note on two computers before syncing. If both copies change, Git may report a **merge conflict**. That is not necessarily lost data, but it means you must review the competing edits and decide how to combine them.

## 12. What can go wrong?

| Problem | What to check |
| --- | --- |
| `git` is not recognized | Git may not be installed or the terminal may need to be reopened after installation. |
| GitHub keeps asking for a password | GitHub account passwords are not accepted for Git operations over HTTPS. Configure Git Credential Manager or SSH. |
| Obsidian cannot find the vault | Open the actual cloned repository folder, not its parent folder or a different empty vault. |
| Push is rejected | Pull and inspect remote changes first. Do not force-push as a first response. |
| ChatGPT cannot find the repository | Check the GitHub app's repository permissions, the connected account and feature availability. Newly authorized repositories can take a while to appear. |
| ChatGPT proposes an incorrect change | Treat AI output as a draft. Verify it, apply it yourself and use Git history to keep track of the change. |
| Two computers have different versions | Pull before editing and push after committing. Resolve conflicts carefully. |

If something goes wrong, stop before deleting files, reinitializing the repository or force-pushing. Make a copy of the affected notes and inspect the Git status and history first.

## 13. Security, privacy and backup

This setup gives you control and a remote copy, but it is not magic.

- A private GitHub repository is visible to the account owner and any people or apps you authorize. It is not the same as end-to-end encrypted storage.
- ChatGPT can process content from repositories you authorize. Check the current ChatGPT connected-app and data settings before connecting personal notes.
- Do not store passwords, recovery codes, API keys, private keys, financial credentials or highly sensitive information in the repository.
- Git history can retain information even after you delete it from the latest version of a file. Avoid committing secrets in the first place.
- GitHub is a useful remote copy, but it should not be your only backup. Keep a separate backup of important notes, for example on an external drive or another backup service.
- Be selective about what you put in the vault. A personal notes repository does not need to contain every private document you own.

## 14. Why this is useful

The real advantage is that each tool solves a different problem without taking control away from you.

- **Obsidian** gives you a pleasant place to think and write.
- **Git** gives you a transparent history and a way to recover earlier versions.
- **GitHub** gives you an off-device repository and a way to access it from other computers.
- **ChatGPT** gives you an AI helper that can search and reason over the notes you choose to share with it.

You are not building a complicated database or depending on one proprietary notes platform. You are combining ordinary files with a history system, remote hosting and an optional AI assistant.

### The one-sentence version

**Write your notes in Obsidian, track their history with Git, store the repository on GitHub, and let ChatGPT help you understand and improve the information.**

---

## Official resources

- [Obsidian: Download](https://obsidian.md/)
- [Obsidian: Help and getting started](https://help.obsidian.md/)
- [Obsidian Git plugin: Installation](https://publish.obsidian.md/git-doc/Installation)
- [Obsidian Git plugin: Getting Started](https://publish.obsidian.md/git-doc/Getting%20Started)
- [Git: Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [GitHub: Set up Git](https://docs.github.com/en/get-started/git-basics/set-up-git)
- [GitHub: About remote repositories](https://docs.github.com/en/get-started/git-basics/about-remote-repositories)
- [GitHub: Authentication](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)
- [OpenAI: Connecting GitHub to ChatGPT](https://help.openai.com/en/articles/11145903-connecting-github-to-chatgpt)

*Menus, plugin options and ChatGPT feature availability can change. Use the official documentation if an installation screen looks different from the steps above.*
