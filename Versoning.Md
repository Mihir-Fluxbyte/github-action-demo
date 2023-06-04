# To add versioning and releases for your GitHub Action, follow these steps

- Create and validate a release on a release branch (such as `release/v1`) before creating the release tag (for example, `v1.0.2`). This allows you to separate your releases from your main development branch.

- Create a release using semantic versioning. You can do this manually or by using the GitHub CLI. For more information, see [Managing releases in a repository](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).

To create a release with the GitHub CLI, use the following command (replace `TAG` with the desired tag for the release):

```bash
gh release create TAG
```

For example, to create a prerelease with the specified title and notes, use:

```bash
gh release create v1.3.2 --title "v1.3.2 (beta)" --notes "this is a beta release" --prerelease
```

- Move the major version tag (such as `v1`, `v2`) to point to the Git ref of the current release. For more information, see [Git basics - tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging).

- Introduce a new major version tag (e.g., `v2`) for changes that will break existing workflows. For example, changing an action's inputs would be a breaking change.

- Major versions can be initially released with a beta tag to indicate their status, for example, `v2-beta`. The `-beta` tag can then be removed when ready.

Your users can then reference your action using major release tags (e.g., `v1`) or specific patch release tags (e.g., `v1.0.1`):

```yaml
steps:
  - uses: your-username/your-repo@v1
```

or

```yaml
steps:
  - uses: your-username/your-repo@v1.0.1
```

For more information on using tags for release management, refer to the [GitHub Actions documentation](https://docs.github.com/en/actions/creating-actions/about-custom-actions#using-tags-for-release-management) ([Source 3](https://docs.github.com/en/actions/creating-actions/about-custom-actions)).
