Git Commands Cheatsheet
Essential commands for everyday development

The Core Workflow (You'll Use This Daily)
			git status                    				# Check what's changed
			
			git add filename.js          			# Stage a specific file

			git add .                     				# Stage ALL changed files

			git commit -m "your message"  		# Save changes with a description

			git push origin main          			# Send commits to GitHub

			git pull origin main          			# Get latest changes from GitHub


The Daily Cycle:
    1. Make changes in VS Code
    2. git status - see what changed
    3. git add . - stage everything
    4. git commit -m "description" - save with message
    5. git push origin main - upload to GitHub


📋 Repository Setup Commands

Starting a New Project

	Option A: Create locally first

			mkdir my-project              	# Create folder

			cd my-project                 	# Go into folder

			git init                      		# Initialize git repo

			git add .                     		# Stage all files

			git commit -m "Initial commit"
# Then create repo on GitHub and connect it (see below)


Option B: Clone existing repo

			cd ~/Developer                	# Go to your projects folder
			git clone https://github.com/username/repo-name.git
			cd repo-name                  	# Go into the cloned folder


Connecting Local Repo to GitHub

			git remote add origin https://github.com/username/repo-name.git
			git branch -M main            		# Rename branch to main
			git push -u origin main       		# Push and set upstream

Checking Status & History
			git status                    			# What files changed? What's staged?
			git log                       			# See commit history (press 'q' to exit)
			git log --oneline             		# Compact commit history
			git log --oneline --graph     		# Visual branch history
			git diff                      			# See exact line changes (unstaged)
			git diff --staged             		# See changes that are staged
			git show                     	 		# Show last commit details

Pro tip: git status is your best friend. Run it constantly!


Committing Changes
		Basic Commits

			git add filename.js           					# Stage one file
			
			git add file1.js file2.js     					# Stage multiple specific files

			git add .                    	 					# Stage everything in current folder

			git add -A                    						# Stage everything in entire repo

			git commit -m "Add login feature"             		# Commit with message

			git commit -m "Fix bug" -m "Details here"      	# Commit with description
			
			git commit --amend -m "New message"           # Change last commit message


Unstaging Files

			git reset filename.js         	# Unstage a file (keeps changes)

			git reset                     		# Unstage all files (keeps changes)

Discarding Changes

			git checkout -- filename.js   	# Discard changes to a file (DANGER!)

			git restore filename.js       		# Same as above (newer syntax)

			git clean -fd                 			# Delete untracked files (DANGER!)

⚠️ Warning: Discard commands permanently delete your work!


Branching (Important for Features)
Branches let you work on features without affecting main code.

Basic Branch Commands

			git branch                    				# List all branches (* = current)

			git branch feature-name       		# Create new branch

			git checkout feature-name     		# Switch to branch

			git checkout -b feature-name  		# Create AND switch to new branch

			git branch -d feature-name    		# Delete branch (safe)

			git branch -D feature-name    		# Force delete branch

Branch Workflow Example

			git checkout -b add-login    		 # Create branch for new feature
			# ... make changes and commits ...

			git checkout main             			# Switch back to main

			git merge add-login           			# Merge feature into main

			git branch -d add-login       			# Delete feature branch
	
Modern Syntax (Git 2.23+)
	
			git switch main               		# Switch to main branch

			git switch -c feature-name    	# Create and switch to new branch



Syncing with GitHub

	Pushing (Upload your commits)
			git push origin main          			# Push main branch to GitHub
			
			git push origin branch-name   		# Push specific branch

			git push -u origin main       			# Push and set upstream (first time)
	
			git push                      				# Push to default upstream

	Pulling (Download changes)
			git pull origin main          	# Get latest from GitHub

			git pull                      		# Pull from default upstream

			git fetch origin             		# Download changes but don't merge

	When Push is Rejected

			# Someone else pushed changes first
			git pull origin main          				# Get their changes first

			# Fix any conflicts if needed
			git push origin main          				# Now push your changes


Merging & Conflicts
	Basic Merge
			git checkout main            		# Switch to main
		
			git merge feature-branch      	# Merge feature into main

	When Conflicts Happen
			git merge feature-branch      # Conflict occurs!
	
		# 1. Open conflicted files in VS Code
		# 2. Look for <<<<<<, ======, >>>>>> markers
		# 3. Edit to keep what you want
		# 4. Remove conflict markers

			git add .                     		# Stage resolved files

			git commit                    		# Complete the merge (no -m needed)

	Abort a Merge
			git merge --abort             	# Cancel merge, go back to before

	Undoing Things
		Undo Last Commit (Keep Changes)
			git reset --soft HEAD~1       # Undo commit, keep changes staged

			git reset HEAD~1             	# Undo commit, unstage changes

			git reset --hard HEAD~1      # Undo commit, DELETE changes (DANGER!)

	Undo Multiple Commits
			git reset --soft HEAD~3       # Undo last 3 commits, keep changes

	Revert a Commit (Safe for Shared Repos)
			git revert abc123             # Create new commit that undoes abc123

			git revert HEAD               # Undo last commit with new commit

Difference:
                    * reset - rewrites history (use on local only)
                    * revert - creates new commit (safe for shared repos)


	Tags (Version Releases)
			git tag                       				# List all tags

			git tag v1.0.0                				# Create lightweight tag

			git tag -a v1.0.0 -m "Release 1.0"  	# Create annotated tag

			git push origin v1.0.0        			# Push specific tag

			git push origin --tags        			# Push all tags

			git tag -d v1.0.0             			# Delete local tag


	Viewing & Searching
			git log --author="Your Name"  		# Commits by specific person

			git log --since="2 weeks ago" 		# Recent commits

			git log --grep="bug"          			# Search commit messages

			git log filename.js           			# History of specific file

			git blame filename.js         			# Who changed each line?

			git show abc123               			# Show specific commit details


	Stashing (Temporary Storage)
	Save work-in-progress without committing:
			
			git stash                     				# Save current changes

			git stash save "description"  		# Save with description

			git stash list                				# List all stashes

			git stash pop                 			# Apply last stash and remove it

			git stash apply               			# Apply last stash, keep it

			git stash drop                			# Delete last stash

			git stash clear               			# Delete all stashes


	Use Case: You're working on a feature, but need to quickly switch to main:
			git stash                     				# Save your work

			git checkout main             			# Switch branches
			# ... do urgent fix ...

			git checkout feature-branch   		# Back to your feature

			git stash pop                 			# Continue where you left off



Configuration
	
	User Settings

			git config --global user.name "Your Name"

			git config --global user.email "you@example.com"

			git config --global core.editor "code --wait" 		 	# Use VS Code

			git config --list             								# See all settings

	Repository Settings

			git remote -v                 				# Show remote URLs

			git remote add origin url     			# Add remote repository

			git remote set-url origin url 			# Change remote URL

			git remote remove origin      		# Remove remote

	.gitignore
	Create a .gitignore file to tell Git what NOT to track:

		# Example .gitignore content
			.DS_Store                     		# Mac system files

			node_modules/                 	# Dependencies (large!)

			.env                          		# Secret keys

			*.log                         		# Log files

			dist/                         		# Build folders

			.vscode/                      		# Editor settings

	After creating .gitignore:

			git add .gitignore
			git commit -m "Add gitignore"

	Remove already-tracked files:
			git rm --cached filename      		# Stop tracking a file
			git rm --cached -r folder/    			# Stop tracking a folder


Emergency Commands

	Recover Deleted Commits

			git reflog                    			# See ALL actions (even deleted commits)

			git checkout abc123          		# Restore to a specific commit

	Discard ALL Local Changes

			git reset --hard HEAD         		# Discard all changes, back to last commit

			git clean -fd                 			# Remove untracked files

	Fix "Detached HEAD"
		
			git checkout main             		# Get back to main branch


Best Practices
	Good Commit Messages
	# ❌ Bad
			git commit -m "fix"
			git commit -m "changes"
			git commit -m "update"

	# ✅ Good
			git commit -m "Fix login button not responding on mobile"
			git commit -m "Add user authentication with JWT"
			git commit -m "Update README with installation instructions"

	Format:
            * Start with a verb (Add, Fix, Update, Remove, Refactor)
            * Be specific but concise
            * Present tense ("Add feature" not "Added feature")

Commit Frequency
        * Commit often (every meaningful change)
        * Don't commit broken code to main
        * Each commit should be one logical change

Before Pushing
			git status                    		# Check what you're committing
	
			git log --oneline -5          	# Review recent commits
			
			git push origin main          	# Push to GitHub


Common Workflows
	Feature Development
			
			git checkout -b add-dark-mode          		# New feature branch
			# ... make changes ...

			git add .

			git commit -m "Add dark mode toggle"

			git push origin add-dark-mode          			# Push feature branch
		
			# Create Pull Request on GitHub
			# After PR is merged:

			git checkout main

			git pull origin main                   				# Get merged changes

			git branch -d add-dark-mode            			# Clean up local branch


	Daily Development
			git pull origin main                   				# Start day with latest code
			# ... work on features ...

			git add .

			git commit -m "descriptive message"

			git push origin main                   				# End day, push work


	Fixing a Bug
			git checkout -b fix-login-bug
			# ... fix the bug ...

			git add .

			git commit -m "Fix login redirect bug"

			git push origin fix-login-bug
			# Create PR, get reviewed, merge


Quick Reference Card
	Most Used (90% of the time):
			git status

			git add .

			git commit -m "message"

			git push origin main

			git pull origin main

			git log --oneline

	Branch Work:
			git checkout -b feature-name

			git checkout main

			git merge feature-name

	Undo Mistakes:
			git reset HEAD~1              		# Undo last commit

			git checkout -- filename      	# Discard file changes
			
			git stash                     			# Save work temporarily


Learning Resources
    * Official Docs: git-scm.com/doc
    * Interactive Tutorial: learngitbranching.js.org
    * Visualizer: git-school.github.io/visualizing-git
    * Cheatsheet: education.github.com/git-cheat-sheet-education.pdf

Practice Exercises
1. Create a test repo: mkdir git-practice && cd git-practice
2. git init
3. echo "# Practice" > README.md
4. git add . && git commit -m "Initial commit"
5. 
6. Practice branching: git checkout -b test-branch
7. echo "new feature" > feature.txt
8. git add . && git commit -m "Add feature"
9. git checkout main
10. git merge test-branch
11. 
12. Practice undoing: echo "mistake" > oops.txt
13. git add . && git commit -m "Oops"
14. git reset HEAD~1              # Undo it!
15. 

Keep this cheatsheet handy - you'll reference it constantly in your first few months!
Pro Tip: Print this out or save it in your learning-journal repo for quick access.