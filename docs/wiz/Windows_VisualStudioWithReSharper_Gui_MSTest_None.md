<!--
GENERATED FILE - DO NOT EDIT
This file was generated by [MarkdownSnippets](https://github.com/SimonCropp/MarkdownSnippets).
Source File: /docs/mdsource/wiz/Windows_VisualStudioWithReSharper_Gui_MSTest_None.source.md
To change this file edit the source file and then run MarkdownSnippets.
-->

# Getting Started Wizard

[Home](/docs/wiz/readme.md) > [Windows](Windows.md) > [Visual Studio with ReSharper](Windows_VisualStudioWithReSharper.md) > [Prefer GUI](Windows_VisualStudioWithReSharper_Gui.md) > [MSTest](Windows_VisualStudioWithReSharper_Gui_MSTest.md) > No build server

## Add NuGet packages

Add the following packages to the test project:


<!-- snippet: MSTest-nugets -->
<a id='snippet-mstest-nugets'></a>
```csproj
<PackageReference Include="Microsoft.NET.Test.Sdk" Version="17.4.1" />
<PackageReference Include="MSTest.TestAdapter" Version="3.0.2" />
<PackageReference Include="MSTest.TestFramework" Version="3.0.2" />
<PackageReference Include="Verify.MSTest" Version="19.7.0" />
```
<sup><a href='/src/NugetUsage/MSTestNugetUsage/MSTestNugetUsage.csproj#L7-L12' title='Snippet source file'>snippet source</a> | <a href='#snippet-mstest-nugets' title='Start of snippet'>anchor</a></sup>
<!-- endSnippet -->


## Implicit Usings

**All examples use [Implicit Usings](https://docs.microsoft.com/en-us/dotnet/core/project-sdk/msbuild-props#implicitusings). Ensure the following is set to have examples compile correctly `<ImplicitUsings>enable</ImplicitUsings>`** <!-- include: implicit-usings. path: /docs/mdsource/implicit-usings.include.md -->

If `ImplicitUsings` are not enabled, substitute usages of `Verify()` with `Verifier.Verify()`. <!-- endInclude -->


## Source Control

### Includes/Excludes

 * **All `*.received.*` files should be excluded from source control.** <!-- include: include-exclude. path: /docs/mdsource/include-exclude.include.md -->

eg. add the following to `.gitignore`

```
*.received.*
```

If using [UseSplitModeForUniqueDirectory](/docs/naming.md#usesplitmodeforuniquedirectory) also include:

`*.received/`


All `*.verified.*` files should be committed to source control. <!-- endInclude -->

### Line Endings

All text extensions of `*.verified.*` and have eol set to `lf`. <!-- include: line-endings. path: /docs/mdsource/line-endings.include.md -->

eg add the following to `.gitattributes`

```
*.verified.txt text eol=lf
*.verified.xml text eol=lf
*.verified.json text eol=lf
```

Note that this is a suggested subset of verified text extension. Add others as required based on the file types being verified. <!-- endInclude -->


## DiffEngineTray

Install [DiffEngineTray](https://github.com/VerifyTests/DiffEngine/blob/main/docs/tray.md)

DiffEngineTray sits in the Windows tray. It monitors pending changes in snapshots, and provides a mechanism for accepting or rejecting those changes.

```
dotnet tool install -g DiffEngineTray
```

This is optional, but recommended. Also consider enabling [Run at startup](https://github.com/VerifyTests/DiffEngine/blob/main/docs/tray.md#run-at-startup).


## ReSharper Plugin

Install the [ReSharper Plugin](https://plugins.jetbrains.com/plugin/17241-verify-support)

Provides a mechanism for contextually accepting or rejecting snapshot changes inside the ReSharper test runner.

This is optional, but recommended.

## DiffPlex

The text comparison behavior of Verify is pluggable. The default behaviour, on failure, is to output both the received
and the verified contents as part of the exception. This can be noisy when verifying large strings.

[Verify.DiffPlex](https://github.com/VerifyTests/Verify.DiffPlex) changes the text compare result to highlighting text differences inline.

This is optional, but recommended.

### Add the NuGet

```xml
<PackageReference Include="Verify.DiffPlex" Version="*" />
```

### Enable

```cs
[ModuleInitializer]
public static void Initialize() =>
    VerifyDiffPlex.Initialize();
```


## Sample Test

<!-- snippet: SampleTestMSTest -->
<a id='snippet-sampletestmstest'></a>
```cs
[TestClass]
public class Sample :
    VerifyBase
{
    [TestMethod]
    public Task Test()
    {
        var person = ClassBeingTested.FindPerson();
        return Verify(person);
    }
}
```
<sup><a href='/src/Verify.MSTest.Tests/Snippets/Sample.cs#L3-L17' title='Snippet source file'>snippet source</a> | <a href='#snippet-sampletestmstest' title='Start of snippet'>anchor</a></sup>
<!-- endSnippet -->

## Diff Tool

Verify supports many [Diff Tools](https://github.com/VerifyTests/DiffEngine/blob/main/docs/diff-tool.md#supported-tools) for comparing received to verified.
While IDEs are supported, due to their MDI nature, using a different Diff Tool is recommended.

Tools supported by Windows:

 * [BeyondCompare](https://www.scootersoftware.com)
 * [P4Merge](https://www.perforce.com/products/helix-core-apps/merge-diff-tool-p4merge)
 * [DeltaWalker](https://www.deltawalker.com/)
 * [WinMerge](https://winmerge.org/)
 * [DiffMerge](https://www.sourcegear.com/diffmerge/)
 * [TortoiseGitMerge](https://tortoisegit.org/docs/tortoisegitmerge/)
 * [TortoiseGitIDiff](https://tortoisegit.org/docs/tortoisegitmerge/)
 * [TortoiseMerge](https://tortoisesvn.net/TortoiseMerge.html)
 * [TortoiseIDiff](https://tortoisesvn.net/TortoiseIDiff.html)
 * [KDiff3](https://github.com/KDE/kdiff3)
 * [Guiffy](https://www.guiffy.com/)
 * [ExamDiff](https://www.prestosoft.com/edp_examdiffpro.asp)
 * [Diffinity](https://truehumandesign.se/s_diffinity.php)
 * [Rider](https://www.jetbrains.com/rider/)
 * [Vim](https://www.vim.org/)
 * [Neovim](https://neovim.io/)
