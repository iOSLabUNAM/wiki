# frozen_string_literal: true

declared_trivial = github.pr_title.include? '#trivial'

warn('PR is classed as Work in Progress') if github.pr_title.include? '[WIP]'

warn('Big PR') if git.lines_of_code > 500

commit_lint.check

prose.language = 'es-es'
prose.check_spelling '_posts/*.md'
