---
layout: post
title: Intellij Refactorig Magic
subtitle: Intellij refactoring tips
tags: [Productivity, Intellij]
---

**Inline Method**

Use when there is Disruption in the flow of method.

You can Invoke context actions by using `Alt + Enter.`
Move Carot to previous word with `Option + Shift + left`
Move Carot to next word with Selection with `Ctrl + Shift + right`

```r
List<String> getSortedListOfNames(List<Speaker> speakers) {
        List<String> speakerNames = extractNamesFromSpeakerList(speakers);
        sortSpeakerNames(speakerNames);
        return speakerNames;
    }

private void sortSpeakerNames(List<String> speakerNames) {
        Collections.sort(speakerNames);
}

private List<String> extractNamesFromSpeakerList(List<Speaker> speakers) {
        List<String> result = new ArrayList<>();
        for (Speaker speaker : speakers) {
            result.add(speaker.getName());
        }
        return result;
}
```

**Let's use latest java functions and refactor above code**

Use `Option + CMD + N` for inline method action. This will give various options and you can replace method call with it's contents.

Here’s the refactored code for you to compare with the original code:

```r
List<String> getSortedListOfNames(List<Speaker> speakers) {
    return speakers.stream()
            .map(Speaker::getName)
            .sorted()
            .collect(Collectors.toList());
}
```

First use inline method and replace method call with code. Then use context actions and convert for loop into streams.

Jump to next suggestions and errors by using `F2`. Use options in context actions like **Inline variable** to remove redundent variables.

Select a code block and use extract method command `⌃⌥M -> Ctrl + Option + M` to put that code into a function.

Simply using `F2`, `Alt+Enter` in sequence can help us refactor our code to a great extent.

**Extract variable**

If you come across an expression that is hard to understand or it is duplicated in several places throughout you code, the Extract Variable refactoring can help you deal with those problems placing the result of such expression or its part into a separate variable that is less complex and easier to understand. Plus, it reduces the code duplication.

Use `⌃⌥V` for extracting variable.

<div style="text-align:center;">
    <img src="http://techdesserts.com/assets/img/inline-method-refactoring-2.gif" alt="refactoring gif">
</div>

<br/><br/>

<div style="text-align:center;">
    <img src="http://techdesserts.com/assets/img/inline-method-refactoring-3.gif" alt="refactoring gif">
</div>

<br/><br/>

Reference : https://blog.jetbrains.com/idea/2019/07/refactoring-inline-method-in-intellij-idea/

<br/>
