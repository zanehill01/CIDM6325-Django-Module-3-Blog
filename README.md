# CIDM6325 Django Blog Project

This repo is a small Django blog used for Module 3 coursework. It demonstrates authentication, CRUD, forms and validation, HTMX interactions, and basic accessibility considerations.

## Quick run

1. Create and activate a virtual environment (PowerShell):

```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

2. Open http://localhost:8000/ to see the post list.

## What is implemented (mapping to rubric)

- Auth / CRUD / Workflow (40 pts)
  - Login/logout: Provided by Django's auth (`/accounts/` urls). Template at `templates/registration/login.html`.
  - CRUD: Post create/edit/delete in `blog/views.py` and templates `templates/post_form.html`, `templates/blog/post_detail.html`, `templates/blog/post_list.html`.
  - Workflow: `Post.status` with values draft/review/published. Publishing is gated by `blog.can_publish` permission.
  - Role-based permissions: `can_publish` and `can_review` defined in `Post.Meta.permissions`. Views check for `change_post` and `delete_post` and `can_publish`.
  - Bootstrap styling: Included in `templates/base.html`.
  - HTMX interactions: `hx_post_search` and `hx_post_inline_edit` implemented in `blog/views.py` and wired from `templates/blog/post_list.html` and `templates/blog/partials/_post_row.html`.

- Forms & Validation (Part A, 30 pts)
  - `PostForm` in `blog/forms.py` has custom validation `clean_title` and `clean`, `tags_csv` parsing, and a save method that attaches tags.
  - `CommentForm` validates against banned words.

- Multi-Model Design (Part B, 30 pts)
  - Models: `Post`, `Tag` (ManyToMany), `Comment` (OneToMany). See `blog/models.py`.

## Missing / Partial items (what I will implement next)

- CI/CD: No GitHub Actions workflow yet. I will add a minimal workflow that runs tests.
- Tests: `blog/tests.py` is empty. I will add unit tests for `PostForm` validation and permission checks.
- Documentation: This README (created) but I will add a rubric mapping section and a short schema diagram file.
- Accessibility: Some a11y improvements and WCAG notes are missing; I will add `ACCESSIBILITY.md` with items and small template fixes.

## Files of interest
- `blog/models.py` — data models and permissions.
- `blog/forms.py` — `PostForm` and `CommentForm`.
- `blog/views.py` — list/detail views, CRUD, and HTMX endpoints.
- `templates/` — project templates.
- `requirements.txt` — dependencies.

## Next steps I'm ready to implement
1. Add unit tests for forms and permissions.
2. Add GitHub Actions workflow for CI.
3. Add `ACCESSIBILITY.md` and make small template adjustments.
4. Produce a schema diagram (SVG or PNG) and migration notes.

If you'd like me to proceed, tell me which of the next steps to start with (I suggest tests → CI → accessibility → docs).

## Running tests and CI

Automated tests are included in `blog/tests.py`. To run tests locally:

```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py test
```

A minimal GitHub Actions workflow is included at `.github/workflows/ci.yml` which installs dependencies, runs migrations, and executes the test suite on pushes and PRs to `main`.