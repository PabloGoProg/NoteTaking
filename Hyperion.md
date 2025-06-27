g* Are the test results valid? *
The tests added or modified  in the pr fail in the before results JSON/Log and pass successfully in the after results JSON/Log.

Test Results Before:
tests/_async/test_document.py::test_doc_with_pipe_type_hints FAILED      [  6%]

Test Results After:
tests/_async/test_document.py::test_doc_with_pipe_type_hints PASSED      [  6%]

----

The json contains the tests added in the pr:

{
        "name": "tests/_async/test_document.py::test_doc_with_pipe_type_hints",
        "status": "FAILED"
},

-----------------------------------------------------------------------------------------------------------------------

1. Categorization of the issue
Rate the specificity of the original problem statement. The specificity rating is a measure of how much detail the problem statement/PR contains and how clear the desired solution is.

Imagine that you are an experienced software engineer who has been instructed to create a PR that successfully resolves the follow GitHub issue. You have full access to the codebase and can see the issue description above. However, you are not able to ask for clarification and would need to work exclusively from this information. What rating would you give this issue?

The rubric for rating specificity is below:

- 1/2: It is almost impossible to understand what is being asked without further information.
- 3: The issue is vague and there is room for ambiguity. It is unclear what a successful solution would look like.
- 4: There are some blanks to fill in, but there is a sensible interpretation of what is required for a solution.
- 5: The issue is well-specified and it is clear what is required for a successful solution.

Note that ratings of 5 should be rare and reserved for GREAT problem statements.

Give me the rate and the justification (Be specific).

< INIT PROBLEM STATEMENT >

</ END PROBLEM STATEMENT >

----

Based on the problem statement classify the issue. Select a minimum of 1 choice; maximum of 4 choices. Choices:

- BUG: Critical, Major, Minor, Regression, Performance, Security, Data, UI / UX, Compatibility, Edge Case and Integration

- Feature: Core, UI / UX,API, Performance, Integration, Accessibility, Localization, Analytics, Customization, Security and Mobile

- Enhancement: Performance, Code Quality, Refactoring, Testing, UI / UX, Accessibility, Technical Debt, Dev Ops, Security, Scalability and Documentation

If you select more than one choice, make sure they are all from the same category (bug, feature, enhancement).

----

Now, categorize the knowledge required to solve the issue in any of these knowledge categories. Select a minimum of 1 choice and a maximum of 4 choices. Choices:

Front End, Back End, Full Stack, Web, Mobile, Desktop, Database, API, Infrastructure, Dev Ops, Cloud, Networking, Security, Authentication / Authorization, Data Science, ML / AI, UI / UX, Accessibility, Performance, QA Testing,Game Development, AR / VR, IOT / Embedded and Blockchain.

----

Rewrite this in natural language as a problem statement in markdown format. Keep this in mind:

- describe the *current issue*
- what was wrong before the fix
- If the original PR was had a specificity score of 2, your problem statement should also match a specificity of 2. The specificity of this text is 2.
- **DO NOT provide more context than the original description has provided**
- Problem statements should be formatted like real GitHub issues with titles and issue headings that are marked as issue headings using clear formatting.
- Avoid simply restating what was changed in the PR.
- Focus on why the issue mattered—what impact did it have?
- Do not mention how the problem was fixed.

< INIT TEXT >

</ END TEXT>

Use this sections if is possible: Expected behavior, Error messages, stack traces, or logs, Steps to reproduce, Additional context (optional)

-----------------------------------------------------------------------------------------------------------------------

2. Requirement Creation Instructions
	Create a well specified requirement describing the problem to be solved. This requirement should be well specified and include all relevant context around the problem that is required to remove ambiguity and create a solution. Note that the requirement should only include context around the problem and not leak details about the solution.
	
	A strong problem requirement should:
	
	- Clearly define the expected behavior (i.e., what the system should be doing).
	- Include relevant context to remove ambiguity in identifying and solving the issue.
	- Avoid specifying how to fix the problem, focusing only on what needs to be addressed.
	- Be structured so it can be referenced independently in future development work.
	- DOES NOT leak the solution (Do not mention name of files or the creation of file/class/function)
	- Remove the ambiguity in the problem statement.
	- Does not include explicit instructions on how to solve the problem.
	
	Please ensure your requirement is not leaking the solution. You should not provide the LLM with implementation details to solve the problem (e.g., update function X, create file Y). Instead you should provide high level requirements of what a good solution would accomplish.
	
	Give me only the **Requirement** in list format.
	
	# FOLLOW THIS STRCUCTURE EXAMPLE #
	
	** Original Problem Statement **
	Title: add support for email request
	Description:
	The feature
	For emails, you should figure out how to import and understand .mbox files. Gmail allows you to export all your emails in one go and exports them in .mbox format
	
	** Patch **
	diff --git a/embedchain/chunkers/gmail.py b/embedchain/chunkers/gmail.py
	@@ -0,0 +1,22 @@
	22 insertions, 0 deletions
	
	diff --git a/embedchain/data_formatter/data_formatter.py b/embedchain/data_formatter/data_formatter.py
	@@ -1,6 +1,7 @@
	@@ -22,6 +23,7 @@
	@@ -84,6 +86,7 @@ def _get_loader(self, data_type: DataType, config: LoaderConfig) -> BaseLoader:
	@@ -128,6 +131,7 @@ def _get_chunker(self, data_type: DataType, config: ChunkerConfig) -> BaseChunke
	4 insertions, 0 deletions
	
	diff --git a/embedchain/loaders/gmail.py b/embedchain/loaders/gmail.py
	@@ -0,0 +1,124 @@
	124 insertions, 0 deletions
	
	diff --git a/embedchain/models/data_type.py b/embedchain/models/data_type.py
	@@ -28,6 +28,7 @@ class IndirectDataType(Enum):
	@@ -55,3 +56,4 @@ class DataType(Enum):
	2 insertions, 0 deletions
	
	diff --git a/embedchain/utils.py b/embedchain/utils.py
	@@ -259,6 +259,8 @@ def is_openapi_yaml(yaml_content):
	2 insertions, 0 deletions
	
	diff --git a/pyproject.toml b/pyproject.toml
	@@ -168,9 +168,19 @@ dataloaders=[
	10 insertions, 0 deletions
	
	** Requirement **
	- Add Gmail loader functionality to allow loading emails from Gmail using Google API
	- Use llama_index library which provides Gmail reader functionality
	- Support Gmail search query syntax for filtering emails to load
	- Require user to authenticate with Google OAuth2 credentials stored in credentials.json
	- Parse email content including metadata like subject, date, from/to addresses
	- Clean and format email content by removing unnecessary HTML elements
	- Add new data type GMAIL to support Gmail specific loading
	- Install extra dependencies via pip install embedchain[gmail] command

-----------------------------------------------------------------------------------------------------------------------

3. Write an interface for any files/functions/classes created

For any new files/functions/classes that are introduced you should define the interface of the addition. The interface includes the name of the new file/function/class, any input parameters, and any output parameters. Please use the exact names from the golden patch.

For example: "Implement a class Foo, with class methods: bar which has a, b, c as string parameters and returns optional float and summary of the functionality"

If no new files, classes, or functions are added, then write "No new interfaces are introduced" here.

# FOLLOW THIS STRCUCTURE EXAMPLE #
Implement a new "artistic" module in the `imgaug/augmenters/artistic.py` file that will contain the following:

-`stylize_cartoon` function: Takes an image as a NumPy array, a blur_ksize as an integer defining the kernel size for blurring, a segmentation_size as an integer that controls the size of segmented color regions, a saturation parameter as a floating-point number to adjust color intensity, an edge_prevalence as a float to determine how strongly edges are blended into the image, a suppress_edges flag as a boolean to enable or disable small edge suppression, and an optional from_colorspace as a constant specifying the input image's color space. This function applies a cartoon-like effect to the original image, and it returns a NumPy array representation of the stylized image.

- `find_edges_canny` function: Takes an image as a NumPy array, an edge_multiplier as a float, and an optional from_colorspace as a constant value indicating the color space of the input image. It detects edges using the Canny edge detection algorithm, returning a NumPy array containing the edge-detected image.

-----------------------------------------------------------------------------------------------------------------------

4. Rate the test coverage
Give a Test Coverage Rating and justify why. Test Coverage rating aims to evaluate if the test cases are comprehensive and not restrictive.

- Comprehensiveness here means that the test cases cover all the possible functions introduced/modified by the golden patch across all possible scenarios. A comprehensive test suite will accurately identify (by failing the test) any incorrect code implementation in a potential patch

- A test case is considered “restrictive” if it is too specific to the golden patch’s implementation of the solution. For example, let’s say that a new private method named “foo” is introduced in the golden patch, and there is a test case that checks the accuracy of the “foo” function. A potential solution need not contain this “foo” function, so the test case would fail and unfairly reject the patch.

Based on your evaluation of the tests that were changed, assign a test coverage rating. You will use the following rubric to evaluate test coverage:

- Bad: The tests are too restrictive or they look for something different from the issue.
- Ok: The tests work, but some reasonable solutions may be missed or edge cases may not be covered by the test.
- Perfect: The tests cover perfectly all possible solutions.

Give me only the Test Coverage Rating and the justification. In the justification try to write something specific of the test, n¿do not be general.

** Are you sure the test covers all cases?
