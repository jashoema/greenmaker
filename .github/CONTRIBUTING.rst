TODO: Update with public version of contribution instructions

Contributing to Your Tool Name
==============================

Thanks for taking the time to contribute!

.. contents :: Summary


The following is a set of guidelines for contributing to AIDE's Your Tool Name, which is hosted in the `AIDE Organization <https://wwwin-github.cisco.com/AIDE>`__ on GitHub. These are mostly guidelines, not rules. Use your best judgment, and feel free to propose changes to this document in a pull request.


Code of Conduct
---------------

This project and everyone participating in it is governed by the `Code of Conduct <CODE_OF_CONDUCT.md>`__. By participating, you are expected to uphold this code.

How Can I Contribute?
---------------------

Reporting Bugs
~~~~~~~~~~~~~~

This section guides you through submitting a bug report for AIDE's Your Tool Name. Following these guidelines helps maintainers and the community understand your report, reproduce the behavior, and find related reports.

Before creating bug reports, please check `this list <#before-submitting-a-bug-report>`__ as you might find out that you don't need to create one. When you are creating a bug report, please `include as many details as possible <#how-do-i-submit-a-good-bug-report>`__.

.. note::
   If you find a **Closed** issue that seems like it is the same thing that you're experiencing, open a new issue and include a link to the original issue in the body of your new one.


How Do I Submit A (Good) Bug Report?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bugs are tracked as `GitHub issues <https://guides.github.com/features/issues/>`__. Create an issue on that repository and provide the following information by filling in the template.

Explain the problem and include additional details to help maintainers reproduce the problem:

-  **Use a clear and descriptive title** for the issue to identify the problem.
-  **Describe the exact steps which reproduce the problem** in as many details as possible. For example, start by explaining which browser you are using to connect.
-  **Explain what you expected to see instead and why.**
-  **Include screenshots and animated GIFs** which show you following the described steps and clearly demonstrate the problem.

Suggesting Enhancements
~~~~~~~~~~~~~~~~~~~~~~~

This section guides you through submitting an enhancement suggestion for AIDE's Your Tool Name, including completely new features and minor improvements to existing functionality. Following these guidelines helps maintainers and the community understand your suggestion and find related suggestions.

Before creating enhancement suggestions, please check `this list <#before-submitting-an-enhancement-suggestion>`__ as you might find out that you don't need to create one. When you are creating an enhancement suggestion, please `include as many details as possible <#how-do-i-submit-a-good-enhancement-suggestion>`__.


Before Submitting An Enhancement Suggestion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Perform a `cursory search <https://wwwin-github.cisco.com/search?q=+is:issue+user:aide>`__ to see if the enhancement has already been suggested. If it has, add a comment to the existing issue instead of opening a new one.


How Do I Submit A (Good) Enhancement Suggestion?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Enhancement suggestions are tracked as `GitHub issues <https://guides.github.com/features/issues/>`__.

Your First Code Contribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Unsure where to begin contributing to AIDE's Your Tool Name? You can start by looking through these ``beginner`` and ``help-wanted`` issues:

-  [Beginner issues][beginner] - issues which should only require a few lines of code, and a test or two.
-  [Help wanted issues][help-wanted] - issues which should be a bit more involved than ``beginner`` issues.

Both issue lists are sorted by total number of comments. While not perfect, number of comments is a reasonable proxy for impact a given change will have.

Tesing Locally
^^^^^^^^^^^^^^

AIDE's Your Tool Name can be tested locally. For instructions on how to do this, see the following section in the `User
Guide <https://wwwin-github.cisco.com/pages/AIDE/User-Guide/stable/about/contributing.html#testing-locally-before-submittting>`__

Pull Requests
~~~~~~~~~~~~~

The process described here has several goals:

-  Maintain quality
-  Fix problems that are important to users
-  Engage the community in working toward the best possible User Guide
-  Enable a sustainable system for the User Guide's maintainers to review contributions

Please follow these steps to have your contribution considered by the maintainers:

1. Follow all instructions in `the template <PULL_REQUEST_TEMPLATE.md>`__
2. Follow the `styleguides <#styleguides>`__
3. After you submit your pull request, verify that all `status checks <https://help.github.com/articles/about-status-checks/>`__ are passing What if the status checks are failing? If a status check is
   failing, and you believe that the failure is unrelated to your change, please leave a comment on the pull request explaining why you believe the failure is unrelated. A maintainer will re-run the status check for you. If we conclude that the failure was a false positive, then we will open an issue to track that problem with our status check suite.

While the prerequisites above must be satisfied prior to having your pull request reviewed, the reviewer(s) may ask you to complete additional design work, tests, or other changes before your pull request can be ultimately accepted.

Styleguide
----------

When contributing to AIDE Your Tool Name, please ensure that you follow the following style guides. Reviewers will ensure that these are followed and will ask you to adhere to them.

Git Commit Messages
~~~~~~~~~~~~~~~~~~~

-  Use the present tense ("Add feature" not "Added feature")
-  Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
-  Limit the first line to 50 characters or less
-  Reference issues and pull requests liberally after the first line
-  When only changing documentation (e.g. changing README.md or PULL\_REQUEST.md), include ``[skip ci]`` in the commit title
-  Consider starting the commit message with an applicable emoji:

   -  art: ``:art:`` when improving the format/structure of the code
   -  racehorse: ``:racehorse:`` when improving performance
   -  memo: ``:memo:`` when writing docs
   -  bug: ``:bug:`` when fixing a bug
   -  fire: ``:fire:`` when removing code or files
   -  green\_heart: ``:green_heart:`` when fixing the CI build
   -  white\_check\_mark: ``:white_check_mark:`` when adding tests
   -  lock: ``:lock:`` when dealing with security
   -  arrow\_up: ``:arrow_up:`` when upgrading dependencies
   -  arrow\_down: ``:arrow_down:`` when downgrading dependencies
   -  shirt: ``:shirt:`` when removing linter warnings

Additional Notes
----------------

Issue and Pull Request Labels
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section lists the labels we use to help us track and manage issues and pull requests.

`GitHub search <https://help.github.com/articles/searching-issues/>`__ makes it easy to use labels for finding groups of issues or pull requests you're interested in. For example, you might be interested in open pull requests in ``AIDE/aide-python-agent`` `which haven't been reviewed yet <https://wwwin-github.cisco.com/search?q=is%3Aopen+is%3Apr+repo%3AAIDE%2Faide-python-agent+comments%3A0&type=Repositories>`__.

To help you find issues and pull requests, each label is listed with search links for finding open items with that label in ``AIDE/aide-python-agent`` only and also across all AIDE repositories. We encourage you to read about `other search filters <https://help.github.com/articles/searching-issues/>`__ which will help you write more focused queries.

The labels are loosely grouped by their purpose, but it's not required that every issue have a label from every group or that an issue can't have more than one label from the same group.

Please open an issue on ``AIDE/aide-python-agent`` if you have suggestions for new labels, and if you notice some labels are missing on some repositories, then please open an issue on that repository.

Type of Issue and Issue State
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Label name                    | Description                                                                                                                                                 |
+===============================+=============================================================================================================================================================+
| ``enhancement``               | Feature requests.                                                                                                                                           |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``documentation``             | Applicable only when working with documentation that is not part of the guide.                                                                              |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``bug``                       | Confirmed bugs or reports that are very likely to be bugs.                                                                                                  |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``question``                  | Questions more than bug reports or feature requests (e.g. how do I do X).                                                                                   |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``feedback``                  | General feedback more than bug reports or feature requests.                                                                                                 |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``help wanted``               | The AIDE User Guide core team would appreciate help from the community in resolving these issues.                                                           |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``beginner``                  | Less complex issues which would be good first issues to work on for users who want to contribute to AIDE.                                                   |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``more information needed``   | More information needs to be collected about these problems or feature requests (e.g. steps to reproduce).                                                  |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``blocked``                   | Issues blocked on other issues.                                                                                                                             |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``duplicate``                 | Issues which are duplicates of other issues, i.e. they have been reported before.                                                                           |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``wontfix``                   | The AIDE Your Tool Name core team has decided not to fix these issues for now, either because they're working as intended or for some other reason.         |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``invalid``                   | Issues which aren't valid (e.g. user errors).                                                                                                               |
+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

Pull Request Labels
^^^^^^^^^^^^^^^^^^^

+------------------------+------------------------------------------------------------------------------------------------+
| Label name             | Description                                                                                    |
+========================+================================================================================================+
| ``work in progress``   | Pull requests which are still being worked on, more changes will follow.                       |
+------------------------+------------------------------------------------------------------------------------------------+
| ``needs review``       | Pull requests which need code review, and approval from maintainers or User Guide core team.   |
+------------------------+------------------------------------------------------------------------------------------------+
| ``under review``       | Pull requests being reviewed by maintainers or core team.                                      |
+------------------------+------------------------------------------------------------------------------------------------+
| ``requires changes``   | Pull requests which need to be updated based on review comments and then reviewed again.       |
+------------------------+------------------------------------------------------------------------------------------------+

