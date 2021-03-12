# Coding Standards

Maintaining consistent coding standards is an essential part of developing clean, uniform, easily readable code. We
follow best practices for our  Python codebases.

- [Coding Standards](#coding-standards)
  - [Python](#python)

---

## Python

We follow the most of the Python coding standards used by the
[Django project](https://docs.djangoproject.com/en/1.11/internals/contributing/writing-code/coding-style/). The major
areas of standardization are:

- **Linting**: Use [pylint](https://www.pylint.org/) to lint all Python code. We use a line width of 119 to match the
- Django project.
- **Indentation**: Use tabs for indentation.
- **Class Names**: Use CamelCase for class names (e.g. DentalVists).
- **Other Names**: Use lowercase and underscores for variable, function and method names (e.g. api.get_num_objects().
- **Constants**: Use all-capitals.
