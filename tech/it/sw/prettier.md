# Overview

- https://prettier.io
- Prettier is an opinionated code formatter.
    + Prettier takes your code and reprints it from scratch by taking
      the line length into account.
    + It removes all original styling and ensures that all outputted
      code conforms to a consistent style.
- By far the biggest reason for adopting Prettier is to stop all the
  ongoing debates over styles.
    + Yet the more options Prettier has, the further from the above goal
      it gets. The debates over styles just turn into debates over which
      Prettier options to use. Formatting wars break out with renewed
      vigour: “Which option values are better? Why? Did we make the
      right choices?”
    + Prettier has a few options because of history. But we won’t add
      more of them.

# Rationale

- Correctness
    + Same behavior after formatting
- Strings
    + Chooses the one which results in the fewest number of escapes. In
      case of a tie or the string not containing any quotes, Prettier
      defaults to double quotes. (this can be changed via the
      singleQuote option)
    + JSX has its own options: jsxSingleQuote
- Empty lines
    + Collapses multiple blank lines into a single blank line.
    + Empty lines at the start and end of blocks (and whole files) are
      removed. (Files always end with a single newline, though.)
- Multi-line objects
    + keeps objects multiline if there’s a newline between the { and the
      first key in the original source code. A consequence of this is
      that long singleline objects are automatically expanded, but short
      multiline objects are never collapsed.

# Plugins

## Sort imports

- https://github.com/trivago/prettier-plugin-sort-imports
