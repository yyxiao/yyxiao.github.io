---
bg: "tools.jpg"
layout: post
title:  IDEA常用插件
crawlertitle: "plugin"
summary: "IDEA plugin Translation"
date: 2017-03-30 17:53:00
categories: posts
tags: ['Tools']
author: Xander
---

本文主要归纳一些老夫用到感觉比较不错的IDEA插件，如有不足请联系老夫。

### Translation

主要方便老夫查看一些源码注释。

![]({{ site.images }}/post/170330/1.gif)

* Translation是一个翻译插件，支持中英互译、单词朗读。  General Usage Instructions:
* 选择需要翻译的文本 > 点击鼠标右键 > 点击Translate.
* 或者使用快捷键Alt + 0/1/2/3/R/T(Mac下可能无效，需要自定义快捷键)进行翻译。
* 你可以直接翻译如"getTranslatedString"和"HELLO_WORLD"这样的文本。

#### 自定义快捷键（Mac下默认快捷键可能无效）
     
打开 Preferences(Settings) > Keymap, 然后搜索 Translation. 在需要修改快捷键的 Action 上点击鼠标右键，
然后点击 "add Keyboard Shortcut..." 设置新的快捷键。 另外，按 ESC 键可关闭气泡和翻译对话框。
     
[![1]({{ site.images }}/post/170330/1.png)]({{ site.images }}/post/170330/1.png)


### Live Templates

| Item        | Description   |
| ------------- |:-------------:|
| annotated("annotation qname") | Creates a symbol of type with an annotation that resides at the specified location. For an example, see Live Templates in the iterations group. |
| anonymousSuper()| Suggests a supertype for a Kotlin object expression.|
| сamelCase(String)|Returns the string passed as a parameter, converted to camel case. For example, my-text-file/my text file/my_text_file will be converted to myTextFile.|
| capitalize(String)|Capitalizes the first letter of the name passed as a parameter.|
| capitalizeAndUnderscore(sCamelCaseName)|Capitalizes the all letters of a CamelCase name passed as a parameter, and inserts an underscore between the parts. For example, if the string passed as a parameter is FooBar, then the function returns FOO_BAR.|
| castToLeftSideType()|Casts the right-side expression to the left-side expression type. It is used in the iterations group to have a single template for generating both raw-type and Generics Collections.|
| className(sClassName)|Returns the name of the current class (the class where the template is expanded).|
| classNameComplete()|This expression substitutes for the class name completion at the variable position.|
| clipboard()|Returns the contents of the system clipboard.|
| camelCase(String)|Returns CamelCase string out of snake_case string. For example, if the string passed as a parameter is foo_bar, then the function returns fooBar.|
| complete()|This expression substitutes for the code completion invocation at the variable position.|
| completeSmart()|This expression substitutes for the smart type completion invocation at the variable position.|
| componentTypeOf (<array variable or array type>)|Returns component type of an array. For example, see the Live Templates in the iterations group in the other group.|
| currentPackage()|Returns the current package name.|
| date(sDate)|Returns the current system date in the specified format.|
| By default, the current date is returned in the default system format. However, if you specify date format in double quotes, the date will be presented in this format:|
| decapitalize(sName)|Replaces the first letter of the name passed as a parameter with the corresponding lowercase letter.|
| descendantClassEnum(<String>)|Shows the children of the class entered as a string parameter.|
| enum(sCompletionString1,sCompletionString2,...)|List of comma-delimited strings suggested for completion at the template invocation.|
| escapeString(sEscapeString)|Escapes the specified string.|
| expectedType()|Returns the type which is expected as a result of the whole template. Makes sense if the template is expanded in the right part of an assignment, after return, etc.|
| fileName(sFileName)|Returns file name with extension.|
| fileNameWithoutExtension()|Returns file name without extension.|
| firstWord(sFirstWord)|Returns the first word of the string passed as a parameter.|
| groovyScript("groovy code")|Returns Groovy script with the specified code.|
| guessElementType (<container>)|Makes a guess on the type of elements stored in a java.util.Collection. To make a guess, IntelliJ IDEA tries to find the places where the elements were added to or extracted from the container.|
| iterableComponentType(<ArrayOrIterable>)|Returns the type of an iterable component, such as an array or a collection.|
| iterableVariable()|Returns the name of a variable that can be iterated.|
| lineNumber()|Returns the current line number.|
| lowercaseAndDash(String)|Returns lower case separated by dashes, of the string passed as a parameter. For example, the string MyExampleName is converted to my-example-name.|
| methodName()|Returns the name of the embracing method (where the template is expanded).|
| methodParameters()|Returns the list of parameters of the embracing method (where the template is expanded).|
| methodReturnType()|Returns the type of the value returned by the current method (the method within which the template is expanded).|
| qualifiedClassName()|Returns the fully qualified name of the current class (the class where the template is expanded).|
| Clear the Shorten FQ names check box.|
| rightSideType()|Declares the left-side variable with a type of the right-side expression. It is used in the iterations group to have a single template for generating both raw-type and Generics Collections.|
| snakeCase(sCamelCaseText)|Returns snake_case string out of CamelCase string passed as a parameter.|
| spaceSeparated(String)|Returns string separated with spaces out of CamelCase string passed as a parameter. For example, if the string passed as a parameter is fooBar, then the function returns foo bar.|
| subtypes(sType)|Returns the subtypes of the type passed as a parameter.|
| suggestIndexName()|Suggests the name of an index variable. Returns i if there is no such variable in scope, otherwise returns j if there is no such variable in scope, etc.|
| suggestVariableName()|Suggests the name for a variable based on the variable type and its initializer expression, according to your code style settings that refer to the variable naming rules.|
| For example, if it is a variable that holds an element within iteration, IntelliJ IDEA makes a guess on the most reasonable names, also taking into account the name of the container being iterated.|
| suggestFirstVariableName(sFirstVariableName)|Doesn't suggest true, false, this, super.|
| time(sSystemTime)|Returns the current system time.|
| typeOfVariable(VAR)|Returns the type of the variable passed as a parameter.|
| underscoresToCamelCase(sCamelCaseText)|Returns the string passed as a parameter with CamelHump letters substituting for underscores. For example, if the string passed as a parameter is foo_bar, then the function returns fooBar.|
| underscoresToSpaces(sParameterWithSpaces)|Returns the string passed as a parameter with spaces substituting for underscores.|
| user()|Returns the name of the current user.|
| variableOfType(<type>)|Suggests all variables that may be assigned to the type passed as a parameter, for example variableOfType("java.util.Vector"). If you pass an empty string ("") as a parameter, suggests all variables regardless of their types.|
| JsArrayVariable|Returns JavaScript array name.|
| jsClassName()|Returns the name of the current JavaScript class.|
| jsComponentType|Returns the JavaScript component type.|
| jsMethodName()|Returns the name of the current JavaScript method.|
| jsQualifiedClassName|Returns the complete name of the current JavaScript class.|
| jsSuggestIndexName|Returns a suggested name for an index.|
| jsSuggestVariableName|Returns a suggested name for a variable.|
