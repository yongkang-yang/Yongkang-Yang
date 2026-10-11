# Writing guide

For anyone (or any agent) drafting a post for this site from Yongkang's
reading notes. The notes come from BlogWatcher's `/api/ideas` export; see
CLOUD.md in the blogwatcher repo.

## Posts

- One Markdown file per post in `content/posts/`, named like
  `my-post-title.md`. Pushing to `master` publishes it.
- Front matter, with `draft: true` until Yongkang approves:

  ```yaml
  ---
  title: "Post title"
  date: 2026-10-11
  author: Yongkang Yang
  draft: true
  tags:
    - AI
  categories:
    - Technology
  ---
  ```

## Style

- English, for an international academic audience.
- Make one point clearly rather than translating or summarising whole sources.
- Short: normally 400–700 words.
- First-person claims come from Yongkang's own notes, never invented.
- Link the sources. Keep his views apart from the sources' claims; label
  uncertainty.
- Don't expose unpublished manuscripts, personal data, credentials, or private
  notes verbatim.
- AI proposes; Yongkang decides. Never publish or merge a post on its own.
