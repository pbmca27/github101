The error you're seeing: remote: Support for password authentication was removed on August 13, 2021. remote: Please see https://docs.github.com/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.

Answer remote: Support for password authentication was removed on August 13, 2021. means that GitHub no longer accepts password-based authentication for Git operations. Instead, GitHub now requires you to use:

* Personal Access Token (PAT)
* SSH Keys
* GitHub CLI How to Fix This (Use PAT for HTTPS):
1. Generate a Personal Access Token (PAT): Go to GitHub > Click on your profile > Settings. In the left sidebar, select Developer Settings > Personal Access Tokens > Tokens (classic). Click Generate new token. Select scopes: repo (for repository access) workflow (for GitHub Actions) write:packages (if needed) delete_repo (optional) Generate token and copy it (you won't see it again).
2. Cache the Token in Git (Recommended): bash Copy code git config --global credential.helper store This caches the token for reuse, so you don't need to re-enter it.
3. Push Using the Token: When Git asks for your password during git push, use the token instead of your GitHub password.

Alternatively, update the remote URL directly to include the token:

bash Copy code git remote set-url origin https://:@github.com//.git Example:

bash Copy code git remote set-url origin https://pbmca27:ghp_ABC1234567890xyz@github.com/pbmca27/github101.git

Alternative (Use SSH): Generate SSH Key (if not already done): bash Copy code ssh-keygen -t ed25519 -C "your-email@example.com" Add the SSH Key to GitHub: bash Copy code cat ~/.ssh/id_ed25519.pub Copy the key and add it under GitHub > Settings > SSH and GPG keys. Update Remote to SSH: bash Copy code git remote set-url origin git@github.com:pbmca27/github101.git Testing: bash Copy code git push -u origin main This should now work without prompting for a password.
Links: 
* Beginner & Professional: https://www.youtube.com/watch?v=S7XpTAnSDL4 
* Advanced: https://www.youtube.com/watch?v=qsTthZi23VE 
* GitHub + GitHub Actions: https://www.udemy.com/course/github-actions-the-complete-guide/learn/lecture/34155388#overview