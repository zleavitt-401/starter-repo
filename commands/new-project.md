Ask the user: "What would you like to name your project?"

Wait for their response, then use that name as the project name throughout.

Create a new project with GitHub repo and Spec Kit:

1. Create project folder on my desktop named [project-name]
2. Navigate to that folder
3. Run: specify init . --ai claude
   (This downloads all Spec Kit templates and slash commands)
4. Initialize git repo
5. Create initial commit with Spec Kit files
6. Create GitHub repo named [project-name]
7. Push to GitHub
8. Provide:
   - Repo URL
   - Git clone command
   - Confirmation that folder is ready to open in VS Code

After I open the folder in VS Code, I'll run:
- /speckit.constitution with my project rules
- /speckit.specify with my feature specs
- Then continue with /speckit.plan, /speckit.tasks, /speckit.implement
