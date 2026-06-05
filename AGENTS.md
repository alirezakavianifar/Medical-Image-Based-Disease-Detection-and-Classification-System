# Agent Instructions

## Git Remote

Changes must be pushed to: **https://github.com/alirezakavianifar/Medical-Image-Based-Disease-Detection-and-Classification-System.git**

Ensure the remote `origin` points to this URL. If not configured, use: `git remote add origin https://github.com/alirezakavianifar/Medical-Image-Based-Disease-Detection-and-Classification-System.git` or `git remote set-url origin <url>` to update).

## .gitignore

If `.gitignore` does not exist, create one based on the codebase structure and language. Adapt entries to match the project's technologies and build output locations.

## Git Push Workflow

When the user uses the keyword "push" in a request (e.g., "please push these changes", "push", or similar), you MUST follow this specific workflow:

1. **Stage all changes**: standard `git add .`
2. **Infer Commit Message**: Generate a concise, descriptive, and professional commit message based on the recent file changes and conversation context. Do not ask the user for a commit message unless they explicitly provide one.
3. **Commit**: `git commit -m "<inferred_message>"`
4. **Push**: `git push` (or `git push -u origin <branch>` if the upstream is not set).

**Note:** You should proactively execute these commands without asking for extra confirmation if the user explicitly said "push".

## README File

Always create a `README.md` file in the git repository that explains everything about the project (how to run it, how to get the results, etc.) and contains any necessary details so that future users can understand exactly how to run and verify the project.

## Language Rule

- Always respond and answer in English. Even if the user asks questions or provides input in another language (such as Persian), the agent must write all explanations, responses, and comments in English.
