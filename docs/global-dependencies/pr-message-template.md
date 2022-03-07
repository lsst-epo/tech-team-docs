### Commit Message Template

You may copy and paste the following into a file, and then [implement that file in your repo to see the template propagate to Github PRs](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)

```markdown
JIRA: https://jira.lsstcorp.org/browse/<ID>

## What this change does

A few sentences describing the outcome of the change (“fixes a thing”; "adds the stuff") and how you tackled it (“added a prop to prevent lazyloading in the presence of barbara walters”). How successful is the change? And how are you measuring that success?

## Notes for reviewers

Where should the reviewer look for the change? Do they review the change on the frontend? How extensive is the change? Does it affect Components used in a variety of contexts? Anything you'd like reviewers to pay particular attention to or questions you have about the change.

Include an indication of how detailed a review you want on a 1-10 scale.

- 1 = "I barely need review on this"
- 5 = "Please make sure there are no obvious errors and that you believe it does what it says it does"
- 10 = "I think it works, maybe, but we need to look at it together"

## Testing

How did you test this change? Can the reviewer test this change for themselves?

If you wrote new tests in the change it's fine to just put "New tests in PR". If you haven't added any tests but you think your change is covered by existing tests you can say "Existing tests". And if you're not sure how to test it, say that.

## Screenshots (optional)

### Before:

### After:
```

### Why'd we do this?

In an effort to standardize our team's expectations and use of PRs we created a template that indicates what sort of information is most useful for a reviewer.  Broadly speaking, we're looking for a couple components in a PR message:

1. What change did you make?

2. How do you know the change is valid?

3. How can a reviewer validate your change?
