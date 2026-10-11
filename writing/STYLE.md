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
- Hyperlink every primary source where it is mentioned: the original
  report, paper, announcement or interview, not a news digest or a
  secondary write-up. Use secondary coverage only for facts the primary
  source doesn't state, and link that too.
- Keep his views apart from the sources' claims; label uncertainty.
- Don't expose unpublished manuscripts, personal data, credentials, or private
  notes verbatim.
- AI proposes; Yongkang decides. Never publish or merge a post on its own.

## Public writing safeguards

- Protect privacy by default. Do not reveal private agent names, account access,
  permissions, system configuration, internal workflows, private conversations,
  unpublished work, or details of a personal incident. Do not quote private notes.
- First-person opinions are fine, but replace identifiable personal experiences
  with a general example or a linked public source. Never invent an experience.
- Avoid political opinions, partisan statements, criminal allegations, and
  sensitive or controversial commentary. Focus on the technical or research
  point. If an external source discusses a sensitive event, include only the
  neutral, verified facts needed to explain the point, or omit the example.
- Before sharing a draft, check the body, title, front matter, quotations,
  images, captions, and links for private information and sensitive claims.
  Flag any uncertain detail for review; do not assume it is safe to publish.
- Keep `draft: true` and require explicit approval before publication or
  merging any pull request.
