# Commit Message Guidelines

In order to ensure that your commit history is descriptive and clear, a set of guidelines need to be established to maintain consistency across repositories as well as ensure readability.

Commit messages are meant to help in understanding what changes were made during a specific checkpoint in the repositories history. Meaningful commit messages help reduce the amount of time it takes to bring yourself or another developer up to date on the current state of the repository.

#### Commit message format

Use the following format for commit messages: 
```
[type]([optional scope]): [short description]
```

- `[type]`: One of the following types:
    - `feat`: New feature or functionality
    
    - `fix`: Bug fix or correction

    - `docs`: Documentation update or addition

    - `style`: Code style or formatting change

    - `refactor`: Code refactoring or optimization

    - `perf`: Performance improvement

    - `test`: Test addition or update
    
    - `chore`: Maintenance or administrative task

    - `revert`: Revert a previous commit

- `[optional scope]`: Optional scope or context for the commit (e.g., ui, api, database)

- `[short description]`: Brief summary of the changes made (50-72 characters)

#### Commit Message Best Practices

- Use imperative mood (e.g., "Add feature" instead of "Added feature")

- Keep the first line concise and focused on the main change

- Use bullet points or short paragraphs for longer descriptions

- Avoid using unnecessary words or phrases (e.g., "this commit")

- Use consistent verb tense throughout the commit message

#### Examples

```
feat: add new API endpoint for user authentication

- update app router to include new endpoint
- update authenticated routes to accept handle authentication
- add handlers for authentication errors
```

```
fix(ui): correct layout issue on mobile devices
```

```
docs: update README with new installation instructions
```

```
style: refactor code to follow PEP 8 guidelines
```

```
refactor(database): optimize query performance for large datasets
```

#### Tools and Resources

Use a commit message linter and tmeplate to ensure consistency and adherence to guidelines.

*TODO: add resource for using commit-msg hook to lint commit messages as well as resource for adding custom commit message template to system.*
