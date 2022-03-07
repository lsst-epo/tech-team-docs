You may copy and paste the following into a file, and then [reference that file in your git config](https://thoughtbot.com/blog/better-commit-messages-with-a-gitmessage-template)

```markdown
# [LABEL] SHORT SUMMARY WRITTEN IN IMPERATIVE ####
############################################ c50 ↑

# Leave SECOND LINE BLANK. Use the IMPERATIVE VOICE ############# c72 ↓
# For git: "Resolves <ISSUE_NUMBER>"
#
# For JIRA: "<ISSUE_KEY> #<transition_name> #comment <comment_string>"
# Transitions: IN-PROGRESS | IN-REVIEW
##################################################################### ↓
```

### Why'd we do this?

#### Log Line

```markdown
# [LABEL] SHORT SUMMARY WRITTEN IN IMPERATIVE ###
########################################### c50 ↑ 
```

`[LABEL]` We use 3 different labels, and they tend to be enough to describe any type of commit:

* `[C]` A chore; any change that adds value but does not significantly affect performance or functionality.  For example: Changing what a button does is not a chore. A chore is changing the text or color of a button.
* `[F]` A feature; any change that adds/improves/changes functionality. Changing the data a graph renders is not a feature. A feature is changing what the graph does with the data.
* `[B]` A bug; any change that fixes a performance or functionality issue.  Refactoring a JS component for legibility is not a bug. A bug is altering or replacing a JS component so it does what it's suppose to.

`SHORT SUMMARY WRITTEN IN IMPERATIVE` A reminder to be succinct and to use the [imperative voice](https://en.m.wikipedia.org/wiki/Imperative_mood). This voice uses verbs that are commands in the present tense, and lends itself to writing short summaries.

`############################################ c50 ↑` A reminder to BE SUCCINCT. You can, and in many cases should, be verbose in the next section of your commit message but the log line should be < 50 characters whenever possible. This will ensure that it will read well in any context and will help others review many short logs at a glance and have a good understanding of what's going on. This line, as well as the one above it, are each 50 characters long so if your log line stretches past them, consider taking another stab at it.

#### Summary

```markdown
# Leave SECOND LINE BLANK. Use the IMPERATIVE VOICE ############# c72 ↓
```

`Leave SECOND LINE BLANK.` The log line should be followed by a blank line. This blank line tells git where the log line (what show up in short logs) ends, and where the bulk of your commit message (what show up in long logs) begins.

`Use the IMPERITIVE VOICE` Another reminder to USE THAT THERE IMPERATIVE VOICE.

`############# c72 ↓` Add a carriage return after 72 characters so that your commit message fits in the terminal well. This line is 72 characters long. This is far less critical than the log line length as most of us wrap our terminal text.  In fact, when Github displays the full commit messages, these carriage returns can look awkward as the text seems to be wrapping unnecessarily. A bit of a toss up.

`# For git: "Resolves <ISSUE_NUMBER>"` Generally the EPO team tracks all issue in JIRA.  However, occasionally, you may want to [associate a commit with a Github issue](https://help.github.com/en/articles/closing-issues-using-keywords). To do so, use the `Resolves` keyword followed by the issue number `#111`. For instance, you might create Github issues that each address separate aspects of a larger JIRA ticket. You could then close out issues by associating them with commits, and close out a JIRA ticket by associating it with a pull request. This is a not a predetermined pattern that EPO is using currently, but if it works for you, it works.

```
# For JIRA: "<ISSUE_KEY> #<transition_name> #comment <comment_string>"
# Transitions: IN-PROGRESS | IN-REVIEW
```

`<ISSUE_KEY>` To associate a commit with a JIRA ticket just include the ticket key (i.e EPO-1111) as the first thing on a new line.  A link to your commit will now automatically show up alongside the ticket description in JIRA.

`#<transition_name>` To set the state of the JIRA ticket using your commit message, first associate it with a ticket (see above), then, on the same line, use `#` + `TRANSITION-NAME`. Two states you might want to set are `IN-PROGRESS` or `IN-REVIEW`.  You should not set the state to `DONE` as all JIRA tickets should be reviewed by someone other than the author before they are closed. This functionality is not particularly useful for our development because you typically want to indicate a ticket is in progress before you have work to commit, and there is not currently a way to assign (or auto assign) a review when transitioning to `IN-REVIEW` necessitating you interact with the JIRA web app regardless of what you told it to do from git.

`#comment <comment_string>"` To add a comment to the JIRA ticket, first associate it with a ticket (see above), then, on the same line, use `#comment` + `YOUR COMMENT`. This can be quite a time saver as you may often find yourself copying text from your commit message verbatim for your JIRA comment. Unfortunately there is not currently support for adding work log comments.

`##################################################################### ↓` This line is also 72 characters long.

In our project management ecosystem a commit should be <= to a JIRA ticket.  That is, it should be the only commit in a pull request that lines up to a JIRA ticket, or it should be one of several commits in a pull request that lines up to a JIRA ticket.  A commit message should really never reference more than one JIRA ticket.