# Contributing at Nextday

**Naming and structure are a top priority.** Follow [NAMING.md](NAMING.md) for every repo,
Worker, database, folder, file, binding and URL.

1. **Branch** from `main` with a prefix: `feat/`, `fix/`, `chore/`, `docs/`.
2. **Commit** using [Conventional Commits](https://www.conventionalcommits.org):
   `feat: add order export`, `fix: handle empty cart`.
3. **Open a pull request** early (draft is fine). Fill in the template.
4. **Review**: one approval and green CI before merging. We squash-merge.
5. **Clean up**: the branch is deleted automatically after merge.

Never commit secrets, credentials, `.env` files or customer data.
