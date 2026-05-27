# Reference card

## Admonition types

::: note
Use for supplementary information that enriches understanding but is not
required to complete the exercise — background context, terminology, or a clarifying detail.
:::

::: tip
Use for practical shortcuts, good habits, or things that will noticeably improve the learner's workflow.
:::

::: guidance
Use for procedural help that keeps the learner on track — things to watch out for during an exercise step, or instructions that clarify expected behaviour. 
:::

::: service
Use for ready-to-run commands or longer actions that the learner should copy and execute without necessarily understanding every detail yet.
:::

::: question
Use to prompt reflection or discussion at the end of a section - open-ended questions that encourage the learner to think before moving on. For self-checked multiple-choice or short-answer questions, use the **quiz** type instead.
:::

::: beware
Use for genuine warnings: operations that are hard to reverse or behaviours that commonly catch beginners off guard.
:::

## Quiz types

Questions are stored in `questions.gift` in the course directory and embedded in markdown with `:::quiz <question-id>`. Three question types are supported.

**Multiple choice** - one correct answer (`=`), any number of wrong answers (`~`). Options are shuffled on each page load.

:::quiz ref-multichoice
:::

**True / False** - a statement the learner marks true or false.

:::quiz ref-truefalse
:::

**Short answer** - free-text input, matched case-insensitively against one or more accepted answers.

:::quiz ref-shortanswer
:::

### GIFT format reference

```
// Multiple choice
::question-id::Question text? {
=Correct option text
~Wrong option #Optional per-choice feedback
~Another wrong option
####Optional general feedback shown after any answer
}

// True / False
::question-id::Statement text. {TRUE ####Optional feedback}

// Short answer  (multiple = lines = multiple accepted answers)
::question-id::Question text? {
=accepted answer
=alternative accepted answer
####Optional feedback
}
```

The `####` general feedback and per-choice `#feedback` are both optional.
