Schema diagram and notes

Models:

- Post
  - id (pk)
  - author -> FK to User
  - title
  - slug
  - body
  - status (draft/review/published)
  - created_at
  - updated_at
  - tags (M2M to Tag)

- Tag
  - id
  - name

- Comment
  - id
  - post -> FK to Post
  - user -> FK to User
  - body
  - created_at
  - is_approved

Migration notes:
- Initial migration created `Post`, `Tag`, and `Comment` models (see `blog/migrations/0001_initial.py`).

Business/analytics assumptions:
- `status` is used to track editorial workflow. Reports can count posts by status and by author.
- Tags are used for categorization; a simple tag cloud or tag counts table can be derived from the `Post.tags` M2M.
- Comments are freetext; `is_approved` allows moderation and analytics on engagement.
