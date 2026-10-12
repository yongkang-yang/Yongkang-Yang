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
- **Opinion posts:** 500 words maximum.
- **In-depth articles:** 1,000 words maximum.
- Count words in the published article body (including headings and quoted text),
  excluding Markdown front matter. Edit down rather than treating these as targets.
- First-person claims come from Yongkang's own notes, never invented.
- Hyperlink every primary source where it is mentioned: the original
  report, paper, announcement or interview, not a news digest or a
  secondary write-up. Use secondary coverage only for facts the primary
  source doesn't state, and link that too.
- Keep his views apart from the sources' claims; label uncertainty.
- Don't expose unpublished manuscripts, personal data, credentials, or private
  notes verbatim.
- AI proposes; Yongkang decides. Never publish or merge a post on its own.

## Voice: direct, natural, specific

- Write like a person with a point to make, not an AI assistant trying to sound
  balanced. State the point plainly and let evidence and examples do the work.
- Remove defensive caveats that add no useful information, such as
  "It is a proposal, not an announced company policy—but it captures the point."
  Do not add a disclaimer after every claim.
- Avoid stock AI phrasing: "It is important to note," "This highlights the
  importance of," "It is worth considering," and other empty transitions.
- Cut repeated explanations, padded introductions, abstract summaries, and
  formulaic "not X but Y" constructions. Use concrete examples when useful.
- Prefer clear verbs, short sentences, and natural sentence variation.
  Do not turn every paragraph into a three-part list or a mini-conclusion.
- Keep necessary distinctions: state what a study actually found, attribute
  opinions correctly, and qualify claims when the uncertainty changes their
  meaning. Accuracy is not a reason to write defensively.
- In the final edit, delete any sentence that only repeats, softens, or explains
  the preceding point without adding evidence or insight.

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
